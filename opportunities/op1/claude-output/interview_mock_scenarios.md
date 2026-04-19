# Mock Interview Scenarios
## Quorum Data & AI Platform - Enterprise & Engineering Architect Interview

This document contains realistic interview scenarios with follow-up questions to help you practice.

---

## Scenario 1: Azure Well-Architected Framework Deep Dive

### Initial Question
**Enterprise Architect**: "We're concerned about costs spiraling out of control as we scale the platform. Walk me through how you'd apply the Azure Well-Architected Framework's Cost Optimization pillar to keep our Azure spend under control while maintaining performance."

### Your Response Framework
Start with the WAF Cost Optimization pillar overview, then provide specific strategies:
- Compute optimization (job clusters, autoscaling, Spot VMs)
- Storage optimization (lifecycle management, compression)
- Monitoring and chargeback
- Target: 20-30% cost reduction

### Follow-up Question 1
**Enterprise Architect**: "That sounds good, but how do you balance cost optimization with the Reliability pillar? If we use Spot VMs for cost savings, doesn't that compromise our 99.9% uptime SLA?"

**How to Answer**:
- Acknowledge the trade-off (this is key - show you understand WAF pillars can conflict)
- Explain when Spot VMs are appropriate vs not:
  - ✅ **Safe for Spot**: Dev/test environments, fault-tolerant batch jobs (can retry), non-time-sensitive ETL
  - ❌ **Not for Spot**: Production real-time pipelines, critical Gold layer queries, regulatory reporting
- Risk mitigation:
  - Use Spot only for 20-30% of compute (non-critical workloads)
  - Implement automatic fallback to on-demand VMs if Spot capacity unavailable
  - Databricks can mix Spot and on-demand in same cluster (On-Demand for driver, Spot for workers)
- Result: Achieve cost savings without compromising SLA

**Key Point**: "WAF pillars are not absolutes - we make informed trade-offs based on workload criticality. I document these trade-offs in Architecture Decision Records (ADRs) so the reasoning is transparent."

---

### Follow-up Question 2
**Engineering Lead**: "You mentioned chargeback by segment team. How would you implement that technically, and how does that help with cost optimization?"

**How to Answer**:
- **Technical Implementation**:
  1. **Tagging Strategy**: Tag all Azure resources with: `CostCenter`, `Segment`, `Environment`, `Owner`
  2. **Enforce Tags**: Use Azure Policy to require tags (block deployment if missing)
  3. **Cost Allocation**: Azure Cost Management API to aggregate costs by tag
  4. **Dashboard**: Power BI dashboard showing cost by segment, trend over time
  5. **Budgets & Alerts**: Set budgets per segment, alert at 80% and 100%

- **How It Helps**:
  - **Visibility**: Segment teams see their own spending (awareness drives behavior change)
  - **Accountability**: Teams optimize their own workloads when they "own" the cost
  - **Right-sizing**: Identify underutilized resources (e.g., cluster idle 80% of time)
  - **Trend Analysis**: Detect anomalies (sudden 50% increase week-over-week)

- **Example**: "In a prior project, implementing chargeback reduced costs by 25% in 6 months - teams started terminating idle clusters, right-sizing VMs, and questioning whether they needed daily refreshes vs weekly."

---

### Follow-up Question 3
**Enterprise Architect**: "We're hearing a lot about Microsoft Fabric. Should we use Fabric instead of Databricks to save costs, given that we already have Microsoft licenses?"

**How to Answer** (This is a trap - they're testing if you'll chase shiny objects):
- **Acknowledge the question**: "That's a great question - Fabric is interesting and Microsoft is investing heavily."
- **But don't throw away the platform decision**:
  - Databricks was chosen for specific reasons (likely: Unity Catalog maturity, Delta Lake ecosystem, ML capabilities, Photon performance)
  - Fabric is newer (GA in late 2023) - less mature than Databricks in key areas:
    - Unity Catalog equivalent (OneLake) is less feature-rich
    - Spark performance (Photon is proven faster than Fabric Spark)
    - ML capabilities (Databricks MLflow, AutoML more mature)
