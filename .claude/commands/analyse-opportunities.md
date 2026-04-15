

# analyse-opportunities Command (Claude)

## Objective
This command helps Claude analyze work opportunities provided to the user.

Claude must:
- look into the `opportunities/` folder
- list the available opportunities
- ask the user which opportunity to analyze
- analyze the selected opportunity against the user's capabilities
- create a `claude-output/` folder under the selected opportunity
- generate output that shows which capabilities are a full match, partial match, and which areas require learning

---

## Step 1: List Available Opportunities
- Scan the `opportunities/` folder
- Identify all available opportunity folders
- Present the list to the user
- Ask: which opportunity should be analyzed

### Output Format
| Opportunity Name | Description (if available) |
|---|---|
| opportunity_1 | ... |
| opportunity_2 | ... |

---

## Step 2: Load the Selected Opportunity
- After the user selects an opportunity, read all relevant files from that opportunity folder
- Treat file names and folder names as case-insensitive
- Focus only on meaningful business, technical, delivery, and architecture information
- Ignore duplicate, irrelevant, or ad-like content

---

## Step 3: Load Capability Files
- Read the user's capability files
- Use them as the reference point for comparison
- Do not assume capabilities that are not documented

---

## Step 4: Analyze Opportunity Against Capabilities
- Compare the opportunity requirements with the user's documented capabilities
- Identify capability alignment at three levels:
  - Full Match
  - Partial Match
  - Learning Needed
- Keep the analysis crisp, clear, and in plain English
- Do not hallucinate or invent missing details
- If information is missing, mark it as missing

### Output Format
| Capability Area | Match Type | Observations |
|---|---|---|
| Data Architecture | Full Match | Strong alignment with documented architecture and platform experience |
| Databricks | Partial Match | Relevant experience exists, but some opportunity-specific details are missing |
| Domain Knowledge | Learning Needed | Requires additional learning based on the opportunity context |

---

## Step 5: Generate Summary Files in claude-output
- Create a `claude-output/` folder under the selected opportunity if it does not already exist
- Save all outputs in that folder

### Files to Generate
- `opportunity_analysis.md`
- `capability_match.md`
- `learning_needs.md`

---

## Step 6: Required Content for Output Files

### 1. opportunity_analysis.md
Include:
- opportunity name
- short summary of the opportunity
- key business needs
- key technical needs
- key delivery expectations
- missing information that needs clarification

### 2. capability_match.md
Include a structured table:

| Capability Area | Full Match | Partial Match | Learning Needed | Notes |
|---|---|---|---|---|
| Example Capability | Yes/No | Yes/No | Yes/No | Explanation |

Also include three grouped sections:
- Fully Matching Capabilities
- Partially Matching Capabilities
- Learning Areas

### 3. learning_needs.md
Include:
- topics the user needs to learn for this opportunity
- why each topic is needed
- priority level: High / Medium / Low

### Output Format
| Learning Topic | Reason | Priority |
|---|---|---|
| Security Model | Needed for opportunity-specific access requirements | High |
| Domain Terms | Needed to understand the business context better | Medium |

---

## Step 7: Execution Rules
- Always ask the user which opportunity to analyze before starting detailed analysis
- Use only documented capability files and selected opportunity files
- Do not hallucinate, guess, or invent information
- If the selected opportunity already has a `claude-output/` folder with `.md` files, read those files first before creating new analysis
- Validate previous Claude output against the current opportunity files before reusing it
- Keep the wording crisp, clear, and easy to understand
- Use plain English
- Prefer structured tables over long narrative text

---

## Notes
- Treat folder names, file names, and references as case-insensitive
- Focus on actual alignment between the opportunity and documented capabilities
- Clearly separate confirmed facts, missing information, and learning needs
- Highlight only real gaps supported by the opportunity documents