---
title: Bug - Calendar 2 workouts in a day
type: note
permalink: trainer-day/os-projects/td-web/backlogs/bug-calendar-2-workouts-in-a-day
tags:
- '["bug"'
- '"calendar"'
- '"later"'
- '"backlog"]'
---

# Bug - Calendar 2 workouts in a day

## Status
- **Priority**: Later
- **Type**: Bug
- **Labels**: Bug
- **Created**: 2025-01-03
- **Updated**: 2025-01-03

## Description
Issue with calendar displaying or handling 2 workouts scheduled on the same day.

## Details
- Forum link available describing the issue
- User reported problem with multiple workouts on same day
- Unclear if this is a display issue or functionality problem

## Technical Notes
- Check calendar component rendering logic
- Verify data model supports multiple workouts per day
- Review calendar event handling for overlapping workouts
- Test edge cases with 3+ workouts on same day

## Acceptance Criteria
- [ ] Calendar properly displays multiple workouts on the same day
- [ ] Users can schedule and manage multiple workouts per day
- [ ] UI clearly differentiates between multiple workouts
- [ ] No overlapping or display issues
- [ ] Performance remains acceptable with multiple workouts

## Resources
- Forum link with user report and discussion

## Notes
- May need to consider different views (day/week/month) separately
- Could impact workout scheduling logic
- Consider mobile vs desktop display differences