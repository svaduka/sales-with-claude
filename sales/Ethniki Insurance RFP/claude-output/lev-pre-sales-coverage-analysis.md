# Lev's Pre-Sales Coverage Analysis
## Three-Way Comparison: Input → Claude Analysis → Lev's Review

**Date:** 2026-04-14
**Participants:** Sai (Solution Architect), Lev (Pre-Sales Lead)
**Focus:** Pre-sales estimation impact only (cost, duration, team composition)

---

## Executive Summary

**Lev's Guidance:** "Questions must impact cost, duration, team composition for the proposal - defer delivery details"

**Key Finding:** Lev's meeting covered **11 estimation-critical topics**. Analysis shows:
- ✅ **11 topics COVERED** in Lev's review (all align with Claude's questions)
- ⚠️ **7 topics NOT YET COVERED** but critical for estimation
- 🎯 **Total Pre-Sales Questions Needed:** ~25-30 (filtered from Claude's 236)

---

## Part 1: What Lev Already Covered (11 Topics)

| # | Topic | Lev's Coverage | Claude Question IDs | Estimation Impact | Status |
|---|-------|---------------|-------------------|------------------|--------|
| **1** | **AWS Architecture Direction** | ✅ AWS confirmed; need serverless vs containers | ARCH-001 (answered), ARCH-002 | **HIGH** - Affects team skills, cost model | ✅ COVERED |
| **2** | **Pre-Sales Focus Filter** | ✅ Guidance to filter 236→25 questions | N/A (meta-guidance) | **CRITICAL** - Avoids overwhelming client | ✅ GUIDANCE |
| **3** | **Delivery Timelines** | ✅ "1 month first lot" feasibility; EPAM will propose alternative | TIME-001 to TIME-008 | **CRITICAL** - Timeline drives team size | ✅ COVERED |
| **4** | **Nine Systems Integration** | ✅ Need system list, APIs, auth, volumes | ARCH-006, Integration questions | **CRITICAL** - Largest effort variable | ✅ COVERED |
| **5** | **Data Quality & Extraction** | ✅ Document types, quality, accuracy thresholds | ENG-007, ENG-008, NFR-003 | **HIGH** - Affects preprocessing effort | ✅ COVERED |
| **6** | **Compliance (GDPR/EU AI)** | ✅ Need specific frameworks, data residency | Compliance questions | **HIGH** - Affects documentation effort | ✅ COVERED |
| **7** | **AWS Bedrock vs External** | ✅ Model approval; integration complexity | AI-001, AI-002, AI-003 | **MEDIUM** - Affects integration scope | ✅ COVERED |
| **8** | **AWS Region Constraints** | ✅ EU region; need specific (Frankfurt/Milan) | ARCH-011 | **HIGH** - Affects service availability | ✅ COVERED |
| **9** | **Multi-Tenancy & DR** | ✅ Single vs multi; RTO/RPO requirements | ARCH-004, ARCH-005 | **MEDIUM** - Affects architecture complexity | ✅ COVERED |
| **10** | **Vendor Coordination** | ✅ Multi-vendor governance, dependencies | PM-010, RACI questions | **HIGH** - Affects schedule risk | ✅ COVERED |
| **11** | **Next Steps** | ✅ Send refined questions; prepare proposal | N/A (action items) | **CRITICAL** - Execution plan | ✅ DEFINED |

**Assessment:** Lev's 11 topics align well with Claude's analysis. All have corresponding questions in Claude's 236-question set.

---

## Part 2: What Lev Did NOT Cover (But Impacts Estimation)

### CRITICAL Gaps (High Impact on Cost/Duration/Team):

| # | Topic | Why It Matters for Estimation | Claude Analysis | Estimation Impact | Priority |
|---|-------|------------------------------|----------------|------------------|----------|
| **12** | **LOT B2-B7 Definitions** | Cannot price undefined LOTs; scope unknown | Identified in clarification_topics.md as CRITICAL | **CRITICAL** - Cannot estimate undefined work | 🔴 **MISSING** |
| **13** | **BA Availability & Experience** | BA availability = 25-50% timeline variance (Step 12) | Step 12 analysis: 8 questions (BA-001 to BA-008) | **CRITICAL** - Timeline depends on BA support | 🔴 **MISSING** |
| **14** | **RACI Matrix (Test Data, UAT, Integration)** | Who provides test data? Who does integration? Affects effort | Step 12 analysis: 10 questions (RACI-001 to RACI-010) | **CRITICAL** - Responsibility = effort allocation | 🔴 **MISSING** |
| **15** | **Commercial Model (T&M vs Fixed-Price)** | Fixed-price needs 60% buffer; T&M more flexible | Step 12: Strong T&M recommendation | **CRITICAL** - Pricing model affects risk | 🔴 **MISSING** |
| **16** | **Proposal Due Date** | Need deadline to know how much analysis time available | Identified in clarification_topics.md as CRITICAL | **CRITICAL** - Urgency drives depth | 🔴 **MISSING** |
| **17** | **Budget Range** | Budget shapes solution scope and approach | Identified in SALES-003 as CRITICAL | **CRITICAL** - Cannot scope without budget guidance | 🔴 **MISSING** |

### HIGH Priority Gaps (Medium-High Impact):

| # | Topic | Why It Matters for Estimation | Claude Analysis | Estimation Impact | Priority |
|---|-------|------------------------------|----------------|------------------|----------|
| **18** | **Functional/Non-Functional Requirements Detail** | Performance, accuracy, availability targets affect sizing | Step 12: NFR-001 to NFR-010 | **HIGH** - NFRs drive infrastructure sizing | 🟡 **MISSING** |

---

## Part 3: Filtered Pre-Sales Question Set (25 Questions)

**Based on Lev's guidance:** "Questions must impact cost, duration, team composition"

### Estimation-Critical Questions to Send to Client:

#### A. Architecture & Infrastructure (6 questions)

| ID | Question | Why It Impacts Estimation | Lev Coverage |
|----|----------|---------------------------|--------------|
| **ARCH-002** | What AWS architecture pattern is required? (serverless with Lambda/Fargate vs. ECS/EKS containers) | Serverless = lower ops cost but Lambda limits; containers = more control but higher ops | ✅ Covered |
| **ARCH-003** | What are the scalability requirements? (concurrent users, requests/second, document processing volume per LOT) | Drives infrastructure sizing and cost | ✅ Covered |
| **ARCH-004** | Should the architecture support multi-tenancy (across vendors) or single-tenant? | Multi-tenancy = more complex isolation, affects dev effort | ✅ Covered |
| **ARCH-005** | What are the disaster recovery requirements? (RTO, RPO, multi-AZ, cross-region) | DR affects environment count, replication, backup costs | ✅ Covered |
| **ARCH-006** | What is the integration approach for the 9+ existing systems? (AWS API Gateway, point-to-point, ESB?) | Integration pattern drives API development effort | ✅ Covered |
| **ARCH-011** | Which AWS region is required? (eu-central-1 Frankfurt or eu-south-1 Milan for GDPR?) | Region affects service availability, latency, compliance | ✅ Covered |

#### B. AI/ML & Data Processing (4 questions)

| ID | Question | Why It Impacts Estimation | Lev Coverage |
|----|----------|---------------------------|--------------|
| **AI-001** | Which Amazon Bedrock models are acceptable? (Claude, Titan, Llama, Mistral?) | Model choice affects licensing, integration, compliance | ✅ Covered |
| **ENG-007** | What is the expected document processing volume per hour/day for each use case? | Processing volumes drive compute capacity and cost | ✅ Covered |
| **ENG-008** | What document formats and types must be supported? (PDF quality, scanned vs digital, handwritten?) | Poor quality documents = preprocessing effort | ✅ Covered |
| **NFR-003** | What are the accuracy requirements? (OCR accuracy %, extraction accuracy %, classification precision %) | Higher accuracy = more validation, QA effort, rework | ✅ Covered |

#### C. Integration & Systems (3 questions)

| ID | Question | Why It Impacts Estimation | Lev Coverage |
|----|----------|---------------------------|--------------|
| **INT-001** | What are the 9+ systems requiring integration? (system names, owners, current interfaces) | System count and complexity is largest timeline variable | ✅ Covered |
| **INT-002** | What are the integration protocols and authentication methods? (REST APIs, SOAP, file drops, OAuth, SAML?) | Protocol mismatch = custom adapter development | ✅ Covered |
| **INT-003** | What is the expected data exchange volume and frequency per system? (records/day, batch vs real-time) | Data volumes affect processing capacity and cost | ✅ Covered |

#### D. Compliance & Security (2 questions)

| ID | Question | Why It Impacts Estimation | Lev Coverage |
|----|----------|---------------------------|--------------|
| **COMP-001** | What specific compliance frameworks are required? (GDPR articles, EU AI Act risk level, DORA requirements, certifications) | Compliance scope affects documentation and audit effort | ✅ Covered |
| **COMP-002** | What are the data residency and cross-border processing constraints? (data must stay in Greece? EU-wide allowed?) | Residency constraints limit architecture options, affect cost | ✅ Covered |

#### E. Project Scope & Governance (5 questions) - **NOT COVERED BY LEV**

| ID | Question | Why It Impacts Estimation | Lev Coverage |
|----|----------|---------------------------|--------------|
| **SCOPE-001** | What is the scope of LOTs B2-B7? (undefined in RFP) | **CRITICAL** - Cannot estimate undefined work | 🔴 NOT COVERED |
| **SCOPE-002** | What is the proposal submission deadline? | Affects depth of analysis and proposal quality | 🔴 NOT COVERED |
| **SCOPE-003** | What is the budget range for this program (overall or per-LOT)? | Budget shapes solution scope and team size | 🔴 NOT COVERED |
| **SCOPE-004** | What commercial model is preferred? (Fixed-price, T&M, or hybrid?) | Fixed-price needs 60% buffer; T&M more flexible | 🔴 NOT COVERED |
| **SCOPE-005** | Will there be a formal Q&A window for RFP clarifications? | Affects when we'll get answers to inform proposal | 🔴 NOT COVERED |

#### F. Team & Responsibilities (5 questions) - **NOT COVERED BY LEV**

| ID | Question | Why It Impacts Estimation | Lev Coverage |
|----|----------|---------------------------|--------------|
| **RACI-001** | Who provides test data for each use case? (Vendor, Ethniki IT, Business Units) | If vendor must create test data = significant effort | 🔴 NOT COVERED |
| **RACI-002** | Who is accountable for UAT sign-off and go-live approval? | Approval delays affect timeline | 🔴 NOT COVERED |
| **RACI-005** | Is Ethniki responsible for integration with existing 9+ systems, or is this vendor scope? | **CRITICAL** - Integration ownership = huge effort difference | 🔴 NOT COVERED |
| **BA-001** | Will Ethniki assign a dedicated Business Analyst (BA) to each LOT? | No BA = 25-50% timeline increase (Step 12) | 🔴 NOT COVERED |
| **BA-002** | What is the BA's expected time commitment? (full-time, 50%, ad-hoc?) | Part-time BA = timeline delays, rework | 🔴 NOT COVERED |

**Total: 25 Pre-Sales Critical Questions**

---

## Part 4: Comparison Summary

### Coverage Analysis:

| Category | Lev Covered | Not Covered | Total | Coverage % |
|----------|-------------|-------------|-------|-----------|
| **Architecture & Infrastructure** | 6 | 0 | 6 | 100% ✅ |
| **AI/ML & Data Processing** | 4 | 0 | 4 | 100% ✅ |
| **Integration & Systems** | 3 | 0 | 3 | 100% ✅ |
| **Compliance & Security** | 2 | 0 | 2 | 100% ✅ |
| **Project Scope & Governance** | 0 | 5 | 5 | 0% 🔴 |
| **Team & Responsibilities** | 0 | 5 | 5 | 0% 🔴 |
| **TOTAL** | **15** | **10** | **25** | **60%** |

### Key Findings:

1. ✅ **Lev covered all technical questions** (architecture, AI/ML, integration, compliance)
2. 🔴 **Lev did NOT cover project/commercial questions** (scope, budget, RACI, BA, commercial model)
3. ⚠️ **Gap:** Project management and responsibility questions are critical for estimation but missing

### Why the Missing 10 Questions Matter:

| Missing Area | Estimation Impact | Example |
|-------------|------------------|---------|
| **LOT B2-B7 undefined** | Cannot price 70% of program | If LOT B2-B7 = 7 more use cases → 2-3x effort |
| **BA availability** | Timeline variance: 25-50% | No BA = 3-month project → 4.5-5 months |
| **Integration ownership** | Effort variance: 50-100% | If vendor does all integration → +4-6 months |
| **Commercial model** | Risk allocation | Fixed-price needs 60% buffer vs. T&M |
| **Budget range** | Solution scoping | €500K budget ≠ €2M budget approach |

---

## Part 5: Recommendations for Sai (Solution Architect)

### Immediate Actions (Next 2 Business Days):

1. ✅ **Send Lev's 15 covered questions** to client (architecture, AI, integration, compliance)
   - These are ready; Lev validated them
   - Frame with "Why this impacts our proposal" for each

2. 🔴 **Escalate 10 uncovered questions** to Lev for pre-sales review:
   - **CRITICAL:** LOT B2-B7 scope, BA availability, integration ownership, commercial model, budget
   - Ask Lev: "Should we include these in RFP Q&A, or handle differently?"

3. ⚠️ **Prepare alternative timeline proposal** (per Lev's guidance):
   - Use Claude's Step 12 analysis: CPCU2 (3mo → 6-7mo with buffer)
   - Document assumptions: "Based on current unknowns, realistic timeline is X"

### Follow-Up Actions (Within 1 Week):

4. **Create RACI workshop plan** for post-contract award (Week 1-2)
   - Cannot get RACI answers before RFP, but plan workshop

5. **Document T&M recommendation** in proposal:
   - Use Claude's commercial model analysis from Step 12
   - Justify: "Given undefined LOTs B2-B7, T&M reduces risk"

---

## Part 6: Question Mapping - Claude's 236 → Pre-Sales 25

### How We Filtered 236 → 25:

| Claude's Question Categories | Count | Pre-Sales Relevant | Filtered Count | Filtering Rationale |
|------------------------------|-------|-------------------|----------------|---------------------|
| **Capability-Based** | 50 | Partially | 10 | Kept estimation-impacting (architecture, AI, integration, team) |
| **SDLC-Based** | 48 | No | 0 | Deferred - delivery phase questions (UAT details, deployment procedures) |
| **Domain-Specific** | 92 | Partially | 5 | Kept high-level domain scope (document types, volumes); removed detailed workflows |
| **Step 12 (Timeline & PM)** | 46 | Yes | 10 | Kept all timeline, RACI, BA, commercial model questions |
| **TOTAL** | **236** | | **25** | **89% reduction** |

### Deferred Questions (211 questions - for delivery phase):

**Defer to Post-Award:**
- UAT details (duration, test cases, acceptance criteria)
- Deployment procedures (cutover, rollback, go-live windows)
- Support model (SLA levels, escalation, knowledge transfer)
- Detailed NFRs (UI requirements, response times, logging standards)
- Training scope (end-user training, admin training, materials)
- Change management (adoption strategy, communication plan)
- Domain-specific workflows (underwriting processes, claims handling)

**Rationale:** These questions are important for delivery but **do not change cost/duration/team** for the proposal.

---

## Part 7: Alignment with Lev's Guidance

### Lev's Key Statements Reflected:

| Lev's Guidance | How We Addressed |
|---------------|------------------|
| "Questions must impact cost, duration, team composition" | ✅ Filtered 236 → 25 estimation-critical only |
| "Defer delivery-only questions" | ✅ Deferred 211 SDLC/UAT/support questions |
| "EPAM will propose alternative timeline if unrealistic" | ✅ Use Claude's Step 12 timeline analysis (60% buffer) |
| "Don't ask about staffing geography" | ✅ Excluded hiring location questions |
| "Keep it pre-sales focused" | ✅ All 25 questions have "Why it impacts estimation" |

### What We Added (from Claude's Analysis):

| Addition | Source | Value |
|----------|--------|-------|
| **10 Project/PM questions** | Claude's Step 12 | BA, RACI, commercial model - critical for estimation |
| **60% timeline buffer analysis** | Claude's Step 12 | Justifies alternative timeline proposal |
| **AWS alignment** | Claude's AWS analysis | Confirms AWS-native approach reduces risk |
| **Capability match 82%** | Claude's capability analysis | Supports "we can deliver" confidence |

---

## Conclusion

**Lev's Coverage: 60% (15 of 25 critical questions)**

**What Lev Covered Well:**
- ✅ All technical questions (architecture, AI, integration, compliance)
- ✅ Guidance on pre-sales filtering approach
- ✅ Timeline challenge and alternative proposal direction

**What's Still Missing:**
- 🔴 Project scope questions (LOT B2-B7, budget, proposal deadline)
- 🔴 Responsibility questions (RACI, BA availability, integration ownership)
- 🔴 Commercial model (T&M vs Fixed-Price decision)

**Next Step for Sai:**
Review the 10 uncovered questions with Lev to determine if they should be included in client Q&A or handled differently.
