# Microsoft Fabric & OneLake Strategy for Quorum
## ADLS Gen2 + OneLake Architecture Guide

---

## Executive Summary

**The Core Concept**: OneLake is Microsoft's unified data lake built on ADLS Gen2, designed to eliminate data silos across analytics, data engineering, data science, and BI tools—all using a single copy of data.

**Why It Matters for Quorum**: Instead of copying data between Databricks, Power BI, Azure Synapse, and AI services, OneLake provides a single storage layer that all Microsoft Fabric workloads can access directly, reducing data duplication, lowering costs, and ensuring consistency.

---

## What is Microsoft Fabric?

Microsoft Fabric is an **all-in-one analytics platform** that unifies:

| Fabric Component | Purpose | Quorum Use Case |
|-----------------|---------|-----------------|
| **Data Factory** | Data integration, ETL/ELT pipelines | Ingest from TIPS, QPTM, eONE, FLOWCAL |
| **Synapse Data Engineering** | Spark notebooks, pipelines, delta lake management | Build Bronze/Silver/Gold transformations |
| **Synapse Data Warehouse** | SQL-based analytics, T-SQL queries | Serve data to business analysts via SQL endpoints |
| **Synapse Data Science** | ML model training, notebooks (Python/R) | Train predictive models (production forecasting, lease valuation) |
| **Synapse Real-Time Analytics** | Stream processing with Kusto Query Language (KQL) | Real-time SCADA telemetry, meter data ingestion |
| **Power BI** | Business intelligence, dashboards, reports | Executive dashboards, operational reports for product teams |
| **Data Activator** | Real-time monitoring and alerts | Alert when production drops below threshold, DQ failures |

**Key Insight**: All these workloads share the same underlying data in **OneLake**, eliminating the need for data movement.

---

## What is OneLake?

### The Analogy
Think of OneLake like **OneDrive for data**:
- OneDrive: One storage location for all your personal files, accessible from Word, Excel, PowerPoint, Teams
- OneLake: One storage location for all your enterprise data, accessible from Databricks, Power BI, Synapse, AI services

### Technical Foundation
- **Built on ADLS Gen2**: OneLake is not a replacement for ADLS Gen2—it's a **logical layer on top of it**
- **Delta-Parquet format**: All data stored in open Delta Lake format (Parquet files + transaction logs)
- **Hierarchical namespace**: Organizes data in Workspaces → Items → Tables (like ADLS: Storage Account → Container → Folders)
- **Single copy, multiple interfaces**: Same data accessed via Spark (Databricks), T-SQL (Synapse), Power BI (Direct Lake), Python (notebooks)

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    MICROSOFT FABRIC ONELAKE                      │
│                  (Unified Storage Layer on ADLS Gen2)            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  /Workspace-North-America-OilGas/                               │
│    ├── /lakehouse-bronze/                                       │
│    │     ├── tables/                                            │
│    │     │   ├── tips_production_raw/ (Delta format)            │
│    │     │   ├── qptm_meters_raw/                               │
│    │     │   └── flowcal_measurements_raw/                      │
│    │     └── files/ (landing zone for raw files)                │
│    │                                                             │
│    ├── /lakehouse-silver/                                       │
│    │     └── tables/                                            │
│    │         ├── production_events_cleansed/ (Delta)            │
│    │         ├── meters_master/ (MDM)                           │
│    │         └── wells_master/                                  │
│    │                                                             │
│    └── /lakehouse-gold/                                         │
│          └── tables/                                            │
│              ├── production_daily_summary/ (Delta)              │
│              ├── lease_analytics/                               │
│              └── revenue_by_well/                               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
                             │
                             │ Accessed By (Single Copy!)
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        ▼                    ▼                    ▼
┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│  Databricks   │   │   Power BI    │   │ Azure Synapse │
│               │   │               │   │               │
│ - PySpark     │   │ - Direct Lake │   │ - T-SQL       │
│ - Delta Lake  │   │ - Dashboards  │   │ - SQL Endpoint│
│ - Unity Cat   │   │ - Reports     │   │ - Warehouses  │
└───────────────┘   └───────────────┘   └───────────────┘
        │                    │                    │
        └────────────────────┼────────────────────┘
                             │
                             ▼
                    ┌───────────────┐
                    │  AI Services  │
                    │               │
                    │ - Azure OpenAI│
                    │ - MCP Servers │
                    │ - Agents      │
                    └───────────────┘
