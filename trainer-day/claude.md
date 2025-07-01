---
title: claude
type: note
permalink: trainer-day/claude
---

Testing a change
## Load Claude Code OS
Read: `trainer-day/templates/`, `trainer-day/knowledge-base/`, `trainer-day/system/`

Do not load: `trainer-day/os-projects/`

Respond with to loading with:
Please do not respond with any details other than "OS Loaded" and asking to load or create os-project. Type "command list" to get a list of commands

## Terminology
**"project"** = Current codebase/repository you're working in (standard development terminology)
**"os-project"** = Claude Code OS project structure (backlog, flow, specs, etc.) - stored in `trainer-day/os-projects/`

When working with Claude Code on development tasks, "project" refers to the current codebase. Use "os-project" commands only for Claude Code OS management tasks.

## CRITICAL: Process Compliance
It is VERY, VERY, VERY important to follow the steps defined in this Claude Code Operating System. If Claude Code sees we are not following the documented processes, always pause what you are doing and let me know.

**CRITICAL PATH STRUCTURE**: Always use `trainer-day/os-projects/[name]` never `trainer-day/projects/[name]` - the correct folder is `os-projects` not `projects`.

CRITICAL - When creating a spec or appending a spec to an existing note always read this trainer-day/system/workflows/automated-development/1-spec-process and follow it closely

## Commands
**"open os-project [os-project-name]"** → Load `trainer-day/os-projects/[os-project-name]/`
**"load os-project [os-project-name]"** → Load `trainer-day/os-projects/[os-project-name]/`

**"create os-project [os-project-name]"** → Use `trainer-day/templates/create-new-os-project.md`

**"create backlog [os-project-name] [brief-description]"** → Add item to `trainer-day/os-projects/[os-project-name]/flow/1-backlog.md` using format: `- [brief-description]`

**"create backlog details [task-name]"** → Use `trainer-day/templates/backlog-detail.md`

**"move [task-name] to next"** → Find task in current flow step and move to the next step in sequence (1-backlog → 2-next → 3-in-progress → 4-code-complete → 5-staging → 6-testing → 7-test-results → 8-approved)

**"move [task-name] backlog to next"** → Move task from `trainer-day/os-projects/[current-os-project]/flow/1-backlog.md` to `trainer-day/os-projects/[current-os-project]/flow/2-next.md`

**"process dev queue"** → See `trainer-day/system/workflows/automated-development/0-queue-processing.md`

**"push to stage"** → Deploy current code to staging server: `git push dokku main`

**"push to prod"** → Deploy current code to production server: `git push dokku-prod main`

**"command list"** → Show this list of commands

**"fix backlog links [os-project-name]"** → Check all backlog items and ensure they have proper clickable links to detail files

**"clean permalinks [os-project-name]"** → Identify and report files with incorrect permalink structures (trainer-day/projects vs trainer-day/os-projects)

**"complete [task-name]"** → Move completed task to backlog-completed/ and archive its specification in backlog-specs/

When talking about testing review this document
trainer-day/system/workflows/automated-development/testing-process

## Permalink Fix Process - 2025-07-01

### Issue Identified
Basic Memory is storing incorrect permalinks in its database that start with `projects/trainer-day/trainer-day/` instead of just `trainer-day/`. When Basic Memory syncs, it reverts the files back to these incorrect permalinks.

### Files Found with Incorrect Permalinks
1. `trainer-day/system/troubleshooting/permalink-cleanup-cycling-calculators.md`
   - Had: `projects/trainer-day/trainer-day/system/troubleshooting/permalink-cleanup-cycling-calculators`
   - Should be: `trainer-day/system/troubleshooting/permalink-cleanup-cycling-calculators`

2. `trainer-day/templates/backlog-detail.md`
   - Had: `projects/trainer-day/trainer-day/templates/backlog-detail`
   - Should be: `trainer-day/templates/backlog-detail`

3. `trainer-day/templates/README.md`
   - Had: `projects/trainer-day/trainer-day/templates/readme`
   - Should be: `trainer-day/templates/readme`

4. `trainer-day/system/workflows/README.md`
   - Had: `projects/trainer-day/trainer-day/system/workflows/readme`
   - Should be: `trainer-day/system/workflows/readme`

5. `trainer-day/system/workflows/automated-development/3-testing-process.md`
   - Had incorrect permalink with `projects/trainer-day/trainer-day/` prefix

### Scripts Created

