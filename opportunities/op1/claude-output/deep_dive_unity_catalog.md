# Deep Dive: Unity Catalog for Enterprise Data Governance
## Quorum Data & AI Platform Implementation Guide

This document provides detailed technical knowledge on Unity Catalog - a critical component for the QDAI platform.

---

## What is Unity Catalog?

**Unity Catalog** is Databricks' unified governance solution for data and AI assets across clouds. It provides:
- Centralized metadata management
- Fine-grained access control
- Data lineage and audit logging
- Data discovery and search

**Why Critical for QDAI**: Quorum needs to govern data across 3 segment teams (NA O&T, Upstream, Intl O&T) with centralized control + federated autonomy. Unity Catalog is the governance layer enabling this.

---

## Unity Catalog Architecture

### Hierarchy (4 Levels)

```
Metastore (Regional)
  ├── Catalog (Logical Boundary - e.g., "production", "segment_na_ot")
  │   ├── Schema (Subject Area - e.g., "wells", "production", "land")
  │   │   ├── Table (Data Asset - e.g., "gold_production_daily")
  │   │   ├── View (Derived Asset)
  │   │   ├── Function (UDF)
  │   │   └── Volume (Unstructured Data - files, images)
```

### Key Concepts

#### 1. Metastore
- **What**: Top-level container, tied to an Azure region
- **Scope**: One metastore per region (e.g., East US 2 metastore)
- **Contains**: Catalogs, external locations, storage credentials, users/groups
- **Attached to**: One or more Databricks workspaces in the region
- **QDAI Design**: One metastore for primary region (East US 2), one for DR region (Central US)

#### 2. Catalog
- **What**: Logical container for schemas, often aligned with environment or tenant
- **Scope**: Catalog-level permissions (who can create schemas, access all data in catalog)
- **QDAI Design Options**:
  - **Option A - Catalog per Environment**:
    - `dev`, `test`, `prod` catalogs
    - Pros: Clear environment separation
    - Cons: All segments share same prod catalog (harder to isolate)
  - **Option B - Catalog per Segment** (Recommended):
    - `segment_na_ot`, `segment_upstream`, `segment_intl`, `platform_shared`
    - Pros: Strong segment isolation, chargeback visibility, segment autonomy
    - Cons: More catalogs to manage
  - **Option C - Hybrid**:
    - `platform` (shared Bronze/Silver), `segment_na_ot_gold`, `segment_upstream_gold`, `segment_intl_gold`
    - Pros: Centralized ingestion, federated consumption
    - Cons: Complex permissions (Bronze/Silver in platform catalog, Gold in segment catalog)

**Recommendation for QDAI**: **Option B (Catalog per Segment)** to align with Hub-and-Spoke model.

#### 3. Schema
- **What**: Namespace within a catalog, often aligned with subject area or domain
- **Scope**: Schema-level permissions (who can create tables, access data in schema)
- **QDAI Design**:
  ```
  segment_na_ot/
    ├── bronze/              # Raw ingestion from TIPS, QPTM
    ├── silver/              # Curated, MDM-enriched
    │   ├── wells/
    │   ├── production/
    │   ├── land/
    │   └── accounting/
    └── gold/                # Business-level aggregates
        ├── production_kpis/
        ├── regulatory_reports/
        └── dashboards/
  ```

#### 4. Table / View / Volume
- **Table**: Managed (Unity Catalog owns data) or External (data in ADLS, Unity Catalog tracks metadata)
- **View**: Derived from tables, can apply row-level/column-level security
- **Volume**: Unstructured data (files, images, PDFs) - governed like tables
- **QDAI Design**: Use **external tables** (data in ADLS Gen 2, metadata in Unity Catalog)

---

## Multi-Tenant Isolation Strategies