- **Cost comparison is complex**:
  - Fabric pricing is bundled (capacity units) - hard to compare apples-to-apples with Databricks DBUs
  - Microsoft licenses help, but Databricks has committed use discounts too
- **Recommendation**:
  - "I'd conduct a formal evaluation (PoC) comparing Fabric vs Databricks for 2-3 use cases"
  - "Measure cost, performance, feature gaps, learning curve, operational maturity"
  - "Make data-driven decision, not emotional decision based on vendor relationship"
- **Pragmatic approach**: "If we're already on Databricks, migration cost and risk may outweigh Fabric benefits. But let's evaluate Fabric for specific use cases where it excels (e.g., Power BI integration)."

**Key Point**: "I'm vendor-agnostic - my job is to recommend the best solution for Quorum, not the most familiar or politically convenient solution."

---

## Scenario 2: TOGAF Governance Challenge

### Initial Question
**Enterprise Architect**: "We've had issues in the past where segment teams built data pipelines outside the platform standards - directly querying source systems, storing data in ungoverned locations. How would you prevent this as Platform Solution Architect?"

### Your Response Framework
This is about TOGAF Architecture Governance - explain your governance model:
- Architecture Review Board (ARB)
- Design review process
- Automated compliance checks
- Exception management

### Follow-up Question 1
**Enterprise Architect**: "That sounds bureaucratic. Won't the segment teams push back and say you're slowing them down?"

**How to Answer** (This tests your balance between governance and agility):
- **Acknowledge the concern**: "You're absolutely right - governance done poorly becomes a bottleneck and teams will work around it."
- **Explain the balance**:
  - **Guardrails, not gates**: "My philosophy is 'guardrails, not gates' - enable teams to self-serve within safe boundaries"
  - **Automated compliance**: "Most governance is automated - Unity Catalog policies, Terraform Sentinel policies, CI/CD gates"
  - **Standard patterns auto-approved**: "If segment teams use approved patterns (DLT, standard modules), no ARB review needed"
  - **ARB for new patterns only**: "ARB reviews only when teams want to deviate or introduce new patterns"
- **Make governance valuable**:
  - "ARB provides expertise, not just approval - we help teams solve problems"
  - "Fast turnaround - 5 business days from submission to decision"
  - "Clear documentation of standards - teams know what's expected upfront"
- **Example**: "In a prior project, we had 90% of projects auto-approved using standard patterns. Only 10% needed ARB review. Teams appreciated the clarity and support."

**Key Point**: "Good governance accelerates teams by providing reusable components, clear standards, and expert guidance. Bad governance slows teams down with bureaucracy and unclear rules."

---

### Follow-up Question 2
**Engineering Lead**: "What if a segment team comes to you with a legitimate exception request - they need to use a different technology because of a specific requirement. How do you handle that?"

**How to Answer**:
- **Exception process**:
  1. **Request with justification**: Team submits exception request with business justification, alternatives considered, risk assessment
  2. **Evaluation**: I assess whether the exception is necessary or if existing patterns can solve the problem
  3. **Risk mitigation**: If exception is approved, define mitigations (e.g., additional monitoring, documentation)
  4. **Time-bound approval**: Exceptions are temporary (6-12 months), must re-certify or remediate
  5. **Escalation path**: If I deny and team disagrees, escalate to CTO office for final decision

- **Example exception scenario**:
  - **Request**: "Need to use Azure Synapse dedicated SQL pool for high-concurrency reporting (100+ concurrent users), not Databricks SQL"
  - **Justification**: Databricks SQL doesn't support required concurrency at acceptable cost
  - **Assessment**: Valid concern - Databricks SQL pricing for 100+ concurrent users is expensive
  - **Mitigation**: Limit to this specific use case, federate queries from Unity Catalog for governance, monitor costs closely
  - **Decision**: Approve for 6 months, re-evaluate when Databricks Serverless SQL becomes GA

