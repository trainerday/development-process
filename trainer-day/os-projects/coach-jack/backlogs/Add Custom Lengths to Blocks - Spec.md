---
title: Add Custom Lengths to Blocks - Spec
type: note
permalink: trainer-day/os-projects/coach-jack/backlogs/add-custom-lengths-to-blocks-spec
---

# Add Custom Lengths to Blocks - Requirements

## Current State

Coach Jack currently uses fixed default block lengths (4 or 8 weeks for 3/1 recovery, 3, 6, or 9 weeks for 2/1 recovery). Users cannot customize these lengths to fit their specific training needs or schedules.

## Desired Outcome  

**Primary Goals:**
1. Allow users to override default block lengths while maintaining minimum and maximum constraints
2. Provide flexibility for users with specific event dates or training preferences
3. Maintain system defaults as starting points

**User Experience:** Users can customize block lengths within reasonable bounds (minimum 4 weeks, maximum 16 weeks) while receiving guidance on optimal durations.

## Interaction Mechanism

**Default Settings:**
- Display current default lengths as pre-selected options
- Show recommended ranges for different training phases

**Customization Interface:**
- Slider or input controls for each block type (Base, Build, Peak)
- Real-time validation of minimum (4 weeks) and maximum (16 weeks) constraints
- Visual feedback when approaching limits

**Event-Based Constraints:**
- When event date is specified, automatically calculate total available weeks
- Adjust maximum allowable block lengths to fit timeline
- Provide warnings if desired lengths exceed available time

## Special Requirements

**Validation Rules:**
- Minimum block length: 4 weeks
- Maximum block length: 16 weeks
- Total plan must fit within event timeline when specified
- Maintain recovery week ratios (2/1 or 3/1)

**Default Preservation:**
- System defaults remain as recommended starting points
- User customizations saved for future plan creation
- Option to reset to system defaults

## Additional Context

**Reference:** Trello card gNklcUM2 "Add custom lengths to blocks"

**Implementation Considerations:**
- UI should clearly show the impact of custom lengths on total plan duration
- Validation should prevent impossible combinations (e.g., event in 8 weeks but requesting 12-week blocks)
- Consider progressive disclosure - show defaults first, allow advanced customization on demand