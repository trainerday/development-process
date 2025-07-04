---
title: 2025-07-01-brainstorming
type: note
permalink: trainer-day/system/brainstorming/2025-07-01-brainstorming
---

# Process Brainstorming - July 1, 2025

## Session Overview
Date: July 1, 2025
Purpose: Process brainstorming and ideation

## Ideas & Concepts
## Obsidian Kanban Workflow Process

### Overview
Integration between Obsidian kanban board, GitHub issues, and automated testing pipeline for development task management.

### Step-by-Step Process

1. **Idea Capture**
   - Create new items in Obsidian
   - Items go to either:
     - Future file (separate from kanban)
     - Backlog column (1st column) on kanban board with related note in backlog folder

2. **Backlog Definition**
   - Work with Claude to fully define backlog items
   - Write detailed specs in the backlog notes
   - Refine requirements and acceptance criteria

3. **Priority Management**
   - Move high-priority cards to "Up Next" column
   - Command to Claude triggers:
     - Card movement in Obsidian kanban
     - Creation of GitHub issue in generic repo
     - GitHub issue placed in matching "Up Next" column

4. **Development Phase**
   - Developers check GitHub "Up Next" column for tasks
   - Items move through development phases in GitHub
   - When complete, items reach "On Stage" column in GitHub

5. **Stage Deployment & Testing**
   - Daily Claude process checks for new "On Stage" items
   - Matching kanban cards moved to "On Stage" in Obsidian
   - Triggers automated testing process:
     - Reviews completion requirements
     - Takes automatic screenshots
     - Writes basic tests for staging environment
     - Verifies design standards compliance
     - Checks spelling and quality standards

### Key Integration Points
- Obsidian ↔ GitHub issue sync
- GitHub stage detection → Obsidian updates
- Stage deployment → Automated testing pipeline
## Next Steps

## Notes