- **When to deny**:
  - Request is based on team preference, not technical necessity
  - Security/compliance risk is too high
  - Request fragments the platform (every team uses different tech = no shared knowledge)

**Key Point**: "I'm pragmatic - governance serves the business, not the other way around. But exceptions should be rare and well-justified."

---

### Follow-up Question 3
**Enterprise Architect**: "You mentioned Architecture Decision Records (ADRs). Why are those important, and what do you include in them?"

**How to Answer**:
- **Why ADRs matter**:
  - **Document context**: Future you (or future team) understands why decisions were made
  - **Prevent revisiting**: Without ADRs, teams re-debate the same decisions every 6 months
  - **Onboarding**: New team members understand the reasoning behind architecture
  - **Change management**: When context changes, you can revisit decisions systematically

- **ADR structure** (use standard template):
  ```
  # ADR-001: Why We Chose Databricks Over Azure Synapse

  **Status**: Accepted
  **Date**: 2024-03-15
  **Deciders**: Platform Architect, CTO, Engineering Lead

  ## Context
  Need to choose primary compute engine for data platform. Requirements:
  Spark-based transformations, ML/AI, Delta Lake, Unity Catalog governance.

  ## Decision
  Use Databricks as primary compute engine.

  ## Alternatives Considered
  1. Azure Synapse Spark Pools
  2. Azure HDInsight
  3. Self-managed Spark on VMs

  ## Consequences
  **Positive**:
  - Unity Catalog for governance
  - Photon acceleration (2-3x faster)
  - Delta Lake ecosystem mature
  - ML/AI capabilities (MLflow, AutoML)

  **Negative**:
  - Databricks cost higher than Synapse
  - Vendor lock-in to Databricks

  ## Compliance
  This decision aligns with Azure WAF Performance Efficiency and Operational Excellence pillars.
  ```

- **ADR lifecycle**:
  - **Accepted**: Decision is current
  - **Deprecated**: Decision replaced by newer ADR
  - **Superseded by ADR-XXX**: Point to newer decision

**Key Point**: "ADRs are lightweight - 1-2 pages max. The goal is to capture the 'why', not write a novel."

---

## Scenario 3: Knowledge Graph & Agentic AI

### Initial Question
**Engineering Lead**: "Help me understand the Knowledge Graph. We have relational data in Delta Lake tables - wells, leases, production, owners. Why do we need a separate graph database like Neo4j?"

### Your Response Framework
Explain the difference between relational and graph data models, and the value of Knowledge Graph for Agentic AI.

**How to Answer**:
- **Relational databases (Delta Lake) are optimized for**:
  - Structured data with fixed schemas
  - Aggregations and filtering (e.g., "sum of production by well")
  - Join operations (2-3 table joins are efficient)

- **Graph databases are optimized for**:
  - **Relationship traversal**: Multi-hop queries (e.g., "find all owners affected by this lease sale, 5 levels deep")
  - **Path finding**: Shortest path, impact analysis
  - **Pattern matching**: Find complex relationship patterns

- **Example use case** (critical - make this concrete):
  - **Question**: "If we sell Lease A, which accounts will be impacted and by how much?"
  - **Relational approach** (Delta Lake):
    - Join Lease → Wells → Production → Revenue → Accounts (5 joins)
    - Multiple queries, complex SQL, slow for 5+ hops
  - **Graph approach** (Neo4j):
    - Cypher query: `MATCH (lease:Lease {id:'A'})-[:HAS_WELLS]->(well)-[:PRODUCES]->(production)-[:GENERATES]->(revenue)-[:TO_ACCOUNT]->(account) RETURN account, SUM(revenue)`
    - Single query, optimized for traversal, sub-second response
    - Graph index makes multi-hop traversal fast

- **Why separate from Delta Lake?**:
  - Delta Lake is the **source of truth** for data (Silver/Gold layers)
  - Knowledge Graph is a **specialized index** optimized for relationship queries
  - **Materialization pattern**: Scheduled job reads Delta Lake → materializes graph in Neo4j
  - Best of both worlds: Relational for aggregations, Graph for traversal

