# analyse-sales-input Command (Claude)

## Objective
This command enables Claude to analyze available sales projects, guide the user in selecting a project, perform structured analysis, identify gaps, generate questions, and produce learning outputs.

---

## Step 1: List Available Projects
- Scan directory: `sales/`
- Identify all project folders
- Output a list of available projects

### Output Format
| Project Name | Description (if available) |
|--------------|---------------------------|
| project_1    | ...                       |
| project_2    | ...                       |

---

## Step 2: Project Input Analysis
- Once user selects a project, scan:
  - `sales/<project>/input/`
- Analyze:
  - Documents
  - Architecture files
  - Data models
  - Requirements

### Pre-Analysis Requirement
- During analysis, before reading the input, make sure all the `.md` files in `sales/<project>/claude-output/` are read, if already exist
- Use this as prior context to avoid duplicate work and to understand previous analysis
- Do not assume completeness; validate against input again

### Output
Provide structured analysis:
| Category | Details |
|----------|--------|
| Business Context | |
| Technical Scope | |
| Data Scope | |
| Architecture | |
| Dependencies | |

---

## Step 3: Capability Alignment
- Load user capabilities
- Map project requirements with capabilities

### Output
| Capability Area | Relevance | Observations |
|----------------|----------|--------------|
| Data Engineering | High | |
| Architecture | High | |
| Trading Systems | Medium | |

---

## Step 4: Clarification Topics Generation
- Identify missing or unclear areas
- Generate clarification topics

### Output
| Topic | Missing Information | Reference Needed |
|------|--------------------|------------------|
| Data Source | Not defined | Source systems |
| Security | Partial | RBAC/ABAC details |

---

## Step 5: Capability-Based Questions
- Generate questions aligned with user capabilities

### Output (Excel-style)
| Capability | Question |
|-----------|---------|
| Data Architecture | What is the target architecture pattern? |
| ETL | What ingestion framework is used? |

---

## Step 6: SDLC-Based Questions
- Generate SDLC lifecycle questions

### Output
| SDLC Phase | Question |
|------------|---------|
| Requirement | Are requirements finalized? |
| Design | Is architecture approved? |
| Development | Coding standards defined? |
| Testing | Test strategy available? |
| Deployment | CI/CD defined? |

---

## Step 7: Domain-Specific Questions (Example: Data Ingestion)
- Identify domain of project
- Generate domain-specific validation questions

### Output
| Area | Question |
|------|---------|
| Data Ingestion | What are source systems? |
| Data Ingestion | Batch or streaming? |
| Security | Access controls defined? |
| Architecture | Is medallion architecture used? |

---

## Step 8: Learning Identification
- Identify learning topics from project

### Output
| Topic | Description | Priority |
|------|-------------|----------|
| Delta Lake | Required for ingestion | High |
| Streaming | If applicable | Medium |

---

## Step 9: Output File Generation
All outputs must be saved under:
`sales/<project>/claude-output/`

### Files to Generate
- `project_analysis.md`
- `clarification_topics.xlsx`
- `capability_questions.xlsx`
- `sdlc_questions.xlsx`
- `domain_questions.xlsx`
- `learning_plan.md`

---

## Step 10: File Update Strategy

**CRITICAL**: Update existing files, do NOT create duplicates.

- If `claude-output/` already has analysis files from a prior run:
  - Read existing files first for context
  - Update existing files by appending new findings or merging new information
  - Do not create `project_analysis_v2.md` or similar - update the original file
  - Add dated sections (e.g., `## Updated Analysis (2026-04-14)`) when appending
- If this is the first analysis:
  - Create all files as specified
- Preserve prior analysis context to avoid redundant work

---

## Step 11: Execution Rules
- Always follow step-by-step execution
- Do not skip steps
- Ask user for project selection before proceeding
- Ensure all outputs are structured and complete
- Never modify files in `Input/` folder (read-only)
- Only write to `claude-output/` folder
- Update existing `claude-output/` files rather than creating duplicates

---

---

## Step 12: Timeline Considerations for Sales Input Documents
- Verify if the proposed input has timeline information
- Verify if the proposed timeline is feasible with 360 degree view of the project
- For the timeline, ask all relevant questions and compile the output, including all associated activities
- Maintain a 60% buffer for any fixed-scope projects if it is specified in the sales document
- Ensure that the approach is Time and Materials (T&M) based
- During the analysis phase, ask for the RACI matrix for clarification
- Ask questions about the availability and experience of the Business Analyst (BA)
- Request clarification on requirements definition for both functional and non-functional requirements

---

## Notes
- Ignore irrelevant or advertisement content
- Focus only on meaningful technical and business information
- Maintain formal and structured output format
- Treat all folder names, file names, and references (Input/input, claude-output/Claude-Output) as case-insensitive
- `Input/` and `Output/` are read-only for Claude
- `claude-output/` is the only folder Claude writes to