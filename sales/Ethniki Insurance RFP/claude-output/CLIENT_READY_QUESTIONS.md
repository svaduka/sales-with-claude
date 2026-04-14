# EPAM RFP Clarification Questions
## Ethniki Insurance - Multi-LOT AI/IDP & Automations Delivery Framework

**Submitted By:** EPAM Systems
**Date:** 2026-04-14
**Purpose:** Pre-Sales Estimation and Proposal Development

---

## Introduction

Thank you for the opportunity to respond to this RFP. To provide an accurate proposal with realistic cost estimates, delivery timelines, and team composition, we require clarification on the following 25 questions. Each question directly impacts our ability to estimate effort and propose a feasible solution.

The questions are organized into 6 categories:
- **A. Architecture & Infrastructure** (6 questions)
- **B. AI/ML & Data Processing** (4 questions)
- **C. Integration & Systems** (3 questions)
- **D. Compliance & Security** (2 questions)
- **E. Project Scope & Governance** (5 questions)
- **F. Team & Responsibilities** (5 questions)

---

## A. Architecture & Infrastructure (6 Questions)

### A1. AWS Architecture Pattern
**Question:** What AWS architecture pattern is required or preferred for the Enterprise AI/RAG Control Plane (LOT A)?
- Serverless (AWS Lambda, Fargate)
- Container-based (Amazon ECS/EKS)
- Hybrid approach

**Why this matters:** The architecture pattern affects team skills required, infrastructure cost model, and delivery approach. Serverless reduces operational overhead but has Lambda execution limits. Containers provide more control but require container orchestration expertise.

---

### A2. Scalability Requirements
**Question:** What are the expected scalability requirements for the Control Plane?
- Concurrent users
- Requests per second (RPS)
- Document processing volume per LOT (documents/day)
- Peak load expectations

**Why this matters:** Scalability metrics drive infrastructure sizing, auto-scaling configuration, and operational costs. Under-estimating capacity leads to performance issues; over-estimating increases costs unnecessarily.

---

### A3. Multi-Tenancy Model
**Question:** Should the architecture support multi-tenancy across vendors (if multiple vendors win different LOTs), or is it single-tenant for Ethniki only?

**Why this matters:** Multi-tenancy adds architectural complexity for data isolation, security boundaries, and governance. Single-tenant is simpler but may not support multi-vendor ecosystem goals. This affects design effort and timeline.

---

### A4. Disaster Recovery (DR)
**Question:** What are the disaster recovery requirements?
- Recovery Time Objective (RTO)
- Recovery Point Objective (RPO)
- Multi-AZ deployment required?
- Cross-region failover within EU required?

**Why this matters:** DR requirements determine environment count (production, DR), data replication strategy, backup frequency, and failover testing effort. This significantly affects infrastructure costs and operational complexity.

---

### A5. Integration Approach
**Question:** How should the solution integrate with the 9+ existing systems mentioned in the RFP?
- AWS API Gateway for centralized integration
- Point-to-point integration
- Existing ESB or integration hub

**Why this matters:** Integration architecture affects API development effort, middleware requirements, and ongoing maintenance. Centralized API Gateway provides better governance but requires API design upfront. Point-to-point is faster initially but harder to maintain.

---

### A6. AWS Region Selection
**Question:** Which AWS region should be used for deployment to meet GDPR and DORA compliance?
- eu-central-1 (Frankfurt, Germany)
- eu-south-1 (Milan, Italy)
- Other EU region preference

**Why this matters:** AWS region selection affects service availability (not all AWS services available in all regions), network latency to Greece, and data residency compliance. This is a foundational decision that impacts all downstream architecture choices.

---

## B. AI/ML & Data Processing (4 Questions)

### B1. Amazon Bedrock Model Approval
**Question:** Which Amazon Bedrock foundation models are acceptable for use?
- Claude (Anthropic)
- Titan (Amazon)
- Llama (Meta)
- Mistral
- Custom models via Amazon SageMaker

Are there any models that are explicitly prohibited?

**Why this matters:** Model selection affects licensing costs, integration complexity, multilingual support (Greek language), and compliance posture. Some models have different EU AI Act risk classifications. This choice impacts both cost and delivery approach.

---

### B2. Document Processing Volumes
**Question:** What is the expected document processing volume per hour/day for each use case (CPCU1-CPCU5)?
- CPCU1 (Geocoding): X documents/day
- CPCU2 (Mailroom): 5,000 emails/day (confirmed), peak load?
- CPCU3 (Pricing): X documents/day
- CPCU4 (Tender Intelligence): ~750 tenders/year, documents per tender?
- CPCU5 (Contract Generation): X contracts/day

**Why this matters:** Processing volumes drive compute capacity, AWS Textract API call volumes, storage requirements, and operational costs. Accurate volume estimates are essential for infrastructure sizing and cost modeling.

---

### B3. Document Formats and Quality
**Question:** What document formats and quality levels must be supported?
- PDF (digital vs. scanned, DPI quality)
- Word documents (DOCX)
- Excel spreadsheets (XLSX)
- Images (JPEG, PNG)
- Handwritten documents
- Language mix (Greek, English percentages)