- **Agentic AI connection**:
  - AI agents need to answer complex, multi-step questions
  - Graph allows agents to "follow the relationships" dynamically
  - Example: "Show me all wells with declining production that are connected to leases expiring in 6 months"
    - Agent translates natural language → graph query → retrieves context → generates answer

---

### Follow-up Question 1
**Engineering Lead**: "How do you keep the Knowledge Graph in sync with the Delta Lake data? What if the data changes?"

**How to Answer**:
- **Synchronization strategies**:

  1. **Batch Sync (Recommended for QDAI)**:
     - **Schedule**: Nightly or hourly job (depends on freshness requirements)
     - **Process**:
       - Read changes from Gold layer (Delta table with `_change_data` or full refresh)
       - Transform to graph format (nodes and edges)
       - Upsert to Neo4j (MERGE statements for idempotency)
     - **Pros**: Simple, predictable, cost-effective
     - **Cons**: Graph is eventually consistent (lag of 1 hour or 1 day)

  2. **Streaming Sync (For real-time needs)**:
     - **Trigger**: Delta Lake Change Data Feed (CDF) → Kafka/EventHub → Graph update
     - **Pros**: Real-time or near-real-time (seconds)
     - **Cons**: Complex, higher cost, harder to debug

  3. **Hybrid Approach**:
     - **Core entities** (Wells, Leases): Batch sync nightly (low change frequency)
     - **Transactional data** (Production, Revenue): Streaming sync (high change frequency, real-time needed)

- **Data consistency**:
  - **Version tracking**: Store version/timestamp in graph nodes to track freshness
  - **Validation**: Periodic reconciliation job compares Delta Lake vs Graph, alerts on mismatches
  - **Rollback**: If sync fails, previous graph version is preserved

- **Example**: "For Quorum, I'd recommend nightly batch sync for most entities, with streaming for high-priority use cases like real-time production monitoring."

---

### Follow-up Question 2
**Enterprise Architect**: "Neo4j is another database to manage - licensing costs, operational overhead, disaster recovery. Could we just stay in Delta Lake and use GraphFrames in Databricks?"

**How to Answer** (This tests your pragmatism vs purism):
- **Acknowledge the concern**: "Absolutely valid - adding another technology increases complexity and cost."

- **GraphFrames (Databricks) pros and cons**:
  - **Pros**:
    - No separate database - everything in Delta Lake
    - Databricks-native (no new skills to learn)
    - Good for batch graph analytics (PageRank, connected components)
  - **Cons**:
    - Not optimized for real-time graph queries (slower than Neo4j)
    - Limited graph query language (no Cypher - use DataFrame API)
    - Not ideal for interactive Agentic AI (AI agents need sub-second responses)

- **Neo4j pros and cons**:
  - **Pros**:
    - Purpose-built for graph queries (10-100x faster for multi-hop traversal)
    - Cypher query language (expressive, natural for graph patterns)
    - Real-time queries (sub-second for Agentic AI)
  - **Cons**:
    - Separate database (licensing, operations, DR)
    - Another technology to learn

- **Recommendation** (be pragmatic):
  - **Phase 1 (Pilot)**: Start with GraphFrames in Databricks
    - Validate the Knowledge Graph concept with low investment
    - Build a few graph queries, measure performance
    - Get feedback from AI team on whether it meets their needs
  - **Phase 2 (Scale)**: If GraphFrames performance is insufficient for Agentic AI, migrate to Neo4j
    - By then, you've proven the value of Knowledge Graph (easier to justify investment)
    - You understand the query patterns and requirements
  - **Alternative**: Azure Cosmos DB Gremlin API (managed graph DB - less operational overhead than Neo4j)

**Key Point**: "I'm pragmatic - start simple, validate value, then invest in specialized technology if needed. Don't over-engineer upfront."

---

## Scenario 4: Disaster Recovery Trade-offs

### Initial Question
**Enterprise Architect**: "We need 99.9% uptime SLA. Walk me through your disaster recovery strategy for the platform."

