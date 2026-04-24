# Second Round Interview - Quick Reference Cheatsheet
## Keep This Open During Interviews

---

## Interviewer Quick Profiles

### Shawn Borkar (Enterprise Data Strategy)
- **Background**: 15+ yrs Chevron → Quorum Office of CTO
- **Keywords**: Enterprise architecture, Azure, energy domain, business value, data monetization
- **What He Wants**: Strategic thinking + Azure depth + energy understanding

### Jonathan Birkholz (CTO, AI Strategy)
- **Background**: 20 yrs SaaS, founded Landdox → Quorum CTO, 30+ products, hands-on coder
- **Keywords**: Agentic AI, knowledge graphs, microservices, practical AI at scale
- **What He Wants**: Agentic AI confidence + hands-on tech + pragmatic solutions

### Flower P (SVP Product Portfolio)
- **Background**: 20+ yrs IT, 10+ yrs senior product mgmt, Midstream & Measurement segment
- **Keywords**: Product ROI, team collaboration, business results, operational excellence
- **What She Wants**: Product alignment + measurable outcomes + team enabler

### Eralp P (Solution Architect)
- **Background**: 13 yrs multi-platform solutions, managerial experience
- **Keywords**: Solution architecture, integration complexity, technical depth
- **What He Wants**: Technical credibility + integration patterns + problem-solving

### Brent Turner (Senior Architect)
- **Background**: Senior Architect at Quorum
- **Keywords**: Architecture standards, platform scalability, governance
- **What He Wants**: Technical validation + standards alignment

---

## Your Credibility Numbers (Use These!)

- **Scale**: Designed platform for **200+ concurrent users**, **11K+ queries/day**
- **Migration**: Led **Oracle EBS (8 modules) + Teradata → Databricks**, **2-year program**
- **Performance**: Reduced report time **2 hours → 3 minutes (40x improvement)**
- **Cost**: Achieved **30% cloud cost reduction** via optimization
- **Streaming**: Worked with Kafka at **~130 topics scale**
- **Data Quality**: Implemented **80% pass threshold** with Great Expectations quarantine
- **SLAs**: Designed **P0-P3 tiered SLAs** with 99.9% uptime target
- **Retention**: Architected **Gold (3 years) → Archive (7 years, Glacier)** lifecycle

---

## Azure Services Quick Reference (Address First Round Gap!)

| Service | Quorum Use Case | Your Experience |
|---------|----------------|-----------------|
| **ADLS Gen2** | Bronze/Silver/Gold storage | ✅ Used for medallion architecture |
| **Event Hubs** | Real-time ingestion (SCADA, meters) | ⚠️ Comparable to Kafka experience |
| **Azure Data Factory** | Batch orchestration | ✅ Used for pipeline orchestration |
| **Azure Synapse** | Analytics serving layer | ✅ Used for BI workloads |
| **Azure Purview** | Lineage, catalog | ⚠️ Learning (mention integration with Unity Catalog) |
| **Key Vault** | Secrets management | ✅ Standard pattern for API keys, DB creds |
| **Private Link** | Secure VNet connectivity | ⚠️ Learning (mention Databricks → ADLS private endpoints) |
| **Azure API Management** | Data product APIs, rate limiting | ⚠️ Conceptual (designed pattern for monetization) |
| **Microsoft Fabric** | OneLake unified storage | ⚠️ Researched (mention Power BI + Databricks integration) |

**Strategy**: For ⚠️ items, say "I've designed patterns for this, currently deepening hands-on experience."

---

## Knowledge Graph Fast Facts

**What You Said Round 1**: "Limited experience, done graph modeling in labs only, open about gap."

**What to Say Round 2**:
- "Since our last conversation, I've researched Neo4j and Azure Cosmos DB for Graph."
- "Studied PPDM (Petroleum Product Data Model) for energy ontology."
- "Proposing **6-week PoC sprint**: model Wells/Leases/Meters, build 2 MCP servers, demo 1 agent workflow."
- "Confidence level: **60% today → 90% in 6 weeks** via hands-on learning."

**Simple KG Example** (Wells → Leases):
```
(Well)-[:LOCATED_AT]->(Location)
(Well)-[:BELONGS_TO]->(Lease)
(Well)-[:HAS_METER]->(Meter)
(Meter)-[:RECORDS]->(ProductionEvent)
(Lease)-[:COVERS]->(LandParcel)
```

