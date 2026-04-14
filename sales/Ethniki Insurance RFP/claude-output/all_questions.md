# Comprehensive Question Set
## Ethniki Insurance RFP - Multi-LOT AI/IDP & Automations

---

# 1. CAPABILITY-BASED QUESTIONS

## Architecture Capability Questions

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| ARCH-001 | What is the preferred cloud provider for LOT A Control Plane deployment (AWS, Azure, GCP, multi-cloud)? | Architectural design foundation | CRITICAL |
| ARCH-002 | What is the target architecture pattern for the Enterprise AI/RAG Control Plane? (e.g., microservices, serverless, container-based) | Design approach | HIGH |
| ARCH-003 | What are the scalability requirements for the Control Plane? (concurrent users, requests/second, document volume) | Infrastructure sizing | HIGH |
| ARCH-004 | Should the architecture support multi-tenancy or is it single-tenant for Ethniki only? | Architecture pattern | MEDIUM |
| ARCH-005 | What are the disaster recovery requirements? (RPO, RTO, multi-region deployment) | Resilience design | HIGH |
| ARCH-006 | How should the architecture handle integration with the 9+ existing systems? (API gateway, ESB, point-to-point) | Integration pattern | HIGH |
| ARCH-007 | What is the data flow architecture between LOT A and LOTs B1-B7? | Inter-LOT design | HIGH |
| ARCH-008 | What monitoring and observability tools are required or preferred? | Operational architecture | MEDIUM |
| ARCH-009 | Should the architecture support hybrid cloud or must it be fully cloud-based? | Deployment flexibility | HIGH |
| ARCH-010 | What network architecture constraints exist? (VPN, private endpoints, egress restrictions) | Network design | MEDIUM |

## AI & Innovation Capability Questions

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| AI-001 | What LLM models are preferred or required? (GPT-4, Claude, open-source models like Llama/Mistral, proprietary Greek models) | Model selection | CRITICAL |
| AI-002 | Should AI models be hosted on Ethniki infrastructure or can external APIs be used? (OpenAI API, Anthropic API, etc.) | Deployment model | CRITICAL |
| AI-003 | What vector database is preferred for RAG implementation? (Pinecone, Weaviate, Milvus, Qdrant, pgvector) | RAG architecture | HIGH |
| AI-004 | What are the accuracy requirements for document extraction? (e.g., 95% accuracy, 99% for financial data) | Quality targets | HIGH |
| AI-005 | Should the solution include AI model training/fine-tuning or only use pre-trained models? | AI development scope | HIGH |
| AI-006 | What AI explainability level is required to meet EU AI Act requirements? | Compliance design | HIGH |
| AI-007 | Can Ethniki data be used to train or fine-tune AI models? | Data usage policy | HIGH |
| AI-008 | What is the policy on AI-generated content approval? (human-in-the-loop, full automation, review sampling) | AI governance | HIGH |
| AI-009 | Should the solution support multiple AI models or can it be single-model architecture? | Flexibility requirement | MEDIUM |
| AI-010 | What NLP capabilities are required for Greek language processing? (translation, entity extraction, sentiment analysis) | Greek NLP scope | HIGH |

## Data Engineering & Lead Engineer Capability Questions

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| ENG-001 | What IDP (Intelligent Document Processing) platform is preferred? (UiPath Document Understanding, Abbyy FlexiCapture, Azure Form Recognizer, AWS Textract, other) | Tool selection | CRITICAL |
| ENG-002 | What data storage solution should be used for processed documents? (Data lake, S3, Azure Blob, database, document DB) | Data storage design | HIGH |
| ENG-003 | What is the expected document processing latency? (real-time, near real-time < 1 min, batch processing) | Performance target | HIGH |
| ENG-004 | What data pipeline orchestration tool is preferred? (Airflow, Databricks Workflows, Azure Data Factory, AWS Step Functions) | Orchestration choice | MEDIUM |
| ENG-005 | What are the data retention requirements for processed documents and AI outputs? | Data lifecycle | MEDIUM |
| ENG-006 | Should the solution include automated data quality checks and validation? | Quality assurance | HIGH |
| ENG-007 | What is the expected document ingestion volume per hour/day for each use case? | Capacity planning | HIGH |
| ENG-008 | What data formats must be supported beyond PDF, DOCX, XLSX? (images, scanned docs, emails, HTML) | Format support | MEDIUM |
| ENG-009 | What is the expected error rate tolerance for document processing? | Quality threshold | MEDIUM |
| ENG-010 | Should the solution include automated reprocessing for failed documents? | Error handling | MEDIUM |

