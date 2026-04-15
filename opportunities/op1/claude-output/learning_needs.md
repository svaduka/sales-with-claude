# Learning Needs: Quorum Data & AI Platform (op1)

## Overview
This document outlines the learning topics required to strengthen capability alignment for the Quorum Data & AI Platform opportunity. Topics are prioritized based on their criticality to the role and the opportunity's core requirements.

---

## Priority Definitions

- **HIGH**: Core requirement for the role; directly impacts ability to deliver on primary responsibilities
- **MEDIUM**: Important for comprehensive coverage; enhances effectiveness but not immediately critical
- **LOW**: Valuable for long-term success; supports advanced or future capabilities

---

## High Priority Learning Topics

### 1. Azure Data Factory (ADF)
**Reason**: Core ingestion tool for the platform. The DevOps Data Engineer must "build the automated, reusable pipelines to land data in Bronze" using ADF. Job description explicitly lists ADF as required deep expertise.

**Learning Objectives**:
- Understand ADF pipeline design patterns (Copy Activity, Data Flow, Control Flow)
- Learn ADF integration with Databricks (via Linked Services, Notebooks)
- Master parameterized pipelines and dynamic configurations
- Understand ADF monitoring, logging, and troubleshooting
- Learn Private Link integration for secure Quorum product connectivity
- Practice Change Data Capture (CDC) patterns for source systems

