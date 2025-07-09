---
title: Make Micro Sprints Optional - Spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/make-micro-sprints-optional-spec
---

# Make Micro Sprints Optional - Requirements

## Current State

Coach Jack workouts automatically include micro sprints in many sessions. Some users prefer to focus solely on the primary training stimulus without additional neuromuscular work, especially during endurance-focused periods.

## Desired Outcome  

**Primary Goals:**
1. Make micro sprints an optional component that users can enable/disable
2. Provide clear information about the benefits of micro sprint work
3. Allow customization at workout or plan level

**User Experience:** Users have control over whether their workouts include micro sprints, with clear guidance about when they're most beneficial.

## Interaction Mechanism

**Settings Interface:**
- Global toggle for micro sprints (on/off)
- Per-workout override option
- Clear explanation of micro sprint benefits

**Information Display:**
- Tooltip or help text explaining micro sprint purpose
- Warning about reduced neuromuscular training when disabled
- Guidance on when micro sprints are most valuable

**Workout Adaptation:**
- Seamless removal of micro sprint intervals when disabled
- Maintain core workout structure and timing
- Optional replacement with recovery or extended main work

## Special Requirements

**User Education:**
- Explain that micro sprints maintain neuromuscular power
- Clarify that they don't significantly impact endurance adaptations
- Provide guidance on when to include vs exclude them

**Workout Integrity:**
- Removing micro sprints shouldn't break workout flow
- Maintain total workout duration or provide clear time adjustments
- Preserve primary training objectives

**Default Behavior:**
- New users should default to including micro sprints
- Advanced users can make informed decisions to exclude them
- Consider training phase recommendations (base vs build vs peak)

## Additional Context

**Reference:** Trello card 91mECl7J "Make Micro Sprints optional"

**Training Rationale:**
- Micro sprints maintain neuromuscular power during base periods
- Some athletes prefer pure aerobic focus
- Elite athletes may have separate neuromuscular training
- Recovery-focused periods may benefit from simplified workouts

**Implementation Considerations:**
- Settings persistence across sessions
- Integration with existing workout customization
- A/B testing to understand user preferences
- Impact on workout library organization