#### 1. Fix Permalinks Script (`/Users/alex/Documents/Projects/fix_permalinks.py`)
```python
#!/usr/bin/env python3
"""
Fix permalinks in markdown files that incorrectly start with 'projects/trainer-day/trainer-day'
and update them to start with just 'trainer-day'
"""

import os
import re
from pathlib import Path

def fix_permalinks(root_dir):
    """
    Walk through all markdown files and fix incorrect permalinks
    """
    root_path = Path(root_dir)
    fixed_files = []
    
    # Pattern to match permalinks starting with projects/trainer-day/trainer-day
    permalink_pattern = re.compile(r'^permalink:\s*projects/trainer-day/trainer-day/(.*)$', re.MULTILINE)
    
    for md_file in root_path.rglob('*.md'):
        try:
            with open(md_file, 'r', encoding='utf-8') as f:
                content = f.read()
            
            # Check if file contains the incorrect permalink pattern
            if permalink_pattern.search(content):
                # Replace the incorrect pattern
                new_content = permalink_pattern.sub(r'permalink: trainer-day/\1', content)
                
                # Write the fixed content back
                with open(md_file, 'w', encoding='utf-8') as f:
                    f.write(new_content)
                
                fixed_files.append(str(md_file.relative_to(root_path)))
                print(f"Fixed: {md_file.relative_to(root_path)}")
        
        except Exception as e:
            print(f"Error processing {md_file}: {e}")
    
    return fixed_files

def main():
    # Path to the TrainerDay project
    project_root = "/Users/alex/Documents/bm-projects/TrainerDay"
    
    print(f"Searching for incorrect permalinks in: {project_root}")
    print("-" * 60)
    
    fixed_files = fix_permalinks(project_root)
    
    print("-" * 60)
    if fixed_files:
        print(f"\nFixed {len(fixed_files)} files:")
        for file in sorted(fixed_files):
            print(f"  - {file}")
    else:
        print("\nNo files with incorrect permalinks found.")

if __name__ == "__main__":
    main()
```

#### 2. Comprehensive Permalink Check Script (`/Users/alex/Documents/Projects/comprehensive_permalink_check.py`)
```python
#!/usr/bin/env python3
"""
Comprehensive check for any permalink issues in all markdown files
"""

import os
import re
from pathlib import Path

def check_all_permalinks(root_dir):
    """
    Recursively check ALL markdown files for permalink issues
    """
    root_path = Path(root_dir)
    total_files = 0
    files_with_permalinks = 0
    problematic_files = []
    
    # Patterns to check for
    problems = [
        (re.compile(r'^permalink:\s*projects/trainer-day/trainer-day/.*$', re.MULTILINE), 
         'projects/trainer-day/trainer-day/'),
        (re.compile(r'^permalink:\s*project/trainer-day/trainer-day/.*$', re.MULTILINE), 
         'project/trainer-day/trainer-day/'),
        (re.compile(r'^permalink:\s*projects/trainer-day/.*$', re.MULTILINE), 
         'projects/trainer-day/'),
        (re.compile(r'^permalink:\s*project/trainer-day/.*$', re.MULTILINE), 
         'project/trainer-day/'),
    ]
    
    print("Recursively checking all .md files...")
    print("-" * 80)
    
    for md_file in root_path.rglob('*.md'):
        total_files += 1
        try:
            with open(md_file, 'r', encoding='utf-8') as f:
                content = f.read()
            
            # Check if file has a permalink
            if re.search(r'^permalink:', content, re.MULTILINE):
                files_with_permalinks += 1
            
            # Check for problematic patterns
            for pattern, problem_desc in problems:
                if pattern.search(content):
                    match = pattern.search(content)
                    problematic_files.append({
                        'file': str(md_file.relative_to(root_path)),
                        'issue': problem_desc,
                        'line': match.group(0)
                    })
                    
        except Exception as e:
            print(f"Error reading {md_file}: {e}")
    
    return total_files, files_with_permalinks, problematic_files

def main():
    project_root = "/Users/alex/MyGoogleDrive/notes-basic-memory/Projects/TrainerDay"
    
    print(f"Comprehensive permalink check in: {project_root}")
    print("=" * 80)
    
    total, with_permalinks, problems = check_all_permalinks(project_root)
    
    print(f"\nScan complete!")
    print(f"Total .md files scanned: {total}")
    print(f"Files with permalinks: {with_permalinks}")
    print(f"Files with issues: {len(problems)}")
    
    if problems:
        print("\n" + "=" * 80)
        print("❌ PROBLEMS FOUND:")
        print("-" * 80)
        for problem in problems:
            print(f"\nFile: {problem['file']}")
            print(f"Issue: Contains '{problem['issue']}'")
            print(f"Line: {problem['line']}")
    else:
        print("\n" + "=" * 80)
        print("✅ ALL PERMALINKS ARE CORRECT!")
        print("No files found with problematic permalink patterns.")

if __name__ == "__main__":
    main()
```

### Solution Required
The issue is that Basic Memory's database has the incorrect permalinks stored. When Basic Memory syncs, it overwrites the corrected permalinks in the files with the incorrect ones from its database.

**To fix this permanently:**
1. Stop Basic Memory server
2. Run the fix_permalinks.py script to correct all permalinks in the files
3. Restart Basic Memory server so it reads the corrected permalinks from the files and updates its database
4. The permalinks should then stay correct

### Additional Notes
- Found 34 relative backlog links in kanban board files (e.g., `../backlogs/filename.md`) - these are working correctly and don't need to be changed
- All markdown links appear to be using correct paths (no `projects/trainer-day/trainer-day` found in links)
- Total of 67 markdown files were scanned in the TrainerDay project