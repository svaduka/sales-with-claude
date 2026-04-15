# analyse-sales-output Command (Claude)

## Objective
This command enables Claude to perform a **three-way comparison** between:
1. **Input/**: Client-provided requirements (source of truth)
2. **claude-output/**: Claude's automated baseline analysis
3. **Output/**: Human team's manual analysis

The goal is to identify gaps, mismatches, and inconsistencies, then generate clarification questions for internal team discussions.

---

## Pre-Requisite Check

**CRITICAL**: Before proceeding, verify that `sales/<project>/claude-output/` exists and contains `.md` files.

- If `claude-output/` does NOT exist OR no `.md` files are present:
  - **STOP** and prompt user: "Claude baseline analysis not found. Please run `/analyse-sales-input` first to establish the baseline."
  - Cannot proceed without Claude's analysis as the comparison baseline
- If `.md` files exist:
  - Read and understand all available `.md` files first
  - Use these files as prior Claude analysis context before comparing with team-generated output

---

## Step 1: List Available Projects
- Scan directory: `sales/`
- Identify all project folders
- Prompt user to select a project

---

## Step 2: Three-Way Data Load

### 2.1 Load Client Requirements (Input/ - Source of Truth)
- Scan directory: `sales/<project>/Input/`
- Read all files: PDF, DOCX, XLSX, MD
- Extract: RFPs, requirements, technical specifications, assessments
- Document what client actually requested

### 2.2 Load Claude's Baseline Analysis (claude-output/)
- Scan directory: `sales/<project>/claude-output/`
- Read all existing `.md` files:
  - `project_analysis.md`
  - `capability_alignment.md`
  - `clarification_topics.md`
  - `all_questions.md`
  - `ANALYSIS_SUMMARY.md`
- Also read Excel files if present: `clarification_topics.xlsx`, `capability_questions.xlsx`, `sdlc_questions.xlsx`, `domain_questions.xlsx`
- Understand Claude's prior analysis, identified gaps, and generated questions

### 2.3 Load Human Team's Manual Analysis (Output/)
- Scan directory: `sales/<project>/Output/`
- Read all available files (proposals, analysis, designs, etc.)
- Document what human team has produced

### Output Summary
| Source | Location | File Count | Summary |
|--------|---------|-----------|---------|
| Client Input | Input/ | X files | RFP, specifications, requirements |
| Claude Baseline | claude-output/ | Y files | Automated analysis, questions, gaps |
| Human Analysis | Output/ | Z files | Manual proposals, designs |

---

## Step 3: Three-Way Comparison Analysis

### 3.1 Input vs Output (Client Requirements vs Human Analysis)
**Question**: Did the human team address what the client requested?

| Requirement Area | Input Status | Output Status | Gap/Match | Comments |
|-----------------|-------------|--------------|-----------|----------|
| Business Context | Defined in Input | Partial in Output | GAP | Missing X, Y, Z |
| Technical Scope | Defined in Input | Complete in Output | MATCH | Fully covered |
| Architecture | Required by Input | Missing in Output | GAP | Not addressed |
| Security | Required by Input | Partial in Output | GAP | Missing RBAC details |

### 3.2 claude-output vs Output (Claude's Analysis vs Human Analysis)
**Question**: Did the human team address what Claude identified?

| Analysis Area | Claude Identified | Human Included | Gap/Mismatch | Comments |
|--------------|------------------|----------------|--------------|----------|
| Capability Gaps | Listed 5 gaps | Addressed 2 gaps | GAP | Missing 3 gaps |
| Questions Generated | 45 questions | Answered 12 questions | GAP | 33 questions not addressed |
| Learning Topics | Identified 3 topics | Not mentioned | GAP | No learning plan in Output |
| Architecture Recommendations | Medallion pattern | Not specified | GAP | No architecture design |

### 3.3 Consistency Check (All Three Sources)
**Question**: Are there contradictions across the three sources?

| Topic | Input Says | Claude Says | Output Says | Issue Type |
|-------|-----------|-------------|-------------|-----------|
| Architecture | Cloud-native required | Medallion recommended | On-premise design | MISMATCH |
| Timeline | 6 months | Not specified by Claude | 3 months | INCONSISTENT |
| Security Model | RBAC/ABAC | Partial info in Input | Not addressed | GAP |

---

## Step 4: Gap Identification

Categorize all gaps with priority:

| Gap Category | Description | Impact | Priority | Reference |
|-------------|------------|--------|----------|-----------|
| Input → Output | Architecture design not in Output | High | High | Input Doc A (page 5), Output/ has no arch doc |
| claude-output → Output | 33 questions not addressed | Medium | High | Claude generated 45, Output addresses 12 |
| Input → Output | Security RBAC model missing | High | High | Input requires RBAC, Output doesn't mention |
| claude-output → Output | Learning topics not pursued | Low | Medium | Claude identified IDP, RAG, Insurance domain |

---

## Step 5: Mismatch Identification

Identify conflicting information:

| Mismatch Area | Input Requirement | Output Approach | Claude Recommendation | Clarification Needed |
|--------------|------------------|----------------|---------------------|---------------------|
| Architecture | Cloud-native | On-premise | Hybrid (Medallion) | Why diverge from Input requirement? |
| Data Model | Not specified in Input | Not specified in Output | Medallion (Bronze/Silver/Gold) | What data model is being used? |
| Timeline | 6 months | 3 months | Not specified | Is 3-month timeline realistic? |

---

## Step 6: Generate Clarification Questions

### 6.1 Input → Output Gap Questions
Questions about missing client requirements:

| Topic | Question | Reason | Priority |
|-------|----------|--------|----------|
| Architecture | Why is the cloud-native architecture requirement (from Input RFP page 5) not addressed in Output? | Required by client, missing in team's work | High |
| Security | Where is the RBAC/ABAC model defined as requested in Input Attachment 3? | Required by client, not found in Output | High |
| Business Context | Why are the business objectives from Input not referenced in Output proposal? | Client context missing | Medium |

### 6.2 claude-output → Output Gap Questions
Questions about Claude's identified gaps not addressed by human team:

| Topic | Question | Reason | Priority |
|-------|----------|--------|----------|
| Clarification Questions | Why were 33 out of 45 questions identified by Claude not answered in Output? | Many open questions remain | High |
| Capability Gaps | Why were the 3 capability gaps identified by Claude not addressed in Output? | Skill gaps not acknowledged | Medium |
| Learning Topics | Are the learning topics (IDP, RAG, Insurance Domain) being pursued? | Claude identified skill gaps | Low |
| Architecture | Why isn't the Medallion architecture pattern (recommended by Claude) mentioned in Output? | No architecture design present | High |

### 6.3 Mismatch Questions
Questions about conflicting information across sources:

| Topic | Question | Reason | Priority |
|-------|----------|--------|----------|
| Architecture Approach | Why does Output propose on-premise when Input requires cloud-native? | Direct contradiction with client requirement | High |
| Timeline | Is the 3-month timeline in Output realistic given Input's 6-month scope? | Inconsistent estimates, risk of under-delivery | High |
| Scope | Why does Output include features X, Y not requested in Input? | Potential scope creep | Medium |

---

## Step 7: Capability-Based Validation

Validate Output using documented capabilities:

| Capability Area | Expected Coverage (per capabilities/) | Output Status | Gap? | Question |
|----------------|--------------------------------------|--------------|------|----------|
| Data Engineering | High | Partial | YES | What data ingestion approach is used in Output? |
| Architecture | High | Missing | YES | Why is architecture design not included in Output? |
| Program Management | Medium | Not addressed | YES | Where is project governance defined in Output? |
| AI & Innovation | High | Partial | YES | How are AI/ML components addressed in Output? |

---

## Step 8: SDLC Lifecycle Validation

Check Output completeness across SDLC phases:

| SDLC Phase | Input Requirement | Claude Analysis | Output Status | Gap? | Question |
|------------|------------------|----------------|--------------|------|----------|
| Requirements | Complete | Analyzed by Claude | Partial in Output | YES | Are all requirements from Input documented in Output? |
| Design | Architecture required | Gaps identified by Claude | Missing in Output | YES | Where is the architecture design in Output? |
| Development | Standards needed | Not specified in Input | Not addressed in Output | YES | What development standards apply? |
| Testing | Strategy required | Not found by Claude in Input | Not addressed in Output | YES | What is the testing strategy? |
| Deployment | CI/CD expected | Not specified in Input | Not addressed in Output | YES | Is CI/CD approach defined? |

---

## Step 9: Domain-Specific Validation

For the identified domain (e.g., Data Ingestion, IDP, Insurance), validate completeness:

| Domain Area | Input Requirement | Claude Identified | Output Coverage | Gap? | Question |
|------------|------------------|------------------|----------------|------|----------|
| IDP (Intelligent Document Processing) | Required by Input | Analyzed by Claude, learning topic created | Not specified in Output | YES | How is IDP implemented in Output proposal? |
| Data Ingestion | Batch + Streaming | Gaps found by Claude | Not specified in Output | YES | What ingestion patterns are used? |
| Security | RBAC/ABAC | Partial in Input, questions by Claude | Not addressed in Output | YES | What access control model is implemented? |
| Architecture | Medallion suggested by Claude | Recommended | Not mentioned in Output | YES | Is medallion architecture used? |

---

## Step 10: Update claude-output Files

**CRITICAL**: Update existing files in `claude-output/`, do NOT create duplicates.

### Files to Update:

1. **clarification_topics.md**
   - Add new section: `## Output Comparison Results (YYYY-MM-DD)`
   - Document gaps and mismatches found
   - Reference specific Input, claude-output, and Output files
   - Include three-way comparison tables

2. **all_questions.md**
   - Append new section: `## Questions from Output Analysis (YYYY-MM-DD)`
   - Add Input→Output gap questions
   - Add claude-output→Output gap questions
   - Add mismatch questions
   - Organize by priority (High/Medium/Low)

3. **capability_alignment.md**
   - Add section: `## Capability Validation Against Output (YYYY-MM-DD)`
   - Document capability gaps found in Output
   - Reference Output/ files that should have covered these capabilities

4. **ANALYSIS_SUMMARY.md**
   - Update with comparison summary
   - Highlight critical gaps and mismatches
   - Add executive summary of three-way comparison

5. **Excel Files** (update existing, don't create new):
   - `clarification_topics.xlsx`: Add new rows for Output gaps
   - `capability_questions.xlsx`: Add capability validation questions
   - `sdlc_questions.xlsx`: Add SDLC gap questions
   - `domain_questions.xlsx`: Add domain-specific validation questions

### Update Format Example:
```markdown
## Output Comparison Results (2026-04-14)

### Three-Way Comparison Summary

**Sources Analyzed:**
- **Input/** (Client Requirements): 8 files - RFP, technical specs, vendor questionnaire
- **claude-output/** (Claude Baseline): 5 MD files, 4 Excel files - prior analysis complete
- **Output/** (Human Team): 3 files - proposal.md, solution-design.md, pricing.md

### Key Findings

#### Gaps Identified
| Gap Type | Count | Priority Distribution |
|----------|-------|---------------------|
| Input → Output | 12 gaps | High: 5, Medium: 4, Low: 3 |
| claude-output → Output | 8 gaps | High: 3, Medium: 3, Low: 2 |

#### Mismatches Identified
| Mismatch Area | Severity | Description |
|--------------|---------|-------------|
| Architecture | High | Output proposes on-premise, Input requires cloud-native |
| Timeline | High | Output: 3 months, Input: 6 months |

### Detailed Gap Analysis
[Tables from Step 4]

### Detailed Mismatch Analysis
[Tables from Step 5]

### Clarification Questions
[Tables from Step 6]

### Recommendations
1. Review Input requirements for architecture (page 5) and align Output
2. Address 33 outstanding questions identified by Claude
3. Include architecture design document in Output
4. Clarify timeline discrepancy with stakeholders
```

---

## Step 11: Execution Rules

- **MANDATORY: Reference sources precisely**: EVERY gap, mismatch, and finding MUST cite:
  - **Input source**: Document name, page number, section (e.g., "Technical Description.pdf, Page 12, Section 3.2")
  - **Output source**: File name, section, line numbers (e.g., "proposal.md, Section 2.1, lines 45-52")
  - **claude-output source**: File name, section (e.g., "project_analysis.md, Architecture section")
- **Do not assume or invent missing information** - document only what's actually present in the three sources
- **Clearly distinguish**:
  - **Gaps**: Information present in Input or claude-output but missing from Output (cite sources for both)
  - **Mismatches**: Contradictions between Input, claude-output, and Output (cite all three sources)
  - **Inconsistencies**: Conflicting statements or assumptions within or across sources (cite conflicting sources)
- **Keep answers crisp, clear, and in plain English**
- **Always update existing files** in claude-output/, never create new versions (e.g., no `clarification_topics_v2.md`)
- **Generate actionable questions**: Questions should be specific, answerable, include source references, and context (why the question matters)
- **Preserve prior analysis**: Don't delete or overwrite prior work in claude-output/, append new findings
- **Use comparison context**: Always frame questions with reference to the three-way comparison WITH source citations
- **Prioritize findings**: Mark gaps and mismatches as High/Medium/Low priority based on impact

---

## Notes

- Ignore irrelevant or advertisement content
- Focus on meaningful technical and business alignment
- Highlight only real gaps and mismatches, not assumptions
- Treat all folder names as case-insensitive (Input/input, Output/output, claude-output/Claude-Output)
- If Output/ folder doesn't exist or is empty, document this clearly: "No human team analysis found in Output/"
- **Three-way comparison is the core value**:
  - Input (what client needs)
  - claude-output (what Claude found and recommended)
  - Output (what human team produced)
- The goal is to help the team see what they might have missed from either the client requirements or Claude's analysis