## Program Management Capability Questions

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| PM-001 | What is the expected overall program duration from contract award to final LOT delivery? | Timeline planning | CRITICAL |
| PM-002 | Should LOTs be delivered sequentially or can they be parallel? If sequential, what is the priority order? | Delivery sequencing | CRITICAL |
| PM-003 | What is the governance structure for this program? (steering committee, working groups, decision authority) | Governance model | HIGH |
| PM-004 | What are the key program milestones and their expected dates? | Milestone planning | HIGH |
| PM-005 | How should dependencies between LOT A and LOTs B be managed? | Dependency management | HIGH |
| PM-006 | What reporting frequency and format is expected? (weekly, bi-weekly, dashboards, status reports) | Reporting requirements | MEDIUM |
| PM-007 | What is the change control process for scope, timeline, or budget changes? | Change management | HIGH |
| PM-008 | Who are the key stakeholders and decision-makers for each LOT? | Stakeholder mapping | MEDIUM |
| PM-009 | What risk management approach is expected? (RAID log, risk registers, mitigation plans) | Risk management | MEDIUM |
| PM-010 | How will multi-vendor coordination be managed if different vendors win different LOTs? | Vendor coordination | HIGH |

## Sales & Client Engagement Capability Questions

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| SALES-001 | What evaluation criteria will be used to assess proposals? (technical, price, experience, etc.) and their weighting? | Evaluation understanding | CRITICAL |
| SALES-002 | Are there preferred vendors or incumbents for any LOT? | Competitive landscape | HIGH |
| SALES-003 | What is the budget range for this program (overall or per-LOT)? | Budget alignment | CRITICAL |
| SALES-004 | What are the key success factors that will influence vendor selection? | Value proposition | HIGH |
| SALES-005 | Who will be the primary client contacts and decision-makers during implementation? | Engagement model | MEDIUM |
| SALES-006 | What is the expected level of client involvement during implementation? (daily, weekly check-ins, milestone reviews) | Collaboration model | MEDIUM |
| SALES-007 | What are the expectations for knowledge transfer and training? | Training scope | MEDIUM |
| SALES-008 | What post-implementation support model is expected? (duration, SLA levels, support team structure) | Support planning | MEDIUM |
| SALES-009 | Are there reference site visits or customer references required as part of the evaluation? | Reference requirements | LOW |
| SALES-010 | What contract type is preferred? (fixed price, time & materials, hybrid) | Commercial model | HIGH |

---

# 2. SDLC-BASED QUESTIONS

## Requirements Phase

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| REQ-001 | Are the use case requirements final or subject to change? | Scope stability | HIGH |
| REQ-002 | Are detailed functional requirements available beyond the RFP documents? | Requirements completeness | HIGH |
| REQ-003 | Will Ethniki provide business process documentation for each use case? | Process understanding | MEDIUM |
| REQ-004 | Who will be the business SMEs for each LOT/use case? | SME engagement | MEDIUM |
| REQ-005 | What is the requirements sign-off and change approval process? | Requirements governance | MEDIUM |
| REQ-006 | Are there non-functional requirements documented? (performance, security, usability) | NFR clarity | HIGH |
| REQ-007 | What are the acceptance criteria for each use case? | Success definition | HIGH |
| REQ-008 | Are there user personas and user stories available? | User-centric design | LOW |

## Design Phase

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| DES-001 | What is the approval process for architecture and design documents? | Design governance | MEDIUM |
| DES-002 | Are there existing design standards or templates to follow? | Design standards | MEDIUM |
| DES-003 | What level of design documentation is expected? (HLD, LLD, data models, interface specs) | Documentation scope | MEDIUM |
| DES-004 | Should design reviews include Ethniki IT architecture team? | Review process | MEDIUM |
| DES-005 | Are there UI/UX design requirements or guidelines? | UX standards | LOW |
| DES-006 | What security architecture review is required? | Security approval | HIGH |
| DES-007 | Should integration designs be reviewed with system owners? | Integration approval | HIGH |
| DES-008 | What data model approval is needed? | Data governance | MEDIUM |