**Why this matters:** Document quality directly affects extraction accuracy and preprocessing effort. Poor-quality scanned documents require OCR optimization, image enhancement, and more extensive validation. Handwritten documents add significant complexity. This impacts both timeline and cost.

---

### B4. Accuracy Requirements
**Question:** What are the minimum accuracy thresholds for AI/IDP processing?
- OCR accuracy (%): e.g., 95%, 99%
- Data extraction accuracy (%): e.g., 98% for critical fields
- Classification precision (%): e.g., 90% for email routing

What is the acceptable error rate, and what is the rework/validation process?

**Why this matters:** Higher accuracy requirements demand more sophisticated models, extensive validation workflows, human-in-the-loop review processes, and quality assurance effort. Accuracy targets directly impact both development timeline and operational staffing levels.

---

## C. Integration & Systems (3 Questions)

### C1. Nine Systems List and Details
**Question:** Can you provide the list of 9+ existing systems requiring integration, along with:
- System names
- System owners/departments
- Current integration capabilities (APIs available, batch interfaces, file drops)
- Documentation availability

**Why this matters:** Integration scope is the largest variable in effort estimation. API availability vs. custom integration development can change timeline by 30-50%. Without knowing which systems and their integration readiness, we cannot provide accurate estimates.

---

### C2. Integration Protocols and Authentication
**Question:** For the 9+ systems requiring integration, what are the:
- Integration protocols (REST API, SOAP, database direct access, file-based)
- Authentication methods (OAuth 2.0, SAML, API keys, mutual TLS)
- Data formats (JSON, XML, CSV, proprietary)
- Security requirements (VPN, PrivateLink, encryption standards)

**Why this matters:** Protocol and authentication mismatch requires custom adapter development. For example, if systems only support SOAP but solution is REST-native, we need transformation layers. Authentication complexity (e.g., mutual TLS) adds security implementation effort. This affects both timeline and technical team composition.

---

### C3. Data Exchange Volumes and Frequency
**Question:** For each of the 9+ systems, what is the expected:
- Data exchange volume (records per day, MB/GB per transfer)
- Frequency (real-time, hourly, daily batch)
- Criticality (business-critical real-time vs. nice-to-have batch)

**Why this matters:** Real-time integration requires event-driven architecture (AWS EventBridge, Kinesis), increasing complexity. High-volume integrations require buffering, queuing, and throttling. Batch integration is simpler but less responsive. This affects architecture design and infrastructure costs.

---

## D. Compliance & Security (2 Questions)

### D1. Compliance Frameworks and Standards
**Question:** What specific compliance frameworks and standards must the solution meet?
- GDPR: specific articles or requirements beyond general GDPR
- EU AI Act: risk classification level (high-risk, limited-risk, minimal-risk)
- DORA (Digital Operational Resilience Act): specific requirements
- Industry certifications: ISO 27001, SOC 2, others?
- Audit requirements: frequency, depth, external auditor involvement

**Why this matters:** Compliance scope determines documentation effort, audit trail implementation, explainability requirements (EU AI Act), and ongoing compliance validation. High-risk EU AI Act classification adds significant design and documentation effort. This affects both initial delivery and ongoing operational costs.

---

### D2. Data Residency and Cross-Border Processing
**Question:** What are the data residency and cross-border processing constraints?
- Must data remain within Greece, or is EU-wide processing acceptable?
- Are there restrictions on data transfer between EU regions?
- Can personal data be processed for AI model training/fine-tuning?
- What are the retention periods for processed documents, logs, and AI outputs?

**Why this matters:** Strict data residency (e.g., Greece-only) limits AWS region and service choices, potentially increasing costs or limiting capabilities. Cross-border restrictions affect DR strategy. Data retention policies drive storage costs and compliance overhead.

---

## E. Project Scope & Governance (5 Questions)

### E1. LOT B2-B7 Scope Definition
**Question:** The RFP defines LOT A and LOT B1 use cases (CPCU1-CPCU5) in detail. What is the scope of LOTs B2-B7?
- Are they additional use cases similar to CPCU1-CPCU5?
- Are they different lines of business (Motor, Corporate P&C, Group Life & Health)?
- What is the expected timeline for LOTs B2-B7 definition?

**Why this matters:** CRITICAL - We cannot estimate or bid on undefined work. If LOTs B2-B7 represent 7 additional use cases of similar complexity to CPCU1-CPCU5, this could be 2-3x the effort and cost. This is essential for accurate proposal scoping.

---

### E2. Proposal Submission Deadline
**Question:** What is the final deadline for proposal submission?
- Technical proposal due date
- Financial proposal due date
- Q&A cutoff date (last day to submit questions)
- Expected decision/award date

**Why this matters:** Proposal deadline determines how much analysis depth we can provide and whether we need clarification answers before submission or can proceed with assumptions. This affects proposal quality and our ability to derisk the estimate.

---

### E3. Budget Range
**Question:** Is there a budget range or budget ceiling for this program (overall or per-LOT)?