**MCP Server Concept**: Each Gold dataset exposes API via MCP protocol → agents call these to retrieve data → Unity Catalog RBAC applies.

---

## Multi-Region DR/HA (Address First Round Gap!)

**What You Missed Round 1**: Specifics on RPO/RTO, cross-region replication, failover.

**What to Say Round 2**:
- **Pattern**: Active-Active across Azure paired regions (East US + West US)
- **RPO**: < 1 hour (Event Hubs continuous ingestion)
- **RTO**: < 4 hours (DNS failover + Unity Catalog metastore sync)
- **ADLS Replication**: Use Azure GRS (Geo-Redundant Storage) for disaster recovery
- **Unity Catalog**: Replicate metastore metadata via Delta Sharing or manual sync
- **Data Residency**: EU customers' data stays in EU region (GDPR)
- **Failover Test**: Quarterly DR drills—switch traffic to secondary region, validate data freshness

---

## Tenant Onboarding IaC Blueprint (Address First Round Gap!)

**What You Missed Round 1**: Detailed IaC/CI-CD for tenant bootstrap.

**What to Say Round 2**:
1. **Terraform Module**: `module "tenant_onboard"` with parameters (tenant_id, region, data_sources, SLAs)
2. **Provisions**: ADLS containers, Unity Catalog schemas, Key Vault secrets, Grafana dashboards
3. **GitHub Actions Trigger**: PR with tenant YAML file → Terraform plan → policy check (OPA) → apply → integration test
4. **Data Contracts**: JSON schema per source system, Bronze ingestion validates, alerts on drift
5. **Policy-as-Code**: OPA enforces rules (e.g., Gold tables need encryption tags, Silver must have DQ checks)

**Result**: Onboard new tenant in **< 1 day** (automated), not weeks.

---

## Energy Domain Key Terms (Show You're Learning!)

| Term | Meaning | Quorum Context |
|------|---------|----------------|
| **PPDM** | Petroleum Product Data Model (industry standard) | Use for Knowledge Graph ontology |
| **OSDU** | Open Subsurface Data Universe (cloud data platform) | Chevron uses this—ask Shawn if Quorum aligns |
| **SCADA** | Supervisory Control and Data Acquisition (real-time from wells) | Event Hubs ingestion source |
| **Production Allocation** | Dividing output among joint venture partners | Complex Silver MDM logic |
| **Lease Lifecycle** | Land rights from acquisition → expiration | Knowledge Graph relationship |
| **Joint Venture (JV)** | Multiple companies co-own wells/production | Multi-tenant pattern analogy |
| **Midstream** | Transportation, storage (pipelines, tanks) | Flower's product portfolio |
| **Upstream** | Exploration, drilling, production | One of Quorum's 3 segments |

**When to Use**: Drop 1-2 terms naturally—"For SCADA telemetry, Event Hubs handles real-time ingestion..." Shows domain curiosity.

---

## STAR Examples (Ready to Tell)

### STAR #1: Complex Migration Success
- **Situation**: Company had 8 Oracle EBS modules + Teradata, fragmented reporting
- **Task**: Migrate to unified Databricks lakehouse
- **Action**:
  - Designed medallion architecture with Silver MDM
  - Strangler Fig pattern—migrated high-value domains first
  - Parallel run for 6 months to build trust
  - Trained 200+ users on new platform
- **Result**:
  - 40x faster reports (2 hrs → 3 min)
  - 30% cost reduction
  - 200+ users adopted in 6 months

### STAR #2: Conflict Resolution (Platform vs Product Team)
- **Situation**: Product team wanted direct DB access to skip MDM (faster development)
- **Task**: Enforce platform guardrails without alienating team
- **Action**:
  - Ran 2-week PoC—their approach vs MDM approach
  - Measured bugs, schema change handling, performance
  - MDM had 15 fewer bugs, handled schema changes automatically
- **Result**: Team voluntarily adopted MDM after seeing data

### STAR #3: Innovation (Data Quality Automation)
- **Situation**: Customers complained about bad data in reports
- **Task**: Implement automated DQ checks
- **Action**:
  - Integrated Great Expectations into pipelines
  - Set 80% pass threshold—below that, quarantine data
  - Built Grafana dashboard tracking DQ trends per source system
