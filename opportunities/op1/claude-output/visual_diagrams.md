# Visual Architecture Diagrams
## Quorum Data & AI Platform (QDAI)

This document contains architecture diagrams to help visualize key concepts for the interview. These diagrams are in Mermaid format and can be rendered in most markdown viewers or converted to images.

---

## Diagram 1: Azure Well-Architected Framework Applied to QDAI

```mermaid
graph TD
    subgraph "Azure Well-Architected Framework for QDAI"
        A[Cost Optimization] --> A1[Job Clusters vs Always-On]
        A --> A2[Storage Lifecycle Management]
        A --> A3[Spot VMs for Dev/Test]
        A --> A4[Chargeback by Segment]
        A --> A5[Reserved Instances]

        B[Operational Excellence] --> B1[Infrastructure as Code - Terraform]
        B --> B2[CI/CD Pipelines - Azure DevOps]
        B --> B3[Monitoring - Azure Monitor]
        B --> B4[Runbooks & Documentation]
        B --> B5[Knowledge Transfer & Training]

        C[Performance Efficiency] --> C1[Databricks Autoscaling]
        C --> C2[Delta Lake OPTIMIZE & Z-ORDER]
        C --> C3[Photon Acceleration]
        C --> C4[Partition Strategy]
        C --> C5[Delta Cache]

        D[Reliability] --> D1[Multi-Region HA/DR]
        D --> D2[GRS for ADLS Gen 2]
        D --> D3[Unity Catalog Backup]
        D --> D4[Retry Logic & Circuit Breakers]
        D --> D5[99.9% Uptime SLA]

        E[Security] --> E1[Zero Trust - Private Endpoints]
        E --> E2[Azure AD + MFA]
        E --> E3[Encryption At-Rest & In-Transit]
        E --> E4[Unity Catalog RBAC]
        E --> E5[Audit Logging]
    end

    style A fill:#90EE90
    style B fill:#87CEEB
    style C fill:#FFB6C1
    style D fill:#FFD700
    style E fill:#FF6347
```

**How to Use in Interview**: "Let me walk you through how I'd apply the 5 pillars of Azure WAF to QDAI..."

---

## Diagram 2: TOGAF ADM Phases for QDAI

```mermaid
graph LR
    subgraph "TOGAF Architecture Development Method"
        P[Preliminary:<br/>Architecture Capability] --> A[Phase A:<br/>Architecture Vision]
        A --> B[Phase B:<br/>Business Architecture]
        B --> C[Phase C:<br/>Information Systems]
        C --> D[Phase D:<br/>Technology Architecture]
        D --> E[Phase E:<br/>Opportunities & Solutions]
        E --> F[Phase F:<br/>Migration Planning]
        F --> G[Phase G:<br/>Implementation Governance]
        G --> H[Phase H:<br/>Architecture Change Mgmt]
        H --> A

        R[Requirements Management] -.-> P
        R -.-> A
        R -.-> B
        R -.-> C
        R -.-> D
        R -.-> E
        R -.-> F
        R -.-> G
        R -.-> H
    end

    style P fill:#E6E6FA
    style A fill:#FFE4B5
    style B fill:#98FB98
    style C fill:#87CEEB
    style D fill:#DDA0DD
    style E fill:#F0E68C
    style F fill:#FFA07A
    style G fill:#20B2AA
    style H fill:#DB7093
    style R fill:#FFB6C1
```

**QDAI Application**:
- **Preliminary**: Establish ARB, architecture principles
- **Phase A**: Hub-and-Spoke vision, stakeholder buy-in
- **Phase B**: Business capabilities (Ingestion, Transformation, Governance, Consumption, AI/ML)
- **Phase C**: Medallion Architecture, Unity Catalog, Knowledge Graph
- **Phase D**: Azure + Databricks + ADLS Gen 2 + Neo4j
- **Phase E**: 4-phase implementation roadmap (Foundation → Pilot → Scale → Innovate)
- **Phase F**: Phased migration (domain by domain, parallel run)
- **Phase G**: ARB design reviews, compliance checks
- **Phase H**: Continuous monitoring, change requests, technology radar

