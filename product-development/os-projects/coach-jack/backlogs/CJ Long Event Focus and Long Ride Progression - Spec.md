---
title: CJ Long event focus and long ride progression   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/CJ Long Event Focus and Long Ride Progression - Spec
---

# CJ Long Event Focus and Long Ride Progression - Requirements

## Current State

Coach Jack currently doesn't have specific functionality to help users prepare for long endurance events. The long ride progression is generic and doesn't scale appropriately based on target event duration.

## Desired Outcome  

**Primary Goals:**
1. Allow users to specify a target long event (distance/duration)
2. Build long ride progression that peaks at 50% of the target event duration
3. Provide event-specific training adaptations

**User Experience:** Users training for long events (centuries, gran fondos, multi-day tours) receive progressively longer rides that prepare them appropriately without overreaching.

## Interaction Mechanism

**Event Specification:**
- Input field for target event distance or duration
- Event type selection (century, gran fondo, multi-day, etc.)
- Target event date

**Long Ride Progression:**
- Progressive build starting from current fitness level
- Peak long rides at 50% of target event duration
- Appropriate tapering before event date

**Adaptive Scheduling:**
- Long rides scheduled based on weekly training availability
- Integration with overall periodization plan
- Recovery considerations after long efforts

## Special Requirements

**Progression Logic:**
- Start from user's current long ride capability
- Gradual increase (typically 10-15% per week)
- Peak at 50% of target event duration
- Include plateau periods and step-backs for adaptation

**Event Types:**
- Century rides (100 miles / 160km)
- Gran fondos (variable distances)
- Multi-day tours (consecutive long days)
- Ultra-endurance events (200+ miles)

**Safety Considerations:**
- Cap maximum single ride duration
- Ensure adequate recovery between long efforts
- Consider user's experience level and fitness

## Additional Context

**Reference:** Trello card bvmOW4Ej "CJ - Add the ability to focus on a specific long event and make the long ride build up to 50% of that long ride"

**Training Philosophy:**
- 50% rule prevents overreaching while building endurance
- Long rides should be aerobic base-building efforts
- Focus on fueling, pacing, and endurance rather than intensity

**Implementation Notes:**
- Need algorithm to calculate optimal progression
- Integration with existing Coach Jack periodization
- Consider seasonal timing and weather factors