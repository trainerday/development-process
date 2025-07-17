---
title: product-decision-statistics
type: note
permalink: docs-for-devs/product-decision-statistics
---

# Product Decision Statistics

*Created: July 15, 2025*

## Purpose
Key statistics and metrics that inform product decisions, extracted from data analysis sessions and strategic planning. These numbers help validate hypotheses and guide development priorities.

## Core Business Metrics

### Product Quality Indicators
- **App Store Rating**: 4.7 stars with 3,800+ reviews
- **Support Volume**: Only ~10 tickets/week from 6,000+ active users
- **Cancellation Sentiment**: 90% of cancellations are positive ("I'll be back" or "can't train anymore")
- **Product Issues**: Only 3-5% cite product problems or missing features, no ai.... as reason for cancellation

### User Engagement Patterns (30-day window)
- **New Registrations**: ~2,500/month (varies 2k-4k seasonally)
- **Meaningful Action Rate**: 25.2% take action within 30 days
- **Non-Engagement Rate**: 74.8% register but don't engage meaningfully
- **Device Connection Rate**: 12.3% of registrants connect devices
- **Conversion Among Device Users**: 28.8% convert to paid

### Platform Performance
- **App Downloads**: ~34k annually (20.1k iOS + 13.9k Android)
- **Download → Registration Rate**: 62.4%
- **Registration Abandonment**: 37.6% don't complete registration
- **Web Traffic**: 201k annual visitors
- **Web Registration Rate**: 3.8%

## Conversion Funnel Analysis

### Overall Conversion Rates
- **Baseline Conversion**: 13-17% of new registrants convert within 30-60 days
- **Seasonal Variation**: Higher in winter, lower in summer
- **Goal Conversion**: 20-25% (realistic improvement target)

### Registration Abandonment Breakdown
- **37.6% don't register** after app download
- **~50% are returning users** who just login (estimated)
- **~18.5% are new users** who don't register
- **~9.25% are genuinely interested** but won't register first
- **True opportunity**: ~3,145 people/year

### Mobile App Engagement (3-day window)
- **52% start a workout** (678 out of 1,302 registrants)
- **Device connection required**: 153 users connect devices
- **Completion rate**: 28% of starters complete workouts
- **Real engagement**: 11.8% actually do device-connected training

## User Behavior Insights

### Plan Usage Patterns
- **50% follow some structured plan** at least part of the year
- **25% use Coach Jack plans** (TrainerDay's built-in plans)
- **25% use other plans** (created, imported, external)
- **50% prefer individual workout selection** over structured plans

### Feature Usage Statistics
- **Today feature**: Liked and used by 20% of users
- **HR+ feature**: Used by 10% of most happy users
- **Swimming/rowing**: Only 1-2% of users use this
- **Export features**: Significant usage among "planner" persona

### User Segmentation
- **70-80% mobile app users** (indoor training focused)
- **20-30% web-only users** (workout creation/export focused)
- **Geographic**: Primarily European and global users
- **Experience level**: Mostly experienced cyclists, fewer beginners

## Technical Performance Metrics

### Platform Reliability
- **App crashes**: 1-2% of users experience monthly
- **Bluetooth connectivity**: "Fairly significant" connection issues reported
- **Performance issues**: Android 15 compatibility problems
- **Error rates**: Need quantification for app errors

### Platform Expectations
- **App registrants**: 70% expect complete indoor training app, 30% want creation tools
- **Web registrants**: 70% expect workout/plan creation tools, 30% want indoor training
- **Mismatch impact**: 30% of users on each platform hit immediate friction

## Market Context

### Competitive Landscape
- **TrainerRoad positioning**: "Makes you faster" - premium, rigid
- **Zwift positioning**: Virtual cycling game - entertainment focused
- **TrainerDay positioning**: "Flexible & Affordable" - validated by customers
- **Price sensitivity**: Major factor in user decisions

### Customer Feedback Themes
- **Most valued**: "Affordable" mentioned consistently
- **Second most valued**: "Flexible" training approach
- **User profile**: Smart, research-driven, value-conscious cyclists
- **Word-of-mouth**: Strong organic growth through cycling community

## Decision-Making Implications

### High-Confidence Decisions
- **Product quality is good** - 4.7 stars, low support volume
- **Conversion problem exists** - 75% register but don't engage
- **Platform friction is real** - Users expect app to be complete
- **Positioning works** - "Flexible & Affordable" resonates

### Medium-Confidence Insights
- **Registration abandonment**: ~18% true opportunity
- **AI features demand**: Unknown, needs validation
- **Seasonal patterns**: Predictable but variable
- **Feature usage**: Plan following vs individual workouts

### Low-Confidence Assumptions
- **Exact conversion triggers** - Need behavioral analysis
- **Optimal free tier limits** - Requires testing
- **Feature development ROI** - Most features used by small %
- **User acquisition channels** - Which efforts drive quality users

## Key Metrics to Track

### Primary Success Indicators
- **Engagement rate**: % taking meaningful action within 30 days
- **Device connection rate**: % of registrants connecting devices
- **Conversion rate**: % of registrants becoming paid users
- **Quality maintenance**: App store rating and support volume

### Secondary Indicators
- **Time to first workout**: How quickly users experience value
- **Platform switching**: App → web or web → app usage
- **Feature adoption**: Usage rates for new features
- **Word-of-mouth growth**: Organic discovery patterns

## Data Collection Priorities

### Critical Missing Data
1. **Converter behavior analysis** - What do paying users do differently?
2. **Platform usage patterns** - How do users actually use app vs web?
3. **Feature usage correlation** - Which features drive conversions?
4. **Seasonal user journey** - How does timing affect behavior?

### Nice-to-Have Data
- **User acquisition attribution** - Which channels drive quality users
- **Retention patterns** - What keeps users engaged long-term
- **Feature request frequency** - What do users actually ask for
- **Competitive switching** - Why users leave competitors

## Bottom Line Insights

**The Numbers Support the Strategy:**
- Product quality is proven (4.7 stars, 90% positive cancellations)
- Engagement is the primary challenge (75% never take meaningful action)
- Platform friction is measurable (users expect app completeness)
- Conversion opportunity is significant (13-17% baseline with room for improvement)

**Data-Driven Priorities:**
1. **Reduce friction** - Get more registered users to engage
2. **Optimize existing features** - Focus on what drives engagement
3. **Test incrementally** - Small improvements, measure impact
4. **Maintain quality** - Don't sacrifice what's working