---

## Diagram 3: Medallion Architecture (Bronze → Silver → Gold)

```mermaid
graph LR
    subgraph "Source Systems"
        S1[TIPS]
        S2[QPTM]
        S3[eONE]
        S4[FLOWCAL]
    end

    subgraph "Bronze Layer - Raw"
        B1[bronze/tips]
        B2[bronze/qptm]
        B3[bronze/eone]
        B4[bronze/flowcal]
    end

    subgraph "Silver Layer - Curated + MDM"
        SI1[silver/wells]
        SI2[silver/production]
        SI3[silver/land]
        SI4[silver/accounting]
        MDM[Master Data:<br/>Meters, Locations, Products]
    end

    subgraph "Gold Layer - Business Metrics"
        G1[gold/production_kpis]
        G2[gold/regulatory_reports]
        G3[gold/dashboards]
        G4[gold/knowledge_graph_nodes]
    end

    subgraph "Consumption"
        C1[Power BI Dashboards]
        C2[Agentic AI]
        C3[Regulatory Reporting]
        KG[Knowledge Graph<br/>Neo4j]
    end

    S1 --> B1
    S2 --> B2
    S3 --> B3
    S4 --> B4

    B1 --> SI1
    B2 --> SI1
    B3 --> SI2
    B4 --> SI3

    SI1 --> MDM
    SI2 --> MDM
    SI3 --> MDM
    SI4 --> MDM

    MDM --> G1
    MDM --> G2
    MDM --> G3
    MDM --> G4

    G1 --> C1
    G2 --> C3
    G3 --> C1
    G4 --> KG

    KG --> C2

    style B1 fill:#FFE4B5
    style B2 fill:#FFE4B5
    style B3 fill:#FFE4B5
    style B4 fill:#FFE4B5
    style SI1 fill:#98FB98
    style SI2 fill:#98FB98
    style SI3 fill:#98FB98
    style SI4 fill:#98FB98
    style MDM fill:#87CEEB
    style G1 fill:#FFD700
    style G2 fill:#FFD700
    style G3 fill:#FFD700
    style G4 fill:#FFD700
```

**Key Points**:
- **Bronze**: Immutable, raw, append-only (audit trail)
- **Silver**: Cleansed, conformed, MDM-enriched (single source of truth)
- **Gold**: Business-ready, pre-aggregated, semantic layer

---

## Diagram 4: Hub-and-Spoke Operating Model

```mermaid
graph TD
    subgraph "Hub - Control Tower"
        PSA[Platform Solution Architect<br/>'Supreme Court']
        DE1[DevOps Data Engineer 1]
        DE2[DevOps Data Engineer 2]
    end

    subgraph "Spoke 1 - NA O&T Segment"
        NA_Arch[NA O&T Architect]
        NA_Eng[NA O&T Engineers]
        NA_Data[NA O&T Data Products]
    end

    subgraph "Spoke 2 - Upstream Segment"
        UP_Arch[Upstream Architect]
        UP_Eng[Upstream Engineers]
        UP_Data[Upstream Data Products]
    end

    subgraph "Spoke 3 - Intl O&T Segment"
        IN_Arch[Intl Architect]
        IN_Eng[Intl Engineers]
        IN_Data[Intl Data Products]
    end

    subgraph "Platform Services"
        UC[Unity Catalog<br/>Governance]
        ADLS[ADLS Gen 2<br/>Storage]
        DBC[Databricks<br/>Compute]
        CICD[CI/CD Pipelines]
        MON[Monitoring & Alerts]
    end

    PSA --> NA_Arch
    PSA --> UP_Arch
    PSA --> IN_Arch

    DE1 --> UC
    DE1 --> ADLS
    DE2 --> DBC
    DE2 --> CICD

    NA_Arch --> NA_Eng
    UP_Arch --> UP_Eng
    IN_Arch --> IN_Eng

    NA_Eng --> NA_Data
    UP_Eng --> UP_Data
    IN_Eng --> IN_Data

    NA_Data --> UC
    UP_Data --> UC
    IN_Data --> UC

    NA_Data --> ADLS
    UP_Data --> ADLS
    IN_Data --> ADLS

    NA_Eng --> DBC
    UP_Eng --> DBC
    IN_Eng --> DBC

    UC --> MON
    ADLS --> MON
    DBC --> MON

    style PSA fill:#FF6347
    style DE1 fill:#FFB6C1
    style DE2 fill:#FFB6C1
    style NA_Arch fill:#90EE90
    style UP_Arch fill:#90EE90
    style IN_Arch fill:#90EE90
    style UC fill:#87CEEB
    style ADLS fill:#87CEEB
    style DBC fill:#87CEEB
```

