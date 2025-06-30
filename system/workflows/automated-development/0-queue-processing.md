---
title: queue-processing
type: note
permalink: claude-code-os/system/workflows/automated-development/queue-processing-1
---

# Queue Processing Instructions (For Claude Code)

## When user says "process dev queue":

### Step 1: Check Queue Status
1. Read `3-in-progress.md`
2. If contains a task → go to Step 2
3. If empty → move one task from `2-next.md` to `3-in-progress.md` and start with spec generation

### Step 2: Execute Current Automation Step
Check task status and continue from current step:

**Spec Generation**
- Follow spec process (see [[1-spec-process]])
- Create confidence-based specification using HIGH CONFIDENCE, NEEDS CLARIFICATION, ASSUMPTIONS, CRITICAL DECISIONS format
- Add specifications to backlog detail document as `[task-name]-spec.md`
- Update task: `- [ ] **Spec approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Implementation** 
- Write code based on approved specifications
- Update task: `- [ ] **Implementation approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Local Testing**
- Run local testing process (see [[3-testing-process]]):
- **Automated Quality Control Loop:**
  - If tests PASS → Update task: `- [ ] **Local testing approval PENDING** ← Current step`
  - If tests FAIL → Fix issues automatically and retest
  - **Maximum 5 retry attempts** - if still failing after 5 tries, stop and request human help
  - Track retry count: `- [ ] **Local testing (Attempt X/5) PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Ready for Staging**
- Move entire task from `3-in-progress.md` to `4-staging.md`
- Continue with normal staging workflow

### Step 3: Handle Human Responses
- **"approved"** → Mark current step complete, advance to next step
- **"fix [feedback]"** → Incorporate requested changes, retry current step

### Step 4: Update Task Format
Always maintain this format in `3-in-progress.md`:
```markdown
## [Task Name]
- [x] Spec generation COMPLETED
- [ ] **Implementation approval PENDING** ← Current step
- [ ] Local testing
- [ ] Ready for staging
```
## When user says "process dev queue":

### Step 1: Check Queue Status
1. Read `3-in-progress.md`
2. If contains a task → go to Step 2
3. If empty → move one task from `2-next.md` to `3-in-progress.md` and start with spec generation

### Step 2: Execute Current Automation Step
Check task status and continue from current step:

**Spec Generation**
- Follow spec process (see [[1-spec-process]])
- Create confidence-based specification using HIGH CONFIDENCE, NEEDS CLARIFICATION, ASSUMPTIONS, CRITICAL DECISIONS format
- Add specifications to backlog detail document as `[task-name]-spec.md`
- Update task: `- [ ] **Spec approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Implementation** 
- Write code based on approved specifications
- Update task: `- [ ] **Implementation approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Local Testing**
- Run local testing process (see [[3-testing-process]]):
  - Start local server
  - Take screenshots and send to OpenAI for analysis  
  - Check console/network errors
  - Test basic functionality
- **Automated Quality Control Loop:**
  - If tests PASS → Update task: `- [ ] **Local testing approval PENDING** ← Current step`
  - If tests FAIL → Fix issues automatically and retest
  - **Maximum 5 retry attempts** - if still failing after 5 tries, stop and request human help
  - Track retry count: `- [ ] **Local testing (Attempt X/5) PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Ready for Staging**
- Move entire task from `3-in-progress.md` to `4-staging.md`
- Continue with normal staging workflow

### Step 3: Handle Human Responses
- **"approved"** → Mark current step complete, advance to next step
- **"fix [feedback]"** → Incorporate requested changes, retry current step

### Step 4: Update Task Format
Always maintain this format in `3-in-progress.md`:
```markdown
## [Task Name]
- [x] Spec generation COMPLETED
- [ ] **Implementation approval PENDING** ← Current step
- [ ] Local testing
- [ ] Ready for staging
```
## Command: "process dev queue"