## Development Phase

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| DEV-001 | What coding standards and best practices must be followed? | Code quality | MEDIUM |
| DEV-002 | What development environment will be provided? (dev, test, UAT, prod) | Environment setup | HIGH |
| DEV-003 | What source code management tool should be used? (GitHub, GitLab, Azure DevOps, Bitbucket) | SCM choice | MEDIUM |
| DEV-004 | What CI/CD tools are preferred or required? | CI/CD setup | MEDIUM |
| DEV-005 | Should code reviews be conducted jointly with Ethniki team? | Code review process | LOW |
| DEV-006 | What documentation must be delivered during development? (code comments, API docs, configuration guides) | Documentation requirements | MEDIUM |
| DEV-007 | What development team composition is expected? (onshore/offshore ratio, Greek-speaking members) | Team structure | MEDIUM |
| DEV-008 | Are there specific development tools or IDEs that must be used? | Tool standards | LOW |

## Testing Phase

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| TEST-001 | What testing phases are required? (unit, integration, system, UAT, performance, security) | Testing scope | HIGH |
| TEST-002 | What test coverage is expected? (e.g., 80% code coverage, 100% use case coverage) | Quality target | MEDIUM |
| TEST-003 | Who will conduct UAT? (Ethniki business users, IT team, joint) | UAT responsibility | HIGH |
| TEST-004 | What is the expected UAT duration per LOT? | Timeline planning | HIGH |
| TEST-005 | Will Ethniki provide test data or must vendor create synthetic test data? | Test data source | HIGH |
| TEST-006 | What performance testing is required? (load testing, stress testing, endurance testing) | Performance validation | MEDIUM |
| TEST-007 | Is security/penetration testing required before go-live? | Security testing | HIGH |
| TEST-008 | What test documentation must be delivered? (test plans, test cases, test results) | Test deliverables | MEDIUM |
| TEST-009 | What are the UAT sign-off criteria and process? | Acceptance process | HIGH |
| TEST-010 | Should testing include multi-vendor integration testing (if different vendors for LOTs A and B)? | Integration testing | HIGH |

## Deployment Phase

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| DEP-001 | What is the deployment strategy? (big bang, phased by department, phased by use case) | Deployment approach | HIGH |
| DEP-002 | What deployment windows are available? (weekends, after-hours, maintenance windows) | Deployment timing | MEDIUM |
| DEP-003 | Is a parallel run period required before cutover? | Transition approach | MEDIUM |
| DEP-004 | What rollback plan is expected if deployment fails? | Risk mitigation | HIGH |
| DEP-005 | What deployment documentation must be delivered? (runbooks, deployment guides, configuration docs) | Deployment deliverables | MEDIUM |
| DEP-006 | Who has approval authority for production deployment? | Deployment governance | HIGH |
| DEP-007 | What post-deployment validation is required? | Go-live validation | MEDIUM |
| DEP-008 | Should deployment be automated or manual? | Deployment automation | MEDIUM |

## Maintenance & Support Phase

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| MAIN-001 | What is the expected warranty/support period after go-live? | Support duration | HIGH |
| MAIN-002 | What SLA levels are required for production support? (response time, resolution time, availability) | SLA targets | HIGH |
| MAIN-003 | What support model is expected? (24/7, business hours, tiered support) | Support structure | MEDIUM |
| MAIN-004 | How should incidents and service requests be managed? (ticketing system, escalation process) | Support process | MEDIUM |
| MAIN-005 | What ongoing maintenance activities are expected? (patching, updates, enhancements) | Maintenance scope | MEDIUM |
| MAIN-006 | Should vendor provide ongoing model retraining and optimization? | AI maintenance | HIGH |
| MAIN-007 | What knowledge transfer is required to Ethniki support team? | Knowledge transfer | MEDIUM |
| MAIN-008 | Are there expected enhancements or Phase 2 functionality post-initial delivery? | Future scope | LOW |

---

# 3. DOMAIN-SPECIFIC QUESTIONS (AI/IDP & Insurance)