**Key Points**:
- **Hub (Control Tower)**: Platform team provides shared services, sets standards, enforces guardrails
- **Spokes (Segment Teams)**: Build data products within platform guardrails, autonomy with governance
- **Platform Services**: Unity Catalog, ADLS, Databricks, CI/CD, Monitoring (shared by all segments)

---

## Diagram 5: Unity Catalog Hierarchy for QDAI

```mermaid
graph TD
    subgraph "Unity Catalog Architecture"
        M[Metastore<br/>Region: East US 2]

        subgraph "Catalog: segment_na_ot"
            C1_B[Schema: bronze]
            C1_S[Schema: silver]
            C1_G[Schema: gold]

            C1_B --> T1[Table: tips_wells]
            C1_B --> T2[Table: qptm_production]

            C1_S --> T3[Table: wells_curated]
            C1_S --> T4[Table: production_curated]

            C1_G --> T5[Table: production_kpis]
            C1_G --> T6[Table: regulatory_reports]
        end

        subgraph "Catalog: segment_upstream"
            C2_B[Schema: bronze]
            C2_S[Schema: silver]
            C2_G[Schema: gold]
        end

        subgraph "Catalog: segment_intl"
            C3_B[Schema: bronze]
            C3_S[Schema: silver]
            C3_G[Schema: gold]
        end

        subgraph "Catalog: platform_shared"
            C4[Schema: common]
            C4 --> T7[Table: reference_data]
        end

        M --> C1_B
        M --> C2_B
        M --> C3_B
        M --> C4
    end

    subgraph "Access Control"
        PlatformTeam[Platform Team:<br/>Metastore Admin]
        NATeam[NA O&T Team:<br/>Catalog Owner]
        Analysts[Analysts:<br/>Gold Layer SELECT]
    end

    PlatformTeam --> M
    NATeam --> C1_B
    Analysts --> C1_G

    style M fill:#FF6347
    style C1_B fill:#FFE4B5
    style C1_S fill:#98FB98
    style C1_G fill:#FFD700
    style C2_B fill:#FFE4B5
    style C2_S fill:#98FB98
    style C2_G fill:#FFD700
    style C3_B fill:#FFE4B5
    style C3_S fill:#98FB98
    style C3_G fill:#FFD700
    style PlatformTeam fill:#FF6347
    style NATeam fill:#90EE90
    style Analysts fill:#87CEEB
```

**Key Points**:
- **Catalog per Segment**: Strong isolation, autonomy, chargeback visibility
- **Schemas by Layer**: Bronze, Silver, Gold within each catalog
- **Access Control**: Platform team (Metastore admin), Segment teams (Catalog owners), Analysts (Gold layer read-only)

---

## Diagram 6: Knowledge Graph Architecture

