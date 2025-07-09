---
title: CJ Reduce excessive cadence targets   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/CJ Reduce Excessive Cadence Targets - Spec
---

# CJ Reduce Excessive Cadence Targets - Requirements

## Current State

Some Coach Jack workouts, particularly longer versions like "Collywobbles," contain too many cadence targets (one or more per minute in some cases). This creates excessive complexity and distraction during hard workouts.

## Desired Outcome  

**Primary Goals:**
1. Limit cadence targets to maximum 1 every 5 minutes
2. Cap total cadence targets at 12 per workout maximum
3. Maintain cadence training benefits while reducing complexity

**User Experience:** Workouts feel more manageable with strategically placed cadence work that enhances rather than overwhelms the primary training stimulus.

## Interaction Mechanism

**Cadence Target Algorithm:**
- Automatically space cadence targets with minimum 5-minute gaps
- Prioritize placement during easier portions of workouts
- Remove excessive targets while preserving training intent

**Workout Analysis:**
- Scan existing workouts for cadence target density
- Identify workouts exceeding guidelines (>12 targets or <5min spacing)
- Apply reduction algorithm while maintaining workout structure

**Quality Over Quantity:**
- Focus cadence work on key intervals rather than continuous drilling
- Align cadence targets with workout objectives (endurance vs intensity)
- Preserve neuromuscular training benefits

## Special Requirements

**Reduction Rules:**
- Maximum 1 cadence target per 5-minute period
- Total workout limit of 12 cadence targets
- Preserve targets during primary work intervals when possible

**Workout Priority:**
- Hard workouts get fewer cadence targets to maintain focus
- Easy/recovery workouts can accommodate more cadence work
- Interval workouts prioritize power/intensity over cadence

**Existing Workout Updates:**
- Audit current workout library for violations
- Update "Collywobbles" and other problematic workouts
- Test updated workouts for training effectiveness

## Additional Context

**Reference:** Trello card UioJk6wL "CJ - Too many cadence targets"

**Problem Example:**
- "Collywobbles" workout when extended has excessive cadence targets
- Creates distraction during already challenging intervals
- Reduces focus on primary training stimulus

**Training Philosophy:**
- Cadence work should complement, not compete with main workout goals
- Quality cadence training beats quantity
- Simplicity improves workout execution and user satisfaction

**Implementation Approach:**
- Create cadence placement algorithm
- Batch update existing workouts
- Monitor user feedback on updated workouts