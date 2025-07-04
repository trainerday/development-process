---
title: Plan Matching Algorithm with User and Plan Tags - Spec
type: note
permalink: trainer-day/os-projects/coach-jack/backlogs/plan-matching-algorithm-with-user-and-plan-tags-spec
---

# Plan Matching Algorithm with User and Plan Tags - Requirements

## Current State

Coach Jack currently uses rule-based plan selection. For AI-powered personalization, a sophisticated tag-matching system is needed that compares user characteristics with plan metadata to find optimal training matches.

## Desired Outcome  

**Primary Goals:**
1. Implement tag-based plan matching using cosine similarity algorithms
2. Create comprehensive plan tag database with expert-assigned metadata
3. Enable weighted category matching (Goals > Preferences)
4. Provide transparent similarity scoring and explanations

**User Experience:** Users receive highly personalized plan recommendations with clear explanations of why plans match their specific needs, goals, and constraints.

## Interaction Mechanism

**Tag Matching Process:**
- User tags generated from LLM questionnaire analysis
- Plan tags manually assigned by domain experts (coaches)
- Vector similarity calculation between user and plan tags
- Category weighting for prioritized matching

**Similarity Scoring:**
- Overall match score (0.0 to 1.0)
- Category breakdown scores (Goals, Experience, Style, Constraints)
- Ranked recommendations with explanations
- Fallback options for edge cases

**Plan Metadata:**
- Training phase focus (Base, Build, Peak, Recovery)
- Intensity distribution and workout types
- Time requirements and flexibility
- Equipment needs and constraints
- Experience level requirements

## Special Requirements

**Algorithm Implementation:**
- Cosine similarity calculation for tag vectors
- Weighted scoring by category importance
- Handling of missing or incomplete tag data
- Performance optimization for large plan libraries

**Plan Database:**
- Expert curation of plan tags by certified coaches
- Standardized tag vocabulary and definitions
- Version control for plan metadata
- Quality assurance and validation processes

**Hard Constraints:**
- Medical restrictions (low intensity only)
- Equipment limitations
- Time availability constraints
- Experience level safety requirements

## Additional Context

**Reference:** Trello card P6VCXp1J "Plan Match - User Tags vs Plan Tags"

**Matching Categories:**
- **Goals** (highest weight): Event preparation, fitness improvement, weight loss
- **Experience**: Training history, current fitness level, coaching experience
- **Style**: Intensity preferences, indoor/outdoor, workout variety
- **Constraints**: Time, equipment, health limitations, schedule

**Quality Assurance:**
- A/B testing of matching algorithms
- User feedback on plan recommendations
- Coach review of tag assignments
- Continuous refinement based on outcomes

**Technical Architecture:**
- Scalable vector database for plan storage
- Real-time similarity calculation
- Caching for improved performance
- Integration with existing Coach Jack infrastructure