```mermaid
graph TD
    subgraph "Delta Lake - Source of Truth"
        DL1[Gold: wells]
        DL2[Gold: leases]
        DL3[Gold: production]
        DL4[Gold: owners]
        DL5[Gold: accounts]
    end

    subgraph "Graph Materialization Job"
        J1[Read Delta Tables]
        J2[Transform to Graph Format]
        J3[Generate Nodes & Edges]
        J4[Load to Neo4j]
    end

    subgraph "Neo4j Knowledge Graph"
        N1[Node: Well]
        N2[Node: Lease]
        N3[Node: Production]
        N4[Node: Owner]
        N5[Node: Account]

        N1 -->|belongs_to| N2
        N2 -->|owned_by| N4
        N1 -->|produces| N3
        N3 -->|generates_revenue| N5
        N4 -->|has_interest_in| N5
    end

    subgraph "Query Layer"
        GQL[GraphQL API]
        CYPHER[Cypher Queries]
    end

    subgraph "Consumers"
        AI[Agentic AI:<br/>Multi-hop Questions]
        AN[Analysts:<br/>Impact Analysis]
        DASH[Dashboards:<br/>Relationship Viz]
    end

    DL1 --> J1
    DL2 --> J1
    DL3 --> J1
    DL4 --> J1
    DL5 --> J1

    J1 --> J2
    J2 --> J3
    J3 --> J4

    J4 --> N1
    J4 --> N2
    J4 --> N3
    J4 --> N4
    J4 --> N5

    N1 --> GQL
    N2 --> GQL
    GQL --> CYPHER

    CYPHER --> AI
    CYPHER --> AN
    CYPHER --> DASH

    style DL1 fill:#FFD700
    style DL2 fill:#FFD700
    style DL3 fill:#FFD700
    style DL4 fill:#FFD700
    style DL5 fill:#FFD700
    style J1 fill:#87CEEB
    style J2 fill:#87CEEB
    style J3 fill:#87CEEB
    style J4 fill:#87CEEB
    style N1 fill:#98FB98
    style N2 fill:#98FB98
    style N3 fill:#98FB98
    style N4 fill:#98FB98
    style N5 fill:#98FB98
    style GQL fill:#FFB6C1
    style AI fill:#FF6347
```

**Key Points**:
- **Delta Lake = Source of Truth**: Gold layer tables are authoritative
- **Graph = Specialized Index**: Optimized for relationship traversal
- **Materialization**: Scheduled job (nightly/hourly) syncs Delta → Neo4j
- **Query Layer**: GraphQL API abstracts Cypher complexity
- **Consumers**: Agentic AI, impact analysis, relationship visualization

---

## Diagram 7: Disaster Recovery Multi-Region Architecture

```mermaid
graph TD
    subgraph "Primary Region - East US 2"
        P_DBC[Databricks Workspace]
        P_ADLS[ADLS Gen 2 - GRS]
        P_UC[Unity Catalog Metastore]
        P_APP[Applications & Pipelines]
    end

    subgraph "Secondary Region - Central US"
        S_DBC[Databricks Workspace<br/>Dormant]
        S_ADLS[ADLS Gen 2 - GRS Replica]
        S_UC[Unity Catalog Backup<br/>Hourly]
        S_APP[Infrastructure Pre-Deployed<br/>via Terraform]
    end

    subgraph "Failover Process"
        F1[1. Detect Primary Region Outage]
        F2[2. ADLS GRS Failover]
        F3[3. Restore Unity Catalog]
        F4[4. Activate Databricks Secondary]
        F5[5. Update DNS/Traffic Manager]
        F6[6. Run Smoke Tests]
        F7[7. Resume Production]
    end

    P_ADLS -.->|Async Replication<br/>~15 min lag| S_ADLS
    P_UC -.->|Hourly Backup| S_UC

    P_DBC --> P_ADLS
    P_APP --> P_DBC
    P_APP --> P_UC

    F1 --> F2
    F2 --> F3
    F3 --> F4
    F4 --> F5
    F5 --> F6
    F6 --> F7

    F2 --> S_ADLS
    F3 --> S_UC
    F4 --> S_DBC
    F7 --> S_APP

    style P_DBC fill:#90EE90
    style P_ADLS fill:#90EE90
    style P_UC fill:#90EE90
    style P_APP fill:#90EE90
    style S_DBC fill:#FFB6C1
    style S_ADLS fill:#FFB6C1
    style S_UC fill:#FFB6C1
    style S_APP fill:#FFB6C1
    style F1 fill:#FF6347
    style F2 fill:#FF6347
    style F3 fill:#FF6347
    style F4 fill:#FF6347
    style F5 fill:#FF6347
    style F6 fill:#FF6347
    style F7 fill:#FF6347
```

