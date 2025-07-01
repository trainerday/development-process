---
title: kanban-board-template
type: note
permalink: trainer-day/templates/kanban-board-template
---

# Kanban Board Template

This template creates an Obsidian Kanban board for OS project workflow management using the new kanban-based automation approach.

## Template Content
```
---
kanban-plugin: board
permalink: [os-project-name]/kanban-board
---

## backlog
- [ ] [Example Backlog 1 - Spec](../backlogs/Example%20Backlog%201%20-%20Spec.md)
- [ ] [Example Backlog 2 - Spec](../backlogs/Example%20Backlog%202%20-%20Spec.md)

## next

## in process

## dev complete

## on stage

## on production

%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[false,false,false,false,false,false]}
```
%%
```

## Kanban Stage Descriptions

### backlog
- **Purpose**: All planned backlogs and features
- **Who manages**: Human (product owner/developer)
- **Action**: Prioritize and move to `next` when ready

### next  
- **Purpose**: Prioritized backlogs ready for development
- **Who manages**: Human (prioritization decisions)
- **Action**: Automation picks up with "process dev queue"

### in process
- **Purpose**: Active development with automation tracking
- **Who manages**: Claude Code automation
- **Format**: Backlogs include sub-steps with approval gates
- **Example**:
```markdown
- [ ] [Active Backlog - Spec](../backlogs/Active%20Backlog%20-%20Spec.md)
  - [x] Spec generation COMPLETED
  - [ ] **Implementation approval PENDING** ← Current step
  - [ ] Local testing
  - [ ] Ready for staging
```

### dev complete
- **Purpose**: Development finished, ready for staging
- **Who manages**: Claude Code automation moves here after local testing passes
- **Action**: Human deploys to staging environment

### on stage
- **Purpose**: Deployed to staging environment for testing
- **Who manages**: Human (staging deployment decision)
- **Action**: Staging tests run, human approves for production

### on production
- **Purpose**: Live in production environment
- **Who manages**: Human (production deployment decision)  
- **Action**: Eventually archived to `backlogs-completed/`

## Backlog Format in Kanban Board

### Basic Backlog (backlog, next, dev complete, on stage, on production)
```markdown
- [ ] [Backlog Name - Spec](../backlogs/Backlog%20Name%20-%20Spec.md)
```

### In Process Backlog (with automation tracking)
```markdown
- [ ] [Backlog Name - Spec](../backlogs/Backlog%20Name%20-%20Spec.md)
  - [x] Spec generation COMPLETED
  - [x] Implementation COMPLETED  
  - [ ] **Local testing approval PENDING** ← Current step
  - [ ] Ready for staging
```

## Usage
When creating a new OS project, this template will be used to generate `kanban-board.md` in the project root with the correct permalink based on the project name.

**IMPORTANT**: Always ensure the kanban board file has the `.md` extension so it's visible in Obsidian.

## Integration with Automation
- **"process dev queue"**: Moves backlogs from `next` through `in process` to `dev complete`
- **Human gates**: Prioritization (`backlog` → `next`), staging deployment (`dev complete` → `on stage`), production deployment (`on stage` → `on production`)
- **Completion**: Backlogs in `on production` eventually get archived to `backlogs-completed/`