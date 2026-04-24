# Technical Whiteboarding Scenarios - Round 2 Preparation
## Practice These Before Your Interview

---

## Scenario 1: Multi-Region, Multi-Tenant Azure Architecture

### The Challenge
**Interviewer**: "Draw the end-to-end architecture for Quorum's data platform. It needs to be multi-region (US + Europe for data residency), multi-tenant (100+ customers), support both real-time and batch workloads, and enable AI agents to query across product boundaries."

### What to Draw

```
┌─────────────────────────────────────────────────────────────────────┐
│                          AZURE GLOBAL                                │
├─────────────────────────────────────────────────────────────────────┤
│  Azure Front Door (Global Load Balancer)                            │
│  ├─ Route: /api/production → East US                                │
│  └─ Route: /api/eu-production → West Europe (GDPR)                 │
└─────────────────────────────────────────────────────────────────────┘

┌───────────────────────────────┐  ┌───────────────────────────────┐
│    REGION: EAST US (Primary)  │  │  REGION: WEST EUROPE (DR)     │
├───────────────────────────────┤  ├───────────────────────────────┤
│                               │  │                               │
│  ┌─────────────────────────┐ │  │  ┌─────────────────────────┐ │
│  │  Azure VNet (Hub-Spoke) │ │  │  │  Azure VNet (Hub-Spoke) │ │
│  │  ┌────────────────────┐ │ │  │  │  ┌────────────────────┐ │ │
│  │  │ Hub VNet           │ │ │  │  │  │ Hub VNet           │ │ │
│  │  │ - Azure Firewall   │ │ │  │  │  │ - Azure Firewall   │ │ │
│  │  │ - Azure Bastion    │ │ │  │  │  │ - Azure Bastion    │ │ │
│  │  │ - Private DNS      │ │ │  │  │  │ - Private DNS      │ │ │
│  │  └────────────────────┘ │ │  │  │  └────────────────────┘ │ │
│  │                         │ │  │  │                         │ │ │
│  │  ┌────────────────────┐ │ │  │  │  ┌────────────────────┐ │ │
│  │  │ Spoke 1: Ingestion │ │ │  │  │  │ Spoke 1: Ingestion │ │ │
│  │  │ - Event Hubs       │ │ │  │  │  │ - Event Hubs       │ │ │
│  │  │ - ADF Pipelines    │ │ │  │  │  │ - ADF Pipelines    │ │ │
│  │  └────────────────────┘ │ │  │  │  └────────────────────┘ │ │
│  │                         │ │  │  │                         │ │ │
│  │  ┌────────────────────┐ │ │  │  │  ┌────────────────────┐ │ │
│  │  │ Spoke 2: Databricks│ │ │  │  │  │ Spoke 2: Databricks│ │ │
│  │  │ - Clusters         │ │ │  │  │  │ - Clusters         │ │ │
│  │  │ - Unity Catalog    │ │ │  │  │  │ - Unity Catalog    │ │ │
│  │  │ - DLT Pipelines    │ │ │  │  │  │ - DLT Pipelines    │ │ │
│  │  └────────────────────┘ │ │  │  │  └────────────────────┘ │ │
│  │                         │ │  │  │                         │ │ │
│  │  ┌────────────────────┐ │ │  │  │  ┌────────────────────┐ │ │
│  │  │ Spoke 3: Serving   │ │ │  │  │  │ Spoke 3: Serving   │ │ │
│  │  │ - AKS (MCP Servers)│ │ │  │  │  │ - AKS (MCP Servers)│ │ │
│  │  │ - API Management   │ │ │  │  │  │ - API Management   │ │ │
│  │  │ - Cosmos DB (KG)   │ │ │  │  │  │ - Cosmos DB (KG)   │ │ │
│  │  └────────────────────┘ │ │  │  │  └────────────────────┘ │ │
│  └─────────────────────────┘ │  │  └─────────────────────────┘ │
│                               │  │                               │
│  ┌─────────────────────────┐ │  │  ┌─────────────────────────┐ │
│  │ ADLS Gen2 (Medallion)   │ │  │  │ ADLS Gen2 (Medallion)   │ │
│  │ /bronze/tenant-001/     │◄┼──┼──│ GRS Replication         │ │
│  │ /silver/tenant-001/     │ │  │  │                         │ │
│  │ /gold/tenant-001/       │ │  │  │                         │ │
│  └─────────────────────────┘ │  │  └─────────────────────────┘ │
│                               │  │                               │
│  ┌─────────────────────────┐ │  │  ┌─────────────────────────┐ │
│  │ Observability           │ │  │  │ Observability           │ │
│  │ - Azure Monitor         │ │  │  │ - Azure Monitor         │ │
│  │ - Log Analytics         │ │  │  │ - Log Analytics         │ │
│  │ - Application Insights  │ │  │  │ - Application Insights  │ │
│  │ - Grafana Dashboards    │ │  │  │ - Grafana Dashboards    │ │
│  └─────────────────────────┘ │  │  └─────────────────────────┘ │
│                               │  │                               │
│  ┌─────────────────────────┐ │  │  ┌─────────────────────────┐ │
│  │ Security & Governance   │ │  │  │ Security & Governance   │ │
│  │ - Key Vault             │ │  │  │ - Key Vault             │ │
│  │ - Azure Purview         │ │  │  │ - Azure Purview         │ │
│  │ - Private Link Endpoints│ │  │  │ - Private Link Endpoints│ │
│  │ - Azure AD / Entra ID   │ │  │  │ - Azure AD / Entra ID   │ │
│  └─────────────────────────┘ │  │  └─────────────────────────┘ │
└───────────────────────────────┘  └───────────────────────────────┘

DATA FLOW:
1. Sources (TIPS, QPTM, eONE, FLOWCAL) → Event Hubs (real-time) or ADF (batch)
2. Event Hubs/ADF → Bronze (ADLS Gen2, Delta format, raw data)
3. Databricks DLT → Silver (cleansed, MDM, DQ checks)
4. Databricks DLT → Gold (aggregates, business metrics)
5. Gold → Knowledge Graph (Cosmos DB for Graph) + MCP Servers (AKS)
6. AI Agents query MCP Servers → Unity Catalog enforces RBAC

MULTI-TENANCY:
- Storage: ADLS containers per tenant (/bronze/tenant-001/, /silver/tenant-001/)
- Compute: Shared Databricks clusters with Unity Catalog row-level security
- API: Rate limiting per tenant via API Management
- Cost Tracking: Tags at container and cluster level

DISASTER RECOVERY:
- RPO: < 1 hour (Event Hubs continuous ingestion)
- RTO: < 4 hours (DNS failover via Azure Front Door + Unity Catalog sync)
- ADLS: GRS replication (East US → West US)
- Failover: Quarterly DR drills
```