**Key Metrics**:
- **RTO**: 4 hours (Recovery Time Objective)
- **RPO**: 1 hour (Recovery Point Objective - GRS lag ~15 min, Unity Catalog backup hourly)
- **Cost**: +12% (secondary region infrastructure dormant, GRS +50% on storage)
- **Testing**: Quarterly DR drills in non-prod, annual prod failover

---

## Diagram 8: CI/CD Pipeline for Data Platform

```mermaid
graph LR
    subgraph "Source Control"
        GIT[Git Repository<br/>Azure DevOps Repos]
        BR1[Branch: main]
        BR2[Branch: develop]
        BR3[Branch: feature/na-pipeline]
    end

    subgraph "CI Pipeline - Build & Test"
        BUILD[Build Artifacts]
        LINT[Lint: black, flake8]
        TEST[Unit Tests: pytest]
        SCAN[Security Scan]
        PACKAGE[Package: wheels, notebooks]
    end

    subgraph "CD Pipeline - Deploy"
        DEPLOY_DEV[Deploy to Dev]
        SMOKE_DEV[Smoke Tests]
        DEPLOY_TEST[Deploy to Test]
        INT_TEST[Integration Tests]
        APPROVAL[Manual Approval Gate]
        DEPLOY_PROD[Deploy to Prod]
        SMOKE_PROD[Smoke Tests Prod]
    end

    subgraph "Environments"
        ENV_DEV[Dev Databricks Workspace]
        ENV_TEST[Test Databricks Workspace]
        ENV_PROD[Prod Databricks Workspace]
    end

    BR3 --> GIT
    GIT -->|PR Merge to develop| BR2
    BR2 --> BUILD

    BUILD --> LINT
    LINT --> TEST
    TEST --> SCAN
    SCAN --> PACKAGE

    PACKAGE --> DEPLOY_DEV
    DEPLOY_DEV --> ENV_DEV
    ENV_DEV --> SMOKE_DEV

    SMOKE_DEV -->|Auto-Deploy| DEPLOY_TEST
    DEPLOY_TEST --> ENV_TEST
    ENV_TEST --> INT_TEST

    INT_TEST --> APPROVAL

    BR2 -->|PR Merge to main| BR1
    BR1 --> APPROVAL
    APPROVAL -->|Approved| DEPLOY_PROD
    DEPLOY_PROD --> ENV_PROD
    ENV_PROD --> SMOKE_PROD

    style GIT fill:#FFE4B5
    style BUILD fill:#87CEEB
    style LINT fill:#87CEEB
    style TEST fill:#87CEEB
    style SCAN fill:#87CEEB
    style DEPLOY_DEV fill:#98FB98
    style DEPLOY_TEST fill:#FFD700
    style APPROVAL fill:#FF6347
    style DEPLOY_PROD fill:#FF6347
```

**Key Points**:
- **Git Workflow**: Feature → Develop → Main (no direct commits to main)
- **CI**: Lint, test, scan on every PR
- **CD**: Auto-deploy to dev/test, manual approval for prod
- **Infrastructure as Code**: Terraform in same pipeline for infra changes

---

## Diagram 9: Cost Optimization Strategies