### Your Response Framework
Cover RTO/RPO, multi-region HA, DR procedures (from the main prep guide).

### Follow-up Question 1
**Enterprise Architect**: "99.9% uptime allows 43 minutes downtime per month. But multi-region deployment doubles our Azure costs. How do you justify that?"

**How to Answer** (This tests Cost Optimization vs Reliability trade-off):
- **Cost of downtime analysis**:
  - Calculate business impact of downtime:
    - **Regulatory reporting**: If platform down during month-end, miss state reporting deadline = fines, compliance issues
    - **Agentic AI**: If AI agents can't answer customer questions = lost productivity, customer dissatisfaction
    - **Analytics**: If dashboards down = business decisions delayed
  - Example calculation:
    - Platform downtime = 1 hour
    - 500 knowledge workers can't access data = 500 hours lost productivity
    - Average loaded cost per hour = $100
    - **Cost of 1 hour downtime = $50,000**

- **DR cost analysis**:
  - Multi-region deployment doesn't double costs (common misconception):
    - **Primary region**: Full deployment (100% cost)
    - **Secondary region (passive standby)**:
      - Compute: Dormant (0% cost) or minimal (5% cost for standby clusters)
      - Storage: GRS for ADLS adds ~50% to storage cost (but storage is ~20% of total cost)
      - Networking: Minimal cost for VNet, Private Endpoints (pre-deployed but unused)
    - **Total DR incremental cost**: ~10-15% of primary region cost, not 100%

- **Risk mitigation value**:
  - 99.9% SLA = 43 min downtime/month allowed
  - Without DR: Single region failure = 4-8 hours downtime (8-11x SLA breach)
  - With DR: Failover in 4 hours = meet SLA, no business impact

- **Alternative (if budget constrained)**:
  - **Cold DR**: Secondary region infrastructure defined in Terraform, but not deployed
    - Deploy on-demand when primary region fails (RTO = 8 hours, not 4 hours)
    - Cost: Near zero (just Terraform code)
    - Trade-off: Longer RTO, but meets "eventual recovery" if 99.9% SLA is aspirational

**Key Point**: "DR is insurance - you pay a premium to avoid catastrophic loss. The question is: what's the right coverage level for Quorum's risk tolerance?"

---

### Follow-up Question 2
**Engineering Lead**: "How do you test disaster recovery without disrupting production?"

**How to Answer**:
- **DR testing strategy**:

  1. **Non-Prod DR Drills (Quarterly)**:
     - Full failover test in **dev environment**
     - Simulate primary region failure (shut down Databricks workspace, make ADLS unavailable)
     - Execute DR runbook step-by-step
     - Measure actual RTO (time to restore service)
     - Measure actual RPO (data loss)
     - Document issues, update runbook

  2. **Prod DR Validation (Annually)**:
     - **During low-traffic window** (e.g., weekend, holiday)
     - Announce maintenance window to users
     - Perform **live failover** to secondary region
     - Run production workloads in secondary region for 2-4 hours
     - Fail back to primary region
     - Validate no data loss, no corruption

  3. **Partial DR Tests (Monthly)**:
     - Test individual components without full failover:
       - **Restore Unity Catalog backup** to test environment
       - **Failover ADLS** (GRS failover) to test environment
       - **Deploy infrastructure** to secondary region (Terraform apply in test)

  4. **Chaos Engineering (Continuous)**:
     - Use Azure Chaos Studio to inject failures:
       - Terminate random Databricks clusters
       - Simulate ADLS throttling
       - Introduce network latency
     - Validate automatic retries, circuit breakers, health checks work

- **Success criteria**:
  - RTO ≤ 4 hours (measured, not assumed)
  - RPO ≤ 1 hour (measured, not assumed)
  - Runbook accurate (no missing steps discovered during test)
  - Team confident in DR procedures

**Key Point**: "DR testing is not optional - untested DR is worse than no DR (false confidence). We test quarterly in non-prod, annually in prod."

---

## Scenario 5: Hub-and-Spoke Conflict

