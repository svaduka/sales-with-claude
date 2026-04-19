# Interview Quick Reference Guide
## Quorum Data & AI Platform (op1) - Enterprise & Engineering Architect Interview

**Role**: Senior Data Platform DevOps Engineer / Platform Solution Architect
**Interviewers**: Enterprise Architect, Engineering Lead Architect
**Duration**: TBD

---

## Key Project Context

**Platform Goal**: Transform fragmented data silos → Unified Knowledge Graph → Enable Agentic AI

**Technology Stack**: Azure + Databricks + Microsoft Fabric + Knowledge Graph

**Operating Model**: Hub-and-Spoke
- **Hub (Control Tower)**: Platform Solution Architect + 2 DevOps Engineers
- **Spokes**: 3 Segment Teams (NA O&T, Upstream, Intl O&T)

**Key Requirements**:
- 99.9% uptime SLA
- Cost-competitive, reliable, secure
- Advisory-first approach
- Knowledge transfer and training
- Hub-and-Spoke governance

---

## Azure Well-Architected Framework (5 Pillars)

### 1. Cost Optimization
- **Compute**: Job clusters (not all-purpose), autoscaling, Spot VMs, right-sizing
- **Storage**: Lifecycle management (Hot → Cool → Archive), compression, OPTIMIZE/VACUUM
- **Monitoring**: Cost anomaly detection, chargeback by segment
- **Target**: 20-30% cost reduction

### 2. Operational Excellence
- **IaC**: Terraform for all infrastructure, version-controlled
- **CI/CD**: Automated deployments for notebooks, DLT, infrastructure
- **Monitoring**: Azure Monitor, Log Analytics, custom dashboards
- **Runbooks**: Documented procedures for DR, incident response
- **Metrics**: MTTD, MTTR, change failure rate, deployment frequency

### 3. Performance Efficiency
- **Databricks**: Autoscaling, Photon acceleration, cluster pools
- **Delta Lake**: OPTIMIZE, Z-ORDER, partition strategy
- **Caching**: Delta Cache, SQL Warehouse result caching
- **Metrics**: Query latency (P50, P95, P99), pipeline execution time

### 4. Reliability
- **HA**: ZRS for ADLS, multi-region deployment, zone redundancy
- **DR**: RTO=4h, RPO=1h, GRS for ADLS, Unity Catalog backup
- **Resilience**: Retry logic, circuit breakers, health checks
- **Metrics**: Uptime (99.9%), failed pipeline rate, data quality score

### 5. Security
- **Zero Trust**: Private endpoints, no public access, assume breach
- **Identity**: Azure AD, MFA, Managed Identities
- **Encryption**: At-rest (SSE with CMK), in-transit (TLS 1.2+)
- **Access Control**: Unity Catalog RBAC, column-level security, dynamic masking
- **Monitoring**: Audit logs, SIEM integration

---

## TOGAF Architecture Development Method (ADM)

### Key Phases for QDAI:

**Preliminary**: Establish architecture capability
- Architecture Review Board (ARB)
- Architecture principles
- Governance model

**Phase A - Architecture Vision**:
- Business context: Fragmented silos → Knowledge Graph for Agentic AI
- Hub-and-Spoke operating model
- Stakeholder concerns (CTO, Segments, Platform, InfoSec)

**Phase B - Business Architecture**:
- Business capabilities: Data Ingestion, Transformation, Governance, Consumption, AI/ML
- Value streams: Regulatory reporting, Agentic AI queries, Self-service analytics
- Operating model: Hub-and-Spoke

**Phase C - Information Systems (Data + Application)**:
- Medallion Architecture (Bronze/Silver/Gold)
- Unity Catalog governance
- MDM in Silver layer (Meters, Locations, Products)
- Knowledge Graph for relational intelligence

**Phase D - Technology Architecture**:
- Azure: ADLS Gen 2, Databricks, Data Factory, Key Vault
- DevOps: Terraform, Azure DevOps, Git
- Monitoring: Azure Monitor, Log Analytics

**Phase E - Opportunities and Solutions**:
- Phased implementation: Foundation → Pilot → Scale → Innovate
- 12-month roadmap

**Phase F - Migration Planning**:
- Phased migration (domain by domain)
- Parallel run with legacy systems
- Rollback plan

