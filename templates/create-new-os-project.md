---
title: create-new-os-project
type: note
permalink: claude-code-os/templates/create-new-os-project
---

# Create OS-Project Command

**Command**: "create os-project [os-project-name] and [brief-description]"

## Generated Structure
```
[os-project-name]/
├── system-state-hierarchy.md
├── tech-stack.md
├── design-standards.md
├── flow/
│   ├── 1-backlog.md
│   ├── 2-next.md
│   ├── 3-in-progress.md
│   ├── 4-code-complete.md
│   ├── 5-staging.md
│   ├── 6-testing.md
│   ├── 7-test-results.md
│   └── 8-approved.md
├── stage-testing/
│   ├── task-list-and-status.md
├── backlog-details/
├── backlog-completed/
│   ├── backlog-specs/
│   └── backlog-completed.md
└── conversations/
    ├── decision-summaries/
    └── review-summaries/
```

## Initial Backlog Item

**1-backlog.md** should include one example task:

```
# Backlog

## New Features
- OS-Project setup - Initial os-project structure and basic functionality

## Improvements
- (Future improvements will be added here)

## Bug Fixes
- (Bug fixes will be added here)
```

## Post-Creation
After os-project creation, if Claude Code is running in an empty project folder, ask:
"Would you like to set up a new Express project?"

If yes, use template: `claude-code-os/templates/express-setup.md`