- **Result**:
  - 60% reduction in data quality incidents
  - Proactive identification of source system issues

---

## Tough Questions - Quick Answers

### "Why you vs someone with energy domain experience?"
**Answer**: "Deep technical expertise + domain adaptability > shallow domain + weak technical. I've delivered in finance (Oracle EBS, SOX) and insurance (regulatory reporting). Energy has nuances (PPDM, OSDU), but data engineering fundamentals are domain-agnostic. I'll ramp via pairing with your SMEs. Within 90 days, I'll be fluent. Shawn and Jonathan provide domain leadership—I bring architectural execution."

### "How confident in Knowledge Graphs?"
**Answer**: "Honest: **60% today → 90% in 6 weeks**. Plan: Neo4j cert, PPDM study, Wells/Leases PoC, MCP server demo. I'm demonstrating **learning velocity + hands-on execution**. If Quorum has KG expert, I'll co-develop. If not, I'll bring Neo4j consultants short-term for knowledge transfer."

### "Why contractor vs FTE?"
**Answer**: "Three reasons:
1. **Speed**: Start in 2-4 weeks vs 3-6 months FTE hire
2. **Specialized expertise**: Databricks + Azure + KG + DevOps is rare combo
3. **Knowledge transfer focus**: Enable your team, not build dependency
Open to FTE conversion if strategic fit emerges. Outcome-focused—engagement model is secondary."

