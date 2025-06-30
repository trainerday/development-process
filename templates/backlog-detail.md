---
title: backlog-detail
type: note
permalink: claude-code-os/templates/backlog-detail
---

# Backlog Detail Template

**Command**: "create backlog details [task-name]"

## Generated File
Creates: `backlog-details/[task-name].md`

## Template Content
```markdown
# [Task Name] - Requirements

## Current State


## Desired Outcome  


## Interaction Mechanism


## Special Requirements


## Additional Context

```

## Process Steps
1. **Create detail file**: `backlog-details/[task-name].md` using template
2. **Update backlog link**: Replace the backlog item with link format:
   ```markdown
   - [Task name](../backlog-details/task-name.md) - Brief description
   ```
3. **CRITICAL**: Always verify the link works - never leave plain text items in backlog
4. **Path validation**: Ensure using correct structure `claude-code-os/os-projects/` not `claude-code-os/projects/`
5. **Test link**: Click the link to verify it resolves to the detail file