```mermaid
graph TD
    subgraph "Cost Optimization Framework"
        A[Total Azure Cost: $180K/month]

        A --> B[Compute: $99K - 55%]
        A --> C[Storage: $36K - 20%]
        A --> D[Network: $18K - 10%]
        A --> E[Other: $27K - 15%]

        B --> B1[Job Clusters vs Always-On<br/>Savings: $15K/month]
        B --> B2[Spot VMs for Dev/Test<br/>Savings: $12K/month]
        B --> B3[Right-Sizing Clusters<br/>Savings: $10K/month]
        B --> B4[Photon Optimization<br/>Net Savings: $5K/month]

        C --> C1[Lifecycle Management<br/>Cool/Archive Tiers<br/>Savings: $8K/month]
        C --> C2[Delta Lake OPTIMIZE<br/>Reduce Metadata<br/>Savings: $3K/month]
        C --> C3[Delete Temp Data<br/>Savings: $2K/month]

        D --> D1[Co-locate Resources<br/>Same Region<br/>Savings: $3K/month]
        D --> D2[Private Endpoints<br/>vs Public<br/>Savings: $2K/month]

        E --> E1[Delete Orphaned Resources<br/>Savings: $4K/month]
        E --> E2[Reserved Instances<br/>1-year Commit<br/>Savings: $6K/month]
    end

    subgraph "Total Savings"
        SAVE[Total Monthly Savings:<br/>$70K 38% reduction<br/>New Cost: $110K/month]
    end

    B1 --> SAVE
    B2 --> SAVE
    B3 --> SAVE
    B4 --> SAVE
    C1 --> SAVE
    C2 --> SAVE
    C3 --> SAVE
    D1 --> SAVE
    D2 --> SAVE
    E1 --> SAVE
    E2 --> SAVE

    style A fill:#FF6347
    style B fill:#FFB6C1
    style C fill:#87CEEB
    style D fill:#98FB98
    style E fill:#FFD700
    style SAVE fill:#90EE90
```

**Key Message**: "I achieved 38% cost reduction through systematic optimization across compute, storage, networking, using Azure WAF Cost Optimization best practices."

---

## Diagram 10: Architecture Governance Model (TOGAF)

```mermaid
graph TD
    subgraph "Architecture Review Board - ARB"
        CHAIR[Platform Solution Architect<br/>Chair]
        M1[NA O&T Architect]
        M2[Upstream Architect]
        M3[Intl Architect]
        M4[Lead DevOps Engineer]
        M5[InfoSec Representative]
    end

    subgraph "Design Review Process"
        S1[Team Submits Design]
        S2[Self-Assessment vs Standards]
        S3[ARB Review Meeting<br/>Bi-weekly]
        D1{Decision}
        D2[Approved]
        D3[Approved with Conditions]
        D4[Rejected with Feedback]
        S4[Implement]
        S5[Re-submit]
    end

    subgraph "Automated Compliance"
        A1[Terraform Sentinel Policies]
        A2[Unity Catalog Policies]
        A3[CI/CD Gates]
        A4[Azure Policy]
        A5[Quarterly Audit]
    end

    subgraph "Standards & Patterns"
        STD1[Architecture Principles]
        STD2[Terraform Modules]
        STD3[DLT Pipeline Templates]
        STD4[ADRs - Decision Records]
        STD5[Design Patterns Catalog]
    end

    CHAIR --> S3
    M1 --> S3
    M2 --> S3
    M3 --> S3
    M4 --> S3
    M5 --> S3

    S1 --> S2
    S2 --> S3
    S3 --> D1
    D1 --> D2
    D1 --> D3
    D1 --> D4
    D2 --> S4
    D3 --> S4
    D4 --> S5
    S5 --> S3

    S4 --> A1
    S4 --> A2
    S4 --> A3
    S4 --> A4

    A1 --> A5
    A2 --> A5
    A3 --> A5
    A4 --> A5

    STD1 -.-> S2
    STD2 -.-> S2
    STD3 -.-> S2
    STD4 -.-> S3
    STD5 -.-> S2

    style CHAIR fill:#FF6347
    style M1 fill:#90EE90
    style M2 fill:#90EE90
    style M3 fill:#90EE90
    style S3 fill:#FFD700
    style D1 fill:#FF6347
    style A1 fill:#87CEEB
    style A2 fill:#87CEEB
    style A3 fill:#87CEEB
    style A4 fill:#87CEEB
    style A5 fill:#87CEEB
```

