# Project Analysis: Ethniki Insurance RFP

## Document Inventory

| Document | Type | Pages/Size | Purpose |
|----------|------|------------|---------|
| RFP_ETHNIKI ASFALISTIKI_MULTI-LOT AI IDP & AUTOMATIONS DELIVERY FRAMEWORK.pdf | PDF | 15 pages | Main RFP document with submission requirements |
| Ethniki Asfalistiki_for Automations 20251107_RFP_use_cases v3.pdf | PDF | 31 pages | Detailed use cases (CPCU1-CPCU5) |
| Attachment 1 - Technical Description.docx/pdf | DOCX/PDF | 931 paras/68 pages | Complete technical requirements and specifications |
| Attachment 2 - Company Information.xlsx | XLSX | 1 sheet | Vendor company information template |
| Attachment 3 - Vendor Assessment Questionnaire.xlsx | XLSX | 6 sheets | Vendor capabilities assessment |
| Attachment 4 - Financial Proposal.docx/xlsx | DOCX/XLSX | 35 paras/9 sheets | Pricing templates and financial requirements |
| Annex N – Q&A Submission Template.docx | DOCX | 4 paras, 1 table | Q&A submission format |

---

## Business Context

| Category | Details |
|----------|---------|
| **Client** | Ethniki, Hellenic General Insurance Company S.A. (ETHNIKI) |
| **Industry** | Insurance - Largest insurance company in Greece |
| **Company Age** | 134 years (founded June 15, 1891) |
| **Recent Change** | Acquired by Piraeus Financial Holdings on November 27, 2025; now part of Piraeus Bank Group |
| **Market Position** | #1 in Greece; 6 admin branches, 1,600+ intermediaries, 130 sales offices, 1,230+ cooperating agencies/brokers |
| **Business Need** | Enterprise-wide AI/IDP transformation to improve customer experience and operational efficiency |
| **RFP Date** | March 2026 |

---

## Technical Scope

| Category | Details |
|----------|---------|
| **Program Type** | Multi-LOT AI/IDP & Automations Delivery Framework |
| **LOT Structure** | LOT A: Enterprise AI/RAG Control Plane<br>LOTs B1-B7: AI/IDP use-case work packages by Line of Business |
| **Primary Technologies** | AI, IDP (Intelligent Document Processing), RAG (Retrieval-Augmented Generation), Automation |
| **Lines of Business** | Underwriting, Claims, Customer Experience, Group Life & Health, Motor, Corporate Property & Casualty |
| **Use Cases Identified** | 5 primary use cases (CPCU1-CPCU5):<br>- CPCU1: Automated Geocoding & GIS Integration<br>- CPCU2: Intelligent Mailroom Automation<br>- CPCU3: Information Aggregation & Pricing Automation<br>- CPCU4: Public Tender Intelligence & Processing<br>- CPCU5: Contract Generation / Automation |
| **Delivery Model** | Turn-key model; vendors submit per LOT; independent evaluation; parallel execution if multi-LOT award |
| **Existing Systems** | 9+ systems for client history/risk info; GEOL GIS platform; Aviva; MOS; shared mailboxes |

---

## Data Scope

| Category | Details |
|----------|---------|
| **Document Types** | Emails (5,000/day), PDFs, Word documents, Excel spreadsheets, Multi-location policy contracts, Risk attachments, Tender documents (60-70 pages) |
| **Data Volume** | 3,000 pending contracts for geocoding backlog; ~750 relevant insurance tenders/year; 5,000 daily emails |
| **Languages** | Greek (technical tender documents), English (RFP documentation) |
| **Integrations** | GIS platform (GEOL), CRM, Multiple underwriting systems (9+), Public tender platforms |
| **Data Privacy** | GDPR compliance required |

---

## Architecture

| Category | Details |
|----------|---------|
| **Architecture Pattern** | Two-layer framework:<br>1. Enterprise AI/RAG Control Plane (LOT A)<br>2. Use-case specific implementations (LOTs B1-B7) |
| **Governance** | Enterprise-grade governance, risk, and compliance controls |
| **Scalability** | Secure, governed, scalable, multi-vendor delivery ecosystem |
| **Reusability** | Build reusable enterprise AI assets to accelerate delivery cycles |
| **Regulatory Compliance** | GDPR, EU AI Act, DORA obligations |
| **Deployment Model** | **AWS Cloud** (project is AWS-funded - confirmed by user 2026-04-14) |

