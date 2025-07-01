---
title: permalink-cleanup-cycling-calculators
type: note
permalink: trainer-day/system/troubleshooting/permalink-cleanup-cycling-calculators
---

# Permalink Cleanup Process

## Issue Identified
Some files exist in the correct directory structure (`trainer-day/os-projects/cycling-calculators/backlog-details/`) but have incorrect permalinks pointing to the old path (`trainer-day/projects/cycling-calculators/backlog-details/`).

## Files with Incorrect Permalinks (Based on Screenshot)
- `Create Route Speed Calculator - Spec`
- `Create Speed to Power Calculator - Spec` 
- `design-main-ui-ux-and-power-to-speed-calculator`
- And potentially others

## Solution Steps

### 1. Identify Problem Files
Files in correct directory but with wrong permalinks:
- **Correct directory**: `trainer-day/os-projects/cycling-calculators/backlog-details/`
- **Wrong permalink**: `trainer-day/projects/cycling-calculators/backlog-details/`
- **Correct permalink**: `trainer-day/os-projects/cycling-calculators/backlog-details/`

### 2. Database Cleanup Required
These appear to be database inconsistencies where:
- File system path is correct
- Database permalink is incorrect
- Search/access fails due to permalink mismatch

### 3. Recommended Action
1. **Manual cleanup**: Remove files with incorrect permalinks from the file system
2. **Recreate properly**: Use Claude Code OS commands to recreate any needed files
3. **Verify links**: Ensure all backlog links point to files with correct permalinks

### 4. Prevention
- Always use `os-projects` not `projects` in path structure
- Verify permalinks match directory structure
- Use the updated create processes that validate paths

## ✅ RESOLVED - Cycling Calculators Cleanup

### Issue Resolution Steps Taken:
1. **Manual permalink fixes** - Human fixed permalinks from terminal and ran basic memory sync
2. **Removed duplicate files** - Deleted 9 duplicate backlog detail files created by Claude
3. **Fixed backlog links** - Updated `1-backlog.md` with proper clickable links to all existing detail files
4. **Deleted incorrect backlog file** - Removed incorrectly named `backlog.md` file

### Final State:
- **✅ Proper flow structure**: All files use correct `1-backlog.md` naming
- **✅ Clickable links**: All 9 backlog items now have working markdown links
- **✅ No duplicates**: Removed Claude's incorrectly created duplicate files
- **✅ Correct permalinks**: All files now use proper `trainer-day/os-projects/` structure

### Files with Working Links:
- Create Route Speed Calculator - Spec.md
- Power Zone Calculator - Spec.md  
- HR Zone Calculator - Spec.md
- Gearing Speed Calculator - Spec.md
- Fat Max Zone Calculator - Spec.md
- Zone 2 Calculator - Spec.md
- FTP from VO2max Calculator - Spec.md
- Create Speed to Power Calculator - Spec.md
- design-main-ui-ux-and-power-to-speed-calculator.md

### Lessons Learned:
- Always use existing `1-backlog.md` file, never create new `backlog.md`
- Check for existing detail files before creating new ones
- Manual permalink fixing + basic memory sync resolves database/filesystem mismatches