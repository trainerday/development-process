---
title: Primary focus identification system   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/Primary Focus Identification System - Spec
---

# Primary Focus Identification System - Requirements

## Current State

Coach Jack creates comprehensive training plans but doesn't clearly identify the "one thing" users should focus on most to achieve their goals. Users can become overwhelmed by complex plans without understanding the key driver of their success.

## Desired Outcome  

**Primary Goals:**
1. Identify the single most important focus area for each user's goal achievement
2. Provide clear guidance on what drives training plan success
3. Simplify complex training concepts into actionable primary focus
4. Align all training recommendations around the identified primary focus

**User Experience:** Users have crystal-clear understanding of their #1 training priority, reducing overwhelm and increasing focus on what matters most for their specific goals.

## Interaction Mechanism

**Focus Identification Process:**
- Analysis of user goals, current fitness, and constraints
- Algorithm to determine highest-impact training focus
- Clear communication of the primary focus area
- Supporting explanation of why this focus is most important

**Potential Primary Focus Areas:**
- **Aerobic Base Building**: For new cyclists or those returning from breaks
- **FTP Development**: For performance-focused riders
- **Endurance Capacity**: For long-event preparation
- **Consistency Building**: For riders with sporadic training history
- **Recovery Optimization**: For overtrained or highly stressed users
- **Technical Skills**: For riders lacking fundamental cycling abilities

**Focus Communication:**
- Simple, clear language explaining the primary focus
- Visual emphasis in plan presentation
- Progress tracking specifically for the primary focus area
- Regular reinforcement of focus importance

## Special Requirements

**Assessment Integration:**
- Training data analysis from Strava or user input
- Goal alignment with focus selection
- Health and recovery status consideration
- Time availability and constraint analysis

**Dynamic Adjustment:**
- Primary focus can evolve as fitness improves
- Seasonal adjustments (base building in winter, specificity before events)
- Response to user feedback and progress
- Integration with plan adaptation system

**Evidence-Based Selection:**
- Algorithm based on coaching expertise and training science
- User survey data to validate focus selection accuracy
- A/B testing of different focus approaches
- Outcome tracking to refine focus selection

## Additional Context

**Reference:** Trello card SVk2KQYo "Evaluation-Primary Focus: Identify the 'one thing' the user should focus on most and ultimately what drives the goal or training plan the most"

**From Training Data Analysis:**
- Consistency patterns and gaps
- Training volume and intensity distribution
- Aerobic base development status
- Power curve weaknesses
- Pacing and execution abilities

**From User Input Assessment:**
- Perceived personal weaknesses
- Training enjoyment factors
- Recovery levels and sleep quality
- Lifestyle stress and constraints
- Equipment and terrain access

**Implementation Strategy:**
- Start with evidence-based algorithm
- Gather user feedback on focus accuracy
- Refine selection criteria based on outcomes
- Integrate with existing Coach Jack infrastructure