## Intelligent Document Processing (IDP)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| IDP-001 | What is the ratio of structured vs. unstructured documents to be processed? | Processing approach | HIGH |
| IDP-002 | What is the ratio of scanned/image-based vs. digital documents? | OCR requirements | HIGH |
| IDP-003 | What OCR accuracy is required for Greek text? | Greek OCR quality | HIGH |
| IDP-004 | Are there handwritten forms or signatures to process? | Handwriting recognition | MEDIUM |
| IDP-005 | What table extraction accuracy is required? | Table processing | MEDIUM |
| IDP-006 | Should the solution handle multi-page document classification? | Document classification | HIGH |
| IDP-007 | What entity extraction is required? (names, addresses, dates, amounts, policy numbers, etc.) | Entity recognition | HIGH |
| IDP-008 | How should document extraction errors be handled? (human review queue, automated retry, rejection) | Error handling | HIGH |
| IDP-009 | What is the expected improvement in processing time per use case? | Success metrics | HIGH |
| IDP-010 | Should the solution include document redaction capabilities for PII? | Privacy feature | MEDIUM |

## Retrieval-Augmented Generation (RAG)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| RAG-001 | What document corpus size is expected for RAG? (number of documents, total GB/TB) | Capacity planning | HIGH |
| RAG-002 | What retrieval accuracy is required for RAG queries? | Quality target | HIGH |
| RAG-003 | Should RAG support multi-lingual retrieval (Greek and English)? | Language support | HIGH |
| RAG-004 | What is the expected query response time for RAG? | Performance target | MEDIUM |
| RAG-005 | Should RAG include citation/source tracking for compliance? | Traceability feature | HIGH |
| RAG-006 | How should RAG handle conflicting information from multiple sources? | Conflict resolution | MEDIUM |
| RAG-007 | What vector embedding model is preferred for Greek language? | Embedding choice | MEDIUM |
| RAG-008 | Should RAG support semantic search, keyword search, or both? | Search capability | MEDIUM |
| RAG-009 | What chunking strategy is preferred for document segmentation? | RAG design | MEDIUM |
| RAG-010 | Should RAG include feedback loops for continuous improvement? | AI learning | MEDIUM |

## Insurance Domain

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| INS-001 | What insurance lines of business are in scope beyond Corporate P&C? (Motor, Life, Health, etc.) | Scope clarity | HIGH |
| INS-002 | What underwriting workflows must the solution support? | Process alignment | HIGH |
| INS-003 | What claims processing workflows must be automated? | Process scope | HIGH |
| INS-004 | Are there specific Greek insurance regulations beyond EU-level requirements? | Regulatory compliance | HIGH |
| INS-005 | What policy document types must be processed? (applications, endorsements, renewals, cancellations) | Document types | MEDIUM |
| INS-006 | What insurance-specific entities must be extracted? (policy numbers, claim numbers, coverage types, limits, deductibles) | Entity extraction | HIGH |
| INS-007 | Should the solution integrate with policy administration systems? If yes, which? | System integration | HIGH |
| INS-008 | What insurance calculation logic must be supported? (premiums, reserves, loss ratios) | Calculation scope | MEDIUM |
| INS-009 | Are there broker or agent portals that need integration? | Distribution channel | MEDIUM |
| INS-010 | What customer communication channels must be supported? (email, portal, phone/IVR, mobile app) | Channel support | MEDIUM |

## Email & Mailroom Automation (CPCU2)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| EMAIL-001 | What email platforms are used? (Exchange, Outlook, Gmail, other) | Platform integration | HIGH |
| EMAIL-002 | What is the current email volume per shared mailbox? | Capacity planning | HIGH |
| EMAIL-003 | What email categories must be classified? (Offer, Contract, Addendum, Question, Claim, etc.) | Classification taxonomy | HIGH |
| EMAIL-004 | What routing rules are required beyond email classification? | Routing logic | MEDIUM |
| EMAIL-005 | Should the solution handle email attachments differently than email body? | Attachment handling | MEDIUM |
| EMAIL-006 | What priority scoring logic is expected? (based on customer tier, urgency keywords, SLA) | Priority rules | MEDIUM |
| EMAIL-007 | Should duplicate email detection be based on exact match or semantic similarity? | Deduplication logic | LOW |
| EMAIL-008 | What happens to unclassifiable emails? (default routing, hold for review, escalation) | Exception handling | MEDIUM |
| EMAIL-009 | Should the solution extract action items and deadlines from emails? | Extraction scope | LOW |
| EMAIL-010 | What email response time SLA should the automation achieve? | Performance target | MEDIUM |

