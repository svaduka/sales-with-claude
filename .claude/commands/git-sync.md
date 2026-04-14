# Git Synchronization Guide for Working with Claude

## Purpose

This document defines the standard Git synchronization process, conflict-resolution workflow, commit discipline, and best practices to follow while working with Claude on a codebase.

---

## 1. Objective

| Item | Description |
|---|---|
| Goal | Keep the local branch synchronized with the source branch in a controlled, auditable, and low-risk manner. |
| Primary concern | Prevent accidental overwrites, preserve developer intent, and maintain clean commit history. |
| Working mode | Claude assists with changes, but the developer remains the final authority for conflict resolution and merge decisions. |

---

## 2. Standard Pull and Synchronization Behavior

| Step | Action | Expected Behavior |
|---|---|---|
| 1 | Start from the correct working branch | Confirm the current branch before any pull, merge, or rebase activity. |
| 2 | Ensure working tree is clean | Stash or commit incomplete work before synchronization. |
| 3 | Pull latest changes | Fetch and integrate incoming changes from the source branch. |
| 4 | Detect conflicts | If conflicts arise, pause automatic progression and review conflict files. |
| 5 | Ask developer for resolution mode | Developer chooses `source`, `target`, or `check`. |
| 6 | Apply resolution | Resolve according to the chosen mode. |
| 7 | Validate repository state | Ensure no unresolved files remain. |
| 8 | Run basic verification | Execute relevant validation such as build, lint, tests, or syntax checks. |
| 9 | Create structured commit | Commit all intended changes with a clear, traceable message. |

---

## 3. Conflict Resolution Modes

When a pull introduces conflicts, the developer must choose one of the following modes.

| Mode | Meaning | Resolution Rule | When to Use |
|---|---|---|---|
| `source` | Accept incoming branch changes | Take all incoming changes from the source branch for the conflicted file or block. | Use when the remote branch has the correct latest implementation and local changes should be discarded for that conflict area. |
| `target` | Keep local branch changes | Retain all local changes from the current target branch for the conflicted file or block. | Use when local development is the desired truth and incoming changes should be ignored for that conflict area. |
| `check` | Review conflict manually | Inspect each conflicted file one by one and decide case by case. | Use when both source and target contain meaningful work that must be merged carefully. |

---

## 4. Detailed Conflict Handling Rules

| Scenario | Required Action |
|---|---|
| Conflict mode is `source` | Accept incoming changes for all identified conflicts and continue. |
| Conflict mode is `target` | Keep local branch content for all identified conflicts and continue. |
| Conflict mode is `check` | Open each conflicted file, review conflict markers, understand intent from both sides, and merge carefully file by file. |
| Mixed conflict intent across files | Use `check` mode and document the rationale in commit message or notes when appropriate. |
| A file contains logic, configuration, and formatting changes together | Resolve logic first, then configuration, then formatting. |
| Conflict is unclear or risky | Do not guess. Escalate to the developer for explicit direction. |

---

## 5. File-by-File Manual Review Process for `check`

| Order | Review Item | What to Verify |
|---|---|---|
| 1 | File purpose | Understand what the file is responsible for. |
| 2 | Conflict sections | Identify exactly which lines differ between source and target. |
| 3 | Business logic | Check whether logic changed intentionally on one or both sides. |
| 4 | Dependencies | Confirm imports, references, interfaces, and contracts remain valid. |
| 5 | Configuration impact | Review environment values, paths, versions, and flags. |
| 6 | Formatting and style | Normalize formatting only after logic is settled. |
| 7 | Validation | Run tests, linting, compile, or dry-run checks where applicable. |

---

## 6. Commit Rules

Every synchronization-related commit must be clear, structured, and attributable.

| Rule | Standard |
|---|---|
| Commit scope | Include only intended synchronization and related resolved changes. |
| Commit content | Do not mix unrelated refactoring with sync work unless explicitly planned. |
| Commit message style | Must mention Topic, Sub-task changes, and Author Claude. |
| Commit quality | Message must explain what changed, not just that a sync happened. |
| Traceability | Important manual conflict decisions should be reflected in the commit body. |

### Commit Message Template

```text
<type>: <topic>

Topic: <high-level topic>
Sub-task Changes:
- <change 1>
- <change 2>
- <change 3>
Author: Claude
```

### Example Commit Message

```text
chore: synchronize feature branch with latest source updates

Topic: Git synchronization for feature branch
Sub-task Changes:
- Pulled latest changes from source branch
- Resolved merge conflicts in pipeline configuration and service layer
- Retained target logic for local trading workflow and accepted source updates for shared utilities
Author: Claude
```

---

## 7. Best Practices While Working with Git