**Key Points**:
- **ARB**: Cross-functional board reviews designs (not a bottleneck - guardrails)
- **Process**: Submit → Self-assess → Review → Decision (5 business days)
- **Automated Compliance**: Most governance automated (not manual gates)
- **Standards**: Reusable components accelerate teams

---

## How to Use These Diagrams in Interview

### Approach 1: Draw on Whiteboard
- If interview is in-person or virtual with whiteboard sharing
- Practice drawing key diagrams from memory (Medallion Architecture, Hub-and-Spoke, Unity Catalog)
- Don't need perfect diagrams - clarity of thinking matters more than artistic skill

### Approach 2: Reference Verbally
- "Let me walk you through the architecture using the Azure WAF pillars..." (refer to Diagram 1)
- "Our Hub-and-Spoke model works like this..." (refer to Diagram 4)
- "The Knowledge Graph sits on top of Delta Lake..." (refer to Diagram 6)

### Approach 3: Bring Printed Version
- Print 2-3 key diagrams (Medallion Architecture, Hub-and-Spoke, Unity Catalog)
- Refer to them during discussion
- Offer to leave copies with interviewers

### Approach 4: Share Screen (Virtual Interview)
- Open this markdown file in a viewer that renders Mermaid diagrams
- Share screen when explaining architecture concepts
- Walk through diagrams step-by-step

---

## Quick Diagram Reference

| Interview Question | Use This Diagram |
|-------------------|------------------|
| "How would you apply Azure WAF to QDAI?" | Diagram 1: Azure WAF |
| "Walk me through your approach using TOGAF" | Diagram 2: TOGAF ADM |
| "Explain the Medallion Architecture" | Diagram 3: Medallion Architecture |
| "How does Hub-and-Spoke work?" | Diagram 4: Hub-and-Spoke Model |
| "Explain Unity Catalog for multi-tenancy" | Diagram 5: Unity Catalog Hierarchy |
| "How does the Knowledge Graph work?" | Diagram 6: Knowledge Graph Architecture |
| "Describe your DR strategy" | Diagram 7: DR Multi-Region |
| "How do you implement CI/CD for data pipelines?" | Diagram 8: CI/CD Pipeline |
| "How would you reduce costs?" | Diagram 9: Cost Optimization |
| "Explain your governance model" | Diagram 10: Architecture Governance |

---

## Converting Diagrams to Images

If you need actual image files (.png):

1. **Online Mermaid Editor**:
   - Go to https://mermaid.live/
   - Paste Mermaid code
   - Export as PNG/SVG

2. **VS Code Extension**:
   - Install "Markdown Preview Mermaid Support" extension
   - Preview this file, right-click diagram, "Copy as Image"

3. **Command-Line**:
   ```bash
   npm install -g @mermaid-js/mermaid-cli
   mmdc -i visual_diagrams.md -o diagrams.pdf
   ```

---

## Practice Tip

**Before the interview**:
1. Pick 3-4 diagrams most relevant to QDAI (Medallion, Hub-and-Spoke, Unity Catalog, Knowledge Graph)
2. Practice drawing them from memory on a whiteboard or paper
3. Practice explaining each component while drawing
4. Aim for clarity, not perfection

**During the interview**:
- Use diagrams to structure your answers (visual thinking)
- Draw simple boxes and arrows (don't worry about aesthetics)
- Label clearly
- Walk interviewer through step-by-step

---

Good luck! 🚀