### Queue Logic
1. **Check 3-in-progress.md** 
   - If has a task → continue automation from current step
   - If empty → move one task from 2-next.md to 3-in-progress.md and start automation

### Automation Steps Within 3-in-progress.md
Each task tracks sub-steps with checkboxes:
```markdown
## [Task Name]
- [x] Spec generation COMPLETED
- [ ] **Spec approval PENDING** ← Current step
- [ ] Implementation 
- [ ] Local testing
- [ ] Ready for staging
```

### Human Response Commands
- **"approved"** - Mark current step complete, continue to next step
- **"fix [feedback]"** - Incorporate changes and retry current step

### Step-by-Step Flow
1. **Spec generation** → wait for "approved"
2. **Implementation** → wait for "approved" 
3. **Local testing** → wait for "approved"
4. **Ready for staging** → move entire task to 4-staging.md

### Completion
When all steps approved, task moves from 3-in-progress.md to 4-staging.md and continues through normal flow (staging → testing → test-results → approved).
## Command: "process dev queue"

### Queue Logic
1. **Check 3-in-progress.md** - Resume active automation
2. **If empty, check 2-next.md** - Start next prioritized task
3. **Update automation-status.md** with current phase and progress

### Human Response Commands
- **"approved"** - Continue to next automation phase
- **"fix [feedback]"** - Incorporate changes and retry current phase

### Automation Phases
1. Spec generation → awaiting approval
2. Implementation → local testing
3. Staging deployment → staging testing  
4. Final results → awaiting approval

### Status Tracking
automation-status.md maintains current task state, phase, progress, and next action required.

## Queue Processing Instructions (For Claude Code)
# Queue Processing Instructions (For Claude Code)

## Command: "process dev queue"

### Queue Logic
1. **Check 3-in-progress.md** 
   - If has a task → continue automation from current step
   - If empty → move one task from 2-next.md to 3-in-progress.md and start automation

### Automation Steps Within 3-in-progress.md
Each task tracks sub-steps with checkboxes:
```markdown
## [Task Name]
- [x] Spec generation COMPLETED
- [ ] **Spec approval PENDING** ← Current step
- [ ] Implementation 
- [ ] Local testing
- [ ] Ready for staging
```

### Step-by-Step Automation Flow

**Spec Generation**
- Follow spec process (see [1-spec-process.md](1-spec-process.md))
- Create confidence-based specification using HIGH CONFIDENCE, NEEDS CLARIFICATION, ASSUMPTIONS, CRITICAL DECISIONS format
- Add specifications to backlog detail document as `[task-name]-spec.md`
- Update task: `- [ ] **Spec approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Implementation** 
- Follow development process (see [2-development-process.md](2-development-process.md))
- Write code based on approved specifications
- Update task: `- [ ] **Implementation approval PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Local Testing**
- Follow testing process (see [3-testing-process.md](3-testing-process.md))
- **Automated Quality Control Loop:**
  - If tests PASS → Update task: `- [ ] **Local testing approval PENDING** ← Current step`
  - If tests FAIL → Fix issues automatically and retest
  - **Maximum 5 retry attempts** - if still failing after 5 tries, stop and request human help
  - Track retry count: `- [ ] **Local testing (Attempt X/5) PENDING** ← Current step`
- Wait for human "approved" or "fix [feedback]"

**Ready for Staging**
- Move entire task from `3-in-progress.md` to `4-staging.md`
- Continue with normal staging workflow

### Human Response Commands
- **"approved"** → Mark current step complete, advance to next step
- **"fix [feedback]"** → Incorporate requested changes, retry current step

### Task Format in 3-in-progress.md
Always maintain this format:
```markdown
## [Task Name]
- [x] Spec generation COMPLETED
- [ ] **Implementation approval PENDING** ← Current step
- [ ] Local testing
- [ ] Ready for staging
```

### Completion
When all steps approved, task moves from 3-in-progress.md to 4-staging.md and continues through normal flow (staging → testing → test-results → approved).