### "How handle teams bypassing guardrails?"
**Answer**: "Framework:
1. Understand 'why'—usually speed or capability gaps
2. Propose alternatives—exception process or extend platform capability
3. Escalate with data if safety at risk (e.g., bypassing RBAC)
4. Build trust—prove platform value early, teams adopt voluntarily
Example: [Use STAR #2 above]"

---

## Questions to Ask (Pick 2-3 Per Interviewer)

### For Shawn Borkar
1. "How does Chevron's OSDU Data Platform influence Quorum's architecture? Are you aligning with OSDU standards?"
2. "What's current Azure environment maturity—greenfield or existing landing zones?"
3. "For data monetization, is Quorum productizing datasets externally (to operators/midstream) or just internal value?"

### For Jonathan Birkholz
1. "What agent use cases are you prioritizing—internal productivity (code gen) or customer-facing (production insights)?"
2. "Proprietary model training vs fine-tuning foundation models (OpenAI, Anthropic, Azure OpenAI)—what's your strategy?"
3. "Long-term vision for microservices ecosystem—API mesh, service mesh (Istio), or event-driven with Kafka/Event Hubs?"

### For Flower P
1. "What product features are delayed due to data integration challenges across segments?"
2. "How do you measure product success—ARR growth, NPS, feature adoption? Can platform directly contribute?"
3. "What's biggest operational pain for your Midstream & Measurement product teams?"

### For Eralp P / Brent Turner
1. "Current pain points in Quorum's data pipelines—performance, reliability, maintainability?"
2. "Any architectural standards or guardrails already established that I should align with?"
3. "How does Quorum handle disaster recovery for customer products? Should data platform match those RPO/RTO SLAs?"

---

## Opening Lines Per Interviewer

### Shawn Borkar
*"Shawn, I've spent the last decade architecting data platforms at enterprise scale—migrating Oracle EBS and Teradata to Databricks lakehouses serving 200+ users with 11K+ queries daily. What resonates with your Chevron experience is transforming fragmented ecosystems into unified, monetizable assets. At Ethniki Insurance, I'm designing an AI platform integrating 9+ legacy systems—similar to Quorum's TIPS/QPTM/eONE/FLOWCAL challenge."*

### Jonathan Birkholz
*"Jonathan, your work operationalizing AI at scale across 30+ products resonates with my current Ethniki project—building Intelligent Document Processing with RAG handling 5,000 emails/day. I'm hands-on with Python, PySpark, and increasingly LangChain/LlamaIndex for agentic patterns. What excites me is applying agentic AI to energy—like agents autonomously navigating Land + Production + Accounting knowledge graphs to answer 'What's our forecast if crude drops to $60?'"*

### Flower P
*"Flower, I understand you're driving results across Midstream & Measurement while overseeing Product Operations. In my last program, architecture decisions aligned with product ROI—reducing report time 2 hours → 3 minutes unlocked $2M annual productivity savings. At Quorum, I see the data platform as a strategic product itself—unlocking new revenue streams (data products), reducing churn (better insights), accelerating feature velocity (less data plumbing)."*

### Eralp P / Brent Turner
*"I've designed multi-platform architectures integrating legacy (Oracle, Teradata) with modern (Databricks, Kafka) and cloud-native (AWS, Azure). For Quorum, complexity is horizontal (TIPS/QPTM/eONE/FLOWCAL sources) and vertical (Bronze → Silver MDM → Gold → Knowledge Graph). I focus on patterns that reduce complexity—reusable frameworks, medallion architecture, Unity Catalog governance—while maintaining product-specific flexibility."*

---

## Closing Lines Per Interviewer

### Shawn Borkar
*"Shawn, I'm energized by this. Transforming Quorum's fragmented data into a unified Knowledge Graph powering agentic AI—that's high-impact, complex work I thrive on. My Oracle EBS migration proves I handle enterprise-scale complexity. Now I'm ready to apply that to energy. If you need someone who can architect Azure + Databricks foundations, co-engineer with your team, and drive toward a monetizable platform, I'm confident I can deliver. What concerns or gaps do you see that I should address?"*

### Jonathan Birkholz
*"Jonathan, your vision of practical AI at enterprise scale resonates deeply. I want to make agentic AI real for energy operators—not demos, production systems. I'll bring hands-on rigor, fast learning on KGs, and focus on solving problems vs buzzwords. Give me a shot, I'll prove value in 30 days with a working KG PoC. What's your biggest worry about whether I can ramp fast enough on agentic AI?"*

### Flower P
*"Flower, I see the data platform as a product enabling your Midstream & Measurement portfolio—and all Quorum products—to deliver cross-product intelligence competitors can't match. I'll partner with your teams to align platform with roadmaps and drive measurable ROI. My track record shows I balance innovation with operational excellence. How can I best support your goals as SVP?"*

### Eralp P / Brent Turner
*"I respect the architectural complexity you're navigating—multi-region, multi-tenant, Azure + Databricks, legacy integration. I've been in those trenches. I'd welcome your technical pushback—let's whiteboard hard problems together. If there are specific areas you'd test my depth (performance tuning, IaC, DR design), I'm ready. What architecture challenges keep you up at night?"*

---

## Red Flags to AVOID

❌ **Over-claiming**: Stay honest about KG gaps (show learning plan)
❌ **Bashing legacy**: TIPS/FLOWCAL are Quorum's products—respect them, "evolution" not "replacement"
❌ **Ignoring energy domain**: Show genuine interest (PPDM, OSDU references)
❌ **Purely theoretical**: Tie architecture to business outcomes or past delivery examples
❌ **Defensive on gaps**: "I hear you—here's how I've addressed that since..."

---

## Confidence Reminders

✅ **You passed the first round**—they see potential
✅ **You have deep Databricks expertise** (Unity Catalog, DLT, medallion)
✅ **You've led complex migrations** (Oracle EBS, Teradata → Databricks)
✅ **You understand enterprise governance** (SOX, RBAC/ABAC, DQ)
✅ **You're hands-on** (PySpark, Terraform, CI/CD)
✅ **You're a fast learner** (demonstrated in past roles)
✅ **You have operational maturity** (SLAs, monitoring, triage)

**They're assessing**:
- Can you learn fast? (Azure, KG, Energy domain)
- Can you execute? (IaC, pipelines, co-engineering)
- Can you collaborate? (Hub-and-spoke, knowledge transfer)
- Do you fit culturally? (Innovation mindset, advisory approach)

---

## Tech Setup Checklist (Day Of)

- [ ] Test video/audio 30 min before
- [ ] Have this cheatsheet open on second monitor
- [ ] Have draw.io or whiteboard tool ready for diagrams
- [ ] Water nearby
- [ ] Clean background
- [ ] Phone on silent
- [ ] Close unneeded browser tabs/apps
- [ ] Have GitHub/LinkedIn profiles ready if they ask for examples

---

## Breathing Exercise (If Nervous)

**4-7-8 Technique**:
1. Inhale through nose for 4 seconds
2. Hold for 7 seconds
3. Exhale through mouth for 8 seconds
4. Repeat 3-4 times

**You've got this!** 💪🚀