**Resources**:
- Microsoft Learn: [Azure Data Factory documentation](https://learn.microsoft.com/en-us/azure/data-factory/)
- Hands-on labs: Create pipelines from multiple source types
- Study ADF + Databricks integration patterns
- Review ADF best practices for enterprise-scale implementations

**Practice/Labs**:
- Build sample ingestion pipeline from SQL Database → ADLS Gen2 → Databricks Bronze
- Implement parameterized pipeline with dynamic source/sink configurations
- Set up monitoring and alerting for pipeline failures
- Create CDC-based incremental load pipeline

**Time Estimate**: 2-3 weeks (intensive)

**Priority**: HIGH

---

### 2. Azure Synapse Analytics
**Reason**: Listed as core technology in the Quorum tech stack. Used for data warehousing and analytics alongside Databricks. Opportunity requires "Azure Synapse Analytics" as deep expertise area.

**Learning Objectives**:
- Understand Synapse workspace architecture
- Learn Synapse Pipelines (similar to ADF but integrated)
- Master Synapse SQL Pools (dedicated and serverless)
- Understand Synapse Spark Pools integration with Databricks
- Learn when to use Synapse vs Databricks for workloads
- Practice data integration patterns between Synapse and Databricks

**Resources**:
- Microsoft Learn: [Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/synapse-analytics/)
- Synapse vs Databricks comparison guides
- Hands-on tutorials for Synapse Pipelines and SQL Pools

**Practice/Labs**:
- Set up Synapse workspace with SQL Pools and Spark Pools
- Create Synapse Pipeline to orchestrate data transformations
- Query data using Synapse Serverless SQL Pool
- Integrate Synapse with Databricks for unified analytics

**Time Estimate**: 2-3 weeks

**Priority**: HIGH

---

### 3. Terraform (Infrastructure as Code)
**Reason**: The role is described as "core builder and maintainer of platform's infrastructure, deploying automation tools using Infrastructure as Code (IaC) principles." Terraform is the industry standard for Azure IaC.

**Learning Objectives**:
- Master Terraform basics (providers, resources, modules, state management)
- Learn Azure provider for Terraform (azurerm)
- Understand Terraform module design for reusability
- Practice CI/CD integration with Terraform (Azure DevOps)
- Learn state management (Azure Storage backend)
- Understand Terraform workspaces for multi-environment management (Dev/QA/Prod)

**Resources**:
- HashiCorp Terraform documentation
- Terraform Azure Provider documentation
- Terraform + Azure DevOps integration guides
- Databricks Terraform provider documentation

**Practice/Labs**:
- Write Terraform modules for Azure Data Factory, Synapse, Databricks workspace
- Set up remote state management using Azure Storage
- Create environment-specific configurations (Dev/QA/Prod)
- Integrate Terraform with Azure DevOps pipeline

**Time Estimate**: 2-4 weeks

**Priority**: HIGH

---

### 4. Azure DevOps Pipelines
**Reason**: Job description requires "CI/CD Management: Design, develop, and maintain the CI/CD process using Azure DevOps." Critical for deployment automation.

**Learning Objectives**:
- Understand Azure DevOps Pipelines (YAML-based)
- Learn pipeline stages, jobs, tasks, and templates
- Master Azure Repos integration for version control
- Understand service connections and secure credential management
- Learn pipeline triggers (CI/CD) and branch policies
- Practice pipeline approval gates for production deployments

**Resources**:
- Microsoft Learn: [Azure DevOps Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/)
- YAML pipeline syntax reference
- Azure DevOps + Terraform integration guides
- Azure DevOps + Databricks integration patterns

**Practice/Labs**:
- Create YAML pipeline for Terraform deployment
- Set up multi-stage pipeline (Build → Test → Deploy)
- Implement approval gates for production stage
- Configure service connections for Azure resources

**Time Estimate**: 1-2 weeks

**Priority**: HIGH

---

### 5. Knowledge Graph / Ontology Design
**Reason**: Strategic differentiator for QDAI platform. Quorum's vision is "Domain-Specific Knowledge Graph: An interconnected understanding linking land, production, and accounting." This is the foundation for Agentic AI. Technology is "TBD - Under Investigation," making early learning valuable for influence.

**Learning Objectives**:
- Understand Knowledge Graph fundamentals (nodes, edges, properties, semantic relationships)
- Learn ontology design principles (classes, relationships, instances)
- Study industry standards: OSDU (Open Subsurface Data Universe), PPDM (Professional Petroleum Data Management)
- Understand Unified Semantic Layer concepts
- Learn tools: Neo4j, Azure Cosmos DB (Gremlin API), RDF/OWL standards
- Explore how Knowledge Graphs power Agentic AI

**Resources**:
- Knowledge Graph books: "Knowledge Graphs" by Hogan et al.
- OSDU Forum documentation (energy industry standard)
- PPDM Association resources
- Neo4j Graph Academy (free courses)
- Azure Cosmos DB Gremlin API documentation
- Research papers on Semantic Layers for AI

**Practice/Labs**:
- Design sample energy domain ontology (Well → Lease → Production → Royalty relationships)
- Model relationships using graph database (Neo4j or Cosmos DB)
- Create OSDU-aligned data model for subset of entities
- Build simple knowledge graph query examples

**Time Estimate**: 3-4 weeks (foundational understanding; ongoing as tech is finalized)

**Priority**: HIGH (strategic opportunity to influence technology selection)

---

## Medium Priority Learning Topics

### 6. Microsoft Fabric
**Reason**: Part of core tech stack: "Microsoft Fabric (Business Intelligence): Utilized for last-mile data publishing and integrated BI reporting, leveraging Power BI." Medium priority because it's BI-focused (not core platform infrastructure).

**Learning Objectives**:
- Understand Microsoft Fabric architecture (OneLake, Lakehouse, Data Warehouse)
- Learn Fabric integration with Databricks
- Understand Fabric's relationship to Power BI
- Practice data publishing patterns from Databricks to Fabric
- Learn Fabric security and governance model

**Resources**:
- Microsoft Learn: [Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/)
- Fabric + Databricks integration guides
- Power BI integration with Fabric

**Practice/Labs**:
- Connect Fabric to Databricks Delta tables
- Create Fabric Lakehouse and publish data from Databricks
- Build Power BI report on Fabric-hosted data

**Time Estimate**: 2-3 weeks

**Priority**: MEDIUM

---

### 7. Ansible (Configuration Management)
**Reason**: Job description lists "Hands-on experience with configuration management tools like Ansible." Used for platform management and operational streamlining. Medium priority as Terraform may cover most IaC needs.

**Learning Objectives**:
- Understand Ansible basics (playbooks, roles, inventory, modules)
- Learn Azure modules for Ansible
- Practice configuration management vs infrastructure provisioning
- Understand when to use Ansible vs Terraform

**Resources**:
- Ansible documentation
- Ansible Azure modules documentation
- Ansible + Azure integration guides

**Practice/Labs**:
- Write Ansible playbook to configure Azure VMs
- Automate application deployment using Ansible
- Integrate Ansible with Azure DevOps

**Time Estimate**: 1-2 weeks

**Priority**: MEDIUM

---

### 8. PowerShell Scripting
**Reason**: Job description requires "Expertise in scripting languages such as Python, PowerShell, and Azure CLI." PowerShell is the native Azure automation language.

**Learning Objectives**:
- Learn PowerShell syntax and scripting basics
- Master Azure PowerShell modules (Az.*)
- Understand PowerShell pipeline and object manipulation
- Practice Azure resource management via PowerShell
- Learn PowerShell DSC (Desired State Configuration) if needed

**Resources**:
- Microsoft Learn: [PowerShell](https://learn.microsoft.com/en-us/powershell/)
- Azure PowerShell documentation
- PowerShell scripting best practices

**Practice/Labs**:
- Write PowerShell script to automate Azure resource creation
- Automate Data Factory pipeline execution via PowerShell
- Create reusable PowerShell modules for common tasks

**Time Estimate**: 1-2 weeks

**Priority**: MEDIUM

---

### 9. Azure CLI
**Reason**: Job description requires "Expertise in scripting languages such as Python, PowerShell, and Azure CLI." Alternative to PowerShell for cross-platform scripting.

**Learning Objectives**:
- Learn Azure CLI command structure
- Master common Azure resource management commands
- Practice scripting with Azure CLI (Bash/Python)
- Understand when to use CLI vs PowerShell vs Terraform

**Resources**:
- Microsoft Learn: [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)
- Azure CLI reference documentation
- Azure CLI scripting examples

**Practice/Labs**:
- Write Bash script using Azure CLI to provision resources
- Automate Databricks workspace configuration via CLI
- Integrate Azure CLI with CI/CD pipelines

**Time Estimate**: 1 week

**Priority**: MEDIUM

---

### 10. Master Data Management (MDM)
**Reason**: Engagement document describes "MDM Architecture Integration" and "Single Source of Truth for Meters, Locations, Products across source systems." MDM resides in Silver layer for cross-system reconciliation.

**Learning Objectives**:
- Understand MDM principles (Golden Records, matching, merging, survivorship)
- Learn MDM patterns in Medallion Architecture (Silver layer focus)
- Practice entity resolution and data quality rules
- Understand MDM tools and techniques
- Learn integration with Unity Catalog and Azure Purview

**Resources**:
- MDM books: "Master Data Management" by David Loshin
- Databricks MDM patterns documentation
- Azure Purview for MDM use cases

**Practice/Labs**:
- Design MDM logic for "Meter" entity across multiple sources
- Implement matching and merging rules in Silver layer
- Create "Golden Record" tables with data quality flags
- Define survivorship rules for conflicting attributes

**Time Estimate**: 2-3 weeks

**Priority**: MEDIUM

---

### 11. Energy Industry Domain (OSDU, PPDM)
**Reason**: Quorum operates in energy (Oil & Gas) domain. Document mentions "industry standards (OSDU/PPDM)" as foundation for future-ready platform. Domain knowledge enhances credibility and effectiveness.

**Learning Objectives**:
- Understand Oil & Gas industry workflows (Upstream, Midstream, Downstream)
- Learn OSDU (Open Subsurface Data Universe) data platform standard
- Study PPDM (Professional Petroleum Data Management) data model
- Understand energy domain entities: Wells, Leases, Production, Land, Royalties
- Learn Quorum's product portfolio context (NA O&T, Upstream Planning, International O&T)

**Resources**:
- OSDU Forum: [OSDU Technical Standard](https://osduforum.org/)
- PPDM Association: [PPDM Data Model](https://ppdm.org/)
- Energy industry overview courses (Coursera, LinkedIn Learning)
- Quorum's public materials and product documentation

**Practice/Labs**:
- Study OSDU data model and compare to Quorum's domain
- Map energy domain concepts to Knowledge Graph design
- Review case studies of data platforms in energy sector

**Time Estimate**: 2-4 weeks (foundational); ongoing

**Priority**: MEDIUM (enhances domain credibility; not immediately critical for platform engineering)

---

## Low Priority Learning Topics

### 12. Azure Data Lake Storage Gen 2
**Reason**: Core storage for platform, but strong Databricks Delta Lake experience provides significant overlap. Mostly configuration and security focus.

**Learning Objectives**:
- Understand ADLS Gen 2 architecture (hierarchical namespace)
- Learn ADLS security model (ACLs, RBAC, encryption)
- Practice integration with Databricks
- Understand performance optimization (partitioning, file sizes)

**Resources**:
- Microsoft Learn: [Azure Data Lake Storage Gen 2](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)

**Time Estimate**: 1 week

**Priority**: LOW (Databricks experience transfers well)

---

### 13. Azure SQL Database
**Reason**: Listed in tech stack but likely limited use given Databricks/Delta Lake focus. Mainly for source system connectivity.

**Learning Objectives**:
- Understand Azure SQL Database service tiers
- Learn connectivity patterns from ADF/Databricks
- Practice query optimization for Azure SQL
- Understand security and networking (Private Endpoints)

**Resources**:
- Microsoft Learn: [Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/)

**Time Estimate**: 1 week

**Priority**: LOW (existing SQL experience transfers)

---

### 14. Azure Purview (Data Catalog & Lineage)
**Reason**: Mentioned in MDM architecture integration: "Azure Purview: Catalog & Lineage: Track how volume records are merged." Important for governance but not core platform building.

**Learning Objectives**:
- Understand Azure Purview architecture
- Learn data cataloging and classification
- Practice lineage tracking for pipelines
- Understand integration with Unity Catalog

**Resources**:
- Microsoft Learn: [Azure Purview](https://learn.microsoft.com/en-us/azure/purview/)

**Time Estimate**: 1-2 weeks

**Priority**: LOW (Unity Catalog provides primary governance)

---

### 15. Azure Private Links / Virtual Networks
**Reason**: Security component mentioned: "Standard Ingress using Azure Data Factory and Private Links." Networking configuration, not core platform logic.

**Learning Objectives**:
- Understand Azure Private Link architecture
- Learn Private Endpoint configuration
- Practice secure connectivity patterns
- Understand Virtual Network integration for data services

**Resources**:
- Microsoft Learn: [Azure Private Link](https://learn.microsoft.com/en-us/azure/private-link/)

**Time Estimate**: 1 week

**Priority**: LOW (infrastructure configuration, not platform logic)

---

## Suggested Learning Path

### Phase 1: Foundation (Weeks 1-4)
**Focus**: Azure-specific services that are immediately required

1. **Azure Data Factory** (2-3 weeks) - HIGH
2. **Azure DevOps Pipelines** (1-2 weeks) - HIGH

**Outcome**: Ability to build ingestion pipelines and CI/CD processes

---

### Phase 2: Infrastructure & DevOps (Weeks 5-8)
**Focus**: IaC and automation tooling

3. **Terraform** (2-4 weeks) - HIGH
4. **PowerShell** (1-2 weeks) - MEDIUM (parallel with Terraform)
5. **Azure CLI** (1 week) - MEDIUM (parallel with Terraform)

**Outcome**: Ability to provision and manage infrastructure as code

---

### Phase 3: Platform Services (Weeks 9-11)
**Focus**: Additional Azure platform services

6. **Azure Synapse Analytics** (2-3 weeks) - HIGH

**Outcome**: Comprehensive Azure data platform capability

---

### Phase 4: Strategic Capabilities (Weeks 12-16)
**Focus**: Innovation and domain expertise

7. **Knowledge Graph / Ontology Design** (3-4 weeks) - HIGH
8. **Microsoft Fabric** (2-3 weeks) - MEDIUM (parallel with Knowledge Graph)

**Outcome**: Strategic differentiation for Agentic AI and BI publishing

---

### Phase 5: Specialized Topics (Ongoing)
**Focus**: Depth in specific areas as needed

9. **Master Data Management (MDM)** (2-3 weeks) - MEDIUM
10. **Ansible** (1-2 weeks) - MEDIUM
11. **Energy Industry Domain (OSDU, PPDM)** (2-4 weeks) - MEDIUM
12. **Azure Purview, Private Links, etc.** (as needed) - LOW

**Outcome**: Comprehensive capability coverage for long-term success

---

## Total Time Investment

- **High Priority Topics**: 10-14 weeks
- **Medium Priority Topics**: 10-14 weeks
- **Low Priority Topics**: 5-7 weeks

**Recommended Pre-Engagement Learning**: Focus on Phase 1-3 (Weeks 1-8) covering ADF, Azure DevOps, Terraform, PowerShell, Azure CLI before starting the engagement. This provides immediate capability to contribute to platform building.

**Parallel Learning During Engagement**: Phase 4-5 can be learned during the engagement as specific needs arise, leveraging project context for deeper learning.

---

## Learning Resources Summary

### Online Platforms
- **Microsoft Learn**: Free, comprehensive Azure learning paths
- **Pluralsight**: Azure and DevOps courses
- **LinkedIn Learning**: Azure fundamentals and advanced topics
- **Coursera**: Azure certifications and specialized topics

### Certifications to Consider
- **Azure Data Engineer Associate (DP-203)**: Covers ADF, Synapse, Databricks, Data Lake
- **Azure Solutions Architect Expert (AZ-305)**: Covers enterprise architecture patterns
- **HashiCorp Terraform Associate**: Validates Terraform expertise

### Hands-On Labs
- **Microsoft Learn Sandbox**: Free Azure environment for practice
- **Azure Free Tier**: 12 months free services for hands-on learning
- **Databricks Community Edition**: Free Databricks environment

---

## Success Metrics

- **Week 4**: Able to build basic ADF pipeline and Azure DevOps CI/CD
- **Week 8**: Able to provision Azure infrastructure using Terraform
- **Week 12**: Able to design end-to-end data platform architecture on Azure
- **Week 16**: Able to contribute to Knowledge Graph design and MDM patterns

---

## Notes

- **Leverage Existing Strengths**: Your Databricks, SQL, PySpark, and program management expertise are already excellent. Focus learning on Azure-specific gaps.
- **Hands-On Practice**: Every topic should include hands-on labs. Reading alone is insufficient for technical mastery.
- **Project Context**: If possible, align learning with a sample project (e.g., build mini-version of QDAI platform for personal portfolio).
- **Community Engagement**: Join Azure community forums, Databricks community, OSDU forums to stay current.
- **Certifications**: Consider pursuing Azure Data Engineer Associate (DP-203) certification as structured learning path covering ADF, Synapse, Data Lake, and Databricks.
