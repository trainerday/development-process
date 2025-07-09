---
title: User attributes data collection system   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/User Attributes Data Collection System - Spec
---

# User Attributes Data Collection System - Requirements

## Current State

Coach Jack currently collects basic user information through traditional questions. For AI-powered plan generation, a comprehensive user attribute collection system is needed that captures all relevant training, lifestyle, and preference data.

## Desired Outcome  

**Primary Goals:**
1. Comprehensive data collection covering all user attributes affecting training
2. LLM-powered extraction of missing information through natural conversation
3. Integration with Strava and other data sources to auto-populate known attributes
4. Progressive data collection that improves over time

**User Experience:** Seamless data collection that feels natural and comprehensive without being overwhelming, with smart defaults and automatic population from available sources.

## Interaction Mechanism

**Data Categories:**

**Goal and Timeline:**
- Primary goals and target events
- Event dates and specific requirements
- Priority ranking of multiple goals

**Scheduling and Location:**
- Available training days and times
- Geographic location and climate considerations
- Travel and schedule constraints

**Health Factors:**
- Current recovery status and sleep patterns
- Injury history and limitations
- Age-related recovery considerations
- Estimated recovery speed and health status

**Training Status:**
- Last 8 weeks training phase and consistency
- Current fitness level and burnout indicators
- Training history and experience level
- Equipment available (trainer types, power meters, etc.)

**Training Preferences:**
- Desired intensity levels and progression style
- Indoor vs outdoor preferences
- Periodization preferences (seasonal, event-focused, etc.)
- Recovery week preferences (2/1 vs 3/1 patterns)

## Special Requirements

**LLM Integration:**
- Intelligent questioning to fill data gaps
- Natural language processing of complex user descriptions
- Context-aware follow-up questions
- Validation of collected information

**Data Source Integration:**
- Strava data import for training history
- Equipment detection and validation
- Calendar integration for scheduling constraints
- Health app integration where available

**Progressive Enhancement:**
- Start with essential data for basic plans
- Collect additional details over time
- Learn from user behavior and plan effectiveness
- Adaptive questioning based on user responses

## Additional Context

**Reference:** Trello card XhDDGeNI "All User Attributes to capture"

**Additional Factors:**
- Commuting impact on training
- Sleep quality and patterns
- Life stress and other commitments
- Nutrition and hydration awareness
- Previous coaching experience

**Implementation Strategy:**
- Prioritize attributes by impact on plan quality
- Balance comprehensiveness with user experience
- Provide value immediately while collecting more data
- Use AI to infer attributes from limited data