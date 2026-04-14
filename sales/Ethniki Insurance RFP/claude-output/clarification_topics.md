# Clarification Topics
## Ethniki Insurance RFP - Missing & Unclear Information

---

## High Priority Clarifications

| Topic | Missing Information | Reference Needed | Impact on Proposal |
|-------|---------------------|------------------|-------------------|
| **LOT A Architecture** | Specific technology stack for Control Plane (cloud provider, LLM models, vector DB) | Technical requirements for LOT A | CRITICAL - Cannot size infrastructure or license costs |
| **Deployment Model** | Cloud vs. on-premise vs. hybrid deployment preference | Infrastructure requirements | CRITICAL - Affects architecture, pricing, compliance |
| **Data Residency** | Where data must be stored/processed (Greece, EU, specific regions) | GDPR/DORA compliance requirements | CRITICAL - Impacts cloud provider and design |
| **Existing AI Infrastructure** | Current AI/ML platforms, tools, or licenses already in place | Technology landscape | HIGH - Affects reuse vs. new build decisions |
| **Integration Details** | APIs, data formats, authentication methods for 9+ existing systems | System integration requirements | HIGH - Critical for effort estimation |
| **LLM Model Preferences** | Proprietary (OpenAI, Anthropic) vs. open-source (Llama, Mistral) vs. local deployment | LOT A technical design | HIGH - Licensing, cost, compliance implications |
| **Budget Range** | Overall program budget or per-LOT budget ranges | Financial constraints | HIGH - Shapes solution scope and approach |
| **Timeline Expectations** | Desired start date, overall program duration, LOT delivery sequence | Program planning | HIGH - Resource allocation and phasing |
| **Greek Language Requirements** | Extent of Greek language processing needed; performance expectations | NLP/AI requirements | HIGH - Technology selection and validation |
| **Volume & Performance** | Document processing volumes per use case; SLA requirements | Capacity planning | MEDIUM - Infrastructure sizing |
| **Vendor Preferences** | Preferred/excluded IDP vendors, AI platforms, cloud providers | Technology selection | MEDIUM - Partner and tooling strategy |
| **Team Composition** | Expected onshore/offshore ratio; required Greek-speaking team members | Staffing model | MEDIUM - Team structure and cost |
| **Training Scope** | End-user training, admin training, knowledge transfer expectations | Change management | MEDIUM - Service scope definition |
| **Support Model** | Post-go-live support duration, SLA levels, escalation procedures | Ongoing services | MEDIUM - Long-term cost model |
| **LOT B Definitions** | Detailed scope for LOTs B1-B7 (only B1 use cases are detailed) | Complete use case inventory | CRITICAL - Can only price what's defined |

---

## Technical Clarifications

| Topic | Current Understanding | What's Missing | Question to Ask |
|-------|----------------------|----------------|-----------------|
| **LOT A: Control Plane** | Must support RAG, governance, multi-vendor ecosystem | Technology stack, capacity, expected load | What are the required components for LOT A? Cloud provider preference? Expected concurrent users and query load? |
| **Document Formats** | PDF, Word, Excel, emails mentioned | Scanned vs. digital; image quality; structured vs. unstructured | What percentage of documents are scanned vs. digital? Are there handwritten forms? Quality standards? |
| **Existing Systems** | 9+ systems mentioned (Aviva, MOS, GEOL GIS) | System names, APIs, data models, authentication | Can we get a complete list of systems requiring integration? Are API docs available? Authentication methods? |
| **Security Architecture** | GDPR, EU AI Act, DORA compliance required | Specific security controls, audit requirements, penetration testing | What specific security certifications are required? Is penetration testing required pre-deployment? Audit frequency? |
| **Data Quality** | Not addressed | Current data quality levels; cleansing expectations | What is the current data quality level? Is data cleansing in scope? Error handling expectations? |
| **Testing Requirements** | Not specified | UAT duration, test data availability, acceptance criteria | What are the testing phases? UAT duration? Who provides test data? Acceptance criteria? |
| **Change Management** | Not addressed | User adoption strategy, training plan, communication plan | Is change management included in turn-key scope? Expected resistance areas? Training format preferences? |
| **Disaster Recovery** | Not specified | RPO, RTO, backup requirements | What are the RPO and RTO requirements? Backup frequency? DR testing expectations? |
| **Monitoring & Logging** | Not addressed | Logging requirements, monitoring tools, alerting | What monitoring tools are currently used? Required log retention period? Alert escalation procedures? |
| **Licensing Model** | Turn-key includes licenses | Per-user, per-document, enterprise agreement? | What licensing model is preferred? Named users vs. concurrent? Document volume tiers? |

