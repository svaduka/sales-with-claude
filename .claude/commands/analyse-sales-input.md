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
`sales/<project>/output/`

### Files to Generate
- `project_analysis.md`
- `clarification_topics.xlsx`
- `capability_questions.xlsx`
- `sdlc_questions.xlsx`
- `domain_questions.xlsx`
- `learning_plan.md`

---

## Step 10: Execution Rules
- Always follow step-by-step execution
- Do not skip steps
- Ask user for project selection before proceeding
- Ensure all outputs are structured and complete

---

## Notes
- Ignore irrelevant or advertisement content
- Focus only on meaningful technical and business information
- Maintain formal and structured output format
- Treat all folder names, file names, and references (input/output) as case-insensitive