# Second Round Interview Preparation Guide
## Quorum Data & AI Platform - Data Solution Architect Role

**Candidate**: Sai (Sina Garajou)
**Interview Date**: TBD
**Duration**: Likely 45-60 minutes per interviewer panel
**Format**: Technical deep-dive with multiple stakeholders

---

## Executive Summary

### First Round Performance
**Overall**: Cautious Pass - Strong Databricks/lakehouse foundation, needs depth in Azure-native and agentic AI

**Strengths Demonstrated**:
- ✅ Databricks lakehouse architecture (medallion, Unity Catalog, DLT)
- ✅ Multi-tenant patterns with RBAC
- ✅ Kafka streaming at scale (~130 topics)
- ✅ Operational maturity (SLAs, monitoring, triage)
- ✅ IaC/CI-CD with Terraform/GitHub Actions
- ✅ Data quality frameworks (Great Expectations)

**Gaps to Address in Round 2**:
- ⚠️ **Azure-native services** (Event Hubs, Fabric vs Synapse, Purview, Key Vault, Private Endpoints)
- ⚠️ **Knowledge graphs/ontologies** for agentic AI/MCP integration
- ⚠️ **Multi-region DR/HA specifics** (RPO/RTO, cross-region replication)
- ⚠️ **Reusable IaC/CI-CD blueprints** for tenant onboarding
- ⚠️ **Trade-off articulation** (RBAC vs ACLs, zero-ETL patterns, monetization)

---

## Second Round Interviewers

### 1. **Shawn Borkar** - Head of Enterprise Data Architecture & Strategy
**Background**: 15+ years energy sector (Chevron 11+ yrs), product/engineering leader, Office of CTO at Quorum

**What He Cares About**:
- Strategic enterprise architecture that drives business value
- Azure + Databricks alignment with energy workflows
- Data monetization and board-level decision support
- Transforming fragmented ecosystems into scalable assets
- Partner co-innovation and product roadmap acceleration

**His Interview Focus**: Strategy, Azure architecture, energy domain, business value

---

### 2. **Jonathan Birkholz** - CTO, AI & Platform Strategy
**Background**: 20 years SaaS (startups + enterprise), founded/exited Landdox ($20M acquisition), leads AI strategy across 30+ Quorum products, 300+ engineers, 6 countries