### Key Points to Explain
1. **Hub-and-Spoke**: Centralized security/networking in Hub, isolated workloads in Spokes
2. **Private Link**: Databricks → ADLS traffic stays on Azure backbone, no public internet
3. **Multi-Region**: Active-Active for ingestion, Active-Passive for DR
4. **Multi-Tenant**: Logical isolation via Unity Catalog + ADLS containers (cost-effective)
5. **Data Residency**: EU customers' data in West Europe (GDPR)
6. **Observability**: Azure Monitor + Grafana for centralized monitoring

---

## Scenario 2: Knowledge Graph for Energy Domain

### The Challenge
**Interviewer**: "Model the relationships between Wells, Leases, Meters, Production Events, and Locations in a Knowledge Graph. Then explain how an AI agent would use this to answer: 'Which leases expiring in 2026 have declining production trends?'"

### What to Draw

```
                     ┌──────────────┐
                     │   Location   │
                     │              │
                     │ - lat/lon    │
                     │ - address    │
                     └──────────────┘
                            ▲
                            │ LOCATED_AT
                            │
        ┌──────────────┐    │    ┌──────────────┐
        │    Lease     │◄───┼────│     Well     │
        │              │    │    │              │
        │ - lease_id   │    │    │ - well_id    │
        │ - start_date │    │    │ - well_name  │
        │ - end_date   │    │    │ - status     │
        │ - operator   │    │    │ - depth      │
        └──────────────┘    │    └──────────────┘
              │             │           │
              │ COVERS      │           │ HAS_METER
              ▼             │           ▼
        ┌──────────────┐    │    ┌──────────────┐
        │  LandParcel  │    │    │    Meter     │
        │              │    │    │              │
        │ - parcel_id  │    │    │ - meter_id   │
        │ - acreage    │    │    │ - meter_type │
        │ - county     │    │    │ - install_dt │
        └──────────────┘    │    └──────────────┘
                            │           │
                            │           │ RECORDS
                            │           ▼
                            │    ┌──────────────┐
                            │    │ProductionEvent│
                            │    │              │
                            │    │ - event_id   │
                            │    │ - timestamp  │
                            │    │ - volume_bbl │
                            │    │ - product    │
                            │    └──────────────┘
                                       │
                                       │ ALLOCATED_TO
                                       ▼
                                ┌──────────────┐
                                │JointVenture  │
                                │              │
                                │ - jv_id      │
                                │ - partners[] │
                                │ - ownership% │
                                └──────────────┘

PROPERTY TYPES:
- Nodes: Well, Lease, Meter, ProductionEvent, Location, LandParcel, JointVenture
- Edges: LOCATED_AT, BELONGS_TO, HAS_METER, RECORDS, COVERS, ALLOCATED_TO

GRAPH QUERY (Cypher for Neo4j or Gremlin for Cosmos DB):
```cypher
MATCH (lease:Lease {end_date: 2026})
      -[:BELONGS_TO]-(well:Well)
      -[:HAS_METER]-(meter:Meter)
      -[:RECORDS]-(pe:ProductionEvent)