---

## Dependencies

| Category | Details |
|----------|---------|
| **Technical Dependencies** | Control Plane (LOT A) must support LOTs B1-B7; Integration with 9+ existing systems; GIS platform integration; Email system integration |
| **Organizational Dependencies** | Cross-departmental coordination; Operations division; Underwriting teams; Claims teams; Customer service; IT/Technology teams |
| **External Dependencies** | Geocoding API; Public tender platform access; Partner request systems |
| **Regulatory Dependencies** | GDPR compliance; EU AI Act adherence; DORA (Digital Operational Resilience Act) compliance |

---

## Program Objectives

1. Improve decision quality and processing speed
2. Reduce manual workload and operational inefficiencies
3. Provide real-time support for customer-facing operations
4. Enforce enterprise-grade governance, risk and compliance controls
5. Build reusable enterprise AI assets and accelerate delivery cycles

---

## Expected Benefits

- Significant reduction in manual processing workload
- Enhanced underwriting quality through structured extraction and automated pricing support
- Faster, more consistent claims processing
- Improved customer experience via real-time AI assistance
- Lower TCO via shared platform services
- Improved compliance posture through embedded safeguards and governance
- Reduced turnaround times for primary and secondary operational processes
- Better customer satisfaction, engagement, and retention
- Increased attractiveness among independent distribution channels

---

## Timeline & Complexity

| Use Case | Timeline | Complexity |
|----------|----------|------------|
| CPCU1: Geocoding & GIS | 1 month (Phase 1: 10 days backlog clearing) | Quick Win |
| CPCU2: Mailroom Automation | 3 months | Quick Win |
| CPCU3: Information Aggregation & Pricing | 3 months | Tactical |
| CPCU4: Public Tender Intelligence | Not specified | Tactical |
| CPCU5: Contract Generation | Not specified | Not specified |

---

## Submission Requirements

| Component | Details |
|----------|---------|
| **File 1** | Technical Proposal: Executive Summary, Technical Proposal, Responsibility Declaration, Company Information |
| **File 2** | Financial Proposal: Pricing Information per LOT |
| **Evaluation** | Independent evaluation per LOT; not contingent on other LOTs |
| **Format** | Separate technical and financial proposals for each LOT |
| **Turn-Key Model** | Must include all technology, business capabilities, services, and software licenses |

---

## Key Observations

1. **Multi-vendor ecosystem**: RFP explicitly designed for multiple vendors across different LOTs
2. **Control Plane first**: LOT A (Enterprise AI/RAG Control Plane) is foundational for LOTs B1-B7
3. **Parallel execution**: Multiple LOTs can run concurrently if single vendor wins multiple
4. **Proven success**: Two AI/automation solutions already in production with marked improvements
5. **Strategic moment**: Recent acquisition by Piraeus Bank Group creates transformation opportunity
6. **Greek market focus**: Documents in Greek; local market leadership position
7. **Compliance-heavy**: GDPR, EU AI Act, DORA all mentioned as requirements
8. **Document-centric**: Heavy focus on document processing, extraction, and automation
9. **Integration complexity**: 9+ existing systems require integration

---

## AWS Infrastructure Alignment (Confirmed 2026-04-14)

**CRITICAL:** Project is **AWS-funded**, which mandates AWS cloud infrastructure alignment.

### AWS Technology Stack Recommendations