**Why this matters:** Budget guidance helps us scope the solution appropriately. A €500K budget implies a different solution approach (smaller team, phased delivery, more vendor-provided components) than a €2M budget (larger team, custom development, comprehensive scope). Without budget guidance, we risk proposing an over-engineered or under-scoped solution.

---

### E4. Commercial Model Preference
**Question:** What commercial model does Ethniki prefer?
- Fixed-price (lump sum per LOT)
- Time & Materials (T&M hourly/daily rates)
- Hybrid (fixed-price for defined scope, T&M for unknowns)

If fixed-price is required, is a contingency buffer acceptable given the undefined LOTs B2-B7 and integration uncertainties?

**Why this matters:** Fixed-price requires risk buffer (typically 40-60% for AI/IDP projects with unknowns), increasing cost. T&M provides flexibility but less cost certainty for Ethniki. This fundamentally changes our pricing approach and risk allocation. Given undefined LOTs B2-B7, T&M or hybrid model reduces risk for both parties.

---

### E5. Q&A Process
**Question:** Will there be a formal Q&A window for RFP clarifications?
- How will questions be submitted (email, portal, template)?
- Will answers be shared with all bidders or confidential?
- What is the expected response timeframe?

**Why this matters:** Formal Q&A process allows us to get clarifications that improve proposal accuracy. Shared answers level the playing field among bidders. Response timeframe affects whether we can use answers in proposal or must proceed with assumptions.

---

## F. Team & Responsibilities (5 Questions)

### F1. Test Data Provision
**Question:** Who is responsible for providing test data for each use case?
- Vendor must create/source test data
- Ethniki IT will provide production-like test data
- Business units will provide anonymized production data
- Joint effort

**Why this matters:** If vendor must create test data (e.g., synthetic documents, sample emails), this adds 2-4 weeks of effort for data generation, labeling, and validation. If Ethniki provides production-like data, testing is faster and more realistic. This affects both timeline and cost.

---

### F2. UAT Sign-Off Accountability
**Question:** Who has the authority to approve UAT sign-off and authorize go-live for each LOT/use case?
- Business owner per LOT
- IT governance committee
- Compliance/audit team
- Multi-party sign-off required

**Why this matters:** Multi-party sign-off extends UAT timeline due to coordination overhead. If approval authority is unclear, UAT can stall indefinitely. Understanding approval chain allows us to plan UAT duration and milestone dependencies accurately.

---

### F3. Integration Ownership
**Question:** For integration with the 9+ existing systems, who is responsible for:
- Building integration APIs: Vendor or Ethniki IT?
- Providing API documentation: Ethniki IT?
- Testing integration: Vendor, Ethniki IT, or joint?
- Ongoing integration maintenance post-go-live: Vendor or Ethniki IT?

**Why this matters:** CRITICAL - Integration ownership is a huge effort differentiator. If Ethniki IT provides APIs and documentation, vendor effort is minimal (2-3 weeks per system). If vendor must build custom integrations without documentation, effort increases 50-100% (4-6 weeks per system). For 9 systems, this is a 4-6 month timeline difference.

---

### F4. Business Analyst (BA) Assignment
**Question:** Will Ethniki assign a dedicated Business Analyst (BA) to each LOT/use case?
- Full-time dedicated BA
- Part-time BA (50% allocation)
- Shared BA across multiple LOTs
- No BA provided (vendor must include BA services)

**Why this matters:** BA availability directly impacts timeline. Full-time BA accelerates requirements validation, UAT coordination, and go-live preparation. Part-time or no BA increases timeline by 25-50% due to decision delays, requirements churn, and rework. If Ethniki cannot provide dedicated BA, vendor must include BA services in scope (additional cost).

---

### F5. BA Experience Level
**Question:** What is the expected experience level of the Ethniki-provided BA (if applicable)?
- Expert in AI/IDP/automation projects
- Intermediate (familiar with digital transformation, new to AI/IDP)
- Domain expert (insurance processes) but new to AI/IDP
- Time commitment: Full-time, 50%, ad-hoc availability?

**Why this matters:** BA experience affects knowledge transfer effort. BA new to AI/IDP requires vendor to provide more education and guidance (2-3 weeks of knowledge transfer effort). Experienced BA accelerates delivery. BA time commitment (full-time vs. ad-hoc) affects how quickly we can get decisions and requirements validated, impacting timeline by 15-30%.

---

## Summary and Next Steps

**Total Questions:** 25 (all directly impact cost, duration, and team composition for our proposal)

**Question Priority:**
- **CRITICAL (Must have before proposal):** E1 (LOT B2-B7 scope), C1 (9 systems list), F3 (integration ownership), F4 (BA assignment), E4 (commercial model)
- **HIGH (Strongly desired before proposal):** A1-A6 (architecture), B1-B4 (AI/ML), C2-C3 (integration details)
- **MEDIUM (Can proceed with assumptions if needed):** D1-D2 (compliance details), E2-E3-E5 (timeline/budget/Q&A), F1-F2-F5 (BA experience)

We appreciate Ethniki's time in reviewing these clarifications. Answers to these questions will enable us to provide an accurate, realistic proposal that meets your needs while managing risk appropriately.

**Contact:** Sai (Solution Architect), EPAM Systems
**For Questions:** [Contact information]