### Strategy 1: Catalog per Tenant (Strong Isolation)
```
Metastore
  ├── segment_na_ot/        # Tenant 1
  │   ├── bronze/
  │   ├── silver/
  │   └── gold/
  ├── segment_upstream/     # Tenant 2
  │   ├── bronze/
  │   ├── silver/
  │   └── gold/
  └── segment_intl/         # Tenant 3
      ├── bronze/
      ├── silver/
      └── gold/
```

**Pros**:
- Strongest isolation (catalog-level permissions)
- Easy chargeback (tag ADLS folders by catalog)
- Segment autonomy (each segment manages their catalog)

**Cons**:
- More catalogs to manage
- Harder to share data across segments (need cross-catalog queries)

**When to Use**: When segments have distinct data with minimal sharing (QDAI fits this model).

---

### Strategy 2: Schema per Tenant (Moderate Isolation)
```
Metastore
  └── production/           # Shared catalog
      ├── segment_na_ot_bronze/
      ├── segment_na_ot_silver/
      ├── segment_na_ot_gold/
      ├── segment_upstream_bronze/
      ├── segment_upstream_silver/
      └── segment_upstream_gold/
```

**Pros**:
- Single catalog (easier to manage)
- Easy cross-segment queries (same catalog)

**Cons**:
- Weaker isolation (schema-level permissions, easier to accidentally grant broad access)
- Harder chargeback (need tagging at table level)

**When to Use**: When segments need frequent data sharing, less autonomy required.

---

### Strategy 3: Row-Level Security (Least Isolation)
```
Metastore
  └── production/
      └── data/
          └── wells (table with `segment_id` column)
              ├── Row 1: segment_id = 'na_ot'
              ├── Row 2: segment_id = 'upstream'
              └── Row 3: segment_id = 'intl'
```

**Pros**:
- Single table, easy to query
- No need to manage multiple catalogs/schemas

