---
title: CJ Ai update questions interface   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/CJ-AI Update Questions Interface - Spec
---

**GitHub Issue:** [#115 - Coach Jack - Update Questions Interface](https://github.com/trainerday/main-app-web/issues/115)
# CJ Questions Interface

## Current State

Coach Jack currently uses a traditional form-based question interface. Based on our analysis and prototyping, we've designed a hybrid approach that combines structured data collection with optional LLM enhancement questions.

## Final Design Decision

**Hybrid Approach:** Instead of a full ChatGPT-style interface, we've created a streamlined questionnaire with optional LLM enhancement questions that provides the best of both worlds:

1. **Fast Core Experience** - 9 essential structured questions for quick plan generation
2. **Optional Deep Personalization** - 8 additional LLM-processed questions for users who want maximum customization
3. **Progressive Disclosure** - Users can get basic recommendations quickly or provide extensive detail

## Question Structure

### Core Questions (9 Required)
1. **Main Training Goal** - Multiple choice with reordered priorities
2. **Self-Perception** - Cyclist identity and motivation
3. **Weekly Training Hours** - Current volume (0-20 hours slider)
4. **Longest Recent Ride** - Fitness assessment 
5. **Recovery Level** - Current energy state
6. **Maximum Weekly Hours** - Target capacity (0-25 hours slider)
7. **Training Intensity Preference** - 4 levels including "Insane pain" option
8. **Upcoming Event** - Yes/No with goal follow-up
9. **Health Limitations** - Constraints and injury considerations

### LLM Enhancement Questions (8 Optional, All Skippable)
10. **Event Details** - Comprehensive race/event information
11. **Additional Events** - Other races and general details
12. **Training Tools & Environment** - Equipment and indoor/outdoor preferences
13. **Recovery & Lifestyle** - Sleep, stress, work/life factors
14. **Training History & Context** - Recent focus and routine changes
15. **Social & Motivation Preferences** - Group vs solo, motivation factors
16. **Health & Wellness** - Broader health considerations
17. **Training Philosophy & Preferences** - Approach and past experiences

## User Experience Flow

**Question Display:**
- One question at a time with progress indicator
- Clean interface without technical question type labels
- Skip functionality only for LLM enhancement questions
- Dynamic follow-up questions based on responses


## Technical Implementation

**Live Prototypes:**
- **Questionnaire:** https://claude.ai/public/artifacts/9295a409-89be-4ddf-a7d7-5a1ed38e8e13
- **Profile Summary:** https://claude.ai/public/artifacts/7c3a4b2d-87f8-4d2d-9c2e-9f3c8b1a5e4f

**Mobile & Theme Requirements:**
- **Dark theme as primary** for TrainerDay app integration
- **Light theme support** for standalone web usage
- **Mobile-first design** with touch-optimized interactions
- **Web popup integration** for in-app questionnaire experience
- **Small screen optimization** with proper spacing and tap targets

**Data Schema Integration:**
- LLM enhancement questions designed to capture user tag schema requirements
- Covers profile preferences, health state, training context, recovery status, and rider preference factors
- Natural language processing extracts structured tags from free-form responses

**UI/UX Principles:**
- Removed question type indicators for cleaner experience
- Progressive disclosure maintains engagement
- Profile strength scoring encourages completion
- Mobile-first responsive design optimized for app integration
- Dark and light theme support with automatic theme switching
- Web popup integration for in-app experience
- Touch-friendly interface with proper tap targets
- Optimized for small screens and mobile interactions

## Implementation Benefits

**User Benefits:**
- **Fast Path:** 9 questions for quick plan generation
- **Comprehensive Path:** 17 questions for maximum personalization
- **Flexible:** Skip any optional questions while maintaining plan quality
- **Intuitive:** Clean, modern interface without technical jargon

**Technical Benefits:**
- **Structured Data:** Core questions provide reliable algorithm input
- **Rich Context:** LLM questions capture nuanced user preferences
- **Scalable:** Can add more optional questions without impacting core flow
- **Cost Effective:** Minimal LLM processing required for basic plans

## Next Steps

1. **Backend Integration** - Connect questionnaire to Coach Jack training block selection
2. **LLM Processing** - Implement tag extraction from enhancement questions
3. **Profile Management** - Build user profile editing and versioning
4. **Mobile Integration** - Implement within TrainerDay app
5. **Testing & Optimization** - User testing and conversion optimization