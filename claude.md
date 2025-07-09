---
title: create-new-os-project
type: note
permalink: product-development/templates/create-new-os-project
---

# Create OS-Project Command

**Command**: "create os-project [os-project-name] and [brief-description]"

## Generated Structure
```
[os-project-name]/
├── backlogs-completed/
│   ├── backlogs-completed.md
│   └── backlog-specs/
├── backlogs/
├── project-standards-and-dev-notes/
│   ├── design-standards.md
│   └── tech-standards.md
├── stage-testing/
│   └── task-list-and-status.md
├── future-backlogs.md
└── kanban-board.md
```

## Initial Kanban Board

**kanban-board.md** should use the kanban board template from `trainer-day/templates/kanban-board-template.md` with the permalink set to `[os-project-name]/kanban-board`.

## Post-Creation
After os-project creation, if Claude Code is running in an empty project folder, ask:
"Would you like to set up a new project?"

If yes, use template: `trainer-day/templates/empty-project-template`

This will:
- Set up git repository and GitHub
- Create .mcp.json for Basic Memory
- Create claude.md linking to the os-project
- Add Dokku remotes
- Then offer specific project type setup (Express, etc.)