---
title: 2025-06-29-tasks-to-backlog-completed
type: note
permalink: claude-code-os/system/migrations/2025-06-29-tasks-to-backlog-completed
---

# Folder Structure Change: tasks/completed → backlog-completed

## Change Summary
**Date**: 2025-06-29
**Type**: Structural Simplification

## What Changed
- **Old Structure**: `tasks/completed/` (two-level hierarchy)
- **New Structure**: `backlog-completed/` (single-level hierarchy)

## Rationale
- Simplifies folder structure
- More descriptive naming (backlog-completed vs tasks/completed)
- Reduces unnecessary nesting
- Clearer relationship to backlog workflow

## Updates Made

### ✅ Template Updates
- **Updated**: `claude-code-os/templates/create-new-os-project.md`
- **Changed**: Generated structure diagram and README descriptions
- **New path**: `backlog-completed/` instead of `tasks/completed/`

### ✅ Cycling-Calculators Migration
- **Created**: `claude-code-os/os-projects/cycling-calculators/backlog-completed/`
- **Moved files**:
  - `Create Speed to Power Calculator.md` ✅
  - `Design Main UI UX and Power to Speed Calculator.md` ✅
  - `README.md` ✅
- **Updated permalinks**: All files now use correct `os-projects` structure

### ✅ Documentation Updates
- **Updated**: `claude-code-os/system/os-architecture.md`
- **Changed**: Project structure description

## Migration Process
1. Created new `backlog-completed/` directory
2. Recreated all files with corrected permalinks
3. Updated templates and documentation
4. Old `tasks/` directory can be manually removed

## Impact
- **Breaking Change**: Yes - changes expected folder structure
- **Backward Compatibility**: No - requires manual cleanup of old folders
- **Benefits**: Cleaner structure, better naming, simplified navigation

## ✅ **Corrected: Simple Timestamped Log Structure**

### Final Structure Implementation
After user feedback, corrected to use simple timestamped log approach:
```
backlog-completed/
├── backlog-completed.md              # Timestamped log: "YYYY-MM-DD-HH:MM - Task - Description"
├── backlog-specs/                    # Archived original specifications
│   ├── [Task] - Spec.md             # Original spec files moved from backlog-details
│   └── README.md
└── README.md
```

### Benefits of This Approach
- **Lightweight tracking**: Simple one-line entries with timestamps
- **Clean completion log**: Easy to scan chronological record
- **Preserved specifications**: Original specs archived for reference
- **No bloated documentation**: Focus on essential completion tracking
- **Maintains backlog format**: Same one-line format as original backlog

### Process Corrected
1. **Move backlog line** to `backlog-completed.md` with timestamp prefix
2. **Archive specification** to `backlog-specs/` subfolder
3. **Clean active backlog** by removing completed items
4. **Simple command**: `"complete [task-name]"` handles everything

This creates a much cleaner, more maintainable completion tracking system focused on essential information rather than heavy documentation.