| Component | AWS Service | Purpose | Rationale |
|-----------|------------|---------|-----------|
| **IDP/Document Processing** | AWS Textract | OCR, form extraction, table detection | Native AWS service, multilingual support including Greek |
| **LLM/GenAI** | Amazon Bedrock | Foundation models (Claude, Titan, Llama) | AWS-native, compliance-ready, multi-model support |
| **RAG Vector Database** | Amazon OpenSearch Service with vector engine | Vector storage and similarity search | Managed AWS service, integrates with Bedrock |
| **Document Storage** | Amazon S3 + S3 Intelligent-Tiering | Raw and processed document storage | Cost-effective, GDPR-compliant with EU regions |
| **Data Processing** | AWS Glue / AWS Step Functions | ETL pipelines and orchestration | Serverless, scalable, integrates with Textract |
| **Real-Time Processing** | Amazon Kinesis Data Streams | Email streaming (5K/day mailroom) | Real-time ingestion and processing |
| **Integration Layer** | Amazon API Gateway + AWS Lambda | Integration with 9+ existing systems | Serverless, scalable, API management |
| **Compute** | AWS Lambda + Amazon ECS/Fargate | Application hosting | Serverless-first for cost optimization |
| **Database** | Amazon RDS (PostgreSQL) + DynamoDB | Structured data and metadata | Managed services, high availability |
| **ML Model Training** | Amazon SageMaker | Custom model training (Greek NLP) | Full ML lifecycle management |
| **Monitoring** | Amazon CloudWatch + AWS X-Ray | Logging, monitoring, tracing | Native AWS observability |
| **Security** | AWS IAM + AWS KMS + AWS Secrets Manager | Access control, encryption, secrets | GDPR/DORA compliance-ready |
| **Networking** | Amazon VPC + AWS PrivateLink | Secure networking, private connectivity | Data residency and security requirements |
| **Compliance** | AWS Artifact + AWS Config | Compliance documentation and monitoring | EU AI Act and DORA compliance support |

### AWS Data Residency for GDPR Compliance

**Recommended AWS Region:** `eu-central-1` (Frankfurt, Germany) or `eu-south-1` (Milan, Italy)

**Rationale:**
- **GDPR Compliance:** Data stays within EU
- **Greece Proximity:** Low latency to Greece from Frankfurt or Milan
- **Service Availability:** Full AWS service portfolio available
- **DORA Compliance:** EU-based operational resilience

**Data Residency Configuration:**
- S3 buckets: Europe region with encryption at rest (KMS)
- RDS/DynamoDB: EU region deployment
- Lambda functions: EU region execution
- CloudWatch logs: EU region storage with retention policies

### AWS Architecture Benefits

| Benefit | AWS Advantage |
|---------|--------------|
| **Cost Optimization** | AWS funding reduces infrastructure costs significantly |
| **Compliance Ready** | AWS GDPR, EU AI Act, DORA compliance frameworks available |
| **Scalability** | Serverless architecture scales automatically with document volume |
| **Integration** | AWS SDK available for all major languages, API Gateway for existing systems |
| **Security** | AWS IAM fine-grained access control, encryption at rest/transit by default |
| **Disaster Recovery** | Multi-AZ deployment, automated backups, cross-region replication options |
| **Greek Language Support** | AWS Textract supports Greek OCR, Bedrock models support multilingual |

### AWS-Specific Capability Gaps

**Previous Gap: "No IDP experience"**
- **AWS Solution:** AWS Textract provides managed IDP
- **Mitigation:** Leverage AWS Textract documentation, AWS training, AWS ProServe consultation

**Previous Gap: "No RAG architecture experience"**
- **AWS Solution:** Amazon Bedrock + OpenSearch vector engine provides managed RAG
- **Mitigation:** AWS Bedrock workshops, reference architectures available

**Previous Gap: "Greek language processing"**
- **AWS Solution:** AWS Textract supports Greek OCR; Bedrock models (Claude, etc.) support Greek
- **Mitigation:** Test Greek accuracy during POC phase; fine-tune if needed with SageMaker

### AWS Cost Implications (Funding Context)

Since project is **AWS-funded**, infrastructure costs are significantly reduced or subsidized:

**Impact on Proposal:**
- **Lower infrastructure pricing** compared to self-hosted or other clouds
- **Focus pricing on:** Services, implementation, training, support (not infra cost)
- **Leverage AWS credits** for development, testing, and pilot phases
- **Highlight AWS partnership** as competitive advantage

---

## Critical Success Factors

