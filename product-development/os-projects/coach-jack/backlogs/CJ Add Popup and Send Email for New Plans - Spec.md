---
title: CJ Add Popup and Send Email for New Plans - Spec
type: note
permalink: product-development/os-projects/coach-jack/backlogs/cj-add-popup-and-send-email-for-new-plans-spec
---

# CJ Add Popup and Send Email for New Plans - Requirements

## Current State

When users complete Coach Jack questions and receive a new training plan, they may want to immediately increase intensity or make changes. Currently, there's no guidance about starting conservatively or information about how to adjust settings later.

## Desired Outcome  

**Primary Goals:**
1. Display informational popup after plan creation explaining the conservative start approach
2. Send follow-up email with instructions for adjusting intensity and ride feel
3. Educate users on the benefits of progressive training

**User Experience:** New users understand why their plan starts conservatively and know how to make adjustments when ready, reducing frustration and improving long-term adherence.

## Interaction Mechanism

**Post-Questions Popup:**
- Appears after answering questions and before showing plan
- Explains the conservative start philosophy
- Highlights ability to easily change intensity later
- Option to increase intensity immediately or proceed with recommendation

**Follow-up Email:**
- Sent 2-3 days after plan starts
- Contains instructions for adjusting Intensity & Ride Feel settings
- Includes tips for recognizing when to increase difficulty
- Links to relevant help documentation

**Messaging Content:**
- Emphasize long-term progress over immediate intensity
- Explain that conservative start reduces injury risk
- Build confidence in the system's approach

## Special Requirements

**Popup Timing:**
- Appears after questions but before plan display
- Dismissible but encourages reading
- Should not block plan access for experienced users

**Email Automation:**
- Triggered by plan creation event
- Personalized with user's name and plan details
- Include unsubscribe option
- Track engagement metrics

**Content Guidelines:**
- Professional but encouraging tone
- Clear, actionable instructions
- Visual elements showing where to find settings

## Additional Context

**Reference:** Trello card 9ZESzDwO "CJ add popup & send email"

**Sample Messaging:**
"When starting a NEW plan, it's best to begin at the recommended intensity level. This allows your body to adapt gradually and builds a foundation for long-term progress. You can easily increase intensity at any time through the Intensity & Ride Feel settings."

**Implementation Notes:**
- Integrate with existing email system
- A/B test different messaging approaches
- Monitor user behavior changes after implementation
- Consider progressive disclosure for advanced users