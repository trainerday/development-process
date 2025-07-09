---
title: Periodization function for ai plan generation   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/Periodization Function for AI Plan Generation - Spec
---

# Periodization Function for AI Plan Generation - Requirements

## Current State

Coach Jack needs an intelligent periodization system that can automatically determine optimal plan length, recovery patterns (2/1 vs 3/1), and block sequencing based on user goals, timeline, and preferences.

## Desired Outcome  

**Primary Goals:**
1. LLM-powered determination of optimal periodization approach for each user
2. Automatic plan length calculation based on goals and constraints  
3. Intelligent block sequencing and length optimization
4. Integration with user preferences and training history

**User Experience:** Users receive perfectly timed training plans that progress logically toward their goals with appropriate periodization for their specific situation.

## Interaction Mechanism

**Periodization Determination:**
- LLM analysis of user goals, timeline, and experience
- Automatic selection between 2/1 and 3/1 recovery patterns
- Total plan length optimization (up to 52 weeks)
- Block type and sequence planning

**Block Structure:**
- **Base Phase**: 8-16 weeks depending on user needs
- **Build Phase**: 8-12 weeks for specific adaptations  
- **Peak Phase**: 4-12 weeks for event preparation
- **Transition**: 1-2 weeks for recovery and planning

**Block Length Options:**
- **3/1 Recovery**: 4 or 8-week blocks
- **2/1 Recovery**: 3, 6, or 9-week blocks
- Dynamic adjustment based on user response and progress

## Special Requirements

**Algorithm Logic:**
- Goal-driven periodization selection
- User experience and training history consideration
- Seasonal timing and event calendar integration
- Recovery capacity and lifestyle factor analysis

**Plan Output Format:**
```
Plan Length: 40 Weeks (ends 7/1/2024)
Blocks: Builder (Base 8w), Jump Start (Base 8w), Sweet Spot Focus (Build 8w), 
        Race Prep (Build 4w), Peak Power (Peak 8w), Final Prep (Peak 4w)
Personal Tags: [Experience: Intermediate], [Goal: Century], [Recovery: Normal]
Goal Tags: [Event: Endurance], [Timeline: 40 weeks], [Phase: Full Build]
Other Tags: [Equipment: Smart Trainer], [Availability: 6h/week]
```

**Visual Presentation:**
- Tabbed interface showing each block
- Example workouts for each training phase
- Calendar view with 8-week block structure
- Progress milestones and checkpoints

## Special Requirements

**LLM Integration:**
- Intelligent analysis of user data for periodization decisions
- Natural language explanation of periodization rationale
- Adaptive recommendations based on user feedback
- Integration with goal evaluation and constraint analysis

**Technical Implementation:**
- Mathematical optimization for block sequencing
- Integration with existing Coach Jack workout library
- Real-time plan adjustment capabilities
- Performance tracking and adaptation algorithms

**Validation and Testing:**
- Coach review of periodization decisions
- User outcome tracking and satisfaction
- A/B testing of different periodization approaches
- Continuous refinement based on results

## Additional Context

**Reference:** Trello card GAK8GiA8 "Periodization Function"

**Example Scenarios:**
- 40-week plan: Base 8 + Base 8 + Build 8 + Build 4 + Peak 8 + Peak 4
- Century preparation with 6 months lead time
- Off-season base building with spring race focus
- Multi-peak season with several target events

**Integration Points:**
- User goal and timeline input
- Training history and fitness assessment
- Event calendar and seasonal considerations
- Recovery pattern preferences and capabilities