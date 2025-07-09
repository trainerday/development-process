---
title: Individualized Difficulty Score IDS System - Spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/individualized-difficulty-score-ids-system-spec
---

# Individualized Difficulty Score (IDS) System - Requirements

## Current State

Coach Jack uses generic difficulty progressions that don't account for individual preferences and capabilities. A more sophisticated system is needed that considers rider preference factors and provides truly personalized difficulty scoring.

## Desired Outcome  

**Primary Goals:**
1. Implement Individualized Difficulty Score (IDS) system for workouts
2. Account for rider preference factors (RPF) in difficulty calculations
3. Provide personalized workout recommendations based on individual scoring
4. Create user tags for difficulty preferences and capabilities

**User Experience:** Workouts feel appropriately challenging and engaging based on individual preferences for steady efforts vs variable intensity, with clear difficulty progression that matches personal capabilities.

## Interaction Mechanism

**IDS Calculation Factors:**
- Critical Power (CP) and W' (anaerobic capacity)
- Rider Preference Factor (RPF) scoring
- Comparison to main work intervals
- Overall workout structure analysis

**Rider Preference Factor (RPF) Scale:**
- **+1.0 The Pacer**: Loves long, steady, relentless pace efforts
- **+0.5 The Grinder**: Prefers sustained efforts, comfortable with steady rhythm
- **0.0 The All-Rounder**: Adaptable, no strong preference for effort style
- **-0.5 The Surger**: Feels engaged by repeated surges and pace changes
- **-1.0 The Attacker**: Thrives on sharp, high-power attacks and sprints

**Workout Assignment:**
- IDS ranges assigned to workout progressions
- Automatic difficulty adjustment based on user RPF
- Progressive difficulty scaling within comfort zone

## Special Requirements

**Calculation Engine:**
- JavaScript functions for IDS calculation
- Integration with existing workout metadata
- Real-time difficulty scoring for custom workouts

**User Assessment:**
- RPF determination through questionnaire or behavior analysis
- User tag creation for difficulty preferences
- Ongoing refinement based on workout feedback

**Workout Categorization:**
- Maximum of 12 cadence targets per workout
- Difficulty ranges for different training phases
- Compatibility with existing Coach Jack progressions

## Additional Context

**Reference:** Trello card EspaKhxt "USER_TAG: IDS - Individualized Difficulty Score for workouts"

**Google Sheets Reference:** Detailed scoring calculations and examples available in linked spreadsheet

**Implementation Components:**
- IDS calculation algorithm
- RPF assessment questionnaire
- Workout difficulty database
- User preference tracking
- Adaptive recommendation engine

**Training Applications:**
- Personalized workout selection
- Difficulty progression optimization
- User satisfaction improvement
- Reduced workout abandonment rates