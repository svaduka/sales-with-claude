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
│   ├── input/               # Client-provided materials
│   │   ├── rfp.md          # RFP or requirements
│   │   ├── transcript.md   # Meeting transcripts
│   │   └── ...             # Any documents from client
│   └── output/             # Generated sales materials
│       ├── questions.md    # Discovery questions for missing info
│       ├── proposal.md     # Technical proposal
│       ├── presentation.md # Presentation materials
│       └── learnings/      # Learning materials for this project
│           ├── subject-1.md # e.g., kubernetes.md
│           ├── subject-2.md # e.g., azure-devops.md
│           └── ...          # One file per subject
└── project-name-2/
    └── ...
```

## Sales Project Workflow

### 1. Starting a New Sales Project

Create the project structure:
```bash
mkdir -p sales/project-name/{input,output}
```

### 2. Process Input Materials

**Input folder** contains everything received from the client:
- RFPs (Request for Proposal)
- SOWs (Statement of Work)
- Meeting transcripts
- Requirements documents
- Technical specifications
- Email threads or communications
- Any other client-provided materials

**Key workflow**:
1. Place all client materials in the `input/` folder
2. Read and analyze all input documents
3. Identify what information is present (full or partial)
4. Identify gaps and missing information

### 3. Generate Output Materials

**Output folder** contains all generated sales materials:

#### Always Start With Discovery Questions
When input materials have missing or incomplete information:
- Create `output/questions.md` with targeted questions
- Organize questions by category (technical, business, timeline, etc.)
- Reference which input document or section needs clarification
- Prioritize questions by importance to the proposal

#### Common Output Documents
- **questions.md**: Discovery questions for missing information
- **proposal.md**: Technical proposal or response to RFP
- **presentation.md**: Presentation outline or slide content
- **solution-design.md**: Technical architecture or solution design
- **pricing.md**: Pricing breakdown and justification
- **timeline.md**: Project timeline and milestones
- **risks-and-mitigations.md**: Risk analysis and mitigation strategies
- **executive-summary.md**: High-level summary for decision makers

### 4. Capture Learning Opportunities

**Critical**: When working on sales projects, identify topics that are new or need deeper understanding.

#### Creating Learning Materials

When a new topic is identified:
1. Create `output/learnings/` folder if it doesn't exist
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

### 5. Using Capabilities

**Critical**: Always read relevant capability files before generating output materials.

Match input requirements to capabilities:
- Cloud/infrastructure needs → `capabilities/architecture.md`
- Team building/technical leadership → `capabilities/lead_engineer.md`
- Customer engagement/sales strategy → `capabilities/sales_representation.md`
- Program delivery/governance → `capabilities/program_management.md`
- AI/ML projects → `capabilities/ai_and_innovation.md`

### 6. Handling Incomplete Information

When input materials are missing critical information:
1. **Don't make assumptions** - note what's missing
2. **Generate questions** - create targeted discovery questions in `output/questions.md`
3. **Create conditional proposals** - if necessary, provide options based on different scenarios
4. **Flag dependencies** - clearly state what information is needed to finalize materials

## Learning System Commands

### Show Learning Materials

When the user asks "show learning" or similar:

1. **Scan all learning folders**:
   ```bash
   find sales/*/output/learnings -name "*.md" -type f
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

   Project: acme-corp-cloud-migration
   - Kubernetes
     • Container orchestration fundamentals
     • Kubernetes networking
     • Helm charts and deployments
   - Terraform
     • Infrastructure as Code basics
     • AWS provider configuration

   Project: beta-inc-data-platform
   - Apache Spark
     • Spark architecture
     • PySpark fundamentals

   Which subject would you like to review?

   User: Kubernetes

   Claude: [Displays full kubernetes.md learning plan with all details]
   ```

## Standard Operating Procedure

When working on a sales project:

1. **Read inputs**: Review ALL files in the `input/` folder
2. **Read capabilities**: Review relevant capability files
3. **Identify gaps**: Determine what information is missing AND what skills are needed
4. **Generate questions**: If gaps exist, create `output/questions.md` first
5. **Create materials**: Generate other output documents based on available information
6. **Capture learnings**: Identify new topics and create/update learning materials in `output/learnings/`
7. **Cross-reference**: Ensure output materials align with documented capabilities
8. **Stay authentic**: Only propose solutions supported by capability files
9. **Avoid hallucination**: Never invent requirements, architecture, timelines, team structures, budgets, tools, or client context.
10. **Be clear**: Write responses in crisp, plain English with short and understandable wording.

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

**Sales Projects**: Each project is independent. Keep input materials unmodified (read-only). All generated work goes in the `output/` folder.

**Learning Materials**: Can be consolidated or reorganized periodically. Consider moving frequently referenced subjects to a global learning repository.

## Commands

### Standard Commands
No build or test commands. This is a documentation repository using markdown files organized in a structured folder hierarchy.

### Custom Commands
- **`/analyse-sales-input`**: Analyzes sales project inputs, identifies gaps, generates questions, and creates learning materials
  - Lists available projects
  - Analyzes project input materials
  - Maps capabilities to requirements
  - Generates clarification questions (capability-based, SDLC-based, domain-specific)
  - Identifies learning topics
  - Creates structured output files in `sales/<project>/output/`

- **`/analyse-sales-output`**: Reviews generated outputs, validates alignment with inputs, identifies gaps
  - Compares input requirements vs generated outputs
  - Validates alignment across business, technical, and SDLC dimensions
  - Generates clarification questions for internal discussions
  - Highlights missing or incomplete areas

- **`/git-sync`**: Git synchronization guide for working with Claude

### Learning Commands
- **Show all learning materials**: Ask "show learning" or "show learnings"
- **Find specific subject**: Ask "show learning for [subject]"
- **List by project**: Ask "show learnings for [project-name]"
