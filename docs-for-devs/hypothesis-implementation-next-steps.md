---
title: hypothesis-implementation-next-steps
type: note
permalink: docs-for-devs/hypothesis-implementation-next-steps
---

# Hypothesis Implementation - Next Steps

*Created: July 15, 2025*

## Purpose
This document contains specific implementation details and technical considerations for testing our hypotheses, extracted from previous strategic planning sessions.

## Priority 1 Implementation Details

### Skip For Now Registration Flow
**Hypothesis**: Registration nudges will convert more "skip for now" users to register

**Current Implementation**:
- "Skip for now" option with clear messaging
- "Start Training in Seconds" + "20 free structured workouts"  
- Social proof: "Join 20,000+ cyclists"
- Trust building: "The free version is great!!!"

**Technical Details**:
- Allow users to explore without registration
- Show register/login popup when they try to save a workout
- Add persistent but subtle registration nudges in the app

**Reference Design**:
![Registration Screen](https://i.ibb.co/0VGFqvY6/first-app-page-jpg.jpg)

### First-Time User Experience Optimization
**Hypothesis**: We should add ways for users to experience the value faster

**Implementation Strategy**:
- **Problem**: New users face learning curve (FTP, blue bars, numbers)
- **Reality**: 80-90% of users know this from other apps
- **Focus**: Optimize for experienced users first, beginners second
- **Goal**: Clear value in first 5 minutes

**Technical Approach**:
- Simplify initial workout selection
- Provide quick setup for experienced users
- Add progress indicators for first session
- Minimize cognitive load in onboarding

## App vs Web Strategy Decisions

### Platform Focus
**Hypothesis**: It's more important to focus on indoor training (apps) than the website for churn and for growth

**Current Reality**:
- Mobile users engage much better than web users
- App-first strategy aligns with indoor training focus
- Web remains important for planning/export features

**Development Implications**:
- Prioritize app performance and reliability
- Reduce friction that forces users to web
- Maintain web functionality but don't over-invest

### React Native Decision
**Hypothesis**: React Native is better than native even though performance is worse

**Strategic Rationale**:
- Lower development costs align with "affordable" positioning
- Single codebase reduces complexity
- Performance trade-offs acceptable for our use case
- Fits our resource constraints

## Technical Priority Framework

### Tier 1: Critical Data Collection
1. **Converter behavior analysis** - Understand what drives conversions
2. **Registration abandonment ROI** - Validate development investment
3. **User engagement patterns** - Where do people drop off?

### Tier 2: Friction Reduction
1. **App performance issues** - Android 15 problems, general slowness
2. **Device connection reliability** - Bluetooth and connectivity issues
3. **Error reduction** - App crashes and technical problems
4. **UX simplification** - Make things more obvious

### Tier 3: Value Communication
1. **Onboarding improvements** - Better education about features
2. **Progress feedback** - Help users see their improvement
3. **Messaging clarity** - "What is TrainerDay?" communication

## Key Metrics to Track

### App Conversion Funnel
- **App Downloads**: Significant volume across iOS and Android
- **Download → Registration Rate**: 62.4% (37.6% abandonment)
- **Registration → Meaningful Action**: ~25% within 30 days
- **Device Connection Rate**: ~12% of registrants
- **Conversion Among Device Users**: ~28%

### Success Criteria
- **Primary**: Free user → Paid conversion rate improvement
- **Secondary**: App download → Registration rate improvement
- **Supporting**: Web visitor → Registration rate (baseline: 3.8%)
- **Quality**: Maintain 4.7 star rating and low support volume

## What We Know Works

### Proven Success Factors
- **Organic Growth**: Reddit, YouTube comparisons, word-of-mouth
- **Product Quality**: 4.7 stars, 90% positive cancellations
- **Price Point**: Affordable alternative to TrainerRoad/Zwift
- **User Base**: Strong paying user base, 30% growth last winter

### Critical Success Factors
1. **Remove friction for pre-sold users** - They come ready to buy but hit barriers
2. **Differentiate through experience** - Let users try before competitors force registration
3. **Focus on experienced cyclists** - They're 80-90% of user base and easier to convert
4. **Trust the organic growth** - Word-of-mouth is working, just remove barriers

## Implementation Decision Framework

### Green Light Criteria (Implement Now)
- High impact (4-5) + Low effort (1-2)
- Addresses Priority 1 strategic goals
- Has clear success metrics
- Minimal technical risk

### Yellow Light Criteria (Implement Soon)
- Medium impact (3) + Medium effort (3)
- Supports multiple strategic priorities
- Can be tested incrementally
- Reasonable resource requirements

### Red Light Criteria (Reconsider)
- Low impact (1-2) or High effort (4-5)
- Doesn't align with strategic priorities
- High technical complexity
- Unclear success metrics

## Next Steps

1. **Review hypothesis backlog** - Prioritize based on current capacity
2. **Set up testing framework** - Ability to measure hypothesis results
3. **Start with Priority 1 items** - Focus on friction reduction
4. **Measure and iterate** - Let user behavior guide next steps

## Bottom Line

**Focus on systematic testing of small improvements rather than building complex features.** The goal is to help registered users experience TrainerDay's value faster, not to rebuild the product.

Success comes from removing barriers to value realization, not from adding more features.