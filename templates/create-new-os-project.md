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
├── kanban-board.md
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

## Initial Kanban Board

**kanban-board.md** should use the kanban board template from `claude-code-os/templates/kanban-board-template.md` with the permalink set to `[os-project-name]/kanban-board`.

## Post-Creation
After os-project creation, if Claude Code is running in an empty project folder, ask:
"Would you like to set up a new Express project?"

If yes, use template: `claude-code-os/templates/express-setup.md`