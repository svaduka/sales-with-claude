# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository supports sales activities by combining documented technical capabilities with project-specific sales materials. The `capabilities/` directory contains the owner's technical expertise, which informs how to approach each sales opportunity in the `sales/` directory. A learning system captures knowledge gaps identified during sales for continuous skill development.

## Response Style and Accuracy Rules

Claude must follow these rules for every sales-project interaction:

- Do not hallucinate, invent, or assume facts that are not present in the input materials, capability files, or explicitly provided by the user.
- If information is missing, incomplete, or unclear, explicitly state that it is missing and add it to the clarification questions.
- Keep answers crisp, clear, and direct.
- Use plain English that is easy for the user to understand.
- Avoid unnecessary jargon, long explanations, or vague wording.
- Separate confirmed facts, assumptions, and open questions whenever needed.
- Prefer short structured outputs over lengthy narrative output.
- When confidence is low, say so clearly instead of guessing.

## Repository Structure

```
capabilities/
├── architecture.md          # Architecture expertise and experience
├── lead_engineer.md         # Lead engineering capabilities
├── sales_representation.md  # Sales and customer-facing skills
├── program_management.md    # Program/project management experience
└── ai_and_innovation.md     # AI and innovation expertise

sales/
├── project-name-1/
│   ├── Input/               # Client-provided materials (READ-ONLY)
│   │   ├── *.pdf            # RFP, requirements (PDF format)
│   │   ├── *.docx           # Technical documents (Word format)
│   │   ├── *.xlsx           # Assessment questionnaires, financial proposals (Excel)
│   │   └── *.md             # Markdown documents
│   ├── Output/              # Human team's manual analysis (READ for comparison)
│   │   ├── proposal.md      # Manual proposal drafts
│   │   ├── solution-design.md
│   │   └── ...              # Any manually created sales materials
│   └── claude-output/       # Claude's automated analysis (WRITE/UPDATE)
│       ├── project_analysis.md          # Structured project analysis
│       ├── capability_alignment.md      # Capability-to-requirement mapping
│       ├── clarification_topics.md      # Identified gaps and missing info
│       ├── all_questions.md            # Combined questions list
│       ├── ANALYSIS_SUMMARY.md         # Executive summary
│       ├── clarification_topics.xlsx   # Questions organized by topic
│       ├── capability_questions.xlsx   # Capability-based questions
│       ├── sdlc_questions.xlsx         # SDLC lifecycle questions
│       ├── domain_questions.xlsx       # Domain-specific questions
│       └── learnings/                  # Learning materials
│           ├── subject-1.md            # e.g., kubernetes.md
│           ├── subject-2.md            # e.g., rag-systems.md
│           └── ...                     # One file per subject
└── project-name-2/
    └── ...
```

