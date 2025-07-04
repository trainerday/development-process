---
title: Set all duplicate workouts to private
type: note
permalink: trainer-day/os-projects/td-web/backlogs/set-all-duplicate-workouts-to-private
tags:
- '["feature"'
- '"maintenance"'
- '"workouts"'
- '"later"'
- '"backlog"]'
---

# Set all duplicate workouts to private (exact same power segments)

## Status
- **Priority**: Later
- **Type**: Feature/Maintenance
- **Labels**: Data Cleanup, Feature
- **Created**: 2025-01-03
- **Updated**: 2025-01-03

## Description
Implement functionality to identify and set all duplicate workouts to private. Duplicates are defined as workouts with exact same power segments.

## Details
- Has detailed discussion about implementation
- Duplicate workouts clutter the public workout library
- Duplicates defined by identical power segment sequences
- Need to preserve the original public workout
- Consider which workout to keep public (oldest, most used, etc.)

## Technical Notes
- Develop algorithm to compare workout power segments
- Consider segment duration, power values, and sequence
- Handle edge cases (warmup/cooldown variations)
- Batch processing for existing workout database
- Performance considerations for large datasets
- Create audit trail of changes made

## Acceptance Criteria
- [ ] Algorithm accurately identifies duplicate workouts
- [ ] System preserves one public version of each unique workout
- [ ] Private workouts remain accessible to their creators
- [ ] Batch process can handle entire workout database
- [ ] Admin interface to review and manage duplicates
- [ ] Rollback capability in case of issues
- [ ] Report generated showing duplicates found and actions taken

## Resources
- Detailed discussion thread about duplicate handling
- Workout database schema
- Power segment comparison logic

## Notes
- Consider user preferences for which workout stays public
- May need to notify users whose workouts are made private
- Could be run as periodic maintenance task
- Consider fuzzy matching for "nearly identical" workouts