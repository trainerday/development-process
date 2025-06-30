---
title: 1-spec-process
type: note
permalink: claude-code-os/system/workflows/automated-development/1-spec-process
---

# Spec Process (For Claude Code)

## Step 1: Repository Understanding
1. **Read existing codebase** - Analyze project structure, tech stack, existing functionality
2. **Read backlog detail file** - Get business context from `backlog-details/[task-name].md`
3. **VERIFY LINK EXISTS** - Ensure the backlog item has a proper clickable link to the detail file

## Step 2: Generate Specification
Create specification in `backlog-details/[task-name]-spec.md` using this format:

```markdown
# [Task Name] - Technical Specification

## ✅ HIGH CONFIDENCE (Claude is sure)
- Bullet points for things Claude knows how to implement
- Clear technical steps with existing patterns
- Database/API changes that are straightforward

## ❓ NEEDS CLARIFICATION (Claude needs input)  
- Questions about user experience decisions
- Unclear business logic or edge cases
- Integration points that need human decision

## ⚠️ ASSUMPTIONS (Claude is guessing)
- Things Claude assumes but isn't certain about
- UI/UX decisions Claude made without guidance
- Performance or technical choices that could go either way

## 🎯 CRITICAL DECISIONS NEEDED
- Major architectural or business decisions
- Privacy, security, or compliance choices
- Breaking changes or migration requirements
```

## Step 3: Wait for Human Approval
- Human reviews spec quickly using confidence-based format
- Responds with "approved" or "fix [feedback]" for specific sections

## Step 4: Link Validation (NEW)
Before proceeding to development:
1. **Verify backlog link exists**: Ensure the task has a clickable link in the backlog file
2. **Update if needed**: If link is missing, update backlog with proper format:
   ```markdown
   - [Task Name](../backlog-details/task-name.md) - Brief description
   ```
3. **Path validation**: Ensure correct structure `claude-code-os/os-projects/` not `claude-code-os/projects/`


## Backlog Management Requirements

### Before Spec Generation
**CRITICAL**: Always verify proper backlog linking before proceeding with specs.

### Creating Backlog Details
**Command**: `"create backlog details [task-name]"`

**Process**:
1. **Add item to backlog** with brief description
2. **Create detailed requirements** using the command above
3. **Fill in business context** in the generated file:
   - Current state and limitations
   - Desired user outcomes
   - Interaction mechanisms
   - Special requirements (compliance, security, etc.)
4. **AUTOMATICALLY UPDATE BACKLOG LINK**: Replace the backlog item with link format:
   ```markdown
   - [Task Name](../backlog-details/task-name.md) - Brief description
   ```

### Link Validation and Fixes
**Command**: `"fix backlog links [os-project-name]"`

**Critical Linking Requirements**:
- **ALWAYS create clickable links** when adding backlog items
- **NEVER leave plain text items** in backlog without links
- **Use relative path format**: `../backlog-details/task-name.md`
- **Update existing items** to use link format if they don't have it

**Common Path Issues to Fix**:
- **Wrong**: `claude-code-os/projects/cycling-calculators/backlog-details/`
- **Correct**: `claude-code-os/os-projects/cycling-calculators/backlog-details/`
- **Relative path**: `../backlog-details/filename.md` (used in links)

**Link Format Requirements**:
- **Correct format**: `- [Task Name](../backlog-details/task-name.md) - Brief description`
- **Incorrect formats to fix**:
  - Plain text: `- Task Name - Brief description` 
  - Wrong paths: `../details/file.md` or `./backlog-details/file.md`
  - Absolute paths: `/claude-code-os/os-projects/...`
  - Missing os-projects: `claude-code-os/projects/...`