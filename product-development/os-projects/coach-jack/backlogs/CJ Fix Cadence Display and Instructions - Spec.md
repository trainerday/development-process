---
title: CJ Fix cadence display and instructions   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/CJ Fix Cadence Display and Instructions - Spec
---

# CJ Fix Cadence Display and Instructions - Requirements

## Current State

Coach Jack workouts display "CAD" (cadence) indicators in the title and description even when the workout is too short to include actual cadence drills. This creates confusion for users who expect cadence work that never appears.

Additionally, when cadence work does exist, users receive no advance warning or guidance about when cadence intervals will occur during the workout.

## Desired Outcome  

**Primary Goals:**
1. **Conditional Cadence Display**: Remove "CAD" indicators from workout titles and descriptions when no actual cadence work exists in the workout
2. **Pre-workout Instructions**: Display a popup after 20 seconds showing when cadence intervals will occur during the workout
3. **Pre-interval Warnings**: Show a message 5 seconds before each cadence interval begins to prepare the user

**User Experience:** Users should have clear expectations about cadence work and receive timely guidance when it occurs.

## Interaction Mechanism

**Pre-workout Popup (after 20 seconds):**
- Display summary of all cadence intervals in the workout
- Show timing and duration of each cadence segment
- Allow user to dismiss the popup

**Pre-interval Warning (5 seconds before):**
- Brief overlay message: "Cadence drill starting in 5 seconds"
- Include target cadence range if available
- Auto-dismiss after interval begins

**Workout Metadata:**
- Only include "CAD" in titles/descriptions when actual cadence targets exist
- Scan workout structure to detect presence of cadence intervals

## Special Requirements

**Cadence Detection Logic:**
- Maximum of 1 cadence target every 5 minutes
- Total maximum of 12 cadence targets per workout
- Only flag workouts with actual cadence programming

**Performance Considerations:**
- Popup should not interfere with workout start
- Messages should be clearly visible but non-intrusive
- Pre-interval warnings must be precisely timed

## Additional Context

**Reference:** Trello card mllrZeN4 "CJ - Fix Cadence... and give instructions"

**Problem Examples:**
- Short workouts showing "CAD" with no actual cadence work
- "Collywobbles" workout having excessive cadence targets when extended
- Users caught off-guard by unexpected cadence intervals

**Implementation Notes:**
- Add interval descriptions to workout metadata
- Implement timing system for pre-workout and pre-interval notifications
- Create cadence detection algorithm for workout validation