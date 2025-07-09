---
title: Automation Spec
type: note
permalink: product-development/system/workflows/automated-development/automation-spec
---

# Automated Development Specification

## Process Overview
Complete end-to-end automated development using a **kanban board approach** where all backlogs flow through a single kanban board file (`kanban-board.md`) rather than separate stage files.

## Kanban Board Workflow

### Board Structure
Each project has one `kanban-board.md` with these sections:
- **backlog**: All planned backlogs
- **next**: Prioritized backlogs ready for development  
- **in process**: Currently active automation
- **dev complete**: Completed development, ready for staging
- **on stage**: Deployed to staging environment
- **on production**: Live in production

### Process Steps
1. **Queue Management**: [0-queue-processing.md](0-queue-processing.md) - Move backlogs through kanban board
2. **Specification Generation**: [1-spec-process.md](1-spec-process.md) - Create technical specs
3. **Development Implementation**: [2-development-process.md](2-development-process.md) - Write code
4. **Testing Validation**: [3-testing-process.md](3-testing-process.md) - Local testing
5. **Backlog Completion**: [backlog-completion.md](backlog-completion.md) - Production deployment

## Backlog Flow Through Kanban Board

### Stage 1: Backlog Management
- **Human Role**: Manage backlog, prioritize backlogs
- **Action**: Move backlogs from `## backlog` to `## next`
- **Trigger**: Human decision on priorities

### Stage 2: Development Automation  
- **Trigger**: "process dev queue" command
- **Claude Role**: Complete automation from `## next` through `## dev complete`
- **Sub-stages** within `## in process`:
  1. Spec generation → wait for approval
  2. Implementation → wait for approval  
  3. Local testing → wait for approval
  4. Move to `## dev complete`

### Stage 3: Staging Deployment
- **Human Role**: Move from `## dev complete` to `## on stage`
- **Claude Role**: Deploy to staging, run tests
- **Result**: Backlog ready for production

### Stage 4: Production Deployment
- **Human Role**: Final approval, move to `## on production`
- **Claude Role**: Deploy to production, monitor
- **Result**: Backlog completed and live

## Kanban Board Backlog Format

### In Backlog/Next
```markdown
## backlog
- [ ] [Power Zone Calculator - Spec](../backlogs/Power%20Zone%20Calculator%20-%20Spec.md)
- [ ] [Route Speed Calculator - Spec](../backlogs/Route%20Speed%20Calculator%20-%20Spec.md)

## next  
- [ ] [Priority Backlog - Spec](../backlogs/Priority%20Backlog%20-%20Spec.md)
```

### In Process (During Automation)
```markdown
## in process
- [ ] [Active Backlog - Spec](../backlogs/Active%20Backlog%20-%20Spec.md)
  - [x] Spec generation COMPLETED
  - [ ] **Implementation approval PENDING** ← Current step
  - [ ] Local testing
  - [ ] Ready for staging
```

### Completed Stages
```markdown
## dev complete
- [ ] [Ready for Staging - Spec](../backlogs/Ready%20for%20Staging%20-%20Spec.md)

## on stage  
- [ ] [Testing on Staging - Spec](../backlogs/Testing%20on%20Staging%20-%20Spec.md)

## on production
- [ ] [Live Feature - Spec](../backlogs/Live%20Feature%20-%20Spec.md)
```

## Development Modes

### Mode 1: Manual Development
**Flow**: Human moves items through all stages
- **backlog → next**: Human decision
- **next → in process**: Human starts work manually
- **in process → dev complete**: Human completes work
- **dev complete → on stage**: Human deploys
- **on stage → on production**: Human promotes

### Mode 2: Kanban Automation (This Specification)
**Flow**: Automated development within kanban board
- **backlog → next**: Human decision (prioritization)
- **next → in process**: Automation triggered by "process dev queue"
- **Within in process**: Full automation with approval gates
- **in process → dev complete**: Automation completes
- **dev complete → on stage**: Human deploys to staging
- **on stage → on production**: Human promotes to production

## Universal Rules
- Only humans move items to `## next` (prioritization decision)
- Only humans move items from `## dev complete` to `## on stage` (staging deployment)
- Only humans move items from `## on stage` to `## on production` (production approval)
- Claude Code owns the automation within `## in process` section
- All backlog state is tracked within the single kanban board file

## Benefits of Kanban Approach
- **Single Source of Truth**: All backlog status in one file
- **Visual Workflow**: Clear progression through stages
- **Flexible Automation**: Automation works within existing kanban structure
- **Human Control**: Clear handoff points for human decisions
- **Simple Tracking**: No need to manage multiple stage files