**Important Notes**:
- Folder names are case-insensitive (Input/input, Output/output treated the same)
- Input materials can be PDF, DOCX, XLSX, or markdown files
- **Input/**: Client materials - never modify, read-only
- **Output/**: Human team's manual work - read for comparison only
- **claude-output/**: Claude's analysis - create and update files here

## Python Requirements

For document analysis, install these packages:

```bash
pip install pypdf python-docx openpyxl pandas
```

These enable reading PDF, Word, and Excel files during sales analysis.

- **pypdf**: Read PDF files
- **python-docx**: Read Word documents (.docx)
- **openpyxl**: Read Excel files (.xlsx)
- **pandas**: Data manipulation for Excel files

## File Format Handling

The repository handles multiple file formats for input materials:

### Reading Input Files

When analyzing input materials, Claude can read:
- **PDF files (.pdf)**: Using `pypdf` library
- **Word documents (.docx)**: Using `python-docx` library
- **Excel files (.xlsx)**: Using `openpyxl` and `pandas` libraries
- **Markdown files (.md)**: Direct text reading

### Generating Output Files

Claude generates outputs in two formats:
- **Markdown (.md)**: For analysis, summaries, and learning materials
- **Excel (.xlsx)**: For structured questions and tabular data

Excel format is preferred for questions because it:
- Allows easy filtering and sorting
- Can be shared with stakeholders directly
- Supports structured data with multiple columns
- Enables collaborative review and response tracking

## Sales Project Workflow

### 1. Starting a New Sales Project

Create the project structure:
```bash
mkdir -p "sales/project-name/Input"
mkdir -p "sales/project-name/Output"
mkdir -p "sales/project-name/claude-output"
```

**Folder purposes**:
- **Input/**: Store all client-provided materials (read-only)
- **Output/**: Store human team's manual analysis and proposals
- **claude-output/**: Store Claude's automated analysis (managed by commands)

### 2. Process Input Materials (Client-Provided)

**Input/ folder** contains everything received from the client:
- RFPs (Request for Proposal) - PDF, Word, or markdown
- SOWs (Statement of Work)
- Meeting transcripts
- Requirements documents
- Technical specifications - Excel, Word, or PDF
- Assessment questionnaires - Excel
- Financial proposal templates - Excel, Word, or PDF
- Email threads or communications
- Any other client-provided materials

**Supported file formats**: PDF (.pdf), Word (.docx), Excel (.xlsx), Markdown (.md)

**Key principles**:
1. Place all client materials in the `Input/` folder
2. **Never modify Input/ files** - they are the source of truth
3. Use `/analyse-sales-input` command to analyze these materials
4. Claude reads Input/ files using Python libraries for document processing

### 3. Human Team Analysis (Output/ folder)

**Output/ folder** contains manual analysis by human team members:
- Manually drafted proposals
- Solution designs created by the team
- Pricing analyses
- Custom presentations
- Any sales materials created by humans (not Claude)

**Key principles**:
1. Human team members create files in Output/ independently
2. Claude **reads** Output/ for comparison but **does not write** to it
3. Output/ serves as the "human baseline" for validation

### 4. Claude's Automated Analysis (claude-output/ folder)

**claude-output/ folder** contains Claude's automated analysis:

#### Command-Generated Files

**Markdown files**:
- `project_analysis.md`: Structured analysis of business context, technical scope, data scope, architecture, dependencies
- `capability_alignment.md`: Mapping of project requirements to documented capabilities
- `clarification_topics.md`: Missing or unclear areas identified
- `all_questions.md`: Combined list of all generated questions
- `ANALYSIS_SUMMARY.md`: Executive summary of the analysis

**Excel files (.xlsx)**:
- `clarification_topics.xlsx`: Gaps organized by topic
- `capability_questions.xlsx`: Questions aligned with capability areas
- `sdlc_questions.xlsx`: Questions organized by SDLC phase (Requirements, Design, Development, Testing, Deployment)
- `domain_questions.xlsx`: Domain-specific validation questions (e.g., data ingestion, security)

**Learning materials**:
- `learnings/`: Directory containing subject-specific learning plans
- One markdown file per subject (e.g., `kubernetes.md`, `rag-systems.md`, `insurance-domain.md`)

#### File Update Strategy
- Claude **updates existing files** instead of creating duplicates
- When new information is found, append or merge into existing files
- Preserve prior analysis context to avoid redundant work

### 5. Capture Learning Opportunities

**Critical**: When working on sales projects, identify topics that are new or need deeper understanding.

#### Creating Learning Materials

When a new topic is identified:
1. Create `claude-output/learnings/` folder if it doesn't exist
2. Create or update a subject-level markdown file (e.g., `kubernetes.md`, `terraform.md`)
3. Use descriptive, specific filenames (e.g., `azure-databricks.md` not `databricks.md`)

#### Learning File Structure

Each subject file should contain:

```markdown
# [Subject Name]

## Overview
Brief description of the subject and why it's relevant

## Topics

### Topic 1: [Specific Topic]
**Why Learn**: Context from the sales opportunity
**Learning Objectives**:
- Objective 1
- Objective 2
- Objective 3

**Resources**:
- [Resource 1]
- [Resource 2]

**Practice/Labs**:
- Hands-on exercise 1
- Hands-on exercise 2

**Time Estimate**: X hours

**Priority**: High/Medium/Low

---

### Topic 2: [Another Topic]
...
```

#### When to Create Learning Materials

Create or update learning materials when:
- Client requires technology or methodology not in current capabilities
- Deeper knowledge needed to be competitive in the opportunity
- New patterns, tools, or frameworks are mentioned in input materials
- Questions reveal knowledge gaps that impact proposal quality
- Competitive intelligence shows skill gaps

### 6. Using Capabilities

**Critical**: Always read relevant capability files before generating analysis.

Match input requirements to capabilities:
- Cloud/infrastructure needs → `capabilities/architecture.md`
- Team building/technical leadership → `capabilities/lead_engineer.md`
- Customer engagement/sales strategy → `capabilities/sales_representation.md`
- Program delivery/governance → `capabilities/program_management.md`
- AI/ML projects → `capabilities/ai_and_innovation.md`

The capability alignment is documented in `claude-output/capability_alignment.md` and capability-based questions are generated in `claude-output/capability_questions.xlsx`.

### 7. Handling Incomplete Information

When input materials are missing critical information:
1. **Don't make assumptions** - note what's missing
2. **Generate questions** - create targeted discovery questions across multiple dimensions:
   - Capability-based questions (aligned with documented expertise)
   - SDLC-based questions (Requirements, Design, Development, Testing, Deployment)
   - Domain-specific questions (e.g., data ingestion, security, architecture patterns)
3. **Document gaps** - clearly identify missing information in `clarification_topics.md`
4. **Flag dependencies** - clearly state what information is needed to finalize proposals

All questions are generated in both markdown and Excel formats for easy sharing and tracking.

## Learning System Commands

### Show Learning Materials

When the user asks "show learning" or similar:

1. **Scan all learning folders**:
   ```bash
   find sales/*/claude-output/learnings -name "*.md" -type f
   ```

2. **Display subjects and topics**:
   - List all subject files found across all projects
   - For each subject, show the topics contained within
   - Format as: `[Project Name] → [Subject] → [List of Topics]`

3. **User selects subject**:
   - Wait for user to choose a specific subject
   - Display the full learning plan for that subject
   - Show all topics with objectives, resources, and time estimates

4. **Interactive workflow**:
   ```
   User: show learning

   Claude: Found learning materials:

   Project: ethniki-insurance-rfp
   - Intelligent Document Processing
     • OCR and document extraction techniques
     • Classification and data validation
     • Integration patterns with business systems
   - Retrieval Augmented Generation (RAG)
     • Vector databases and embeddings
     • Retrieval strategies
     • LLM integration patterns
   - Insurance Domain Knowledge
     • Policy lifecycle and underwriting
     • Claims processing workflows
     • Regulatory compliance requirements

   Project: acme-corp-cloud-migration
   - Kubernetes
     • Container orchestration fundamentals
     • Kubernetes networking

   Which subject would you like to review?

   User: Intelligent Document Processing

   Claude: [Displays full intelligent-document-processing.md learning plan with all details]
   ```

## Standard Operating Procedure

### When Running `/analyse-sales-input`:

1. **Read inputs**: Review ALL files in the `Input/` folder (PDF, DOCX, XLSX, MD)
2. **Check prior work**: Read existing files in `claude-output/` if they exist (for context)
3. **Read capabilities**: Review relevant capability files from `capabilities/`
4. **Analyze and structure**: Extract business context, technical scope, data scope, architecture, dependencies
5. **Map capabilities**: Align project requirements with documented expertise
6. **Identify gaps**: Determine what information is missing from Input materials
7. **Generate questions**: Create structured questions (capability-based, SDLC-based, domain-specific)
8. **Capture learnings**: Identify new topics and create/update learning materials in `claude-output/learnings/`
9. **Create/update files**: Write to `claude-output/` folder (markdown and Excel formats)
10. **Update, don't duplicate**: If files exist, update them rather than creating new versions

### When Running `/analyse-sales-output`:

1. **Pre-check**: Verify `claude-output/` exists; if not, prompt to run `/analyse-sales-input` first
2. **Load three sources**:
   - `Input/`: Client-provided requirements (source of truth)
   - `claude-output/`: Claude's baseline analysis
   - `Output/`: Human team's manual analysis
3. **Three-way comparison**: Identify gaps and mismatches across all three sources
4. **Gap analysis**: Document what's missing in Output/ compared to Input/ and claude-output/
5. **Mismatch analysis**: Document contradictions or unexplained divergences
6. **Generate questions**: Create clarification questions for internal team discussions
7. **Update claude-output/**: Append findings to existing files (don't create duplicates)
8. **Clear documentation**: Mark gaps vs mismatches, with priority levels and references

### General Principles (All Commands):

1. **Cross-reference**: Ensure analysis aligns with documented capabilities
2. **Stay authentic**: Only propose solutions supported by capability files
3. **Avoid hallucination**: Never invent requirements, architecture, timelines, team structures, budgets, tools, or client context
4. **Be clear**: Write responses in crisp, plain English with short and understandable wording
5. **Preserve sources**: Never modify `Input/` or `Output/` folders
6. **Update intelligently**: Always update existing `claude-output/` files rather than creating duplicates
7. **Context awareness**: Use prior `claude-output/` analysis to inform current work

## Capability Files Reference

- **architecture.md**: System design, cloud platforms, scalability, technical architecture
- **lead_engineer.md**: Technical leadership, engineering practices, team development
- **sales_representation.md**: Sales methodology, customer engagement, technical sales
- **program_management.md**: Delivery planning, stakeholder management, program governance
- **ai_and_innovation.md**: AI/ML expertise, innovation initiatives, emerging technologies

## Expertise Summary

*This section updates as capability files are populated*

As capability files are filled in, this section will summarize:
- Core technical strengths and depth areas
- Preferred technologies and methodologies
- Key achievements and experience highlights
- Differentiating expertise for competitive positioning

## Guidelines for Output Generation

### Accuracy and Writing Style
- Only include information that is supported by the input documents, capability files, or direct user instructions
- Clearly mark missing, assumed, or pending information
- Use plain English and keep wording easy to understand
- Keep answers concise unless the user asks for more detail
- Avoid buzzwords, filler, and overcomplicated technical language

### Discovery Questions (questions.md)
- Organize by category (technical, business, timeline, budget, stakeholders)
- Reference specific gaps from input materials
- Prioritize by impact on proposal
- Include context for why each question matters
- Make questions open-ended to encourage detailed responses

### Proposals and Technical Documents
- Lead with strengths from capability files
- Address all requirements found in input materials
- Clearly mark assumptions or areas pending clarification
- Never fabricate client details or technical specifics to make the proposal look complete
- Provide specific examples from documented experience
- Include measurable outcomes and success criteria

### Presentations and Summaries
- Tailor technical depth to audience
- Highlight relevant expertise from capabilities
- Focus on client's problem and proposed solution
- Keep language simple, crisp, and easy to follow
- Include clear next steps and calls to action

### Learning Materials (learnings/*.md)
- One subject per file, descriptive filename
- Organize into specific, actionable topics
- Include learning objectives, resources, and time estimates
- Add priority levels (High/Medium/Low) based on opportunity impact
- Reference the sales context that triggered the learning need
- Keep materials detailed enough to create a concrete learning path
- Update existing files rather than creating duplicates

## Maintenance

**Capability Files**: When modified, update the "Expertise Summary" section in this CLAUDE.md.

**Sales Projects**: Each project is independent with three folders:
- `Input/`: Client materials - **read-only**, never modify
- `Output/`: Human team's work - **read-only** for Claude, used for comparison
- `claude-output/`: Claude's analysis - **read-write**, update existing files rather than creating duplicates

**Learning Materials**: Can be consolidated or reorganized periodically. Consider moving frequently referenced subjects to a global learning repository.

**File Update Policy**: When running commands multiple times on the same project:
- Always read existing `claude-output/` files first
- Update existing files by appending new findings or merging new information
- Do not create duplicate files (e.g., `project_analysis_v2.md`)
- Preserve prior analysis context to avoid redundant work

## Commands

### Standard Commands
No build or test commands. This is a documentation repository using markdown files organized in a structured folder hierarchy.

### Custom Commands

#### `/analyse-sales-input`
**Purpose**: Comprehensive analysis of client-provided input materials

**Workflow**:
1. Lists available projects in `sales/` directory
2. Prompts user to select a project
3. Reads all files in `sales/<project>/Input/` folder (PDF, DOCX, XLSX, MD)
4. Checks if `sales/<project>/claude-output/` exists and reads prior analysis for context
5. Analyzes input materials:
   - Business context, technical scope, data scope, architecture, dependencies
6. Loads relevant capability files from `capabilities/`
7. Maps project requirements to capabilities
8. Identifies gaps and missing information
9. Generates clarification questions across multiple dimensions:
   - **Capability-based questions**: Aligned with documented expertise areas
   - **SDLC-based questions**: Organized by Requirements, Design, Development, Testing, Deployment phases
   - **Domain-specific questions**: E.g., data ingestion patterns, security models, architecture choices
10. Identifies learning topics where expertise needs development
11. Creates/updates structured output files in `sales/<project>/claude-output/`:
    - Markdown files: `project_analysis.md`, `capability_alignment.md`, `clarification_topics.md`, `all_questions.md`, `ANALYSIS_SUMMARY.md`
    - Excel files: `clarification_topics.xlsx`, `capability_questions.xlsx`, `sdlc_questions.xlsx`, `domain_questions.xlsx`
    - Learning files: `learnings/<subject>.md`

**Output Location**: `sales/<project>/claude-output/`

**Key Principles**:
- Never modify files in `Input/` folder
- Update existing files in `claude-output/` rather than creating duplicates
- Use prior `claude-output/` analysis as context to avoid redundant work

---

#### `/analyse-sales-output`
**Purpose**: Three-way comparison between client requirements (Input), human team's analysis (Output), and Claude's analysis (claude-output) to identify gaps and mismatches

**Workflow**:
1. Lists available projects in `sales/` directory
2. Prompts user to select a project
3. **Pre-requisite check**: If `sales/<project>/claude-output/` doesn't exist:
   - Prompt user to run `/analyse-sales-input` first
   - Cannot proceed without Claude's baseline analysis
4. **Three-way data load**:
   - Read `sales/<project>/Input/` - Original client requirements (source of truth)
   - Read `sales/<project>/claude-output/` - Claude's automated analysis (baseline)
   - Read `sales/<project>/Output/` - Human team's manual analysis (comparison target)
5. **Three-way comparison**:
   - **Input vs Output**: What client requirements are missing or incomplete in human team's work?
   - **claude-output vs Output**: What did Claude identify that human team missed?
   - **Consistency check**: Are there contradictions between Input, claude-output, and Output?
6. **Gap identification**:
   - Missing business context in Output
   - Incomplete technical coverage in Output
   - SDLC phase gaps (Requirements, Design, Development, Testing, Deployment)
   - Domain-specific gaps (architecture, security, data patterns)
7. **Mismatch identification**:
   - Areas where Output contradicts Input requirements
   - Areas where Output diverges from Claude's analysis without justification
   - Inconsistent assumptions or interpretations
8. **Generate clarification questions**:
   - Questions about missing information (Input → Output gaps)
   - Questions about divergent approaches (claude-output → Output differences)
   - Questions about unexplained choices or assumptions
9. **Update files in `claude-output/`**:
   - Update existing markdown files (don't create new versions)
   - Update existing Excel files with new comparison questions
   - Add new section "Output Comparison Results" to relevant files
   - Append findings without duplicating prior analysis

**Output Location**: `sales/<project>/claude-output/` (updates existing files)

**Key Principles**:
- Never modify `Input/` or `Output/` folders - read-only
- Always update existing `claude-output/` files rather than creating duplicates
- Clearly distinguish between:
  - Missing information (gaps)
  - Conflicting information (mismatches)
  - Assumptions that need validation
- Focus on actionable clarification questions for internal team discussions
- Document comparison results for stakeholder visibility

**Comparison Output Format**:
- Markdown tables showing Input vs claude-output vs Output
- Gap analysis with priority levels (High/Medium/Low)
- Mismatch details with references to specific documents
- Clarification questions organized by topic area

---

#### `/git-sync`
**Purpose**: Git synchronization guide for working with Claude

### Learning Commands
- **Show all learning materials**: Ask "show learning" or "show learnings"
  - Scans all `sales/*/claude-output/learnings/` folders
  - Lists subjects across all projects
  - Allows selection of specific subject for detailed view
- **Find specific subject**: Ask "show learning for [subject]"
  - Directly displays learning plan for specified subject
- **List by project**: Ask "show learnings for [project-name]"
  - Shows all learning materials for a specific project