**Phase G - Implementation Governance**:
- ARB design reviews
- Architecture compliance checks
- Exception management

**Phase H - Architecture Change Management**:
- Continuous monitoring for drift
- Change request process
- Quarterly technology radar

---

## Medallion Architecture

**Bronze Layer** (Raw):
- Land raw data from sources (TIPS, QPTM, eONE, FLOWCAL)
- Delta Lake, immutable, append-only
- Minimal transformation, maintain lineage

**Silver Layer** (Curated):
- Cleansed, conformed, deduplicated
- **Master Data Management**: Meters, Locations, Products (single source of truth)
- SCD Type 2 for historical tracking
- Data quality checks

**Gold Layer** (Consumption):
- Business-level aggregates and metrics
- Pre-aggregated for performance
- Semantic layer / Knowledge Graph mappings
- RBAC/ABAC access control

---

## Knowledge Graph & Agentic AI

**Knowledge Graph Purpose**: Link land, production, accounting data for relational intelligence

**Architecture**:
- **Ontology**: Entities (Well, Lease, Production, Owner, Account), Relationships
- **Graph DB Options**: Neo4j (primary), Azure Cosmos DB Gremlin API (managed)
- **Integration**: Gold layer → Graph materialization → Graph DB → GraphQL/REST API
- **Use Cases**: Multi-hop queries, impact analysis, Agentic AI context

**Agentic AI**:
- **Framework**: LangChain / Semantic Kernel
- **Tools**: Graph query, SQL query, pipeline trigger, document retrieval (RAG)
- **LLM**: Azure OpenAI (GPT-4)
- **Observability**: Tracing (LangSmith), logging, human-in-the-loop

---

## Hub-and-Spoke Governance Model

**Architecture Review Board (ARB)**:
- **Chair**: Platform Solution Architect
- **Members**: Segment Architects, Lead DevOps Engineer, InfoSec, CTO rep
- **Cadence**: Bi-weekly (design reviews), monthly (strategic)

**Governance Processes**:
1. Segment team creates design proposal
2. Self-assessment against standards
3. Submit to ARB (5 days before meeting)
4. ARB review and decision (Approve / Approve with conditions / Reject)
5. Follow-up: Implement changes, re-submit if needed

**Standards**:
- **Mandatory**: Medallion Architecture, Unity Catalog, no public endpoints, Terraform, Git
- **Recommended**: DLT for ETL, Databricks Workflows, pytest for testing

**Compliance**:
- **Automated**: Terraform Sentinel policies, Unity Catalog policies, CI/CD gates
- **Manual**: Quarterly compliance audits by platform team

---

## Key Technologies Deep Dive

### Unity Catalog
- **Hierarchy**: Metastore → Catalogs → Schemas → Tables/Views
- **Governance**: Access control (GRANT/REVOKE), data masking, audit logging
- **Lineage**: Automatic lineage capture
- **Multi-Tenant**: Catalog per tenant (strong isolation) OR Schema per tenant

### Delta Live Tables (DLT)
- **When to Use**: Declarative ETL, data quality checks, automatic lineage
- **Expectations**: Data quality rules with quarantine
- **Incremental**: Simplified incremental processing
- **Best For**: Bronze → Silver → Gold flows

### Terraform (IaC)
- **Scope**: Azure infrastructure (ADLS, networking, Databricks workspace) + Databricks resources (clusters, jobs, Unity Catalog)
- **Structure**: Modules (reusable) + Environments (dev/test/prod)
- **State**: Azure Storage backend, remote state, locking

### Disaster Recovery
- **RTO**: 4 hours (Recovery Time Objective)
- **RPO**: 1 hour (Recovery Point Objective)
- **Strategy**: Active-Passive with multi-region deployment
- **Data**: GRS for ADLS Gen 2, Unity Catalog backup to secondary region
- **Testing**: Quarterly DR drills

---

## Energy Domain (Oil & Gas)

**Key Data Domains**:
- **Wells**: API number, location, drilling dates, production
- **Production**: Daily/monthly volumes (oil, gas, water)
- **Land**: Leases, legal descriptions, ownership
- **Accounting**: Revenue, joint interest billing, division of interest
- **Regulatory**: Production reporting (state agencies), environmental reporting

**Industry Standards**:
- **PPDM**: Data model for E&P data (North America standard)
- **OSDU**: Open-source cloud-native data platform (growing adoption)