---

## Business Clarifications

| Topic | Current Understanding | What's Missing | Question to Ask |
|-------|----------------------|----------------|-----------------|
| **Success Metrics** | Efficiency, speed, accuracy improvements mentioned | Quantified targets for each use case | What are the quantified success metrics per use case? (e.g., "reduce processing time by 50%") |
| **Prioritization** | Quick wins vs. tactical projects indicated | LOT priority order if sequential delivery needed | If LOTs must be delivered sequentially, what is the priority order? Can LOTs overlap? |
| **Stakeholder Roles** | Operations, Underwriting, Claims, Customer Service mentioned | Decision makers, approval authorities, escalation paths | Who are the key decision makers per LOT? Approval process for UAT sign-off? |
| **Vendor Selection Criteria** | Not detailed beyond turn-key model | Weighting of price vs. technical vs. experience | What is the evaluation criteria weighting? (e.g., 40% technical, 30% price, 30% experience) |
| **Existing Contracts** | Two AI solutions already in production | Current vendor relationships; incumbent advantage/constraint | Who are the current AI/automation vendors? Are they participating in this RFP? Preference for incumbents or new vendors? |
| **Governance Model** | Enterprise-grade governance required | Governance committee, decision-making process, change control | What is the program governance structure? Steering committee composition? Change control process? |
| **Compliance Validation** | GDPR, EU AI Act, DORA mentioned | Third-party audits, certifications, documentation requirements | Are third-party compliance audits required? Required documentation? Ongoing compliance validation process? |
| **Scope Flexibility** | Turn-key model with all licenses | Flexibility to propose alternatives; change order process | Can vendors propose alternative approaches to use cases? Change order process for scope adjustments? |
| **Multi-Vendor Coordination** | Multi-vendor ecosystem expected | Coordination mechanism, integration responsibilities | If LOT A and LOT B are different vendors, who coordinates integration? Joint testing expectations? |
| **Intellectual Property** | Not addressed | IP ownership for AI models, code, configurations | Who owns the IP for custom models, scripts, configurations? Can vendor reuse for other clients? |

---

## Data & Privacy Clarifications

| Topic | Current Understanding | What's Missing | Question to Ask |
|-------|----------------------|----------------|-----------------|
| **Personal Data** | Insurance documents likely contain PII | Types of PII, sensitivity levels, masking requirements | What types of PII are in the documents? Required masking/anonymization? Sensitivity classification system? |
| **Data Retention** | Not specified | Retention periods for processed documents, AI training data, logs | What are the data retention requirements? Can processed documents be used for model training? Log retention period? |
| **Cross-Border Transfers** | GDPR compliance required | If/how data can move outside Greece/EU | Can data be processed outside Greece? Outside EU? Restrictions on cloud regions? |
| **Third-Party Data** | Not addressed | Use of external data sources, APIs, pre-trained models | Are external data sources allowed (geocoding APIs, market data)? Can pre-trained models be used? |
| **AI Model Training** | RAG and AI required | Can client data be used for model training? Separate models per client vs. shared? | Can Ethniki data be used to fine-tune models? Are models isolated or can be reused for other clients (anonymized)? |
| **Data Access Controls** | RBAC/ABAC implied | User roles, approval workflows, audit trails | What are the required user roles? Approval workflow for sensitive data access? Audit trail requirements? |
| **Consent Management** | Not addressed | If/how end-customer consent is obtained for AI processing | Is end-customer consent required for AI processing of their documents? Consent management approach? |
| **Right to Explanation** | EU AI Act requirement | Explainability requirements for AI decisions | What level of explainability is required for AI decisions? Audit trail of AI reasoning? Human-in-the-loop checkpoints? |

---

## Timeline & Delivery Clarifications

