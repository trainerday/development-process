---
title: cadence-problem
type: backlog_item
permalink: product-development/os-projects/td-web/backlogs/cadence-problem
---

# Cadence problem

## Description
While creating a workout, the "Reps" function doesn't recognize the cadence properly and creates additional unwanted columns. This affects the workout creation experience and data accuracy.

## Details
- Original Trello List: Someday Bugs
- Import Date: 2025-01-03
- Priority: Low (Someday Bugs)
- Status: Pending
- Type: Bug

## Problem Details
When users are creating workouts and using the "Reps" feature, the system fails to properly recognize cadence input, resulting in:
- Extra columns being created
- Incorrect data structure
- Poor user experience during workout creation

## Technical Investigation Needed
- Review workout creation code, specifically the Reps handling
- Check cadence parsing logic
- Identify why additional columns are being generated
- Test with various cadence input formats

## Acceptance Criteria
- Cadence is properly recognized in the Reps section
- No extra columns are created
- Workout creation flows smoothly with correct data structure