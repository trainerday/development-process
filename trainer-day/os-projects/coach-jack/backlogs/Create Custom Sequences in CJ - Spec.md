---
title: Create Custom Sequences in CJ - Spec
type: note
permalink: trainer-day/os-projects/coach-jack/backlogs/create-custom-sequences-in-cj-spec
---

# Create Custom Sequences in CJ - Requirements

## Current State

Coach Jack currently uses predefined workout sequences and progressions. Users cannot create custom interval sequences or modify existing workout structures to match their specific training needs or preferences.

## Desired Outcome  

**Primary Goals:**
1. Enable users to create custom interval sequences within Coach Jack
2. Provide intuitive interface for building complex workout structures
3. Integrate custom sequences with existing periodization and progression systems

**User Experience:** Advanced users can build personalized workouts while maintaining the benefits of Coach Jack's periodization and adaptive features.

## Interaction Mechanism

**Sequence Builder Interface:**
- Drag-and-drop interval builder
- Pre-defined interval templates (sweet spot, VO2, recovery, etc.)
- Real-time workout preview and duration calculation

**AI-Assisted Creation:**
- ChatGPT-style interface for describing desired workouts
- Natural language processing to convert descriptions to sequences
- Suggestions for optimal interval structures

**Library Integration:**
- Save custom sequences for reuse
- Share sequences with community (future feature)
- Integration with existing workout library

## Special Requirements

**Workout Validation:**
- Ensure physiologically sound interval structures
- Warning system for potentially harmful combinations
- Power/heart rate zone validation

**Progressive Integration:**
- Custom sequences should work with difficulty progression
- Adaptive features should apply to custom workouts
- Integration with periodization calendar

**Technical Constraints:**
- Compatible with existing workout file formats
- Exportable to .mrc, .zwo, and other formats
- Maintains Coach Jack's adaptive capabilities

## Additional Context

**Reference:** Trello card JLkGDLBw "Future: Create custom sequences in CJ"

**AI Integration Example:**
User input: "Create a 60-minute workout with 4x8 minute sweet spot intervals"
AI output: Structured workout with appropriate warm-up, intervals, recovery, and cool-down

**Implementation Phases:**
1. Basic sequence builder with predefined components
2. AI-assisted workout generation
3. Community sharing and workout library expansion
4. Advanced customization and scripting features

**Training Applications:**
- Race-specific interval training
- Specialty workout creation
- Rehabilitation and return-to-training progressions
- Event simulation workouts