## Geocoding & GIS Integration (CPCU1)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| GEO-001 | What GIS platform is used (GEOL mentioned)? API documentation available? | Platform integration | HIGH |
| GEO-002 | What geocoding API is preferred? (Google Maps, Azure Maps, HERE, OpenStreetMap, local Greek provider) | Geocoding service | HIGH |
| GEO-003 | What address formats must be supported? (Greek addresses, international addresses) | Format support | HIGH |
| GEO-004 | What geocoding accuracy is required? (street-level, building-level, coordinate precision) | Accuracy target | MEDIUM |
| GEO-005 | How should ambiguous or unresolvable addresses be handled? (manual review queue, best-match, rejection) | Error handling | MEDIUM |
| GEO-006 | What coordinate system is required? (WGS84, other) | GIS standard | MEDIUM |
| GEO-007 | Should the solution handle bulk geocoding vs. real-time geocoding differently? | Processing mode | MEDIUM |
| GEO-008 | What catastrophe modeling integrations are required beyond GEOL? | CAT modeling | LOW |
| GEO-009 | Should geocoded data include additional attributes? (flood zones, earthquake zones, risk scores) | Enrichment scope | LOW |
| GEO-010 | What is the target timeline to clear the 3,000-contract backlog? (mentioned as 10 days) | Backlog target | HIGH |

## Information Aggregation & Pricing (CPCU3)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| PRICE-001 | What systems contain the client history and risk information (9+ systems mentioned)? | System mapping | HIGH |
| PRICE-002 | What Excel templates are used for underwriting proposals? Can samples be provided? | Template understanding | HIGH |
| PRICE-003 | What data fields must be auto-populated in the Excel templates? | Field mapping | HIGH |
| PRICE-004 | What underwriter controls must be preserved? (manual overrides, decision checkpoints) | Human-in-loop design | HIGH |
| PRICE-005 | Should the solution integrate with rating tools? If yes, which ones? | Rating integration | MEDIUM |
| PRICE-006 | What partner request document formats must be supported? | Format variety | MEDIUM |
| PRICE-007 | What is the expected reduction in proposal preparation time? (mentioned as "hours to minutes") | Success metric | HIGH |
| PRICE-008 | Should historical proposal data be used for AI training/recommendations? | AI training data | MEDIUM |
| PRICE-009 | What validation rules should be applied to auto-populated data? | Data validation | HIGH |
| PRICE-010 | Should the solution support batch processing of multiple proposals? | Batch capability | LOW |

## Public Tender Intelligence (CPCU4)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| TENDER-001 | What public tender platforms must be monitored? (Greek government sites, EU TED, others) | Platform scope | HIGH |
| TENDER-002 | What defines a "relevant" insurance tender? (keywords, categories, value thresholds) | Filtering rules | HIGH |
| TENDER-003 | What technical requirements sections must be extracted from tender documents? | Extraction scope | HIGH |
| TENDER-004 | How should tender documents be routed to appropriate departments? | Routing logic | MEDIUM |
| TENDER-005 | What is the expected tender volume per year? (mentioned as ~750 relevant tenders) | Volume planning | MEDIUM |
| TENDER-006 | What tender metadata must be captured? (deadline, value, contracting authority, technical requirements) | Metadata extraction | HIGH |
| TENDER-007 | Should the solution provide tender relevancy scoring? If yes, what criteria? | Scoring logic | MEDIUM |
| TENDER-008 | What is the expected improvement in tender discovery time? | Success metric | MEDIUM |
| TENDER-009 | Should the solution track competitor participation in tenders? | Competitive intelligence | LOW |
| TENDER-010 | What alerts or notifications are required for new relevant tenders? | Notification mechanism | MEDIUM |

