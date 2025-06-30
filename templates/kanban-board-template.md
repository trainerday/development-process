---
title: kanban-board-template
type: note
permalink: claude-code-os/templates/kanban-board-template
---

# Kanban Board Template

This template creates an Obsidian Kanban board for OS project workflow management.

## Template Content
```
---
kanban-plugin: board
permalink: [os-project-name]/kanban-board
---
## backlog
## next
## in process
## dev complete
## on stage
## on production
%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[false,false,false,false,false,false]}
```
%%
```

## Usage
When creating a new OS project, this template will be used to generate `kanban-board.md` in the project root with the correct permalink based on the project name.