### Initial Question
**Enterprise Architect**: "You're the Platform Solution Architect with 'Supreme Court' authority over segment architectures. A segment architect strongly disagrees with your decision to reject their design. They escalate to their VP. How do you handle this?"

### Your Response Framework
This tests your leadership, conflict resolution, and governance maturity.

**How to Answer**:
- **Step 1 - Listen and understand**:
  - "First, I'd schedule a 1-on-1 with the segment architect to understand their perspective."
  - "I might have missed something - they know their domain better than I do."
  - "Ask questions: What problem are you trying to solve? Why is this design better than the standard approach?"

- **Step 2 - Explain the decision**:
  - "I'd clearly explain the reasoning behind my rejection - referencing architecture principles, risk assessment, past incidents."
  - "Show empathy - acknowledge that my decision might make their job harder short-term."
  - "Be transparent about trade-offs - 'I understand this adds 2 weeks to your timeline, but here's why it's necessary...'"

- **Step 3 - Explore alternatives**:
  - "Work together to find a solution that meets their needs AND aligns with platform standards."
  - "Maybe there's a compromise - a time-bound exception, a phased approach, or a modification to the standard."

- **Step 4 - Escalation (if no resolution)**:
  - "If we still disagree, I'd suggest we take it to the Architecture Review Board (ARB) as a group decision."
  - "If the ARB still doesn't align with the segment architect, escalate to CTO office for final decision."
  - "I'd present both perspectives objectively - 'Here's the segment team's proposal, here's my concern, here are the trade-offs.'"

- **Step 5 - Accept the decision**:
  - "Once a decision is made (even if I disagree), I commit to it and support the team."
  - "If my decision is overruled, I don't hold a grudge - I document the decision (ADR) and move forward."

- **Principles**:
  - **Assume good intent**: Segment architect is trying to solve a real problem
  - **Be humble**: I might be wrong - be open to changing my mind with new information
  - **Be firm on principles**: Don't compromise on security, governance, or architecture principles for political reasons
  - **Be flexible on implementation**: If there's another way to meet the principles, I'm open
  - **Document the decision**: ADR with context, decision, and rationale (transparency)

**Key Point**: "My role is 'trusted advisor', not 'dictator'. I have authority, but I use it judiciously. The best decisions come from collaboration, not mandates."

---

## Scenario 6: Budget Constraints

### Initial Question
**Enterprise Architect**: "Finance just told us we need to cut the platform budget by 30% next quarter. What would you cut, and what would you protect?"

### Your Response Framework
This tests prioritization, cost vs value trade-offs, and strategic thinking.

**How to Answer**:

**Step 1 - Understand the constraint**:
- "First, I'd clarify: Is this a 30% cut to total Azure spend, or to the platform team budget?"
- "Is this permanent, or a one-time cut for one quarter?"
- "What's driving this? Revenue miss, cost overrun elsewhere, or strategic reprioritization?"

**Step 2 - Categorize platform costs**:
Typical breakdown:
- **Compute** (Databricks): 40-50% of cost
- **Storage** (ADLS): 15-20% of cost
- **Networking** (VNet, Private Endpoints, egress): 5-10% of cost
- **Other** (Key Vault, monitoring, backups): 10-15% of cost
- **Platform team** (people cost): 20-30% of total program cost

**Step 3 - Identify quick wins (no impact to SLA)**:
Cut these first:
1. **Idle resources** (5-10% savings):
   - Terminate clusters idle >1 hour
   - Delete orphaned storage accounts, disks
   - Audit underutilized VMs (CPU <10%)
2. **Spot VMs for dev/test** (10-15% savings):
   - Move all non-prod workloads to Spot VMs
3. **Storage lifecycle** (5% savings):
   - Aggressive lifecycle policies (Cool tier after 30 days, Archive after 90 days)
4. **Right-sizing** (5-10% savings):
   - Downsize over-provisioned clusters (review cluster metrics)

**Total quick wins**: 25-40% savings with no SLA impact