## Contract Generation (CPCU5)

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| CONTRACT-001 | What contract types must be generated? (policies, endorsements, addendums, renewals) | Scope definition | HIGH |
| CONTRACT-002 | What contract templates are used? Can samples be provided? | Template understanding | HIGH |
| CONTRACT-003 | What data sources feed contract generation? (policy admin system, underwriting system, CRM) | Data integration | HIGH |
| CONTRACT-004 | What contract approval workflow is required? | Approval process | MEDIUM |
| CONTRACT-005 | Should contracts be generated in Greek, English, or both? | Language requirement | HIGH |
| CONTRACT-006 | What contract versioning and audit trail is required? | Version control | MEDIUM |
| CONTRACT-007 | Should the solution support contract comparison (old vs. new versions)? | Comparison feature | LOW |
| CONTRACT-008 | What e-signature integration is required? | Signature workflow | MEDIUM |
| CONTRACT-009 | Should contracts include dynamic clauses based on risk assessment? | Dynamic generation | MEDIUM |
| CONTRACT-010 | What is the expected reduction in contract generation time? | Success metric | MEDIUM |

## Greek Language & Localization

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| GREEK-001 | What percentage of documents are in Greek vs. English? | Language distribution | HIGH |
| GREEK-002 | Should the solution support Greek character recognition in scanned documents? | Greek OCR | HIGH |
| GREEK-003 | What Greek NLP capabilities are required? (entity extraction, sentiment analysis, summarization) | Greek NLP scope | HIGH |
| GREEK-004 | Are there Greek-specific terminology or jargon dictionaries to incorporate? | Domain vocabulary | MEDIUM |
| GREEK-005 | Should the UI be in Greek, English, or multilingual? | UI language | MEDIUM |
| GREEK-006 | What Greek regulatory reporting requirements must be supported? | Regulatory reporting | MEDIUM |
| GREEK-007 | Should the solution handle Greek date and number formats? | Localization details | LOW |
| GREEK-008 | Are there Greek keyboard input requirements for user interfaces? | Input method | LOW |
| GREEK-009 | What Greek language model performance is acceptable compared to English models? | Performance expectation | MEDIUM |
| GREEK-010 | Should Greek-English translation be included for reporting or analysis? | Translation feature | LOW |

## Security, Privacy & Compliance

| Question ID | Question | Purpose | Priority |
|-------------|----------|---------|----------|
| SEC-001 | What PII types are in the documents? (names, addresses, IDs, financial data, health data) | PII inventory | HIGH |
| SEC-002 | What data masking or anonymization is required? | Privacy controls | HIGH |
| SEC-003 | What encryption is required? (at rest, in transit, key management) | Encryption requirements | HIGH |
| SEC-004 | What authentication methods are required? (SSO, MFA, AD integration) | Authentication design | HIGH |
| SEC-005 | What user roles and permissions must be supported? | RBAC design | HIGH |
| SEC-006 | What audit logging is required? (user actions, data access, AI decisions) | Audit requirements | HIGH |
| SEC-007 | What penetration testing or security certifications are required? (ISO 27001, SOC 2, etc.) | Security validation | MEDIUM |
| SEC-008 | How should AI model security be ensured? (model versioning, input validation, output filtering) | AI security | HIGH |
| SEC-009 | What data residency requirements exist? (data must stay in Greece/EU) | Data sovereignty | HIGH |
| SEC-010 | What incident response process is expected if a security breach occurs? | Incident management | MEDIUM |

---

# QUESTION SUMMARY

## Total Questions: 190

### By Category:
- **Capability-Based:** 50 questions
  - Architecture: 10
  - AI & Innovation: 10
  - Data Engineering: 10
  - Program Management: 10
  - Sales & Client: 10

- **SDLC-Based:** 48 questions
  - Requirements: 8
  - Design: 8
  - Development: 8
  - Testing: 10
  - Deployment: 8
  - Maintenance: 6

- **Domain-Specific:** 92 questions
  - IDP: 10
  - RAG: 10
  - Insurance: 10
  - Email/Mailroom (CPCU2): 10
  - Geocoding/GIS (CPCU1): 10
  - Pricing (CPCU3): 10
  - Tender Intelligence (CPCU4): 10
  - Contract Generation (CPCU5): 10
  - Greek Language: 10
  - Security/Privacy/Compliance: 10

### By Priority:
- **CRITICAL:** 22 questions
- **HIGH:** 101 questions
- **MEDIUM:** 62 questions
- **LOW:** 15 questions

---

## Next Steps

1. **Review & Prioritize:** Ethniki to review questions and prioritize responses
2. **Q&A Session:** Schedule clarification session with Ethniki stakeholders
3. **Document Responses:** Capture answers in structured format
4. **Update Proposal:** Refine proposal based on answers
5. **Risk Assessment:** Update risk register based on unresolved questions