**Regulatory Compliance**:
- **Production Reporting**: State agencies (monthly)
- **Environmental**: EPA emissions, state DEQ
- **Audit Trail**: Immutable Bronze layer, data quality, lineage

---

## Key Differentiators to Emphasize

1. **Advisory-First Approach**: Strategic partner, not just executor
2. **Enterprise Architecture Frameworks**: Deep understanding of Azure WAF and TOGAF ADM
3. **Hub-and-Spoke Experience**: Federated team models with autonomy + governance
4. **Architecture Governance**: ARB, compliance frameworks, standards enforcement
5. **Knowledge Transfer**: Training programs, runbooks, communities of practice
6. **Cost Optimization**: Track record of 20-30% cost reduction
7. **Reliability & DR**: Designed HA/DR solutions meeting SLA requirements
8. **End-to-End Lifecycle**: Architecture → Implementation → Operations

---

## Questions to Ask Interviewers

1. "What are the biggest architectural challenges you've faced so far in building QDAI?"
2. "How do segment teams and platform team currently collaborate? What friction points exist?"
3. "What drove the choice of Azure + Databricks + Fabric? Any gaps or concerns?"
4. "Where are you in the ontology/knowledge graph investigation? Any leading candidates?"
5. "How will you measure the success of this platform in Year 1? Year 2?"
6. "What does 'advisory-first' mean in practice? Can you share an example where a partner challenged your assumptions productively?"
7. "What does the onboarding process look like? How quickly do you expect the team to ramp up?"

---

## Trade-off Decision Example (WAF)

**Scenario**: Cost Optimization vs Performance for Gold Layer queries

**Options**:
- **A - Maximize Performance**: Pre-compute all aggregations (expensive, fast)
- **B - Minimize Cost**: Compute on-demand (cheap, variable performance)
- **C - Balanced (Chosen)**: Materialize top 20% queries, on-demand for rest

**Decision Framework**:
- User requirements (Agentic AI needs <2s response)
- Budget constraints (cost-competitive platform)
- Usage patterns (query log analysis)
- Data freshness (15 min staleness acceptable)

**Result**: 90% queries <1s, 10% queries 2-5s, storage cost +20% (not +300%)

---

## STAR Format Examples to Prepare

For each domain, prepare a specific example:
- **Situation**: Project context
- **Task**: Your responsibility
- **Action**: What you did (use Azure WAF / TOGAF concepts)
- **Result**: Measurable outcome

**Example Topics**:
- Designed HA/DR solution meeting 99.9% SLA (Reliability)
- Optimized cloud costs by 30% while improving performance (Cost Optimization)
- Established Architecture Review Board and governance model (TOGAF)
- Implemented Unity Catalog for enterprise data governance
- Built Knowledge Transfer program for data platform adoption

---

## Closing Message

"I'm not just a contractor who executes tasks - I'm a strategic partner who brings enterprise architecture discipline (**TOGAF, Azure WAF**) to challenge assumptions, identify opportunities, and build a governed, scalable, cost-optimized platform that enables Quorum's vision of **Agentic AI powered by Relational Intelligence**."

---

## Interview Approach

✅ **Listen First**: Understand their challenges and pain points
✅ **Ask Clarifying Questions**: Show curiosity and depth
✅ **Use Frameworks**: Reference Azure WAF pillars and TOGAF ADM naturally
✅ **Be Honest About Gaps**: Acknowledge unfamiliarity, explain how you'd close gaps
✅ **Demonstrate Value**: Share specific STAR examples
✅ **Position as Partner**: Emphasize advisory role, not just execution

---

## Final Prep Checklist

- [ ] Review Azure Well-Architected Framework 5 pillars
- [ ] Review TOGAF ADM 8 phases
- [ ] Prepare 5-7 STAR examples from past projects
- [ ] Study Unity Catalog, Delta Live Tables, Terraform
- [ ] Review Medallion Architecture pattern
- [ ] Understand Quorum's business context (fragmented silos → Knowledge Graph)
- [ ] Practice explaining Hub-and-Spoke governance model
- [ ] Prepare questions for interviewers
- [ ] Review Knowledge Graph and Agentic AI concepts
- [ ] Understand Oil & Gas domain basics (if applicable)

Good luck! 🚀
