---
title: task-completion
type: note
permalink: claude-code-os/system/workflows/automated-development/task-completion
---

# Task Completion Workflow

## When Moving Tasks to Backlog-Completed

### Command
**"complete [task-name]"** or **"move [task-name] to completed"**

### Process Steps

1. **Add timestamped entry** to `backlog-completed/backlog-completed.md`:
   - Format: `YYYY-MM-DD-HH:MM - [Task Name](backlog-specs/Task%20Name%20-%20Spec.md) - [Brief Description]`
   - Example: `2025-06-28-14:30 - [Create Speed to Power Calculator](backlog-specs/Create%20Speed%20to%20Power%20Calculator%20-%20Spec.md) - Calculate required power for target speeds`

2. **Move original specification** from `backlog-details/` to `backlog-completed/backlog-specs/`:
   - Copy the original spec file to preserve historical record
   - Maintain original filename for easy cross-reference
   - Delete from `backlog-details/` to keep it clean

3. **Update active backlog**:
   - Remove completed item from `flow/1-backlog.md`
   - Clean up any flow stage the task was in

4. **Clean up flow files**:
   - Remove task from whatever flow stage it was in (usually `8-approved.md`)

### File Structure After Completion
```
backlog-completed/
├── backlog-completed.md             # Timestamped log of completed items
└── backlog-specs/
    └── [Task Name] - Spec.md        # Original specification
```

### Benefits
- **Simple completion log**: Clean timestamped list of what's been done
- **Specification archive**: Preserves original requirements for reference
- **Clean active backlog**: Removes completed items from working documents
- **Lightweight tracking**: No documentation bloat, just the essential log
- **No README clutter**: Only functional files, no documentation files

### Integration with Flow
This process should be automated as the final step after a task reaches `8-approved.md` status and is deployed to production.

## Example Commands
- `"complete Create Route Speed Calculator"`
- `"move Power Zone Calculator to completed"`