WHERE pe.timestamp >= date('2025-01-01')
WITH lease, well,
     collect(pe.volume_bbl) AS volumes,
     collect(pe.timestamp) AS timestamps
WHERE volumes[0] > volumes[-1]  // Declining trend
RETURN lease.lease_id, well.well_name,
       volumes[0] AS initial_volume,
       volumes[-1] AS current_volume
```

AI AGENT WORKFLOW:
1. User asks: "Which leases expiring in 2026 have declining production?"
2. Agent plans steps:
   a. Query Knowledge Graph for leases with end_date=2026
   b. Traverse to connected wells
   c. Traverse to production events
   d. Calculate trend (linear regression or simple first/last comparison)
   e. Filter for declining trends
3. Agent calls MCP Server: "QueryProductionData" tool
4. MCP Server translates to graph query (above Cypher)
5. Unity Catalog checks: Does agent have RBAC to lease/well/production data?
6. Return results to agent
7. Agent formats response: "3 leases expiring in 2026 have declining production:
   - Lease #123 (Wells A, B): Down 15% from 500 bbl/day to 425 bbl/day
   - Lease #456 (Well C): Down 22% from 300 bbl/day to 234 bbl/day
   - ..."
```

### Key Points to Explain
1. **Why Graph vs Relational**: Complex relationships (Wells → Leases → Production) easier to traverse
2. **Entity Resolution**: Silver MDM ensures Meters/Wells/Locations are deduplicated across TIPS/FLOWCAL sources
3. **Real-Time Updates**: CDC from Gold → Knowledge Graph (near real-time)
4. **RBAC**: Unity Catalog governs which nodes/edges agent can access (e.g., can't see JV ownership % if not authorized)
5. **Scalability**: Neo4j or Cosmos DB for Graph handle millions of nodes/edges with sub-second query times

---

## Scenario 3: Tenant Onboarding CI/CD Pipeline

### The Challenge
**Interviewer**: "Walk me through the automated workflow for onboarding a new customer tenant. Show me the CI/CD pipeline, IaC, and policy enforcement."

### What to Draw

```
┌─────────────────────────────────────────────────────────────────┐
│                    GITHUB REPOSITORY                             │
│  /tenants/customer-xyz.yaml                                     │
│  ───────────────────────────────                                │
│  tenant_id: customer-xyz                                        │
│  region: east-us                                                │
│  data_sources:                                                  │
│    - type: api                                                  │
│      endpoint: https://tips.customer-xyz.com                    │
│      auth: oauth2                                               │
│    - type: sftp                                                 │
│      host: sftp.customer-xyz.com                                │
│  slas:                                                          │
│    ingestion_frequency: 15min                                   │
│    gold_refresh: 1hour                                          │
│  data_products:                                                 │
│    - production_daily_summary                                   │
│    - lease_analytics                                            │
└─────────────────────────────────────────────────────────────────┘
                            │
                            │ PR Merged (main branch)
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│            GITHUB ACTIONS WORKFLOW (.github/workflows)          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 1: Validate Tenant Config                             ││
│  │ - JSON schema validation                                   ││
│  │ - Check tenant_id uniqueness                               ││
│  │ - Verify region is allowed (east-us, west-eu)             ││
│  │ Result: ✅ PASS                                             ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 2: Terraform Plan (Infrastructure)                    ││
│  │ module "tenant_onboard" {                                  ││
│  │   tenant_id = "customer-xyz"                               ││
│  │   region    = "east-us"                                    ││
│  │   ...                                                      ││
│  │ }                                                          ││
│  │ Provisions:                                                ││
│  │   - ADLS containers (/bronze/customer-xyz/, /silver/...) ││
│  │   - Unity Catalog schema (customer_xyz.bronze/silver/gold)││
│  │   - Key Vault secrets (OAuth tokens, SFTP credentials)    ││
│  │   - Event Hubs namespace + topics                          ││
│  │   - Grafana dashboard (cloned from template)              ││
│  │ Result: Plan shows 18 resources to create                 ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 3: Policy-as-Code Check (OPA)                         ││
│  │ Rules:                                                     ││
│  │   - ADLS containers must have encryption enabled          ││
│  │   - Unity Catalog schemas must have default DENY          ││
│  │   - Event Hubs must have Private Link endpoint            ││
│  │   - Key Vault must enable purge protection                ││
│  │ Result: ✅ All policies PASS                               ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 4: Terraform Apply (requires approval)                ││
│  │ Manual Approval: Platform Team Lead                        ││
│  │ Result: ✅ Approved, provisioning...                        ││
│  │ Outputs:                                                   ││
│  │   - adls_bronze_path: abfss://bronze/customer-xyz@...     ││
│  │   - unity_catalog_schema: customer_xyz.bronze              ││
│  │   - event_hub_namespace: eventhub-customer-xyz             ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 5: Deploy Databricks Assets (DABs)                    ││
│  │ databricks bundle deploy --target customer-xyz             ││
│  │ Deploys:                                                   ││
│  │   - Bronze ingestion notebook (parameterized)             ││
│  │   - DLT pipeline (Silver transformations)                 ││
│  │   - Job definitions (scheduled ingestion)                 ││
│  │   - RBAC grants (Unity Catalog permissions)               ││
│  │ Result: ✅ Assets deployed                                 ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 6: Integration Test                                   ││
│  │ - Upload sample TIPS data to SFTP                          ││
│  │ - Trigger ingestion job                                    ││
│  │ - Validate Bronze table created                            ││
│  │ - Validate Silver DQ checks run                            ││
│  │ - Validate Gold table populated                            ││
│  │ Result: ✅ 3/3 checks PASS                                  ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 7: Configure Monitoring                               ││
│  │ - Create Grafana dashboard from template                  ││
│  │ - Set up alerts (ingestion lag > 30min, DQ < 80%)        ││
│  │ - Configure cost tracking tags                             ││
│  │ Result: ✅ Monitoring live                                  ││
│  └────────────────────────────────────────────────────────────┘│
│                            │                                     │
│                            ▼                                     │
│  ┌────────────────────────────────────────────────────────────┐│
│  │ Step 8: Notification                                       ││
│  │ Slack message to #platform-team:                           ││
│  │ "✅ Tenant customer-xyz onboarded successfully!            ││
│  │  - Bronze: abfss://bronze/customer-xyz@...                ││
│  │  - Dashboard: https://grafana.../customer-xyz              ││
│  │  - Next: Configure source system connections"             ││
│  └────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────┘

TOTAL TIME: < 1 hour (automated)
MANUAL STEPS: 1 (approval before Terraform apply)
```

### Key Points to Explain
1. **GitOps**: Tenant config in Git → triggers CI/CD → infrastructure as code
2. **Policy-as-Code**: OPA enforces guardrails before provisioning (prevents misconfigurations)
3. **Reusability**: Terraform modules + Databricks Asset Bundles = DRY (Don't Repeat Yourself)
4. **Testing**: Integration test validates end-to-end before marking tenant as ready
5. **Observability**: Monitoring configured automatically (not an afterthought)
6. **Result**: Onboard new tenant in < 1 day vs weeks of manual work

---

## Scenario 4: Spark Performance Tuning Diagnosis

### The Challenge
**Interviewer**: "A Gold aggregation query takes 45 minutes. The business needs it under 5 minutes. Walk me through your diagnosis and optimization."

### What to Draw

```
PROBLEM:
Query: SELECT lease_id, SUM(volume_bbl) AS total_volume
       FROM gold.production_events
       WHERE event_date BETWEEN '2025-01-01' AND '2025-12-31'
       GROUP BY lease_id
Runtime: 45 minutes ❌

DIAGNOSIS WORKFLOW:

┌────────────────────────────────────────────────────────────────┐
│ Step 1: Check Spark UI (Stages View)                          │
├────────────────────────────────────────────────────────────────┤
│ Stage 1: Scan production_events table                         │
│   - Duration: 2 minutes ✅                                      │
│   - Input: 500 GB                                             │
│                                                                │
│ Stage 2: Shuffle (Exchange)                                   │
│   - Duration: 40 minutes ❌❌❌ (BOTTLENECK!)                    │
│   - Shuffle Read: 500 GB                                      │
│   - Shuffle Write: 500 GB                                     │
│   - Partitions: 200                                           │
│                                                                │
│ Stage 3: Aggregate (groupBy)                                  │
│   - Duration: 3 minutes ✅                                      │
└────────────────────────────────────────────────────────────────┘

ROOT CAUSE: Massive shuffle (500 GB) because table not partitioned by lease_id

┌────────────────────────────────────────────────────────────────┐
│ Step 2: Check Data Skew (Executor View)                       │
├────────────────────────────────────────────────────────────────┤
│ Executor 1: 15 GB                                             │
│ Executor 2: 18 GB                                             │
│ Executor 3: 220 GB ❌❌ (DATA SKEW!)                            │
│ Executor 4: 12 GB                                             │
│ ...                                                            │
│                                                                │
│ Cause: One lease_id (e.g., "MEGA-LEASE-001") has 40% of data │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────┐
│ Step 3: Check Current Table Schema                            │
├────────────────────────────────────────────────────────────────┤
│ DESCRIBE EXTENDED gold.production_events;                     │
│                                                                │
│ Partitioned by: event_date (YYYY-MM-DD) ✅                     │
│ Z-Ordered by: NONE ❌                                          │
│ Table size: 500 GB                                            │
│ Num files: 50,000 (10 MB each) ❌ (too many small files)      │
└────────────────────────────────────────────────────────────────┘

OPTIMIZATION STRATEGY:

┌────────────────────────────────────────────────────────────────┐
│ Fix 1: Optimize Table (Compaction)                            │
├────────────────────────────────────────────────────────────────┤
│ OPTIMIZE gold.production_events                               │
│ ZORDER BY (lease_id);                                         │
│                                                                │
│ Result:                                                        │
│ - Files: 50,000 → 500 (1 GB each) ✅                           │
│ - Z-Ordering clusters lease_id values together                │
│ - Query can skip 90% of files (data skipping)                │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────┐
│ Fix 2: Enable Adaptive Query Execution (AQE)                  │
├────────────────────────────────────────────────────────────────┤
│ spark.conf.set("spark.sql.adaptive.enabled", "true")         │
│ spark.conf.set("spark.sql.adaptive.skewJoin.enabled", "true")│
│                                                                │
│ Result: Spark dynamically handles skewed lease_id partition   │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────┐
│ Fix 3: Increase Shuffle Partitions (if still slow)            │
├────────────────────────────────────────────────────────────────┤
│ spark.conf.set("spark.sql.shuffle.partitions", "800")        │
│ (Default: 200, increase to 4x for 500 GB shuffle)            │
│                                                                │
│ Result: More parallelism, but AQE usually handles this       │
└────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────┐
│ Fix 4: Consider Materialized View (if query is frequent)      │
├────────────────────────────────────────────────────────────────┤
│ CREATE MATERIALIZED VIEW gold.production_by_lease AS         │
│ SELECT lease_id, event_date, SUM(volume_bbl) AS daily_volume │
│ FROM gold.production_events                                   │
│ GROUP BY lease_id, event_date;                               │
│                                                                │
│ Refresh: Daily via DLT pipeline                               │
│ Result: Query becomes simple SELECT, no aggregation needed    │
└────────────────────────────────────────────────────────────────┘

RESULTS AFTER OPTIMIZATION:

┌────────────────────────────────────────────────────────────────┐
│ Query Runtime: 45 min → 3 min ✅ (15x improvement)             │
│ Shuffle Data: 500 GB → 50 GB (Z-Ordering data skipping)      │
│ Cost: Same cluster size, 15x lower runtime = 15x cost savings│
└────────────────────────────────────────────────────────────────┘
```

### Key Points to Explain
1. **Methodical Diagnosis**: Spark UI first (find bottleneck stage), then drill into executors (skew?), then table schema
2. **Root Causes**: Shuffle volume, data skew, small files, no Z-Ordering
3. **Multi-Pronged Fixes**: Combine compaction, Z-Ordering, AQE, tuning
4. **Business Impact**: 15x speedup = enables real-time dashboards instead of overnight batch reports
5. **Long-Term**: If query repeats often, materialize the result (pre-aggregate)

---

## Scenario 5: Data Quality & Quarantine Flow

### The Challenge
**Interviewer**: "Customers report bad production data in their dashboards. How do you implement automated data quality checks and quarantine bad records?"

### What to Draw

```
DATA QUALITY PIPELINE FLOW:

┌──────────────────────────────────────────────────────────────────┐
│                    BRONZE LAYER (Raw Ingestion)                  │
├──────────────────────────────────────────────────────────────────┤
│ Source: TIPS API → Event Hubs → Bronze Delta Table              │
│ Data: {well_id: "W123", timestamp: "2025-04-21T10:00:00",       │
│        volume_bbl: 350, product: "OIL", meter_id: "M456"}       │
│ Validation: Schema only (data types match?)                      │
│ Result: ✅ Append to bronze.production_raw                        │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                SILVER LAYER (DQ Checks with Great Expectations)  │
├──────────────────────────────────────────────────────────────────┤
│ DLT Pipeline: bronze.production_raw → silver.production_events  │
│                                                                  │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ DQ Check 1: Null Check                                     │ │
│ │ expect_column_values_to_not_be_null(                       │ │
│ │   column="well_id", mostly=1.0                             │ │
│ │ )                                                          │ │
│ │ Sample Record: {well_id: NULL, ...} ❌ FAIL                 │ │
│ │ Action: Quarantine                                         │ │
│ └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ DQ Check 2: Range Check                                    │ │
│ │ expect_column_values_to_be_between(                        │ │
│ │   column="volume_bbl", min_value=0, max_value=10000        │ │
│ │ )                                                          │ │
│ │ Sample Record: {volume_bbl: -50, ...} ❌ FAIL               │ │
│ │ Action: Quarantine                                         │ │
│ └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ DQ Check 3: Referential Integrity                          │ │
│ │ meter_id must exist in silver.meters_master                │ │
│ │ Sample Record: {meter_id: "M999", ...}                     │ │
│ │ Lookup: silver.meters_master WHERE meter_id="M999"         │ │
│ │ Result: NOT FOUND ❌ FAIL                                   │ │
│ │ Action: Quarantine                                         │ │
│ └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│ ┌────────────────────────────────────────────────────────────┐ │
│ │ DQ Check 4: Duplicate Check                                │ │
│ │ expect_compound_columns_to_be_unique(                      │ │
│ │   column_list=["well_id", "timestamp"]                     │ │
│ │ )                                                          │ │
│ │ Sample: Two records with same well_id+timestamp ❌ FAIL     │ │
│ │ Action: Keep latest record, quarantine duplicate           │ │
│ └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│ DQ RESULTS:                                                      │
│ - Total records: 10,000                                         │
│ - Passed all checks: 8,500 (85%) ✅                              │
│ - Failed at least one check: 1,500 (15%) ❌                      │
│                                                                  │
│ THRESHOLD DECISION:                                              │
│ - If pass_rate >= 80%: ✅ Proceed to Silver                      │
│ - If pass_rate < 80%: ❌ FAIL pipeline, alert, quarantine all    │
│                                                                  │
│ Current: 85% > 80% → ✅ Proceed                                  │
│                                                                  │
│ SPLIT DATA:                                                      │
│ - 8,500 good records → silver.production_events                 │
│ - 1,500 bad records → silver_quarantine.production_events       │
│                 (with metadata: dq_fail_reason, quarantine_ts)  │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                    QUARANTINE MANAGEMENT                         │
├──────────────────────────────────────────────────────────────────┤
│ Table: silver_quarantine.production_events                       │
│ Schema: [original_columns] + dq_fail_reason + quarantine_ts      │
│                                                                  │
│ Sample Quarantined Record:                                       │
│ {                                                                │
│   well_id: NULL,                                                │
│   timestamp: "2025-04-21T10:00:00",                             │
│   volume_bbl: 350,                                              │
│   meter_id: "M456",                                             │
│   dq_fail_reason: "well_id is null",                            │
│   quarantine_ts: "2025-04-21T10:05:00",                         │
│   source_file: "bronze/.../file123.parquet"                     │
│ }                                                                │
│                                                                  │
│ AUTO-REMEDIATION (if applicable):                                │
│ - Known pattern: timezone mismatch                               │
│   IF timestamp.hour > 24 THEN adjust timezone                   │
│   THEN reprocess → Silver                                        │
│                                                                  │
│ MANUAL REVIEW WORKFLOW:                                          │
│ - Data steward reviews quarantine daily                          │
│ - Classifies: Fix source system / Update DQ rules / Discard     │
│ - Jira ticket created for source system team                     │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                    OBSERVABILITY (Grafana Dashboard)             │
├──────────────────────────────────────────────────────────────────┤
│ Panel 1: DQ Pass Rate by Source System                          │
│ ┌──────────────────────────────────────────────────────────┐   │
│ │ TIPS:     ████████████████████░░ 85%                     │   │
│ │ QPTM:     ████████████████████░░ 82%                     │   │
│ │ eONE:     ████████████████░░░░░░ 72% ❌ Below threshold!  │   │
│ │ FLOWCAL:  ██████████████████████ 95% ✅                   │   │
│ └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│ Panel 2: Quarantine Growth Over Time                            │
│ ┌──────────────────────────────────────────────────────────┐   │
│ │      📈                                                   │   │
│ │   1500│         ╱────╲                                    │   │
│ │   1000│    ╱───╱      ╲                                   │   │
│ │    500│───╱            ╲──                                │   │
│ │      0└────────────────────                               │   │
│ │       Week1 Week2 Week3 Week4                             │   │
│ │                                                           │   │
│ │ Alert: Quarantine growing! eONE data quality degrading   │   │
│ └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│ Panel 3: Top DQ Failure Reasons                                 │
│ ┌──────────────────────────────────────────────────────────┐   │
│ │ 1. well_id is null (40%)                                  │   │
│ │ 2. meter_id not in master (30%)                           │   │
│ │ 3. volume_bbl out of range (20%)                          │   │
│ │ 4. Duplicate well_id+timestamp (10%)                      │   │
│ └──────────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                    GOLD LAYER (Trusted Data)                     │
├──────────────────────────────────────────────────────────────────┤
│ Only data that passed Silver DQ checks                           │
│ Business users query Gold with confidence                        │
│ Result: Zero customer complaints about bad data ✅                │
└──────────────────────────────────────────────────────────────────┘
```

### Key Points to Explain
1. **Multi-Layered Validation**: Bronze (schema only), Silver (business rules), Gold (trusted)
2. **Great Expectations**: Industry-standard DQ framework, declarative rules
3. **Threshold-Based**: 80% pass rate example—tune per use case
4. **Quarantine != Discard**: Keep bad data for forensics and remediation
5. **Observability**: Track DQ metrics over time, identify degrading sources proactively
6. **Business Impact**: Dashboards show only trusted data, customer complaints → zero

---

## Practice Tips

### Before the Interview
1. **Draw each scenario on paper/whiteboard** 2-3 times until you can do it from memory
2. **Practice explaining out loud** (not just thinking through it)
3. **Time yourself**: Each scenario should take 5-7 minutes to draw + explain
4. **Prepare for follow-up questions**:
   - "What if... (edge case)?"
   - "How would you handle... (scale/failure)?"
   - "Why did you choose X over Y?"

### During the Interview
1. **Ask clarifying questions first**: "Should I assume active-active or active-passive DR?"
2. **Narrate as you draw**: "I'll start with the ingestion layer..."
3. **Use the whiteboard space wisely**: Top-down or left-right flow
4. **Label everything clearly**: Boxes, arrows, data flows
5. **Call out trade-offs**: "I chose Neo4j over Cosmos DB because..."

### After Drawing
1. **Summarize key points**: "To recap, this architecture delivers X, Y, Z..."
2. **Invite critique**: "What would you change or what concerns you?"
3. **Connect to business value**: "This enables Quorum to..."

---

## Common Follow-Up Questions

### Q: "What if the region fails during an active ingestion?"
**A**: "Event Hubs has built-in geo-replication. If East US fails mid-ingestion:
1. Source systems send to Event Hubs (Azure handles regional failover transparently)
2. Bronze ingestion resumes in West US within RTO (< 4 hours)
3. Delta Lake transaction log ensures no duplicate writes (idempotency)
4. Unity Catalog metastore sync ensures Gold queries work in both regions
5. Monitoring detects lag, auto-escalates P0 alert to platform team"

### Q: "How do you prevent one tenant from consuming all cluster resources?"
**A**: "Multi-tenant resource governance:
1. **Databricks Cluster Policies**: Define max workers, instance types per tenant tier
2. **Unity Catalog quotas**: Limit concurrent queries per tenant (e.g., 10 for Tier 1, 50 for Premium)
3. **Cost allocation tags**: Track compute spend per tenant, alert if exceeds budget
4. **Separate clusters for P0 tenants**: High-value customers get dedicated clusters (physical isolation)
5. **Spot instances for lower tiers**: Reduce cost while maintaining SLAs"

### Q: "What if the Knowledge Graph becomes too large to query quickly?"
**A**: "Graph performance at scale:
1. **Sharding**: Partition graph by region or product segment (e.g., US Wells in one shard, EU Wells in another)
2. **Caching**: Cache frequent queries (e.g., 'Top 10 leases by production') in Redis
3. **Materialized paths**: Pre-compute common traversals (e.g., Well → Lease → Location)
4. **Graph algorithms**: Use Neo4j's Cypher query planner to optimize traversals
5. **Fallback to relational**: For simple aggregations, query Gold tables instead of graph"

---

You're well-prepared! Practice these scenarios, and you'll confidently handle any technical deep-dive. 🚀
