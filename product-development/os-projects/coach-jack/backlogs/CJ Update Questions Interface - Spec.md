---
title: CJ Update Questions Interface - Spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/cj-update-questions-interface-spec
---

# CJ Update Questions Interface - Requirements

## Current State

Coach Jack currently uses a traditional form-based question interface. The plan is to replace this with a more engaging, conversational ChatGPT-style interface that can handle both structured questions and open-text LLM responses.

## Desired Outcome  

**Primary Goals:**
1. Replace form-based questions with conversational chat interface
2. Integrate LLM open text questions with structured Coach Jack data collection
3. Maintain question history and allow incremental updates
4. Design for borderless browser view integration within the app

**User Experience:** Natural, conversational interaction that feels like talking to an intelligent coach while efficiently collecting all necessary training data.

## Interaction Mechanism

**Chat Interface:**
- ChatGPT-style conversation flow
- Questions typed with realistic typing animation
- Progressive disclosure of information needs
- Visual progress indicators

**Question Strategy:**
- Start with essential questions (goal, availability, event details)
- "NEXT QUESTIONS" section for detailed personalization
- Skip Strava-available information when connected
- Allow users to answer multiple questions in single responses

**Data Persistence:**
- Save all user responses with timestamp history
- Allow users to start over while preserving original answers
- Track incremental updates and evolution over time
- Never discard or overwrite previous responses

## Special Requirements

**Integration Points:**
- Strava data integration to skip redundant questions
- Borderless browser view compatibility for mobile app
- Visual design matching TrainerDay brand guidelines

**LLM Integration:**
- Open text responses processed by language models
- Structured data extraction from conversational input
- Follow-up question generation based on incomplete responses
- Natural language understanding for complex user descriptions

**Mobile Optimization:**
- Touch-friendly interface design
- Efficient scrolling and navigation
- Offline capability for started conversations
- Seamless handoff between web and mobile app

## Additional Context

**Reference:** Trello card H3HKdzf0 "CJ - Update Questions"

**Technical Architecture:**
- Real-time conversation processing
- Claude AI artifact integration for UI prototyping
- Henry's visual design input for TrainerDay styling
- Backend integration with existing Coach Jack logic

**Implementation Phases:**
1. Basic conversational interface
2. LLM integration for open text processing
3. Strava data integration
4. Mobile app integration
5. Advanced conversation management