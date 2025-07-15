---
title: hypothesis-backlog
type: note
permalink: docs-for-devs/hypothesis-backlog
---

# Hypothesis Testing Backlog

*Created: July 15, 2025*

## Priority Overview - Strategic Order

### 1. 🎯 REDUCE FRICTION (Errors, Confusion, Better Onboarding)
**Goal:** Get more registered users to actually use the app/site

**High Priority Hypotheses:**
- We should add ways for users to experience the value faster. First they need to be defined
- Errors in app cause churn
- Lost device connections cause churn
- Our performance issues in the app cause churn (android 15 and slowing in general)
- Improving education in onboarding will increase adoption
- Device connection guidance increases serious user percentage
- Better UX - specifically simplify and make things obvious will reduce churn
- Getting rid of spelling and grammar issues will stop turning away some users
- Reducing the number of errors we have in the app will reduce churn

### 2. 🤖 AI PLANS
**Goal:** Enhance core product value for engaged users

**High Priority Hypotheses:**
- AI plan generation increases Coach Jack usage
- Having AI choose my plan and it feels personal will help like the last item
- Having adaptive AI training/workouts will reduce churn and attract more users

### 3. 📊 OPTIMIZE CONVERSION (Register → Paid)
**Goal:** First determine if free registered users even use the app or site, then optimize conversion

**High Priority Hypotheses:**
- 50% of our app registrants never connect a device. No compatible device, looking for different app, confused, not obvious value
- Assumption: 50% of our users follow a plan at least part of the year
- We should be designing for our most happy users
- Feeling listened to causes retention and growth (word of mouth)
- Having user directed conversations about training plans and matching their expectations will create less churn and attract new users

### 4. 🔄 REDUCE CHURN
**Goal:** Keep paying users engaged and subscribed

**High Priority Hypotheses:**
- Adding kudos or reports to show progress will reduce churn
- Reducing friction for paying users by forcing them to the website for planning or some settings will reduce churn
- More basic workout variety satisfies non-plan users
- Our Today feature that shows random semi-targeted workouts is liked and used by 20% of users

### 5. 📈 OPTIMIZE NON-REGISTERED → REGISTERED
**Goal:** Improve registration rates from visitors

**High Priority Hypotheses:**
- Registration nudges will convert more "skip for now" users to register
- Clearer "What is TrainerDay" messaging reduces bounce rate
- Need ways to attract more users. Reddit, Youtube, better word of mouth, exiting user incentives

---

## Purpose
Track hypotheses for strategic decisions and prioritize testing based on impact vs effort. Test small, learn fast, decide based on results.

## Active Hypotheses

| Hypothesis | Effort | Impact | Priority | User Request |
|------------|--------|--------|----------|--------------|
| Registration nudges will convert more "skip for now" users to register | 2 | 4 | 1 |  |
| More basic workout variety satisfies non-plan users | 2 | 4 | 1 |  |
| Clearer "What is TrainerDay" messaging reduces bounce rate | 2 | 3 | 2 |  |
| Device connection guidance increases serious user percentage | 3 | 4 | 3 |  |
| AI plan generation increases Coach Jack usage | 5 | 3 | 5 |  |
| Having a web version of our app for trainers will bring more users | 5 | 4 | 4 | Y |
| Better UX - specifically simplify and make things obvious will reduce churn | 4 | 4 | 3 |  |
| Adding support for more devices (like spin bikes or old protocols) will bring more users | 4 | 3 | 4 | Y |
| Having user directed conversations about training plans and matching their expectations will create less churn and attract new users | 3 | 4 | 3 |  |
| Having AI choose my plan and it feels personal will help like the last item | 5 | 3 | 5 |  |
| Reducing the number of errors we have in the app will reduce churn | 3 | 3 | 3 |  |
| Reducing friction for paying users by forcing them to the website for planning or some settings will reduce churn | 3 | 4 | 3 |  |
| Getting rid of spelling and grammar issues will stop turning away some users | 2 | 2 | 3 |  |
| Having adaptive AI training/workouts will reduce churn and attract more users | 5 | 4 | 4 | Y |
| Improving education in onboarding will increase adoption | 3 | 3 | 3 |  |
| Adding kudos or reports to show progress will reduce churn | 3 | 3 | 3 |  |
| It's more important to focus on indoor training (apps) then the website for churn and for growth | 1 | 3 | 2 |  |
| Our performance issues in the app cause churn (android 15 and slowing in general) | 4 | 4 | 3 |  |
| Errors in app cause churn | 3 | 4 | 2 |  |
| Lost device connections cause churn | 3 | 4 | 2 |  |
| Feeling listened to causes retention and growth (word of mouth) | 2 | 4 | 1 |  |
| Swimming and rowing just cause complexity/overload and add limited value (1-2% of our users use this) | 2 | 2 | 4 |  |
| If we can't fix wahoo integration just remove it since it seems mostly broken, or ask David to share his code so we can compare to ours | 2 | 3 | 3 |  |
| Need ways to attract more users. Reddit, Youtube, better word of mouth, exiting user incentives | 3 | 5 | 2 |  |
| 50% of our app registrants never connect a device. No compatible device, looking for different app, confused, not obvious value | 3 | 4 | 2 |  |
| Many serious users want to have a plan for a specific event. Having slopes or some strategic method of workouts designed for that event | 4 | 3 | 4 |  |
| Assumption: 50% of our users follow a plan at least part of the year | 1 | 2 | 4 |  |
| Assumption: Our users use external entertainment. Music, netflix, youtube | 1 | 2 | 4 |  |
| Our Today feature that shows random semi-targeted workouts is liked and used by 20% of users | 2 | 3 | 3 |  |
| Our HR+ is used by 10% of our most happy users | 1 | 2 | 4 |  |
| We should be designing for our most happy users | 1 | 4 | 2 |  |
| Following My plans is more like a dynamic plan but people are so used to calendars they don't get this. Many would prefer it | 3 | 3 | 3 |  |
| React Native is better than native even though the performance is worse, having 2 native apps would cost us more and does not fit our low cost thinking | 1 | 3 | 2 |  |
| We should add ways for users to experience the value faster. First they need to be defined | 3 | 5 | 1 |  |

## Scoring Guide

**Effort Scale (1-5):**
- 1 = Few hours (copy changes, simple banner)
- 2 = Few days (basic feature, A/B test setup)
- 3 = 1-2 weeks (new onboarding flow, UI changes)
- 4 = 1 month (significant feature development)
- 5 = 3+ months (major features like AI)

**Impact Scale (1-5):**
- 1 = Minimal effect on business metrics
- 2 = Small improvement in user experience
- 3 = Moderate improvement in conversion/engagement
- 4 = Significant business impact (revenue/user growth)
- 5 = Game-changing for the business

**Priority Scale (1-5):**
- 1 = Test immediately (high impact, low effort)
- 2 = Test soon (good impact/effort ratio)
- 3 = Test when resources available
- 4 = Test if other priorities completed
- 5 = Reconsider or postpone

**User Request:** Track if this hypothesis is based on direct user feedback/requests (Yes/No or specific details)

**Priority Logic:** High Impact + Low Effort = Test First