**Step 4 - If deeper cuts needed, make trade-offs**:
- **Option A - Delay features** (protect BAU):
  - Pause Knowledge Graph and Agentic AI work (Phase 4)
  - Focus on core data platform (Bronze/Silver/Gold)
  - Savings: Platform team capacity (people cost)
- **Option B - Reduce data freshness** (protect features):
  - Change pipeline frequency (hourly → daily)
  - Reduce Gold layer materialization (daily → weekly for low-priority metrics)
  - Savings: Compute cost (fewer pipeline runs)
- **Option C - Scope reduction** (protect quality):
  - Onboard only 1 segment team, delay others (NA O&T first)
  - Reduce breadth (focus on high-value use cases)
  - Savings: Storage, compute, people cost

**Step 5 - What I'd protect (non-negotiable)**:
- **Security**: No compromise on encryption, access control, audit logging
- **Governance**: Unity Catalog, compliance checks (risk of rogue data is too high)
- **Reliability**: DR infrastructure (GRS storage, secondary region backups)
- **Core platform**: Bronze/Silver/Gold layers (foundation for everything else)

**Recommendation**:
"I'd propose:
1. Quick wins (25% savings, no impact)
2. Delay Phase 4 (Knowledge Graph) by 1 quarter (5% savings)
Total: 30% cut achieved, no impact to current users, delay innovation by 3 months

Alternative: If innovation is non-negotiable, reduce data freshness (hourly → daily) for non-critical pipelines."

**Key Point**: "Budget cuts are about trade-offs. I'd present options with clear impact analysis, then let leadership decide based on business priorities."

---

## General Tips for Mock Interview Practice

### 1. Practice Out Loud
- Don't just read - practice answering out loud
- Record yourself, listen back
- Aim for concise answers (2-3 minutes), not monologues (10 minutes)

### 2. Use the STAR Format
- Situation, Task, Action, Result
- Quantify results ("reduced costs by 30%", "achieved 99.95% uptime")

### 3. Ask Clarifying Questions
- Don't jump to answers - ask questions first
- Shows depth of thinking and structured approach

### 4. Be Honest About Gaps
- If you don't know, say: "I haven't done that specifically, but here's how I'd approach it..."
- Shows learning agility

### 5. Use Frameworks Naturally
- Reference Azure WAF pillars and TOGAF ADM, but don't over-do it
- "This aligns with the WAF Reliability pillar..." (natural)
- "As TOGAF Phase G states..." (sounds robotic)

### 6. Show Humility and Confidence
- "I might be wrong, but here's my thinking..."
- "I'm confident we can solve this, but I need to understand the constraints first..."

---

## Follow-up Questions to Prepare For

These are common "gotcha" questions to test depth:

1. **"How would you handle a situation where your architecture decision was technically correct but politically unpopular?"**
   - Tests: Leadership, pragmatism, stakeholder management

2. **"Tell me about a time your architecture failed in production. What did you learn?"**
   - Tests: Humility, learning from failure, blameless post-mortems

3. **"If you could only implement 3 of the 5 Azure WAF pillars due to budget constraints, which would you choose and why?"**
   - Tests: Prioritization, trade-off analysis

4. **"How do you stay current with rapidly changing technology (Databricks releases every month, Azure announces new services weekly)?"**
   - Tests: Continuous learning, technology radar, pragmatism vs chasing shiny objects

5. **"Describe a time when you had to convince a senior executive to change their mind on a technical decision."**
   - Tests: Communication skills, influencing without authority, data-driven decisions

---

## Mock Interview Role-Play Exercise

**Practice with a colleague**:
1. Give them this document
2. Have them ask questions from Scenarios 1-6
3. Answer without looking at notes
4. Get feedback on:
   - Clarity of answer
   - Confidence level
   - Use of examples
   - Handling of follow-up questions

**Variation**:
- Have them interrupt you mid-answer with "Wait, I don't understand - explain that differently"
- Tests your ability to adjust communication style on the fly

---

Good luck with your interview! Remember: **Listen, Think, Structure, Answer, Provide Example.** 🚀