1. **AWS-native architecture** leveraging AWS services (Textract, Bedrock, OpenSearch) - **NEW #1 PRIORITY**
2. Enterprise AI/RAG Control Plane architecture (LOT A) on AWS
3. GDPR and EU AI Act compliance framework using AWS compliance tools
4. Integration with 9+ existing systems via AWS API Gateway
5. Greek language processing using AWS Textract + Bedrock multilingual models
6. Turn-key delivery model with AWS licenses and services included
7. Parallel execution capability across LOTs using AWS orchestration
8. Real-time processing for customer-facing operations using AWS Kinesis
9. Governance and compliance controls embedded in platform using AWS Config/CloudTrail
10. **EU data residency** in AWS Frankfurt or Milan region for GDPR/DORA compliance

---

## Timeline Feasibility Assessment (Step 12 - Added 2026-04-14)

### Stated Timelines from RFP

| Use Case | Stated Timeline | Classification | Feasibility Rating |
|----------|----------------|----------------|-------------------|
| CPCU1: Geocoding & GIS | 1 month (Phase 1: 10 days for backlog) | Quick Win | ⚠️ AGGRESSIVE |
| CPCU2: Mailroom Automation | 3 months | Quick Win | ❌ UNDERSTATED |
| CPCU3: Information Aggregation & Pricing | 3 months | Tactical | ❌ SIGNIFICANTLY UNDERSTATED |
| CPCU4: Public Tender Intelligence | Not specified | Tactical | 🔍 NEEDS DEFINITION |
| CPCU5: Contract Generation | Not specified | Not specified | 🔍 NEEDS DEFINITION |
| LOT A: Enterprise AI/RAG Control Plane | Not specified | Foundational | 🔍 NEEDS DEFINITION |

### 360-Degree Timeline Analysis

#### Assumptions Requiring Validation:
1. **Team Availability:** Full-time dedicated team vs. shared resources?
2. **Phase Scope:** Development only or includes analysis, testing, UAT, training, go-live?
3. **Dependency Management:** LOT A completion level required before LOT B start?
4. **Resource Readiness:** API access, test data, SME availability on Day 1?
5. **Pilot/POC Phase:** Included in timeline or separate?

#### Timeline Breakdown by Phase (Example: CPCU2 Mailroom)

**Stated Timeline: 3 months**

| Phase | Duration | Activities | Dependencies | Risk Level |
|-------|----------|----------|--------------|------------|
| Requirements & Analysis | 2 weeks | Process mapping, email sample analysis, routing rules definition | BA availability, email system access | MEDIUM |
| Greek NLP Model Setup | 3 weeks | Model selection, Greek training data, accuracy validation | Greek language corpus, labeling | **HIGH** |
| Classification Development | 4 weeks | Model training, category definition, confidence scoring | 5,000 email sample set | MEDIUM |
| Routing Logic & Integration | 3 weeks | Workflow automation, system integration APIs | 9+ system API access | **HIGH** |
| Testing & Validation | 2 weeks | Unit testing, integration testing, edge case validation | Test environment | MEDIUM |
| User Acceptance Testing (UAT) | 2 weeks | Business user validation, feedback incorporation | UAT team availability | MEDIUM |
| Go-Live Support | 1 week | Cutover, monitoring, issue resolution | Production access | LOW |
| **Total (No Buffer)** | **17 weeks (4.25 months)** | | | |
| **With 60% Buffer** | **27 weeks (6.75 months)** | | | |

**Feasibility Assessment:** Stated 3 months is **not realistic**. Minimum 4-5 months without buffer; 6-7 months with industry-standard 60% buffer for AI/IDP projects.

### Recommended Timelines with 60% Buffer (Fixed-Price Model)