| Topic | Current Understanding | What's Missing | Question to Ask |
|-------|----------------------|----------------|-----------------|
| **RFP Timeline** | Key dates mentioned but not detailed | Proposal due date, vendor Q&A deadline, decision date | What is the final proposal submission deadline? Q&A cutoff date? Expected award decision date? |
| **Delivery Timeline** | CPCU1: 1 month, CPCU2/3: 3 months | LOT A timeline, LOTs B2-B7 timelines, dependencies | What is the expected delivery timeline for LOT A? For LOTs B2-B7? Can delivery overlap with LOT A development? |
| **Pilot/POC Phase** | Not mentioned | If pilot/POC required before full implementation | Is a pilot or POC phase required/allowed? If yes, scope and duration? Paid or unpaid? |
| **Phased Rollout** | Quick wins and tactical projects indicated | Phasing within each LOT; roll out by department vs. all at once | Should use cases roll out by department/region or enterprise-wide? Phased user onboarding plan? |
| **Go-Live Dependencies** | LOT A must support LOTs B | Specific dependencies, integration testing timelines | What are the explicit dependencies between LOT A and LOTs B? Integration testing window between LOTs? |
| **Transition Period** | Not addressed | Parallel run period, cutover strategy, rollback plan | Is a parallel run period required? Cutover strategy (big bang vs. phased)? Rollback plan if issues arise? |

---

## Commercial & Contractual Clarifications

| Topic | Current Understanding | What's Missing | Question to Ask |
|-------|----------------------|----------------|-----------------|
| **Pricing Model** | Per-LOT pricing required | Fixed price vs. T&M, payment milestones, warranty period | Is fixed price required or is T&M acceptable? Payment milestone structure? Warranty period expectations? |
| **Contract Duration** | Not specified | Implementation period + support period | What is the expected contract duration? Implementation period + X years support? Option to extend? |
| **Penalty Clauses** | Not mentioned | SLA penalties, delivery delay penalties | Are SLA penalties included? Penalties for delivery delays? Performance guarantees? |
| **Acceptance Criteria** | Not detailed | UAT sign-off process, performance benchmarks | What constitutes successful delivery/acceptance? Performance benchmarks? UAT sign-off authority? |
| **Subcontracting** | Multi-vendor ecosystem implies collaboration | Subcontracting allowed/required, prime contractor responsibility | Is subcontracting allowed? Must prime contractor take full responsibility? Subcontractor approval process? |
| **Exclusivity** | Not addressed | Can vendor work with Ethniki competitors? | Are there exclusivity requirements? Can vendor serve other Greek insurance companies concurrently? |
| **Exit Strategy** | Not addressed | Knowledge transfer, data export, transition assistance | What is the exit strategy if contract ends? Knowledge transfer requirements? Data export formats? |
| **Currency & Payment Terms** | Not specified | Currency (EUR?), payment terms (Net 30/60?), invoicing frequency | What currency for pricing? Payment terms? Invoicing frequency (monthly, milestone-based)? |

---

## Greek Market & Regulatory Clarifications

| Topic | Current Understanding | What's Missing | Question to Ask |
|-------|----------------------|----------------|-----------------|
| **Greek Regulatory Requirements** | GDPR, EU AI Act, DORA mentioned | Greece-specific insurance regulations, Hellenic Data Protection Authority requirements | Are there Greece-specific insurance or data protection regulations beyond EU-level? Local authority approval required? |
| **Language Requirements** | Greek tender documents mentioned | Required language for UI, documentation, support | What language(s) required for: User interface? Documentation? Support team? Training materials? |
| **Local Presence** | Not specified | Required local office, local team members, Greek incorporation | Is a local Greek office required? Percentage of local team members? Must vendor be incorporated in Greece? |
| **Greek Insurance Specifics** | Ethniki is largest Greek insurer | Greek insurance market nuances, local competitive dynamics | Are there Greek insurance market-specific workflows or requirements to consider? Local competitor benchmarks? |
| **Public Sector Interaction** | Public tender intelligence (CPCU4) | Public tender platform access, Greek government API integration | Which public tender platforms must be monitored? API access requirements? Greek government system integration needs? |

---

## Summary of Most Critical Gaps

### Must Have Before Proposal Submission:
1. **LOT A Technology Stack** - Cannot design or price without knowing required components
2. **LOT B2-B7 Definitions** - Cannot bid on undefined LOTs
3. **Deployment Model & Data Residency** - Fundamental architecture decision
4. **Timeline & Budget Range** - Essential for solution scoping
5. **Proposal Due Date** - Need to know deadline

### Should Have for Competitive Proposal:
1. Integration details for existing systems
2. Volume and performance requirements per use case
3. Evaluation criteria and weighting
4. Greek language processing expectations
5. Pilot/POC phase expectations

### Nice to Have for Risk Management:
1. Existing vendor relationships and preferences
2. Governance and decision-making structure
3. IP and licensing model details
4. Compliance validation process
5. Exit strategy requirements
