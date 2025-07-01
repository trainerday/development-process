---
title: 0-queue-processing-updated
type: note
permalink: trainer-day/system/workflows/automated-development/0-queue-processing
---

# Queue Processing Instructions (For Claude Code)

## When user says "process dev queue":

### Step 1: Check Queue Status
1. Read the project's `kanban-board.md` file
2. Check `## in process` section for active backlogs
3. If contains a backlog → go to Step 2
4. If empty → move one backlog from `## next` to `## in process` and start with spec generation

### Step 2: Execute Current Automation Step
Check backlog status in `## in process` section and continue from current step:

**Spec Generation**
- Follow spec process (see [1-spec-process.md](1-spec-process.md))
- Create confidence-based specification using HIGH CONFIDENCE, NEEDS CLARIFICATION, ASSUMPTIONS, CRITICAL DECISIONS format
- Add specifications to backlog detail document as `[backlog-name]-spec.md`
- Update backlog in kanban board: `- [ ] **Spec approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Implementation** 
- Follow development process (see [2-development-process.md](2-development-process.md))
- Write code based on approved specifications
- Update backlog in kanban board: `- [ ] **Implementation approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Local Testing**
- Follow testing process (see [3-testing-process.md](3-testing-process.md))
- **Automated Quality Control Loop:**
  - If tests PASS → Update backlog: `- [ ] **Local testing approval PENDING** ← Current step`
  - If tests FAIL → Fix issues automatically and retest
  - **Maximum 5 retry attempts** - if still failing after 5 tries, stop and request human help
  - Track retry count: `- [ ] **Local testing (Attempt X/5) PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Ready for Staging**
- Move entire backlog from `## in process` to `## dev complete` section
- Continue with normal staging workflow

### Step 3: Handle Human Responses
- **"approved"** → Mark current step complete, advance to next step
- **"fix [feedback]"** → Incorporate requested changes, retry current step

### Step 4: Update Backlog Format in Kanban Board
Always maintain this format in `## in process` section:
```markdown
## in process

- [ ] [Backlog Name](../backlogs/Backlog%20Name%20-%20Spec.md)
  - [x] Spec generation COMPLETED
  - [ ] **Implementation approval PENDING** ← Current step
  - [ ] Local testing
  - [ ] Ready for staging
```

### Step 5: Backlog Flow Through Kanban Board
1. **backlog** → **next** (human decision)
2. **next** → **in process** (automation starts)
3. **in process** → **dev complete** (after local testing approved)
4. **dev complete** → **on stage** (staging deployment)
5. **on stage** → **on production** (production deployment)

### Kanban Board Structure
```markdown
## backlog
- [ ] [Backlog 1](../backlogs/Backlog%201%20-%20Spec.md)
- [ ] [Backlog 2](../backlogs/Backlog%202%20-%20Spec.md)

## next
- [ ] [Priority Backlog](../backlogs/Priority%20Backlog%20-%20Spec.md)

## in process
- [ ] [Active Backlog](../backlogs/Active%20Backlog%20-%20Spec.md)
  - [x] Spec generation COMPLETED
  - [ ] **Implementation approval PENDING** ← Current step
  - [ ] Local testing
  - [ ] Ready for staging

## dev complete
- [ ] [Completed Backlog](../backlogs/Completed%20Backlog%20-%20Spec.md)

## on stage
- [ ] [Staging Backlog](../backlogs/Staging%20Backlog%20-%20Spec.md)

## on production
- [ ] [Live Backlog](../backlogs/Live%20Backlog%20-%20Spec.md)
```

### Completion
When all automation steps are approved, backlog moves from `## in process` to `## dev complete` and continues through the kanban flow.