**Cons**:
- Weakest isolation (relies on application logic, easier to break)
- Performance overhead (filter every query by segment_id)
- Hard to audit (who accessed what segment's data?)

**When to Use**: When all users are trusted, isolation is for convenience (not security).

---

**Recommendation for QDAI**: **Strategy 1 (Catalog per Segment)** for strong isolation aligned with Hub-and-Spoke model.

---

## Access Control in Unity Catalog

### Permission Model (5 Levels)

Unity Catalog uses **privilege-based access control** (similar to SQL GRANT/REVOKE):

1. **Metastore**: `USE CATALOG`, `CREATE CATALOG`
2. **Catalog**: `USE SCHEMA`, `CREATE SCHEMA`
3. **Schema**: `SELECT`, `CREATE TABLE`, `MODIFY`
4. **Table/View**: `SELECT`, `MODIFY`, `READ_METADATA`
5. **Column**: `SELECT` on specific columns (column-level security)

### Permission Inheritance

```
Metastore Admin → Can do anything
  ├── Catalog Owner → Can manage catalog, grant permissions
  │   ├── Schema Owner → Can manage schema, grant permissions
  │   │   └── Table Owner → Can modify table, grant SELECT
```

### QDAI Permission Design

#### Platform Team (Hub)
```sql
-- Platform Architect: Metastore Admin
GRANT CREATE CATALOG ON METASTORE TO `platform_architects`;

-- Platform DevOps: Can create schemas, manage infrastructure
GRANT USE CATALOG, CREATE SCHEMA ON CATALOG `segment_na_ot` TO `platform_devops`;
GRANT USE CATALOG, CREATE SCHEMA ON CATALOG `segment_upstream` TO `platform_devops`;
```

#### Segment Teams (Spokes)
```sql
-- NA O&T Data Engineers: Can create tables in their catalog
GRANT USE CATALOG ON CATALOG `segment_na_ot` TO `na_ot_engineers`;
GRANT USE SCHEMA ON SCHEMA `segment_na_ot`.`bronze` TO `na_ot_engineers`;
GRANT CREATE TABLE, SELECT ON SCHEMA `segment_na_ot`.`bronze` TO `na_ot_engineers`;

-- NA O&T Analysts: Read-only on Gold layer
GRANT USE CATALOG ON CATALOG `segment_na_ot` TO `na_ot_analysts`;
GRANT USE SCHEMA ON SCHEMA `segment_na_ot`.`gold` TO `na_ot_analysts`;
GRANT SELECT ON SCHEMA `segment_na_ot`.`gold` TO `na_ot_analysts`;
```

#### Cross-Segment Access (Limited)
```sql
-- Allow Upstream team to read NA O&T Gold layer (for joint analysis)
GRANT USE CATALOG ON CATALOG `segment_na_ot` TO `upstream_analysts`;
GRANT USE SCHEMA ON SCHEMA `segment_na_ot`.`gold` TO `upstream_analysts`;
GRANT SELECT ON TABLE `segment_na_ot`.`gold`.`production_kpis` TO `upstream_analysts`;
```

---

## Advanced Access Control Features

### 1. Column-Level Security
Hide sensitive columns from unauthorized users:

```sql
-- Create view with column masking
CREATE VIEW gold.production_summary_public AS
SELECT
  well_id,
  well_name,
  production_date,
  oil_volume,
  gas_volume,
  -- Mask owner information
  'REDACTED' AS owner_name,
  'REDACTED' AS owner_ssn
FROM gold.production_summary;

-- Grant access to masked view
GRANT SELECT ON VIEW gold.production_summary_public TO `external_auditors`;
```

### 2. Row-Level Security (Row Filters)
Filter rows based on user attributes:

```sql
-- Create row filter function
CREATE FUNCTION filter_by_segment(segment_id STRING)
RETURN IF(IS_MEMBER('platform_admins'), TRUE, segment_id = CURRENT_USER());

-- Apply row filter to table
ALTER TABLE gold.production_summary
SET ROW FILTER filter_by_segment(segment_id);

-- Now users automatically see only their segment's data
```

### 3. Dynamic Data Masking
Mask data based on user role:

```sql
-- Create masking function
CREATE FUNCTION mask_pii(ssn STRING)
RETURN CASE
  WHEN IS_MEMBER('platform_admins') THEN ssn         -- Full SSN
  WHEN IS_MEMBER('na_ot_managers') THEN CONCAT('XXX-XX-', RIGHT(ssn, 4))  -- Last 4 digits
  ELSE 'REDACTED'                                    -- Fully masked
END;

-- Apply masking to column
ALTER TABLE gold.owner_info
ALTER COLUMN ssn SET MASK mask_pii(ssn);
```

---

## External Locations and Storage Credentials

Unity Catalog needs permissions to access ADLS Gen 2. Two components:

### 1. Storage Credential
**What**: Azure credentials used to access storage accounts
**Options**:
- **Managed Identity** (Recommended): Databricks workspace uses Azure Managed Identity to access ADLS
- **Service Principal**: Azure AD App Registration with secret/certificate

**QDAI Setup**:
```sql
-- Create storage credential using Managed Identity
CREATE STORAGE CREDENTIAL adls_credential
USING AZURE_MANAGED_IDENTITY
COMMENT 'Databricks workspace managed identity';
```

### 2. External Location
**What**: Mapping of ADLS Gen 2 path to Unity Catalog, with associated storage credential
**Purpose**: Allows Unity Catalog to govern data in ADLS (external tables)

**QDAI Setup**:
```sql
-- Create external location for Bronze layer
CREATE EXTERNAL LOCATION bronze_na_ot
URL 'abfss://bronze@quorumdatalake.dfs.core.windows.net/na_ot/'
WITH (STORAGE CREDENTIAL adls_credential)
COMMENT 'Bronze layer for NA O&T segment';

-- Create external location for Silver layer
CREATE EXTERNAL LOCATION silver_na_ot
URL 'abfss://silver@quorumdatalake.dfs.core.windows.net/na_ot/'
WITH (STORAGE CREDENTIAL adls_credential);

-- Create external location for Gold layer
CREATE EXTERNAL LOCATION gold_na_ot
URL 'abfss://gold@quorumdatalake.dfs.core.windows.net/na_ot/'
WITH (STORAGE CREDENTIAL adls_credential);
```

### 3. Create External Tables
```sql
-- Create external table in Unity Catalog pointing to ADLS
CREATE TABLE segment_na_ot.bronze.tips_wells
USING DELTA
LOCATION 'abfss://bronze@quorumdatalake.dfs.core.windows.net/na_ot/tips/wells';

-- Unity Catalog now governs access to this data
```

---

## Data Lineage

Unity Catalog automatically captures lineage for:
- **Table-to-Table**: Which tables are read/written by a query
- **Column-to-Column**: Which columns are derived from which source columns
- **Notebook-to-Table**: Which notebook created/updated a table
- **Dashboard-to-Table**: Which dashboards query which tables

**QDAI Use Cases**:
1. **Impact Analysis**: "If I change the Silver layer wells table schema, which Gold layer tables are affected?"
2. **Root Cause Analysis**: "This Gold layer metric is wrong - trace back to source system"
3. **Compliance**: "Show me the lineage from source system to regulatory report" (audit trail)
4. **Data Discovery**: "Find all tables containing production data"

**Accessing Lineage**:
- **Databricks UI**: Data Explorer → Table → Lineage tab
- **Unity Catalog REST API**: Programmatic access to lineage graph
- **Integration with Azure Purview**: Sync lineage to Purview for enterprise catalog

---

## Audit Logging

Unity Catalog logs all access and modifications:
- **Who**: User/service principal
- **What**: Table/view/schema/catalog accessed
- **When**: Timestamp
- **How**: Query text, notebook, dashboard
- **Result**: Success/failure

**QDAI Audit Use Cases**:
1. **Security**: "Who accessed PII data in the last 30 days?"
2. **Compliance**: "Show all access to production data for SOC 2 audit"
3. **Cost Analysis**: "Which team is running the most expensive queries?"
4. **Troubleshooting**: "Who modified this table schema last week?"

**Accessing Audit Logs**:
- **System Tables**: Unity Catalog publishes audit logs to system tables
  ```sql
  SELECT * FROM system.access.audit
  WHERE table_name = 'segment_na_ot.gold.production_kpis'
  AND event_date > CURRENT_DATE - 30;
  ```
- **Export to SIEM**: Stream audit logs to Azure Sentinel, Splunk, or other SIEM tools

---

## Delta Sharing (Optional for QDAI)

**What**: Securely share data from Unity Catalog with external parties (customers, partners) without copying data

**Use Case for QDAI**: If Quorum wants to share production data with customers (read-only)

**How it Works**:
1. Create a **share** in Unity Catalog
   ```sql
   CREATE SHARE customer_data_share;
   ALTER SHARE customer_data_share ADD TABLE segment_na_ot.gold.production_summary;
   ```
2. Create a **recipient** (external party)
   ```sql
   CREATE RECIPIENT customer_acme;
   GRANT SELECT ON SHARE customer_data_share TO RECIPIENT customer_acme;
   ```
3. Customer accesses data via Delta Sharing protocol (no Databricks workspace needed)

**Benefits**:
- No data copying (single source of truth)
- Access controlled by Unity Catalog
- Audit logs show external access

---

## Unity Catalog Best Practices for QDAI

### 1. Naming Conventions
- **Catalogs**: `segment_<segment_name>` (e.g., `segment_na_ot`)
- **Schemas**: `<layer>` or `<layer>_<domain>` (e.g., `bronze`, `silver_wells`, `gold_production`)
- **Tables**: `<layer>_<domain>_<entity>_<granularity>` (e.g., `gold_production_daily_v1`)

### 2. Separation of Duties
- **Platform Team**: Metastore admin, creates catalogs, external locations
- **Segment Teams**: Catalog owner (their segment), create schemas/tables
- **Analysts**: Read-only on Gold layer, no write access

### 3. Principle of Least Privilege
- Grant permissions at the lowest necessary level (schema or table, not catalog)
- Use groups, not individual users (easier to manage)
- Regularly review permissions (quarterly audit)

### 4. Immutable Bronze Layer
- Bronze layer is append-only (no MODIFY permission for analysts)
- Only platform team can modify Bronze schema

### 5. Versioned Gold Layer
- Gold layer tables include version suffix (e.g., `gold_production_kpis_v1`)
- When breaking schema change, create `v2` (don't drop `v1` immediately)
- Allows gradual migration of downstream consumers

### 6. Documentation
- Use `COMMENT` on catalogs, schemas, tables, columns
  ```sql
  CREATE TABLE segment_na_ot.gold.production_kpis
  COMMENT 'Daily production KPIs aggregated by well, lease, and field'
  (
    well_id STRING COMMENT 'API well identifier (14-digit)',
    production_date DATE COMMENT 'Production date',
    oil_volume_bbl DECIMAL(10,2) COMMENT 'Oil production in barrels'
  );
  ```

### 7. Testing in Dev Catalog
- Create `segment_na_ot_dev`, `segment_na_ot_test`, `segment_na_ot_prod` catalogs
- Test schema changes, permissions in dev before prod

---

## Unity Catalog Deployment (Terraform)

Unity Catalog resources can be managed via Terraform (Infrastructure as Code):

```hcl
# Configure Databricks provider
terraform {
  required_providers {
    databricks = {
      source = "databricks/databricks"
    }
  }
}

provider "databricks" {
  host  = var.databricks_workspace_url
  token = var.databricks_token
}

# Create storage credential
resource "databricks_storage_credential" "adls_credential" {
  name = "adls_credential"
  azure_managed_identity {
    access_connector_id = var.access_connector_id
  }
  comment = "Managed Identity for ADLS access"
}

# Create external location for Bronze layer
resource "databricks_external_location" "bronze_na_ot" {
  name            = "bronze_na_ot"
  url             = "abfss://bronze@${var.storage_account}.dfs.core.windows.net/na_ot/"
  credential_name = databricks_storage_credential.adls_credential.name
  comment         = "Bronze layer for NA O&T segment"
}

# Create catalog
resource "databricks_catalog" "segment_na_ot" {
  name    = "segment_na_ot"
  comment = "Catalog for North America O&T segment"
  properties = {
    purpose = "segment_data"
  }
}

# Create schema
resource "databricks_schema" "bronze" {
  catalog_name = databricks_catalog.segment_na_ot.name
  name         = "bronze"
  comment      = "Raw data from source systems"
}

# Grant permissions
resource "databricks_grant" "na_ot_engineers_bronze" {
  catalog = databricks_catalog.segment_na_ot.name
  principal  = "na_ot_engineers"
  privileges = ["USE_CATALOG", "USE_SCHEMA", "CREATE_TABLE", "SELECT"]
}
```

**Benefits of Terraform for Unity Catalog**:
- **Repeatable**: Deploy same structure to dev/test/prod
- **Version-controlled**: Track changes to permissions, catalogs in Git
- **Auditable**: Who changed what, when
- **Automated**: CI/CD pipeline deploys Unity Catalog changes

---

## Unity Catalog Monitoring

### Key Metrics to Track

1. **Access Patterns**:
   - Which tables are queried most frequently?
   - Which users/groups access sensitive data?
   - Query latency by table

2. **Storage Growth**:
   - Size of tables by catalog/schema
   - Growth rate (GB per day)

3. **Permission Changes**:
   - Who granted/revoked permissions?
   - Frequency of permission changes (too frequent = loose governance)

4. **Failed Access Attempts**:
   - Users trying to access data they don't have permission for
   - Potential security issues (investigate)

**Monitoring Dashboard** (SQL queries on system tables):
```sql
-- Top 10 most accessed tables (last 7 days)
SELECT table_name, COUNT(*) AS access_count
FROM system.access.audit
WHERE event_date > CURRENT_DATE - 7
GROUP BY table_name
ORDER BY access_count DESC
LIMIT 10;

-- Failed access attempts (last 24 hours)
SELECT user_name, table_name, event_time
FROM system.access.audit
WHERE event_date > CURRENT_DATE - 1
AND request_status = 'PERMISSION_DENIED'
ORDER BY event_time DESC;

-- Storage usage by catalog
SELECT catalog_name, SUM(size_bytes) / 1024 / 1024 / 1024 AS size_gb
FROM system.information_schema.tables
GROUP BY catalog_name
ORDER BY size_gb DESC;
```

---

## Common Unity Catalog Issues & Solutions

### Issue 1: "Permission Denied" when accessing table
**Cause**: User doesn't have `USE CATALOG`, `USE SCHEMA`, or `SELECT` permission
**Solution**:
```sql
-- Check permissions
SHOW GRANTS ON TABLE segment_na_ot.gold.production_kpis;

-- Grant necessary permissions
GRANT USE CATALOG ON CATALOG segment_na_ot TO `user@example.com`;
GRANT USE SCHEMA ON SCHEMA segment_na_ot.gold TO `user@example.com`;
GRANT SELECT ON TABLE segment_na_ot.gold.production_kpis TO `user@example.com`;
```

### Issue 2: "External location not found"
**Cause**: External location not created or wrong ADLS path
**Solution**:
```sql
-- Create external location
CREATE EXTERNAL LOCATION bronze_na_ot
URL 'abfss://bronze@quorumdatalake.dfs.core.windows.net/na_ot/'
WITH (STORAGE CREDENTIAL adls_credential);

-- Verify ADLS path is correct (check Azure Portal)
```

### Issue 3: Lineage not showing
**Cause**: Lineage only captured for Unity Catalog-enabled workspaces
**Solution**: Ensure workspace is assigned to Unity Catalog metastore (Admin Console)

### Issue 4: Slow queries after enabling Unity Catalog
**Cause**: Unity Catalog adds slight overhead for permission checks
**Solution**:
- Optimize queries (partition pruning, predicate pushdown)
- Use Delta Lake caching
- Consider materialized views for frequently accessed data

---

## Interview Questions to Prepare

1. **"Explain the Unity Catalog hierarchy and how you'd design it for QDAI."**
   - Answer: Metastore → Catalog (per segment) → Schema (Bronze/Silver/Gold) → Tables

2. **"How do you implement row-level security in Unity Catalog?"**
   - Answer: Row filter functions applied to tables

3. **"What's the difference between managed and external tables in Unity Catalog?"**
   - Answer: Managed = UC owns data, External = data in ADLS (recommended for QDAI)

4. **"How does Unity Catalog integrate with Azure ADLS Gen 2?"**
   - Answer: Storage credentials (Managed Identity) + External locations

5. **"How do you monitor who's accessing sensitive data?"**
   - Answer: Unity Catalog audit logs (system.access.audit table)

6. **"Can Unity Catalog enforce data quality rules?"**
   - Answer: No, UC is governance (permissions, lineage). Use Delta Live Tables for data quality.

---

## Summary

Unity Catalog is the **governance backbone** for QDAI platform:
- **Multi-tenancy**: Catalog per segment (strong isolation)
- **Access Control**: Fine-grained permissions (catalog → schema → table → column)
- **Lineage**: Automatic lineage capture for compliance and troubleshooting
- **Audit**: Who accessed what, when (security and compliance)
- **External Data**: Govern data in ADLS Gen 2 (external tables)

**Key Message for Interview**: "Unity Catalog enables Quorum's Hub-and-Spoke model by providing centralized governance with federated autonomy. Platform team controls standards (Metastore admin), segment teams manage their own data (Catalog owners), and all access is audited for compliance."

---

Good luck! 🚀
