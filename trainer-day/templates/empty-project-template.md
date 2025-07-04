---
title: empty-project-template
type: note
permalink: trainer-day/templates/empty-project-template
---

# Empty Project Setup

**Trigger**: After creating os-project, if Claude Code is running in an empty project folder

**Prerequisites**: Claude Code running in empty project folder

## Commands to Execute
```bash
# Create .gitignore
echo "node_modules/
.env
*.log
.DS_Store" > .gitignore

# Create .mcp.json for Basic Memory integration
echo '{
  "mcpServers": {
    "basic-memory": {
      "command": "uvx",
      "args": [
        "basic-memory",
        "mcp"
      ]
    }
  }
}' > .mcp.json

# Create claude.md file linking to OS project
echo "# Claude Development Notes

## Connected OS Project
This development project is connected to the OS project: **[os-project-name]**

To access the OS project management files, use:
\`memory://os-projects/[os-project-name]/kanban-board\`

## Quick Links
- Kanban Board: \`os-projects/[os-project-name]/kanban-board\`
- Tech Standards: \`os-projects/[os-project-name]/project-standards-and-dev-notes/tech-standards\`
- Design Standards: \`os-projects/[os-project-name]/project-standards-and-dev-notes/design-standards\`
- Testing: \`os-projects/[os-project-name]/stage-testing/task-list-and-status\`

## Development Notes
(Add development-specific notes here)
" > CLAUDE.md

# Initialize git repository
git init

# Create GitHub repository in TrainerDay organization
gh repo create TrainerDay/[project-name] --private --clone

# Initial commit
git add .
git commit -m "Initial project setup"

# Push to repository
git push -u origin main

# Add Dokku remotes for deployment
git remote add dokku dokku@uat.trainerday.com:[project-name]
git remote add dokku-prod dokku@prod.trainerday.com:[project-name]
```

## Critical Completion Checklist
**IMPORTANT: ALL steps must be completed. Do not skip any steps.**

✅ .gitignore created
✅ .mcp.json created for Basic Memory integration
✅ claude.md file created with OS project connection
✅ Git repository initialized
✅ GitHub repository created in TrainerDay organization
✅ Initial commit made
✅ Code pushed to GitHub
✅ Dokku staging and production remotes added

**If any step fails or is skipped, stop and resolve before proceeding.**

## Next Steps
After completing the empty project setup, ask:
"What type of project would you like to create?"

Options:
- Express.js web application → Use `trainer-day/templates/express-js-setup-template`
- [Future: Add other project types]