---
title: Backlog Completion
type: note
permalink: product-development/system/workflows/automated-development/backlog-completion
---

# Backlog Completion Workflow

## When Moving Backlogs to Production

### Command
**"complete [backlog-name]"** or **"move [backlog-name] to production"**

### Kanban Board Process

#### Final Backlog Movement
Move backlog from `## on stage` to `## on production` in the kanban board:

**Before:**
```markdown
## on stage
- [ ] [Backlog Name](../backlogs/Backlog%20Name%20-%20Spec.md)
```

**After:**
```markdown
## on production  
- [ ] [Backlog Name](../backlogs/Backlog%20Name%20-%20Spec.md)
```

#### Completion Logging
1. **Add timestamped entry** to `backlogs-completed/backlogs-completed.md`:
   - Format: `YYYY-MM-DD-HH:MM - [Backlog Name](backlog-specs/Backlog%20Name%20-%20Spec.md) - [Brief Description]`
   - Example: `2025-06-28-14:30 - [Create Speed to Power Calculator](backlog-specs/Create%20Speed%20to%20Power%20Calculator%20-%20Spec.md) - Calculate required power for target speeds`

2. **Move original specification** from `backlogs/` to `backlogs-completed/backlog-specs/`:
   - Copy the original spec file to preserve historical record
   - Maintain original filename for easy cross-reference
   - Delete from `backlogs/` to keep it clean

3. **Clean up kanban board**:
   - Remove completed backlog from `## on production` section
   - Backlog is now archived in backlogs-completed

### Kanban Board Backlog Flow
```markdown
## backlog → ## next → ## in process → ## dev complete → ## on stage → ## on production
```

### File Structure After Completion
```
backlogs-completed/
├── backlogs-completed.md            # Timestamped log of completed items
└── backlog-specs/
    └── [Backlog Name] - Spec.md     # Original specification (archived)

kanban-board.md                      # Backlog removed from ## on production
```

### Benefits of Kanban Completion
- **Clear Backlog Progression**: Visual flow through all stages
- **Simple Completion Log**: Clean timestamped list of what's been done
- **Specification Archive**: Preserves original requirements for reference
- **Clean Active Board**: Removes completed items from working kanban board
- **No File Clutter**: Maintains clean kanban board structure

### Integration with Automation
This process can be automated as the final step after a backlog reaches `## on production` status and is verified in production.

## Example Commands
- `"complete Create Route Speed Calculator"`
- `"move Power Zone Calculator to production"`
- `"archive HR Zone Calculator"` (moves to backlogs-completed)

## Kanban Board Cleanup
After completion, the kanban board only shows active work:
- `## backlog`: Future backlogs
- `## next`: Prioritized backlogs  
- `## in process`: Active development
- `## dev complete`: Ready for staging
- `## on stage`: Testing in staging
- `## on production`: Currently live (until archived)

Completed backlogs are removed from the board and logged in `backlogs-completed/`.