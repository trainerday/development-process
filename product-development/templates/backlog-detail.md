---
title: Backlog Detail
type: note
permalink: product-development/templates/backlog-detail
---

# Backlog Detail Template

**Command**: "create backlog details [backlog-name]"

## Generated File
Creates: `backlog-details/[backlog-name].md`

## Template Content
```markdown
# [Backlog Name] - Requirements

## Current State


## Desired Outcome  


## Interaction Mechanism


## Special Requirements


## Additional Context

```

## Process Steps
1. **Create detail file**: `backlogs/[backlog-name].md` using template
2. **Update backlog link**: Replace the backlog item with link format:
   ```markdown
   - [Backlog name](../backlogs/backlog-name.md) - Brief description
   ```
3. **CRITICAL**: Always verify the link works - never leave plain text items in backlog
4. **Path validation**: Ensure using correct structure `trainer-day/os-projects/` not `trainer-day/projects/`
5. **Test link**: Click the link to verify it resolves to the detail file