| Category | Best Practice | Why It Matters |
|---|---|---|
| Branch hygiene | Work on the correct branch and name branches clearly. | Reduces accidental commits to the wrong branch. |
| Clean state | Pull only when the working tree is clean. | Avoids mixing uncommitted work with incoming changes. |
| Small commits | Commit in logical, focused units. | Easier review, rollback, and audit. |
| Frequent sync | Pull or rebase regularly from the main source branch. | Minimizes large conflict windows. |
| Conflict discipline | Never resolve conflicts blindly. | Prevents hidden regressions and lost logic. |
| Read before merge | Understand both source and target intent before choosing a side. | Avoids destroying valid work. |
| Preserve semantics | Prioritize logic correctness over formatting preferences. | Keeps behavior intact. |
| Validation | Run lint, tests, compile, or smoke checks after merge resolution. | Catches integration issues immediately. |
| Meaningful commits | Use commit messages that explain business or technical intent. | Improves maintainability and team communication. |
| Avoid force push | Do not force push shared branches unless explicitly approved. | Prevents overwriting teammates' work. |
| Review generated code | Inspect Claude-generated changes before commit. | Ensures alignment with repository standards and design. |
| Separate concerns | Keep sync changes, feature changes, and refactoring separate when possible. | Makes debugging and review easier. |
| Protect important branches | Use PRs and branch protection for shared branches. | Reduces production and integration risk. |
| Backup before risky ops | Create a temporary branch before major rebase or conflict-heavy merge. | Provides quick recovery path. |
| Keep history readable | Prefer a clean and understandable history over noisy commit logs. | Supports long-term maintainability. |

---

## 8. Operational Guardrails for Claude-Assisted Git Work

| Guardrail | Expected Practice |
|---|---|
| No silent conflict resolution | Claude should not make hidden assumptions in risky conflicts. |
| No unrelated file edits | Claude should avoid modifying files outside the requested scope. |
| No destructive commands without intent | Commands such as hard reset, force push, or branch deletion must be deliberate and approved. |
| No vague commit messages | Every commit must have a clear topic and sub-task description. |
| No skipping validation | Basic verification should follow any non-trivial merge or conflict resolution. |

---

## 9. Recommended End-to-End Workflow

| Phase | Activity |
|---|---|
| Preparation | Confirm branch, clean working tree, and review pending changes. |
| Synchronization | Pull latest source updates into the current branch. |
| Conflict review | If conflicts occur, ask developer to choose `source`, `target`, or `check`. |
| Resolution | Apply selected conflict strategy and validate all modified files. |
| Verification | Run relevant tests, linting, build, or functional checks. |
| Commit | Create a structured commit with Topic, Sub-task Changes, and Author Claude. |
| Push or PR | Push changes to remote branch and proceed with normal review flow. |

---

## 10. Practical Decision Matrix

| Situation | Preferred Choice |
|---|---|
| Shared utility updated remotely and local branch only changed formatting | `source` |
| Local feature logic is newer and remote change is outdated | `target` |
| Both branches changed the same business logic | `check` |
| Config file changed in both branches with environment-specific values | `check` |
| Generated lock file changed due to dependency update from source branch | Usually `source`, unless local dependency intent must be preserved |
| Documentation changed in both branches | `check`, then combine content carefully |

---

## 11. Short Working Standard

| Rule No. | Standard |
|---|---|
| 1 | Always synchronize from a clean working state. |
| 2 | Always pause and ask the developer when conflicts occur. |
| 3 | Use only `source`, `target`, or `check` as conflict decision modes. |
| 4 | In `check`, resolve file by file, not by assumption. |
| 5 | Validate after resolving conflicts. |
| 6 | Commit with Topic, Sub-task Changes, and Author Claude. |
| 7 | Keep commit history clean, minimal, and meaningful. |

---

## 12. Suggested Reusable Commit Formats

### Sync Commit

```text
chore: sync latest source branch updates

Topic: Branch synchronization
Sub-task Changes:
- Pulled latest updates from source branch
- Resolved merge conflicts using <source/target/check> strategy
- Validated repository state after synchronization
Author: Claude
```

### Feature + Sync Commit

```text
feat: integrate latest source changes with feature updates

Topic: Feature integration and synchronization
Sub-task Changes:
- Pulled latest source branch changes
- Merged conflict updates in <files/modules>
- Preserved local feature logic and aligned shared components
Author: Claude
```

### Fix After Conflict Resolution

```text
fix: correct issues introduced during merge resolution

Topic: Post-merge stabilization
Sub-task Changes:
- Corrected merge-related inconsistencies in <module>
- Updated imports, configuration, and references after sync
- Revalidated build and test flow
Author: Claude
```

---

## 13. Final Guidance

The safest Git synchronization workflow is not the fastest one. While working with Claude, the preferred approach is disciplined synchronization, explicit conflict choice by the developer, careful validation, and structured commits that explain both the technical change and the intent behind it.