**What He Cares About**:
- Agentic AI platform that's practical at enterprise scale
- Unified data across 30+ product lines
- Microservices architecture connecting Quorum's SaaS suite
- Hands-on engineering execution (Elixir, Ruby, JavaScript, C#, Python)
- Operationalizing AI coding tools, rethinking software delivery

**His Interview Focus**: Agentic AI, knowledge graphs, microservices, practical AI implementation

---

### 3. **Flower P** - SVP, Midstream & Measurement Product Portfolio
**Background**: 20+ years IT/software, 10+ years senior product management, oversees major business segment + Product Operations

**What She Cares About**:
- Product ROI and business outcomes
- High-performing teams and innovative methods
- Results-driven execution aligned with product strategy
- Cross-portfolio integration and operational excellence
- New management methodologies and next-trend technologies

**Her Interview Focus**: Product alignment, team collaboration, business results, operational rigor

---

### 4. **Eralp P** - Solution Architect
**Background**: 13 years custom software/hardware solutions, multi-disciplinary projects, managerial experience

**What He Cares About**:
- Solution architecture for dynamic/complex business requirements
- Multi-platform integration and system design
- Problem-solving through established engineering practices
- Technical implementation details

**His Interview Focus**: Solution architecture patterns, integration complexity, technical depth

---

### 5. **Brent Turner** - Senior Architect
**Background**: Senior Architect at Quorum (limited public info)

**What He Cares About**: Likely technical architecture standards, platform scalability, governance

**His Interview Focus**: Architecture review, technical validation

---

## Interview Strategy by Stakeholder

### Strategy for Shawn Borkar (Enterprise Data Architecture Leader)

#### Opening Positioning (First 2 minutes)
*"Shawn, I've spent the last decade architecting data platforms for enterprise finance at scale—migrating legacy systems like Oracle EBS and Teradata to modern Databricks lakehouses serving 200+ concurrent users with 11K+ queries daily. What resonates with your energy domain experience at Chevron is the challenge of transforming fragmented data ecosystems into unified, monetizable assets. At Ethniki Insurance, I'm currently designing an AI-powered RFP platform that integrates 9+ legacy systems—similar to Quorum's challenge with TIPS, QPTM, eONE, and FLOWCAL."*

#### Key Topics to Cover

**1. Azure + Databricks for Energy Workflows**
- **Your Story**: "At my current program, we're Azure-native: ADLS Gen2 for medallion layers, Azure Data Factory for orchestration, Databricks for transformation, and Synapse for analytics. For Quorum's energy data, I'd architect a similar pattern but leverage **Microsoft Fabric OneLake** for unified storage across Power BI, Databricks, and potential real-time analytics via Event Hubs."
- **Azure Services Depth**:
  - **ADLS Gen2**: Zone-based storage (bronze/silver/gold containers), lifecycle policies for archival
  - **Event Hubs**: Real-time ingestion from production meters, SCADA systems (vs Kafka for cross-cloud)
  - **Azure Purview**: Lineage tracking from source (TIPS) → Bronze → Silver MDM → Gold → AI agents
  - **Key Vault**: Secrets for API connections to Quorum products, OAuth tokens, DB credentials
  - **Private Endpoints**: Secure connectivity between Databricks VNets and ADLS, no public internet exposure
- **Energy Domain Bridge**: "Energy workflows have unique patterns—SCADA telemetry from wells, land lease lifecycles, production allocation across joint ventures. These require real-time + batch patterns, and Azure's Event Hubs + Databricks Autoloader combination handles this elegantly."

**2. Data Monetization Architecture**
- **Your Approach**: "Quorum's Knowledge Graph can power **data products as a service**. I'd design Gold layer datasets with consumption metering:
  - **Azure API Management** as the front door: rate limiting, quota enforcement per customer tier
  - **Delta Sharing** for zero-ETL distribution with usage tracking via Unity Catalog audit logs
  - **Cost allocation tags** at Bronze ingestion → track compute costs per product segment → chargeback model
  - **SLA tiers**: P0 (real-time production data for agents), P1 (daily analytics), P2 (historical archive)"
- **Business Value Articulation**: "This enables Quorum to monetize data beyond traditional SaaS licenses—offering production optimization insights, land valuation analytics, or regulatory compliance datasets as standalone products."

**3. Transformation Strategy (Fragmented → Unified)**
- **Your Story**: "I led a 2-year migration from 8 Oracle EBS modules and Teradata to unified Databricks. Key lessons:
  1. **Strangler Fig Pattern**: Built Silver layer MDM for Meters/Locations first (your TIPS/FLOWCAL challenge), proved value, then expanded
  2. **Anti-Corruption Layer**: Bronze adapters for each legacy system, isolate their complexity
  3. **Parallel Run**: Ran legacy and Databricks side-by-side for 6 months, reconciled daily, built trust
  4. **Golden Record in Silver**: Used Informatica MDM patterns in Spark—dedupe rules, survivorship logic, stewardship workflows"

**4. Board-Level Decision Support**
- **Your Pitch**: "The Knowledge Graph isn't just for AI agents—it's for executive dashboards. Imagine Quorum's CEO asking: 'Which customers have the highest production decline risk?' The graph links **Land entities → Lease expirations → Production trends → Equipment maintenance → Accounting revenue impact** in real-time. That's board-level intelligence."

#### Questions to Ask Shawn
1. "How does Chevron's OSDU Data Platform influence Quorum's architecture thinking? Are you aligning with OSDU standards?"
2. "What's the current Azure environment maturity at Quorum—greenfield or existing landing zones?"
3. "For data monetization, is Quorum considering productizing datasets externally (to operators/midstream) or just internal value?"

---

### Strategy for Jonathan Birkholz (CTO, AI Strategy)

#### Opening Positioning (First 2 minutes)
*"Jonathan, your work operationalizing AI at scale across 30+ products resonates with my current challenge at Ethniki Insurance—building an Intelligent Document Processing platform with RAG that must handle 5,000 emails/day and integrate with 9 enterprise systems. I'm hands-on with Python, PySpark, and increasingly with LangChain/LlamaIndex for agentic patterns. What excites me about Quorum is applying agentic AI to energy domain problems—like an agent autonomously answering 'What's our production forecast if crude drops to $60/bbl?'—navigating Land, Production, and Accounting knowledge graphs to reason across product boundaries."*

#### Key Topics to Cover

**1. Agentic AI Platform Architecture**
- **Your Understanding**: "Agentic AI requires three layers:
  1. **Knowledge Graph (Semantic Layer)**: Unified ontology of energy entities (Wells, Leases, Meters, Products, Locations)
  2. **Tool Registry (MCP Servers)**: Microservices that agents call to retrieve data, execute workflows, or write back results
  3. **Agent Orchestration**: LangGraph or similar framework for multi-step reasoning, planning, tool invocation"
- **Your Proposed Stack**:
  - **Ontology**: Start with **Neo4j** or **Azure Cosmos DB for Graph** (if staying Azure-native). Model PPDM entities (Petroleum Product Data Model standard).
  - **MCP Server Pattern**: Each Gold dataset exposes an MCP server via Azure Functions or FastAPI on AKS. Unity Catalog RBAC ensures agents respect access controls.
  - **Vector Search**: Azure AI Search + embeddings for semantic queries over production reports, land documents
  - **Agent Framework**: LangGraph for complex workflows (e.g., "Analyze this lease, predict production, estimate NPV, recommend renewal terms")
- **First Round Gap Addressed**: "I acknowledged limited KG experience in round 1. Since then, I've researched Neo4j's graph data science library and Azure's Knowledge Mining accelerators. I'm proposing a **6-week PoC sprint**: model 3 entity types (Wells, Leases, Meters), build 2 MCP servers, demonstrate one agent workflow end-to-end."

**2. Practical AI at Enterprise Scale**
- **Your Story**: "At Ethniki, we're implementing AI governance:
  - **Model registry** (MLflow on Databricks): version control for embeddings, classification models
  - **Prompt templates** versioned in Git, tested via CI/CD
  - **Hallucination detection**: Compare agent outputs to ground truth Gold data, flag anomalies
  - **Cost controls**: Track token consumption per agent call, set quotas per user/product segment"
- **Quorum Application**: "For 300 engineers across 30 products, you need **AI platform as a service**:
  - Self-service agent templates (e.g., 'Query Production Data Agent')
  - Shared MCP server registry (discover available tools)
  - Centralized observability (trace agent calls → tools → data lineage)"

**3. Microservices Architecture for Data Access**
- **Your Approach**: "Quorum's 30 products can't directly query Databricks Gold—latency and concurrency challenges. I'd design:
  - **Read-optimized serving layer**: Azure Cosmos DB or Azure SQL caching Gold aggregates
  - **GraphQL API** over the Knowledge Graph for flexible queries
  - **Event-driven sync**: When Gold tables update (via Delta Lake CDC), push changes to serving layer
  - **API gateway** (Azure API Management): rate limiting, authentication, telemetry per product"

**4. Hands-On Engineering Mindset**
- **Your Credibility**: "I write production PySpark code daily, not just architecture diagrams. For Quorum's IaC, I use **Databricks Asset Bundles** (DABs) to deploy pipelines/notebooks/jobs as code. For agent workflows, I'd pair-program with your team in Python, building MCP servers using FastAPI. I believe architects must validate their designs in code."

#### Questions to Ask Jonathan
1. "What agent use cases are you prioritizing first—internal productivity (code generation) or customer-facing (production insights)?"
2. "How are you thinking about proprietary model training vs fine-tuning foundation models (OpenAI, Anthropic, Azure OpenAI)?"
3. "What's your long-term vision for the microservices ecosystem—API mesh, service mesh (Istio), or event-driven with Kafka/Event Hubs?"

#### Demo/Artifact to Offer
"If helpful, I can build a mini PoC before a final round: A simple Knowledge Graph (Wells → Production data) with one MCP server, and a Python agent that queries it using LangChain. Would take me ~3 days to prototype on my local Databricks environment."

---

### Strategy for Flower P (SVP, Product Portfolio)

#### Opening Positioning (First 2 minutes)
*"Flower, I understand you're driving results across Midstream & Measurement products while overseeing Product Operations. In my last program, I aligned architecture decisions with product ROI—for example, reducing report generation time from 2 hours to 3 minutes unlocked $2M in annual productivity savings for 200 finance users. At Quorum, I see the data platform enabling cross-product intelligence as a strategic product itself—unlocking new revenue streams (data products), reducing churn (better insights keep customers sticky), and accelerating feature velocity (teams spend less time on data plumbing)."*

#### Key Topics to Cover

**1. Product-Driven Architecture Decisions**
- **Your Framework**: "I use a **Product Value Canvas** for architecture:
  - **User Jobs to Be Done**: What are Midstream product users trying to accomplish? (e.g., optimize pipeline throughput, detect measurement anomalies)
  - **Data Requirements**: What data from other products would help? (e.g., Upstream production forecasts → Midstream capacity planning)
  - **Architectural Enablers**: What platform capabilities unlock this? (e.g., Gold layer 'Measurement Events' dataset with real-time SLAs)
  - **Success Metrics**: How do we measure value? (e.g., 50% reduction in manual data reconciliation time)"
- **Quorum Example**: "For Midstream & Measurement, the Knowledge Graph can link **Meter readings → Product movements → Accounting entries** automatically. Today, operators manually reconcile these. Platform eliminates that pain."

**2. Cross-Portfolio Integration**
- **Your Story**: "I integrated 8 Oracle EBS modules (AP, AR, GL, FA, etc.) into unified Gold models. Each module had its own team (like your product segments). Key to success:
  - **Shared data standards**: Defined 'Customer' and 'Product' dimensions in Silver MDM, all Gold models use them
  - **Federated ownership**: Each product team owns their Gold datasets, Platform team owns Silver MDM
  - **Contract testing**: If one team changes a Silver schema, CI/CD catches downstream breakage
  - **Incentive alignment**: Product teams got credit for enabling cross-product features (KPIs included 'data reuse' metrics)"

**3. Operational Excellence & Team Collaboration**
- **Your Approach**: "I run weekly **Platform <> Product sync** meetings:
  - Product teams present upcoming features requiring new data
  - Platform team assesses feasibility, estimates effort, commits to SLAs
  - We maintain a **Data Request Backlog** in Jira, prioritized by business value
  - Metrics dashboard: Platform uptime (99.9% SLA), pipeline SLAs, data quality scores"
- **For Flower**: "This ensures Product Operations visibility into platform health and alignment with product roadmaps."

**4. ROI and Business Outcomes**
- **Your Track Record**: "Examples of measurable impact:
  - **Cost**: Reduced cloud spend 30% via spot instances for non-prod, archival policies (Gold 3 yrs → Glacier 7 yrs)
  - **Speed**: Accelerated report delivery 40x (2 hours → 3 minutes), enabling daily close vs monthly
  - **Revenue**: Enabled new analytics product line by exposing Gold datasets via APIs (conceptually, your data monetization opportunity)"
- **Quorum Opportunity**: "If Quorum can surface unified Production + Land + Accounting insights, you could offer 'Quorum Intelligence' as a premium tier—customers pay for predictive analytics beyond transactional software."

#### Questions to Ask Flower
1. "What product features are currently delayed due to data integration challenges across segments?"
2. "How do you measure product success—ARR growth, NPS, feature adoption? Can the platform directly contribute to these?"
3. "What's the biggest operational pain point for your Midstream & Measurement product teams today?"

---

### Strategy for Eralp P & Brent Turner (Solution Architects)

#### Opening Positioning (First 2 minutes)
*"I've designed multi-platform data architectures integrating legacy (Oracle, Teradata) with modern (Databricks, Kafka) and cloud-native (AWS, Azure) environments. For Quorum, the complexity is both horizontal (TIPS, QPTM, eONE, FLOWCAL source systems) and vertical (Bronze ingestion → Silver MDM → Gold consumption → Knowledge Graph semantic layer). I focus on patterns that reduce this complexity—reusable ingestion frameworks, medallion architecture, Unity Catalog governance—while maintaining flexibility for product-specific needs."*

#### Key Topics to Cover

**1. Multi-Region, Multi-Tenant Architecture**
- **Your Design**: "Quorum needs global availability with tenant isolation:
  - **Multi-Region Deployment**: Azure paired regions (e.g., East US + West US, Europe + UK)
  - **Active-Active Pattern**: Each region has full Bronze/Silver/Gold stack, Unity Catalog metastore per region
  - **Data Residency**: European customers' data stays in EU region (GDPR compliance)
  - **Replication Strategy**:
    - **Unity Catalog metastore**: Replicate metadata using UC delta sharing or manual sync
    - **ADLS Gen2**: Use Azure Blob replication (GRS) for disaster recovery, but configure geo-blocking for production
    - **RPO/RTO**: RPO < 1 hour (Event Hubs continuous ingestion), RTO < 4 hours (DNS failover + metastore sync)
  - **Multi-Tenancy**: Tenant = Customer (or Product Segment?)
    - **Storage**: ADLS containers per tenant (`/bronze/tenant-123/`, `/silver/tenant-123/`)
    - **Compute**: Shared Databricks clusters with Unity Catalog RBAC (don't need separate clusters per tenant if RBAC is strict)
    - **Cost Allocation**: Tags at container level, track compute per tenant via cluster tags"

**2. Reusable IaC/CI-CD Blueprints for Tenant Onboarding**
- **Your Approach** (Addresses First Round Gap):
  - **Terraform Modules**: `module "tenant_onboard"` takes parameters (tenant_id, region, data_sources, SLAs)
    - Provisions: ADLS containers, Unity Catalog schemas, Azure Key Vault secrets, monitoring dashboards
  - **GitHub Actions Workflow**: Tenant onboarding triggered by YAML file commit:
    ```yaml
    tenant_id: customer-xyz
    region: east-us
    data_sources:
      - type: api
        endpoint: https://tips.customer-xyz.com
        auth: oauth2
    slas:
      ingestion: 15min
      gold_refresh: 1hour
    ```
  - **Policy-as-Code**: Open Policy Agent (OPA) enforces guardrails—e.g., Gold tables must have column-level encryption tags, Silver transformations must include DQ checks
  - **Data Contracts**: Each source system provides JSON schema for their data; Bronze ingestion validates against it, alerts on schema drift

**3. Zero-ETL and Data Sharing Patterns**
- **Your Recommendation** (Addresses First Round Gap):
  - **Delta Sharing** for secure, zero-ETL access: External customers query Gold tables without data duplication
    - **Monetization**: Track query volume via Unity Catalog audit logs → `SELECT tenant_id, table_name, COUNT(*) AS query_count FROM system.access.audit` → billing
    - **Rate Limiting**: Recipient profiles with query quotas (e.g., 10K queries/month for Tier 1 customers)
  - **Azure Fabric Mirroring** for real-time sync to customer Power BI environments (alternative to Delta Sharing)
  - **Observability**: Azure Monitor metrics per recipient—track query latency, failures, data volume transferred

**4. Advanced Spark Performance Tuning**
- **Your Techniques** (Expands First Round Answer):
  - **AQE (Adaptive Query Execution)**: Enable for dynamic join optimization, skew handling
  - **Broadcast Joins**: For dimension tables < 100MB, broadcast to avoid shuffle
  - **Partition Pruning**: Partition Bronze by `ingestion_date`, Silver by `business_date`, Gold by `report_month`
  - **Z-Ordering**: On Gold fact tables for common filter columns (e.g., `ZORDER BY customer_id, transaction_date`)
  - **Photon Engine**: Enable for Databricks SQL queries (3-5x speedup for analytics workloads)
  - **Cluster Policies**: Define presets (e.g., "Small - 2-8 workers, Standard_DS3_v2, autoscale, spot for workers")

**5. Data Quality & Quarantine Strategy**
- **Your Framework** (Strengthens First Round Answer):
  - **Bronze → Silver DQ Gates**:
    - **Great Expectations** rules: Check nulls, ranges, referential integrity (e.g., every `meter_id` in Production must exist in Meters table)
    - **Thresholds**: If < 80% pass, FAIL pipeline → quarantine to `silver_quarantine/` table, send alert
    - **Auto-Remediation**: For known issues (e.g., timezone mismatches), apply fix and reprocess
  - **Observability**: Grafana dashboard showing DQ trends per source system—Quorum can identify which product (TIPS, QPTM) has data issues

#### Questions to Ask Eralp/Brent
1. "What are current pain points in Quorum's existing data pipelines—performance, reliability, maintainability?"
2. "Are there any architectural standards or guardrails already established at Quorum that I should align with?"
3. "How does Quorum handle disaster recovery today for customer-facing products? Should the data platform match those RPO/RTO SLAs?"

---

## Key Talking Points Across All Interviews

### 1. Address First Round Gaps Proactively
*"In our last conversation, I acknowledged gaps in Azure-native services and knowledge graphs. Since then, I've deepened my research—explored Azure Purview for lineage, Private Link for security, and Neo4j for KG modeling. I'm proposing a learning plan: I'd spend my first 2 weeks at Quorum shadowing your Azure team, getting Azure certifications (Azure Data Engineer Associate, AI Engineer), and building a KG PoC. I learn fast when there's real business context."*

### 2. Hub-and-Spoke Operating Model Fluency
*"Quorum's Platform Team as 'Control Tower' model resonates with my experience. At my last program, Platform owned Silver MDM, monitoring, and IaC templates. Product teams (like your segments) owned Gold data products and domain logic. Key to success: Clear contracts, self-service within guardrails, and a feedback loop where segments influence platform roadmap."*

### 3. Energy Domain Credibility (Even Without Deep Experience)
*"While I don't have oil & gas experience, I'm studying PPDM (Petroleum Product Data Model) and OSDU standards. Energy data has unique patterns—hierarchical well structures, joint venture allocation, lease lifecycles. These aren't that different from insurance hierarchies (policies → claims → coverages) I'm currently modeling. I'd plan to pair with your domain SMEs in the first month to deeply understand Quorum's product workflows."*

### 4. Co-Engineering and Knowledge Transfer
*"Quorum emphasized 'extension of our own team' and knowledge transfer. I'm hands-on—I'll pair-program pipelines, run training sessions, document as I build (not at the end), and establish a Community of Practice. My goal is to make Quorum's team self-sufficient, not dependent on consultants. I measure success by how quickly you don't need me anymore—paradoxically, that builds long-term trust."*

### 5. Innovation Mindset
*"Quorum is betting on agentic AI—that's cutting-edge. I'm excited to work at the frontier. For example, I'd experiment with agents that auto-generate SQL from natural language questions, validate outputs against known results, and iteratively improve. This could accelerate your data analysts' productivity 10x. I bring curiosity and willingness to experiment, balanced with production-readiness rigor."*

---

## Potential Tough Questions & How to Answer

### Q: "Why are you the right fit given your limited energy domain experience?"
**Answer**: "Fair question. My philosophy: **deep technical expertise + domain adaptability > shallow domain knowledge + weak technical skills**. I've successfully delivered in finance (Oracle EBS, SOX compliance) and now insurance (regulatory reporting, claims data). Energy has its nuances—PPDM, OSDU, production allocation—but the data engineering fundamentals (medallion architecture, MDM, governance, performance tuning) are domain-agnostic. What I bring is a proven playbook for transforming fragmented legacy systems into modern lakehouse platforms. I'll ramp on energy domain via pairing with your SMEs, and within 90 days, I'll be fluent in Quorum's product workflows. Shawn's Chevron background and Jonathan's platform vision provide strong domain leadership—I complement that with architectural execution."*

### Q: "Knowledge graphs are critical. How confident are you in delivering this?"
**Answer**: "Honest self-assessment: **60% confidence today, 90% in 6 weeks**. Here's my plan:
1. **Week 1-2**: Neo4j certification, study PPDM ontology, prototype Wells → Leases → Production relationships
2. **Week 3-4**: Build first MCP server (e.g., 'Query Production Data'), integrate with simple LangChain agent
3. **Week 5-6**: Demonstrate end-to-end: Agent queries Knowledge Graph → calls MCP server → returns unified insight ('What's total production for this lease?')
I'm not claiming full expertise today—I'm demonstrating **learning velocity and hands-on execution**. If Quorum has an ontology expert, I'll co-develop with them. If not, I'll bring in Neo4j consultants short-term for knowledge transfer."*

### Q: "This is a contractor role with EPAM. Why should we invest in you vs hiring full-time?"
**Answer**: "Three reasons:
1. **Speed**: I can start in 2-4 weeks vs 3-6 months for FTE hire process. Your platform initiative is urgent.
2. **Specialized Expertise**: Databricks + Azure + KG + DevOps is a rare combo. Contractors bring concentrated expertise for platform foundations.
3. **Knowledge Transfer Focus**: My mandate is to enable your team, not build dependency. After 12-18 months, Quorum's team will be self-sufficient, and you'll have optionality to convert me to FTE if there's strategic fit.
Ultimately, I'm outcome-focused—if Quorum's platform succeeds, the engagement model is secondary. I'm open to FTE conversion if it makes sense for both sides."*

### Q: "How do you handle disagreements with product teams who want to bypass platform guardrails?"
**Answer**: "I use a framework:
1. **Understand the 'why'**: Why do they want to bypass? Usually it's speed ('guardrails slow us down') or capability gaps ('platform doesn't support our use case').
2. **Propose alternatives**: 'What if we fast-track your use case via an exception process with monitoring? Or extend the platform capability so it becomes the preferred path?'
3. **Escalation with data**: If safety is at risk (e.g., bypassing Unity Catalog RBAC), I escalate to CTO/Architecture Review Board with risk analysis.
4. **Build trust over time**: Early on, I'm flexible—prove platform value. Once trust is built, teams voluntarily adopt guardrails because they see benefits (security, reliability, reusability).
Example: At my last program, a team wanted direct DB access to skip our Silver MDM (faster, they thought). I ran a 2-week PoC—they used their approach, we used MDM approach. Our approach had 15 fewer bugs and handled schema changes automatically. They adopted MDM voluntarily."*

---

## Technical Deep-Dive Prep: Likely Topics

### 1. Azure Architecture Diagram Exercise
**Scenario**: "Draw the architecture for Quorum's multi-region, multi-tenant data platform."
**What to Include**:
- Azure Landing Zones (hub VNet, spoke VNets per product segment)
- ADLS Gen2 (bronze/silver/gold containers)
- Databricks workspace per region, Unity Catalog metastore
- Event Hubs for streaming, ADF for batch orchestration
- Azure Purview for lineage
- Azure API Management for external consumers
- Private Link endpoints (Databricks → ADLS, no public internet)
- Azure Monitor + Log Analytics for observability
- Azure Key Vault for secrets
- Disaster recovery: Primary (East US) → Secondary (West US), GRS replication for ADLS

### 2. Knowledge Graph Modeling Exercise
**Scenario**: "Model the relationships between Wells, Leases, Meters, Production, and Locations."
**What to Show**:
```
(Well)-[:LOCATED_AT]->(Location)
(Well)-[:BELONGS_TO]->(Lease)
(Well)-[:HAS_METER]->(Meter)
(Meter)-[:RECORDS]->(ProductionEvent)
(Lease)-[:COVERS]->(LandParcel)
(ProductionEvent)-[:ALLOCATED_TO]->(JointVenture)
```
**Explain**: "This graph enables questions like: 'Which leases expiring in 2026 have declining production trends?' Agent traverses: (Lease {expiry_date: 2026})-[:BELONGS_TO]-(Well)-[:HAS_METER]-[:RECORDS]-(ProductionEvent {trend: declining})."*

### 3. CI/CD Pipeline Design Exercise
**Scenario**: "Design the CI/CD pipeline for onboarding a new customer tenant."
**What to Include**:
1. **Trigger**: PR merges to `main` branch with tenant YAML file
2. **Terraform Plan**: Preview infrastructure changes (ADLS containers, Unity Catalog schemas)
3. **Policy Check**: OPA validates tenant config meets governance rules
4. **Terraform Apply**: Provision resources in Azure
5. **Databricks Asset Bundle Deploy**: Deploy ingestion pipelines, DQ notebooks
6. **Integration Test**: Simulate ingestion from sample data, validate Silver transformation
7. **Monitoring Setup**: Create Grafana dashboard for new tenant
8. **Notification**: Slack message to Platform team + Segment team with tenant details

### 4. Performance Tuning Scenario
**Scenario**: "A Gold aggregation query takes 45 minutes. Walk me through your diagnosis."
**Your Steps**:
1. **Spark UI**: Identify longest stage (likely shuffle or wide transformation)
2. **Query Plan**: Check for full table scans vs partition pruning
3. **Data Skew**: Look for executor imbalance (one executor has 10x more data)
4. **Remediation**:
   - Enable AQE for skew join handling
   - Add Z-Ordering on filter columns
   - Partition Silver table by common filter (e.g., `region`, `date`)
   - Cache intermediate results if query is interactive
   - Consider materialized view if query is repeated often
5. **Result**: Query time 45 min → 3 min

---

## Personal Preparation Checklist

### Technical
- [ ] Review Azure Event Hubs vs Kafka trade-offs
- [ ] Study Azure Purview integration with Unity Catalog
- [ ] Review Neo4j graph data modeling patterns
- [ ] Refresh on MCP (Model Context Protocol) spec
- [ ] Review PPDM (Petroleum Product Data Model) basics
- [ ] Prepare Azure architecture diagram (multi-region, multi-tenant)
- [ ] Prepare Knowledge Graph example (Wells/Leases/Production)

### Domain
- [ ] Study Quorum's product portfolio (TIPS, QPTM, eONE, FLOWCAL)
- [ ] Research OSDU Data Platform (energy industry standard)
- [ ] Understand Midstream & Measurement workflows (Flower's domain)
- [ ] Review energy terms: production allocation, lease lifecycle, SCADA, joint ventures

### Behavioral
- [ ] Prepare 3 STAR examples (Situation, Task, Action, Result) for:
  - Complex migration (Oracle/Teradata → Databricks)
  - Conflict resolution (product team vs platform guardrails)
  - Innovation (new capability that drove business value)
- [ ] Prepare questions for each interviewer (3-5 per person)
- [ ] Prepare "Why Quorum?" and "Why this role?" answers

### Logistics
- [ ] Confirm interview format (separate calls or panel?)
- [ ] Confirm duration per interviewer
- [ ] Test video/audio setup
- [ ] Prepare screen-sharing environment (draw.io for diagrams, VS Code for code examples)

---

## Closing Strategy for Each Interview

### Shawn Borkar
*"Shawn, I'm energized by this opportunity. Transforming Quorum's fragmented data into a unified Knowledge Graph that powers agentic AI—that's the kind of high-impact, complex challenge I thrive on. My Oracle EBS migration proved I can handle enterprise-scale complexity. Now I'm ready to apply that to energy domain. If you're looking for someone who can architect the Azure + Databricks foundation, co-engineer with your team, and drive toward a monetizable data platform, I'm confident I can deliver. What concerns or gaps do you see that I should address?"*

### Jonathan Birkholz
*"Jonathan, your vision of practical AI at enterprise scale resonates deeply. I want to be on the team that makes agentic AI real for energy operators—not just demos, but production systems they trust. I'll bring hands-on engineering rigor, willingness to learn fast on knowledge graphs, and focus on solving problems vs buzzwords. If you give me a shot, I'll prove value in the first 30 days with a working KG PoC. What's your biggest worry about whether I can ramp fast enough on agentic AI?"*

### Flower P
*"Flower, I see the data platform as a product that enables your Midstream & Measurement portfolio—and all Quorum products—to deliver cross-product intelligence their competitors can't match. I'll partner with your product teams to ensure platform capabilities align with roadmaps and drive measurable ROI. My track record shows I can balance innovation with operational excellence. How can I best support your goals as SVP?"*

### Eralp P & Brent Turner
*"I respect the architectural complexity you're navigating—multi-region, multi-tenant, Azure + Databricks, legacy integration. I've been in those trenches. I'd welcome your technical pushback—let's whiteboard the hard problems together. If there are specific areas you'd like to test my depth (performance tuning, IaC, DR design), I'm ready. What architecture challenges keep you up at night?"*

---

## Red Flags to Avoid

1. **Don't over-claim**: Stay honest about KG gaps (but show learning plan)
2. **Don't bash legacy systems**: TIPS/FLOWCAL are Quorum's products—respect them, focus on "evolution" not "replacement"
3. **Don't ignore energy domain**: Show genuine interest in learning (PPDM, OSDU references)
4. **Don't be purely theoretical**: Always tie architecture to business outcomes or past delivery examples
5. **Don't be defensive on first round gaps**: "I hear you—here's how I've addressed that since..."

---

## Confidence Builders (Remind Yourself)

✅ **You have deep Databricks expertise** (Unity Catalog, DLT, medallion architecture)
✅ **You've led complex migrations** (Oracle EBS, Teradata → Databricks)
✅ **You understand enterprise governance** (SOX, RBAC/ABAC, data quality)
✅ **You're hands-on** (PySpark, Terraform, CI/CD)
✅ **You're a fast learner** (demonstrated in past roles)
✅ **You have operational maturity** (SLAs, monitoring, triage)
✅ **You passed the first round**—they see potential

**Remember**: They're not expecting perfection. They're assessing:
- **Can you learn fast?** (Azure, KG, Energy domain)
- **Can you execute?** (IaC, pipelines, co-engineering)
- **Can you collaborate?** (Hub-and-spoke, knowledge transfer)
- **Do you fit culturally?** (Innovation mindset, advisory approach)

**You've got this!** 💪

---

## Final Prep: Day Before Interview

1. **Sleep well**: 7-8 hours
2. **Review this doc**: Skim key sections per interviewer
3. **Practice diagram drawing**: Wells/Leases KG model, Azure architecture
4. **Test tech setup**: Video, audio, screen share
5. **Dress**: Business casual (collared shirt, clean background)
6. **Mindset**: Confidence + curiosity + humility

**Good luck!** 🚀