```

---

## OneLake Advantages (When Data is in ADLS Gen2)

### 1. **Zero Data Duplication**

**Traditional Architecture (Without OneLake)**:
```
ADLS Gen2 (Databricks lakehouse)
   ↓ [Copy #1]
Azure Synapse (for SQL queries)
   ↓ [Copy #2]
Power BI Import Dataset
   ↓ [Copy #3]
AI Model Training Dataset
   ↓ [Copy #4]
```
**Problem**: 4 copies of same data = 4x storage cost, 4x inconsistency risk, 4x refresh cycles

**With OneLake**:
```
OneLake (ADLS Gen2 underneath)
   ├─ Databricks reads directly ✅
   ├─ Synapse reads directly ✅
   ├─ Power BI reads directly (Direct Lake mode) ✅
   └─ AI services read directly ✅
```
**Benefit**: Single source of truth, real-time consistency, 1/4 storage cost

---

### 2. **Power BI Direct Lake Mode (Game Changer)**

**What It Is**: Power BI queries Delta tables in OneLake **without importing data**—similar to DirectQuery but with in-memory performance.

**Traditional Power BI**:
- **Import Mode**: Copy data into Power BI dataset → fast queries, but stale data (refresh cycles)
- **DirectQuery Mode**: Query live data → fresh data, but slow queries (every click hits database)

**Direct Lake Mode (OneLake Only)**:
- **Best of both worlds**: Queries OneLake Delta tables in-memory using Parquet columnar format → fast AND fresh
- **Automatic refresh**: When Gold table updates (via Databricks DLT), Power BI dashboard reflects it automatically (no manual refresh)
- **Massive datasets**: Can handle billions of rows (OneLake scales, Power BI just queries the subset needed)

**Quorum Use Case**:
- **Production Dashboard**: Executives view real-time production by lease/well/region
- **Gold table updates**: Databricks DLT pipeline runs every 15 minutes, writes to OneLake Gold
- **Power BI auto-refreshes**: Dashboard shows latest data without manual refresh or import
- **Result**: Real-time intelligence without data duplication

---

### 3. **Unified Governance with Microsoft Purview**

**Integration**:
- OneLake integrates natively with **Microsoft Purview** (Azure's data governance platform)
- Purview scans OneLake, discovers all Delta tables, builds **data catalog + lineage**
- Users can search for "production data" in Purview → find OneLake tables → request access → auto-provisioned

**Governance Features**:
- **Lineage Tracking**: TIPS source → Bronze table → Silver cleansed → Gold aggregated → Power BI report (end-to-end visibility)
- **Data Classification**: Tag columns as PII, Confidential, Public → enforce policies (e.g., PII data can't leave US region)
- **Access Control**: Integrate with Azure AD/Entra ID → RBAC at workspace/table/column level
- **Data Quality Monitoring**: Purview tracks DQ metrics, surfaces in catalog

**Quorum Benefit**: Single governance model across Databricks, Power BI, Synapse, AI—no separate governance per tool

---

### 4. **Seamless Databricks + Fabric Interoperability**

**The Challenge**: Databricks excels at data engineering, but business users prefer Power BI for reporting. Traditionally, you'd export Databricks Gold → Synapse → Power BI (data duplication).

**With OneLake**:
1. **Databricks writes to OneLake**: DLT pipelines write Gold tables to OneLake (Delta format)
2. **OneLake Mirroring**: OneLake can "mirror" Databricks Unity Catalog tables bidirectionally
3. **Power BI reads from OneLake**: Direct Lake mode queries the same Delta tables Databricks writes
4. **Result**: Databricks and Fabric share the same data, zero duplication

**Technical Setup**:
```python
# Databricks writes to OneLake
spark.sql("""
  CREATE TABLE onelake.gold.production_summary
  USING delta
  LOCATION 'abfss://workspace@onelake.dfs.fabric.microsoft.com/lakehouse-gold/tables/production_summary'
  AS SELECT lease_id, SUM(volume_bbl) AS total_volume
  FROM silver.production_events
  GROUP BY lease_id
""")
```

```sql
-- Power BI queries via Direct Lake (no import!)
-- Automatically references the same Delta table
SELECT lease_id, total_volume
FROM gold.production_summary
WHERE total_volume > 10000
```

---

### 5. **Cost Optimization**

**Storage Costs**:
- **OneLake pricing**: $0.023/GB/month (same as ADLS Gen2)
- **Benefit**: No premium for OneLake features—you pay ADLS rates but get Fabric capabilities

**Compute Costs**:
- **Fabric Capacity Model**: Pay for compute capacity (CUs - Capacity Units) across all workloads
- **Example**: 1 F64 capacity = $8.23/hour → shared across Synapse, Power BI, Data Factory, notebooks
- **Vs. Traditional**: Separate Azure Synapse ($$/hour) + Power BI Premium ($$/user) + ADF ($$/pipeline) → consolidated billing

**Data Movement Costs Eliminated**:
- **No egress fees** between Databricks → Synapse → Power BI (all read from OneLake)
- **No ETL jobs** to copy data between systems (saves ADF pipeline costs)

**Quorum Scenario**:
- **Before OneLake**: 1 TB in Databricks → copy to Synapse (1 TB) → import to Power BI (1 TB) = 3 TB storage + copy jobs
- **With OneLake**: 1 TB shared across all = 1 TB storage + zero copy jobs
- **Savings**: ~66% storage cost reduction + eliminated data movement costs

---

### 6. **Real-Time Analytics with KQL (Kusto Query Language)**

**Use Case**: Quorum needs real-time streaming analytics for SCADA telemetry, meter readings, production alerts.

**Fabric Real-Time Analytics**:
- **KQL Database**: High-performance time-series database in Fabric
- **Ingestion**: Azure Event Hubs → KQL DB (sub-second latency)
- **Queries**: Kusto Query Language (similar to SQL but optimized for logs/time-series)
- **OneLake Integration**: KQL DB can query OneLake Delta tables in federated fashion

**Architecture**:
```
SCADA Systems (Wells) → Event Hubs → KQL Database (Real-Time)
                                          │
                                          ▼
                            Real-time alerts (Data Activator)
                                          │
                                          ▼
                            Append to OneLake Bronze (cold storage)
                                          │
                                          ▼
                            Databricks processes to Silver/Gold
```

**Query Example** (KQL joining real-time + historical):
```kql
// Real-time data (last 5 minutes)
realtime_production
| where timestamp > ago(5m)
| summarize current_volume = sum(volume_bbl) by well_id
| join kind=inner (
    // Historical data from OneLake Gold
    evaluate external_data(
      "abfss://workspace@onelake.../gold/production_history"
    )
    | summarize avg_volume = avg(volume_bbl) by well_id
  ) on well_id
| where current_volume < (avg_volume * 0.8)  // Alert if 20% below average
| project well_id, current_volume, avg_volume, alert = "Low Production"
```

---

### 7. **Shortcuts (Symlinks for Data Virtualization)**

**What Are Shortcuts?**: OneLake can create "shortcuts" (like symlinks) to external data without copying it.

**Supported Sources**:
- **ADLS Gen2** (your Databricks Bronze/Silver/Gold containers)
- **AWS S3** (if Quorum has multi-cloud data)
- **Other OneLake workspaces** (federated access across product segments)
- **Databricks Unity Catalog** (reference Databricks tables directly)

**Use Case for Quorum**:
```
Scenario: Databricks manages Bronze/Silver in its own ADLS Gen2 containers.
          You want Power BI to access it without duplicating.

Solution:
1. Create OneLake workspace for "North America O&T" product segment
2. Create shortcut: /lakehouse-gold → points to Databricks ADLS Gold container
3. Power BI reads via Direct Lake as if data is in OneLake
4. Result: Zero copy, Power BI uses Databricks data directly
```

**Visual**:
```
Databricks ADLS Gen2 Container:
  abfss://databricks-gold@quorum.dfs.core.windows.net/production_summary/

OneLake Shortcut:
  /Workspace-NA-OilGas/lakehouse-gold/production_summary/
    → [Shortcut to Databricks ADLS]

Power BI:
  SELECT * FROM gold.production_summary
    → Reads from Databricks ADLS via shortcut (no copy!)
```

---

## Quorum-Specific Architecture: Databricks + OneLake Integration

### Recommended Pattern

```
┌─────────────────────────────────────────────────────────────────┐
│                    DATA INGESTION LAYER                          │
├─────────────────────────────────────────────────────────────────┤
│ Sources: TIPS, QPTM, eONE, FLOWCAL                             │
│   ↓                                                              │
│ Azure Event Hubs (real-time) + Azure Data Factory (batch)      │
│   ↓                                                              │
│ Land in: ADLS Gen2 (Databricks-managed containers)             │
└─────────────────────────────────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│               DATABRICKS (Primary Data Engineering)              │
├─────────────────────────────────────────────────────────────────┤
│ Bronze Layer (ADLS Gen2 - Databricks containers)               │
│   - Raw Delta tables, minimal transformation                    │
│   - Unity Catalog governs access                                │
│                                                                  │
│ Silver Layer (ADLS Gen2 - Databricks containers)               │
│   - DLT pipelines: cleansing, MDM, DQ checks                   │
│   - Master Data: meters_master, wells_master, locations_master  │
│   - Unity Catalog: schema + RBAC                                │
│                                                                  │
│ Gold Layer (ADLS Gen2 - Databricks containers)                 │
│   - DLT pipelines: aggregations, business metrics               │
│   - Tables: production_summary, lease_analytics, revenue_report │
│   - Unity Catalog: RBAC + row-level security                    │
└─────────────────────────────────────────────────────────────────┘
                             │
                             │ OneLake Shortcuts (Zero Copy!)
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                  MICROSOFT FABRIC ONELAKE                        │
├─────────────────────────────────────────────────────────────────┤
│ Workspace: North America O&T                                    │
│   /lakehouse-gold-shortcut/ → Points to Databricks ADLS Gold   │
│                                                                  │
│ Workspace: Upstream Planning                                    │
│   /lakehouse-gold-shortcut/ → Points to Databricks ADLS Gold   │
│                                                                  │
│ Workspace: International O&T                                    │
│   /lakehouse-gold-shortcut/ → Points to Databricks ADLS Gold   │
└─────────────────────────────────────────────────────────────────┘
                             │
        ┌────────────────────┼────────────────────┐
        ▼                    ▼                    ▼
┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│   Power BI    │   │ Synapse SQL   │   │  Knowledge    │
│               │   │               │   │    Graph      │
│ - Dashboards  │   │ - Ad-hoc SQL  │   │               │
│ - Reports     │   │ - BI queries  │   │ - Neo4j reads │
│ - Direct Lake │   │ - T-SQL users │   │   OneLake Gold│
│ - Real-time   │   │ - ODBC/JDBC   │   │ - MCP servers │
└───────────────┘   └───────────────┘   └───────────────┘
```

### Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| **Databricks owns Bronze/Silver/Gold** | Databricks DLT is best-in-class for complex transformations, MDM, DQ |
| **ADLS Gen2 as storage** | Databricks and OneLake both use ADLS Gen2—native compatibility |
| **OneLake shortcuts to Gold** | Power BI/Synapse access Databricks Gold via shortcuts (zero copy) |
| **Unity Catalog as primary governance** | Databricks Unity Catalog enforces RBAC; Purview adds discovery/lineage |
| **Fabric for consumption layer** | Power BI Direct Lake for dashboards, Synapse SQL for ad-hoc queries |
| **Event Hubs for real-time** | Fabric Real-Time Analytics (KQL) for streaming; append to Bronze for batch |

---

## Interview Positioning: How to Talk About Fabric + OneLake

### For Shawn Borkar (Enterprise Data Strategy)

*"Shawn, one advantage I see in Quorum's Azure + Databricks strategy is the opportunity to leverage **Microsoft Fabric OneLake** for unified data access. Here's the pattern I'd propose:*

*Databricks remains the primary data engineering engine—Bronze ingestion, Silver MDM with DQ checks, Gold aggregations—all managed via DLT pipelines and Unity Catalog. The data physically resides in ADLS Gen2 containers that Databricks controls.*

*But here's where OneLake adds value: instead of copying Gold data to separate systems for Power BI dashboards or Synapse SQL queries, we use **OneLake shortcuts** to reference Databricks Gold containers. Power BI can then use **Direct Lake mode** to query those Delta tables in real-time, without importing data. This eliminates data duplication, reduces storage costs by ~66%, and ensures Power BI always reflects the latest Databricks output—no manual refresh cycles.*

*For Quorum's product segments—North America O&T, Upstream, International—each segment gets a Fabric workspace with shortcuts to their respective Gold datasets. This enables federated access: segment teams own their Power BI reports, but the platform team owns the underlying data engineering in Databricks. It's the hub-and-spoke model reflected in the consumption layer.*

*The other benefit is governance: **Microsoft Purview** integrates natively with OneLake, providing end-to-end lineage from TIPS source → Databricks Bronze → Silver MDM → Gold → Power BI report. Stakeholders can search Purview's data catalog, discover production datasets, request access, and it's auto-provisioned via Unity Catalog RBAC.*

*Finally, for real-time use cases—like SCADA telemetry from wells—Fabric's **Real-Time Analytics (KQL DB)** can ingest from Event Hubs, trigger alerts via Data Activator, and then append to Bronze for Databricks batch processing. This hybrid real-time + batch pattern gives Quorum the best of both worlds."*

---

### For Jonathan Birkholz (CTO, AI Strategy)

*"Jonathan, for the agentic AI architecture, OneLake offers an interesting opportunity for **unified data access across AI tools**. Here's how I'm thinking about it:*

*The Knowledge Graph (Neo4j or Azure Cosmos DB for Graph) needs to reference production data, lease data, meter data from Gold tables. Traditionally, you'd ETL Gold → graph database, creating another copy. With OneLake, the graph ingestion process can **read directly from OneLake Gold Delta tables** via ADLS APIs—no duplication.*

*For MCP servers (the tool registry for AI agents), each server can query OneLake Gold datasets using:*
- *Spark API (via Databricks for complex queries)*
- *T-SQL endpoint (via Synapse for simple SQL)*
- *Direct Parquet read (via Python `pyarrow` for lightweight queries)*

*The advantage: **single source of truth**. When Databricks DLT updates production_summary table, the Knowledge Graph and MCP servers reference the latest data automatically. No sync lag, no stale agent responses.*

*OneLake also enables **vector search integration** for RAG patterns. Azure AI Search can index OneLake datasets (production reports, lease documents stored in OneLake Files), generate embeddings, and agents query that vector index alongside the Knowledge Graph. It's all connected via OneLake shortcuts.*

*Finally, for **model training**, data scientists can use Fabric notebooks (Spark, Python, R) to train predictive models (production forecasting, lease valuation) directly on OneLake Gold—no need to copy data to separate ML environments. Models register to MLflow in Databricks, then get deployed as MCP server endpoints for agents to invoke."*

---

### For Eralp P / Brent Turner (Solution Architects)

*"From a technical architecture perspective, OneLake solves a classic problem: **avoiding the medallion architecture duplication tax**. Let me explain:*

*Typically, you build Bronze/Silver/Gold in Databricks (ADLS Gen2), then copy Gold → Azure Synapse for SQL users, then import to Power BI for dashboards, then copy again to AI training environments. That's 3-4 copies of the same data, which means:*
- *3-4x storage costs*
- *3-4x ETL pipelines to maintain (ADF jobs for each copy)*
- *Inconsistency risk (which copy is latest?)*
- *Refresh lag (Power BI refreshes hourly, but Databricks Gold updates every 15 min)*

*With OneLake, Databricks writes Gold to ADLS Gen2 (as usual), but OneLake creates **shortcuts** to those containers. Power BI, Synapse, and AI services all read the same Delta tables via OneLake APIs—zero copies. This is possible because:*
1. *OneLake is built on ADLS Gen2 (same storage layer as Databricks)*
2. *Delta format is open (Parquet + transaction log), so Fabric can read it natively*
3. *Unity Catalog and Purview share governance metadata via integration*

*The architecture pattern I'd propose:*
```
Databricks DLT → writes to → ADLS Gen2 (Databricks containers)
                                  ↓
                        OneLake shortcuts point to ↓
                                  ↓
              Power BI (Direct Lake) + Synapse SQL + AI services
                       (all read same Delta tables)
```

*For multi-region deployment, OneLake supports **geo-redundancy**:*
- *ADLS Gen2 GRS replication ensures Gold data replicates to secondary region*
- *OneLake shortcuts in secondary region point to replicated containers*
- *Failover: DNS switch + Power BI reconnects to secondary OneLake workspace*
- *RPO < 1 hour, RTO < 4 hours (same as Databricks DR plan)*

*Trade-off to acknowledge: OneLake Direct Lake is **read-only** for Power BI. If business users need to write back (e.g., budget adjustments, manual overrides), you'd still need a write-back pattern (Power BI → Azure SQL → Databricks ingests changes). But for 95% of use cases—consumption, dashboards, reports—Direct Lake eliminates the duplication tax."*

---

## Potential Interview Questions & Answers

### Q1: "Why use OneLake if Databricks Unity Catalog already provides unified governance?"

**Answer**:
*"Great question. Unity Catalog is best-in-class for governing Databricks workloads—Delta tables, notebooks, clusters, jobs. But Unity Catalog doesn't extend natively to Power BI, Azure Synapse SQL, or Azure AI services.*

*OneLake bridges this gap. It's not a replacement for Unity Catalog—it's complementary. Here's the division of responsibility:*
- *Unity Catalog: Governs Databricks data engineering (Bronze/Silver/Gold transformations, RBAC, row-level security)*
- *OneLake + Purview: Governs consumption layer (Power BI, Synapse, AI services) and provides enterprise-wide data catalog*

*The integration: Unity Catalog tables can be referenced in OneLake via shortcuts. Purview scans OneLake, discovers those tables, and builds lineage. So you get best of both: Unity Catalog's fine-grained RBAC for Databricks, OneLake's unified consumption layer for Fabric workloads.*

*Specific example: A data analyst who only uses Power BI doesn't need Databricks access. They query Gold tables via OneLake Direct Lake, governed by Fabric workspace permissions (synced with Azure AD). But the underlying data is still governed by Unity Catalog—if Unity Catalog denies them access to a column (e.g., PII), Fabric respects that via the shared RBAC model."*

---

### Q2: "What's the performance difference between Power BI Direct Lake (OneLake) vs DirectQuery (Databricks SQL)?"

**Answer**:
*"Massive difference—Direct Lake is typically **10-100x faster** than DirectQuery, and here's why:*

**DirectQuery (Databricks SQL endpoint)**:
- Every Power BI visual query hits Databricks → Spark cluster spins up → queries Delta table → returns results
- Latency: 3-10 seconds per visual (Spark cold start overhead)
- Concurrency: Limited by Databricks SQL warehouse size (e.g., 10 concurrent queries on Medium warehouse)
- Cost: Databricks SQL DBU consumption per query

**Direct Lake (OneLake)**:
- Power BI reads Parquet files from OneLake directly into memory (columnar format, optimized for analytics)
- Latency: Sub-second (in-memory queries)
- Concurrency: Unlimited (each user queries local cached Parquet data)
- Cost: Only OneLake storage ($0.023/GB/month), no compute per query

**Trade-off**: Direct Lake requires data in OneLake (Delta format). If you're already using Databricks with Delta, it's a perfect fit. But if you need custom Spark transformations per query (e.g., complex joins, window functions), DirectQuery is more flexible."*

---

### Q3: "How do you handle data freshness? If Databricks updates Gold every 15 minutes, does Power BI Direct Lake see it immediately?"

**Answer**:
*"Almost immediately—typically within 1-2 minutes. Here's the flow:*

1. *Databricks DLT pipeline runs, writes new data to ADLS Gen2 Gold table (Delta commit)*
2. *OneLake detects the Delta transaction log update (via ADLS change feed or polling)*
3. *Power BI Direct Lake mode invalidates its Parquet cache for that table*
4. *Next time a user opens the dashboard, Power BI re-reads the updated Parquet files*

*For truly real-time updates (sub-minute), Power BI has an **automatic page refresh** setting—you can configure dashboards to refresh every 30 seconds, 1 minute, etc. This works seamlessly with Direct Lake.*

*Compare this to traditional Power BI Import mode:*
- *Dataset refresh runs on schedule (e.g., hourly)*
- *Between refreshes, data is stale*
- *Refresh takes 10-20 minutes for large datasets (copying millions of rows)*

*With Direct Lake, there's no copy—just re-read Parquet files that changed, which is near-instantaneous."*

---

### Q4: "What if we want to use Databricks for data engineering but don't want to adopt all of Microsoft Fabric? Can we use OneLake selectively?"

**Answer**:
*"Absolutely—and that's the approach I'd recommend for Quorum. Think of it as a hybrid architecture:*

**Databricks remains primary for data engineering**:
- All Bronze/Silver/Gold pipelines run in Databricks (DLT)
- Unity Catalog governs Databricks workloads
- Storage is Databricks-managed ADLS Gen2 containers

**Fabric OneLake is consumption layer only**:
- Use OneLake shortcuts to reference Databricks Gold containers
- Enable Power BI Direct Lake for dashboards (eliminates import mode)
- Optionally use Synapse SQL for ad-hoc queries (if business users need T-SQL interface)
- Optionally use Fabric Real-Time Analytics (KQL) for streaming use cases

**What you DON'T need to adopt**:
- Fabric Synapse Data Engineering (keep Databricks notebooks/DLT)
- Fabric Data Factory (keep Azure Data Factory or Databricks workflows for orchestration)
- Fabric Data Science (keep Databricks MLflow/notebooks for ML)

**Result**: Best-of-breed approach—Databricks for engineering, OneLake for unified consumption, Unity Catalog + Purview for governance."*

---

## Cost Comparison: Traditional vs OneLake Architecture

### Traditional Multi-Copy Architecture

| Component | Monthly Cost (Example: 10 TB data) |
|-----------|-----------------------------------|
| **ADLS Gen2 (Databricks Gold)** | 10 TB × $0.023/GB = $230 |
| **Azure Synapse dedicated pool** (copy of Gold) | 10 TB × $0.023/GB + DW500c ($7.50/hr × 720 hrs) = $230 + $5,400 = $5,630 |
| **Power BI Import datasets** (copy of Gold) | 10 TB × $0.023/GB = $230 (plus Premium P1 capacity $4,995/mo) |
| **ADF pipelines** (copy jobs) | ~$500/month (data movement activities) |
| **Total** | **~$11,585/month** |

### OneLake Architecture (Zero Copy)

| Component | Monthly Cost (Example: 10 TB data) |
|-----------|-----------------------------------|
| **ADLS Gen2 (Databricks Gold)** | 10 TB × $0.023/GB = $230 |
| **OneLake shortcuts** (no additional storage) | $0 (shortcuts are metadata, not data) |
| **Fabric Capacity (F64)** | $5,914/month (replaces Synapse DW + Power BI Premium) |
| **Total** | **~$6,144/month** |

**Savings**: ~$5,400/month (~47% reduction) for 10 TB data

---

## Recommended Architecture Diagram for Interview

When whiteboarding, draw this:

```
┌─────────────────────────────────────────────────────────────────┐
│                 QUORUM DATA PLATFORM ARCHITECTURE                │
│              (Databricks + OneLake Hybrid Pattern)               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ INGESTION LAYER                                          │  │
│  │ TIPS, QPTM, eONE, FLOWCAL                               │  │
│  │   ↓                                                      │  │
│  │ Event Hubs (real-time) + ADF (batch)                    │  │
│  └──────────────────────────────────────────────────────────┘  │
│                           ↓                                      │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ DATABRICKS (Data Engineering)                            │  │
│  │ ┌────────────────────────────────────────────────────┐  │  │
│  │ │ Bronze: Raw Delta tables in ADLS Gen2              │  │  │
│  │ │ Unity Catalog schema: bronze                        │  │  │
│  │ └────────────────────────────────────────────────────┘  │  │
│  │ ┌────────────────────────────────────────────────────┐  │  │
│  │ │ Silver: DLT cleansing, MDM, DQ                     │  │  │
│  │ │ Unity Catalog schema: silver                        │  │  │
│  │ └────────────────────────────────────────────────────┘  │  │
│  │ ┌────────────────────────────────────────────────────┐  │  │
│  │ │ Gold: DLT aggregations, business metrics           │  │  │
│  │ │ Unity Catalog schema: gold                          │  │  │
│  │ └────────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────────┘  │
│                           ↓                                      │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ MICROSOFT FABRIC ONELAKE (Consumption Layer)            │  │
│  │ ┌────────────────────────────────────────────────────┐  │  │
│  │ │ OneLake Shortcuts → Databricks ADLS Gold          │  │  │
│  │ │ (Zero data copy, reference only)                   │  │  │
│  │ └────────────────────────────────────────────────────┘  │  │
│  │                                                          │  │
│  │ Workspace: NA O&T      Workspace: Upstream             │  │
│  │ Workspace: International O&T                            │  │
│  └──────────────────────────────────────────────────────────┘  │
│         ↓                    ↓                    ↓             │
│  ┌──────────┐       ┌──────────┐       ┌──────────┐           │
│  │Power BI  │       │Synapse   │       │Knowledge │           │
│  │Direct    │       │SQL       │       │Graph     │           │
│  │Lake      │       │Endpoint  │       │Neo4j     │           │
│  └──────────┘       └──────────┘       └──────────┘           │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ GOVERNANCE LAYER                                         │  │
│  │ - Unity Catalog (Databricks RBAC)                       │  │
│  │ - Microsoft Purview (Lineage + Catalog)                 │  │
│  │ - Azure AD/Entra ID (Identity)                          │  │
│  └──────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

**Key Callouts**:
1. ✅ **Databricks owns data engineering** (Bronze/Silver/Gold DLT pipelines)
2. ✅ **ADLS Gen2 as physical storage** (Delta format, Unity Catalog governed)
3. ✅ **OneLake shortcuts for consumption** (Power BI, Synapse, AI read Gold via shortcuts)
4. ✅ **Zero data duplication** (single copy, multiple interfaces)
5. ✅ **Unified governance** (Unity Catalog + Purview integration)

---

## Key Takeaways for Interview

1. **OneLake = Single Copy, Multiple Interfaces**: Eliminates 66% storage costs by avoiding duplication
2. **Power BI Direct Lake = Real-Time Dashboards**: No import delays, always fresh data from Databricks Gold
3. **Databricks + OneLake = Best-of-Breed**: Databricks for engineering, OneLake for consumption
4. **Governance**: Unity Catalog (Databricks) + Purview (Fabric) = end-to-end lineage and RBAC
5. **Cost Optimization**: ~47% savings by consolidating Synapse DW + Power BI Premium into Fabric capacity
6. **Shortcuts = Zero-Copy Virtualization**: Reference Databricks ADLS containers from OneLake without moving data

---

**You're now equipped to discuss Microsoft Fabric and OneLake authoritatively in your interview!** 🚀
