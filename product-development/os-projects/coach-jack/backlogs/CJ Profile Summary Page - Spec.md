---
title: CJ Profile summary page   spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/CJ Profile Summary Page - Spec
---

# CJ Profile Summary Page - Spec

## Overview

The profile summary page is the confirmation screen users see after completing the Coach Jack questionnaire. It displays their responses as categorized tags and provides personalized AI insights to make users feel understood before generating their training plan.

## Key Features

### Categorized Tag Display
User responses are organized into 7 categories with schema-aligned tags:

1. **🎯 Performance & Health Goals** - Training objectives and targets
2. **📅 Current Block Schedule and Periodization** - Training volume and progression
3. **🏁 Event Details** - Race information and event specifics
4. **🧠 Riding Style & Motivation** - Psychological profile and preferences
5. **💪 Training Status & Fitness** - Current fitness level and equipment
6. **😴 Recovery & Lifestyle** - Sleep, stress, and lifestyle factors
7. **⚠️ Health & Wellness** - Health status and limitations

### Personalized AI Insights
- **Coach Jack's Initial Assessment** section with personalized analysis
- **4 key insight areas**: Training Readiness, Goal Alignment, Recovery Capacity, Personalization Opportunities
- **Natural language** that demonstrates understanding of their specific situation
- **Profile completeness meter** showing data quality and encouraging additional details

### Interactive Features
- **Edit Profile** button opens LLM-powered modal for updates
- **Generate My Plan** button proceeds to training block selection
- **Start Over** option with confirmation
- **Profile strength scoring** based on completeness

## Technical Implementation

**Live Prototype:** [Coach Jack Profile Summary](https://claude.ai/artifact/coach-jack-summary)

**Data Structure:**
- Tags mapped to user tag schema categories
- Example tags: `[Event: The Big One]`, `[Target: +40W Power]`, `[Equipment: Power Meter]`
- Enhanced with training phase, consistency, and periodization context

**User Psychology:**
- Creates "we really understand you" feeling
- Shows comprehensive analysis of their cycling profile
- Builds confidence before plan generation
- Demonstrates AI coaching intelligence

## User Experience Goals

**Primary Objectives:**
1. **Confirmation** - Show we captured their information accurately
2. **Personalization** - Demonstrate intelligent understanding
3. **Confidence Building** - Prepare them for plan generation
4. **Refinement** - Allow easy profile updates

**Success Metrics:**
- High conversion rate to "Generate My Plan"
- Low "Start Over" usage
- Positive user feedback on personalization
- Increased profile completeness over time

## Next Steps

1. **Backend Integration** - Connect to questionnaire data
2. **LLM Processing** - Generate personalized insights
3. **Tag Extraction** - Process enhancement questions into tags
4. **Profile Management** - Save and version user profiles
5. **Plan Generation** - Connect to training block selection

## Reference Materials

- **Questionnaire Spec:** [[CJ Update Questions Interface - Spec]]
- **Detailed UI/UX Design:** [[TrainerDay/Coach Jack AI/5 - UI/UX]]
- **User Tag Schema:** Comprehensive profiling data structure