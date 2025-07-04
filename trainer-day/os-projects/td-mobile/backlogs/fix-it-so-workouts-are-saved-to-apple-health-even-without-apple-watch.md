---
title: fix-it-so-workouts-are-saved-to-apple-health-even-without-apple-watch
type: note
permalink: trainer-day/os-projects/td-mobile/backlogs/fix-it-so-workouts-are-saved-to-apple-health-even-without-apple-watch
---

# Fix It So Workouts Are Saved to Apple Health Even Without Apple Watch

## Overview
Currently workouts may not be saving to Apple Health properly when no Apple Watch is present. This needs to be fixed to ensure all workouts are recorded in Apple Health.

## Priority
Medium

## Labels
- Apple Health
- iOS
- Integration
- Bug

## Description
Workouts should be saved to Apple Health even when the user doesn't have an Apple Watch connected. May need a separate setting for this functionality.

## Acceptance Criteria
- [ ] Investigate current Apple Health integration
- [ ] Identify why workouts aren't saving without Apple Watch
- [ ] Fix Apple Health saving for non-Apple Watch workouts
- [ ] Consider adding separate setting for this feature
- [ ] Test thoroughly to avoid previous errors
- [ ] Ensure proper permissions are requested
- [ ] Verify workout data is correctly formatted for Apple Health

## Technical Notes
- Previous implementation had lots of errors, so need to be careful
- May need separate setting to control this behavior
- Should test on devices without Apple Watch

## Related Links
- Trello Card ID: #26