| Use Case | Stated | Realistic (No Buffer) | With 60% Buffer | Recommended Proposal |
|----------|--------|----------------------|----------------|---------------------|
| CPCU1: Geocoding | 1 month | 4-5 weeks | 7-8 weeks | **7 weeks (1.75 months)** |
| CPCU2: Mailroom | 3 months | 17 weeks (4.25 months) | 27 weeks (6.75 months) | **6 months** |
| CPCU3: Pricing | 3 months | 20 weeks (5 months) | 32 weeks (8 months) | **7 months** |
| CPCU4: Tender Intelligence | Not stated | 16-18 weeks (4-4.5 months) | 26-29 weeks (6.5-7.25 months) | **6-7 months** |
| CPCU5: Contract Generation | Not stated | 12-14 weeks (3-3.5 months) | 19-22 weeks (4.75-5.5 months) | **5 months** |
| LOT A: Control Plane | Not stated | 24-28 weeks (6-7 months) | 38-45 weeks (9.5-11.25 months) | **10 months** |

### Timeline Risk Factors Requiring Clarification

| Risk Factor | Impact on Timeline | Mitigation | Priority |
|------------|-------------------|------------|----------|
| **Greek Language Processing** | +20-40% if custom model training needed | Validate existing Greek NLP model availability; include POC phase | CRITICAL |
| **9+ System Integration** | +30-50% if APIs unavailable or undocumented | Request API documentation upfront; include integration discovery phase | CRITICAL |
| **Document Quality Unknown** | +15-30% if poor scan quality requires preprocessing | Request document samples; set accuracy tiers | HIGH |
| **BA/SME Availability** | +25-50% if part-time or ad-hoc availability | Secure dedicated BA commitment; vendor provides BA if needed | CRITICAL |
| **UAT Resource Allocation** | +15-25% if business users not dedicated for UAT | Define UAT plan and resource commitment upfront | HIGH |
| **Regulatory Compliance Validation** | +10-20% for EU AI Act compliance documentation | Include compliance workstream in parallel | MEDIUM |

### Commercial Model Recommendation: Time & Materials (T&M)

**Strong Recommendation for T&M Given:**

1. **Undefined Scope:** LOTs B2-B7 not defined (cannot price unknowns)
2. **Integration Uncertainty:** 9+ system APIs not documented (integration effort unpredictable)
3. **AI/IDP Complexity:** Accuracy depends on document quality (not validated via samples)
4. **Greek Language Risk:** Greek NLP maturity unclear; may require model training
5. **Regulatory Evolution:** EU AI Act implementation details emerging
6. **Timeline Ambiguity:** Stated timelines don't specify phase scope (dev only vs. full delivery)

**If Fixed-Price Required:**
- Apply **60% contingency buffer** to all timelines
- Clearly define **exclusions and assumptions** (e.g., "API access within 2 weeks", "document quality meets minimum standards")
- Include **change order provisions** for scope adjustments
- Propose **phase-gated approach:** Fixed-price per phase after discovery validates assumptions

**Hybrid Model (Recommended):**
```
Phase 1 (Months 1-4): T&M
- Discovery & requirements validation
- LOT A architecture design
- CPCU1 pilot (validate approach)
- Integration API assessment
- Greek NLP validation

Phase 2 (Months 5-12): Fixed-Price with Buffer
- CPCU1, CPCU2, CPCU3 delivery
- LOT A Control Plane (if scope clarified)
- Timelines include 60% buffer

Phase 3 (Months 13+): Fixed-Price per LOT
- LOTs B2-B7 once defined
- Separate fixed-price per LOT based on Phase 1/2 learnings
```

### Project Governance: RACI Matrix Requirements

**Critical RACI Clarifications Needed:**

| Activity | Responsible | Accountable | Consulted | Informed |
|----------|------------|-------------|-----------|----------|
| **Requirements Definition** | ? (Vendor BA, Ethniki BA, Joint) | ? | ? | ? |
| **Technical Design Approval** | ? (Vendor architect) | ? (Ethniki IT/Architecture) | ? | ? |
| **Test Data Provision** | ? (Ethniki IT, Business Units) | ? | ? | ? |
| **Integration API Development** | ? (Vendor, Ethniki IT) | ? | ? | ? |
| **UAT Execution** | ? (Business users) | ? (Business owner) | ? | ? |
| **Go-Live Approval** | ? | ? (Who signs off?) | ? | ? |
| **Production Support (0-90 days)** | ? (Vendor, Ethniki IT, Hybrid) | ? | ? | ? |
| **Production Support (90+ days)** | ? | ? | ? | ? |

