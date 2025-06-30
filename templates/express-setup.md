---
title: express-setup
type: note
permalink: claude-code-os/templates/express-setup
---
# Express Project Setup

**Trigger**: After creating project, ask "Would you like to set up a new Express project?"

**Prerequisites**: Claude Code running in empty project folder

## Commands to Execute
```bash
# Create Express project with EJS templating
express -e

# Install dependencies including development tools
npm install
npm install --save-dev nodemon

# Update package.json scripts
npm pkg set scripts.dev="nodemon ./bin/www"
npm pkg set scripts.start="node ./bin/www"

# Create .gitignore
echo "node_modules/
.env
*.log
.DS_Store" > .gitignore

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
" > claude.md

# Initialize git repository
git init

# Create GitHub repository in TrainerDay organization
gh repo create TrainerDay/[project-name] --private --clone

# Initial commit
git add .
git commit -m "Initial Express project setup with nodemon"

# Push to repository
git push -u origin main

# Add Dokku remotes for deployment
git remote add dokku dokku@uat.trainerday.com:[project-name]
git remote add dokku-prod dokku@prod.trainerday.com:[project-name]

# Start development server
npm run dev

# Verify server is running
curl -s -o /dev/null -w "%{http_code}" http://localhost:3000
```


## Critical Completion Checklist
**IMPORTANT: ALL steps must be completed. Do not skip any steps.**

✅ Express project structure created
✅ Dependencies installed (including nodemon)
✅ Scripts configured in package.json
✅ .gitignore created
✅ **claude.md file created with OS project connection** ← Links to associated OS project
✅ Git repository initialized
✅ **GitHub repository created in TrainerDay organization** ← CRITICAL: Do not skip
✅ Initial commit made
✅ Code pushed to GitHub
✅ Dokku staging and production remotes added for deployment
✅ Development server running and responding on localhost:3000
✅ Ready for continuous local testing

**If any step fails or is skipped, stop and resolve before proceeding.**

## Development Workflow (Mode 4 - Autonomous Development Only)
1. **Local Development**: nodemon runs continuously, auto-restarts on changes
2. **Local Testing**: Claude Code tests functionality locally
3. **Staging Deployment**: After local tests pass, deploy to staging
4. **Staging Testing**: Claude Code runs full test suite on staging
5. **Production**: After staging validation, deploy to production

**Note**: For Modes 1-3, humans manage their own local development and testing processes.