---
title: INSTRUCTIONS
type: note
permalink: claude-code-os/instructions
---

## Load Claude Code OS
Read: `claude-code-os/templates/`, `claude-code-os/knowledge-base/`, `claude-code-os/system/`

Do not load: `claude-code-os/os-projects/`

Respond with to loading with:
Please do not respond with any details other than "OS Loaded" and asking to load or create os-project. Type "command list" to get a list of commands

## Terminology
**"project"** = Current codebase/repository you're working in (standard development terminology)
**"os-project"** = Claude Code OS project structure (backlog, flow, specs, etc.) - stored in `claude-code-os/os-projects/`

When working with Claude Code on development tasks, "project" refers to the current codebase. Use "os-project" commands only for Claude Code OS management tasks.

## CRITICAL: Process Compliance
It is VERY, VERY, VERY important to follow the steps defined in this Claude Code Operating System. If Claude Code sees we are not following the documented processes, always pause what you are doing and let me know.

**CRITICAL PATH STRUCTURE**: Always use `claude-code-os/os-projects/[name]` never `claude-code-os/projects/[name]` - the correct folder is `os-projects` not `projects`.

CRITICAL - When creating a spec or appending a spec to an existing note always read this claude-code-os/system/workflows/automated-development/1-spec-process and follow it closely

## Commands
**"open os-project [os-project-name]"** → Load `claude-code-os/os-projects/[os-project-name]/`
**"load os-project [os-project-name]"** → Load `claude-code-os/os-projects/[os-project-name]/`

**"create os-project [os-project-name]"** → Use `claude-code-os/templates/create-new-os-project.md`

**"create backlog [os-project-name] [brief-description]"** → Add item to `claude-code-os/os-projects/[os-project-name]/flow/1-backlog.md` using format: `- [brief-description]`

**"create backlog details [task-name]"** → Use `claude-code-os/templates/backlog-detail.md`

**"move [task-name] to next"** → Find task in current flow step and move to the next step in sequence (1-backlog → 2-next → 3-in-progress → 4-code-complete → 5-staging → 6-testing → 7-test-results → 8-approved)

**"move [task-name] backlog to next"** → Move task from `claude-code-os/os-projects/[current-os-project]/flow/1-backlog.md` to `claude-code-os/os-projects/[current-os-project]/flow/2-next.md`

**"process dev queue"** → See `claude-code-os/system/workflows/automated-development/0-queue-processing.md`

**"push to stage"** → Deploy current code to staging server: `git push dokku main`

**"push to prod"** → Deploy current code to production server: `git push dokku-prod main`

**"command list"** → Show this list of commands

**"fix backlog links [os-project-name]"** → Check all backlog items and ensure they have proper clickable links to detail files

**"clean permalinks [os-project-name]"** → Identify and report files with incorrect permalink structures (claude-code-os/projects vs claude-code-os/os-projects)

**"complete [task-name]"** → Move completed task to backlog-completed/ and archive its specification in backlog-specs/

When talking about testing review this document
claude-code-os/system/workflows/automated-development/testing-process