**Recommendation:** Conduct RACI workshop in Week 1-2 post-contract award to define responsibilities clearly.

### BA Availability & Experience Requirements

**Business Analyst (BA) Criticality:**
- Timeline feasibility **depends heavily** on BA availability and capability
- If Ethniki cannot provide dedicated full-time BA:
  - **Timeline increases 25-50%** due to decision delays and requirements churn
  - **Vendor should include BA services** in scope (additional cost)

**BA Questions Requiring Answers:**
1. Is dedicated BA assigned per LOT? (Yes/No)
2. BA time commitment? (Full-time / 50% / Ad-hoc)
3. BA experience with AI/IDP? (Expert / Intermediate / New)
4. BA domain expertise? (Underwriting / Claims / Operations)
5. BA decision authority? (Can approve requirements / Advisory only)

**Risk Mitigation:**
- If Ethniki BA is part-time or inexperienced: **Include vendor BA services** (T&M basis)
- If Ethniki BA is advisory only: **Identify Accountable decision-maker** with authority

### Functional vs. Non-Functional Requirements (NFR) Gaps

**Functional Requirements (Detailed Workflows):**
- Current: High-level use case descriptions in RFP
- Needed: Step-by-step workflows, business rules, validation logic, exception handling
- **Impact if not clarified:** Requirements churn, rework, timeline overruns

**Non-Functional Requirements (Performance, Accuracy, Security):**

| NFR Category | Current Status | Required Definition | Impact on Timeline |
|-------------|----------------|---------------------|-------------------|
| **Performance** | "Real-time" mentioned | Latency: < 2 sec? < 5 sec? Throughput: docs/hour? | Cannot size infrastructure |
| **Accuracy** | Not specified | OCR: 95%? Extraction: 98%? Classification: 90%? | Cannot commit to SLA |
| **Availability** | Not specified | 99.9%? 99.5%? Maintenance windows? | Affects architecture design |
| **Security** | GDPR/DORA mentioned | Encryption standards? MFA? Audit logging? | Compliance scope undefined |
| **Scalability** | Volumes stated | 3-year growth projection? Peak load handling? | Infrastructure planning |

**Recommendation:** Include **NFR definition workshop** (2-3 weeks, T&M) in Phase 1 before committing to fixed-price delivery.

---

## Updated Timeline & Complexity Table (Including Step 12 Assessment)

| Use Case | Stated Timeline | Complexity | Realistic Timeline (No Buffer) | With 60% Buffer | Feasibility Rating |
|----------|----------------|------------|-------------------------------|----------------|-------------------|
| CPCU1: Geocoding & GIS | 1 month | Quick Win | 4-5 weeks | **7 weeks** | ⚠️ Aggressive but achievable with dedicated team |
| CPCU2: Mailroom Automation | 3 months | Quick Win | 4-5 months | **6-7 months** | ❌ Significantly understated; Greek NLP adds complexity |
| CPCU3: Information Aggregation & Pricing | 3 months | Tactical | 5-6 months | **7-8 months** | ❌ Major understatement; 9+ system integration is complex |
| CPCU4: Public Tender Intelligence | Not specified | Tactical | 4-5 months | **6-7 months** | 🔍 Needs definition; Greek PDF extraction |
| CPCU5: Contract Generation | Not specified | Not specified | 3-4 months | **5 months** | 🔍 Needs definition; template complexity unknown |
| LOT A: Enterprise AI/RAG Control Plane | Not specified | Foundational | 6-8 months | **10-12 months** | 🔍 Critical; supports all LOTs; cannot rush |

**Overall Program Timeline Estimate:**
- **Sequential Delivery:** 24-36 months (all LOTs one after another)
- **Parallel Delivery (3 streams):** 12-18 months (LOT A + 2-3 use cases in parallel)
- **Phased Approach (Recommended):**
  - Phase 1 (Discovery + LOT A foundation): 4-6 months
  - Phase 2 (CPCU1, CPCU2 parallel): 6-8 months
  - Phase 3 (CPCU3, CPCU4, CPCU5): 8-12 months
  - **Total: 18-26 months**
