---
title: express-setup
type: note
permalink: product-development/templates/express-setup
---

# Express.js Project Setup

**Trigger**: After empty project setup, when user chooses Express.js application

**Prerequisites**: Empty project template already completed

## Commands to Execute
```bash
# Create Express project with EJS templating
express -e --force

# Install dependencies including development tools
npm install
npm install --save-dev nodemon

# Update package.json scripts
npm pkg set scripts.dev="nodemon ./bin/www"
npm pkg set scripts.start="node ./bin/www"

# Update .gitignore to include Express-specific items
echo "
# Express specific
public/uploads/
sessions/
*.log
logs/
pids/
*.pid
*.seed
*.pid.lock" >> .gitignore

# Commit Express setup
git add .
git commit -m "Add Express.js with EJS templating and nodemon"
git push

# Start development server
npm run dev

# Verify server is running
curl -s -o /dev/null -w "%{http_code}" http://localhost:3000
```

## Express-Specific Checklist

✅ Express project structure created with EJS
✅ Dependencies installed (including nodemon)
✅ Scripts configured in package.json (dev and start)
✅ .gitignore updated with Express-specific entries
✅ Express setup committed and pushed
✅ Development server running on localhost:3000
✅ Server responding to requests

## Development Workflow
1. **Local Development**: nodemon runs continuously, auto-restarts on changes
2. **Local Testing**: Test functionality locally at http://localhost:3000
3. **Staging Deployment**: `git push dokku main`
4. **Production Deployment**: `git push dokku-prod main`

## Express Project Structure
```
├── app.js              # Main application file
├── bin/
│   └── www            # Server startup script
├── public/            # Static assets
│   ├── images/
│   ├── javascripts/
│   └── stylesheets/
├── routes/            # Route definitions
│   ├── index.js
│   └── users.js
├── views/             # EJS templates
│   ├── index.ejs
│   ├── error.ejs
│   └── layout.ejs
└── package.json       # Dependencies and scripts
```