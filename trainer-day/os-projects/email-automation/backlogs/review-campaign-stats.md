---
title: review-campaign-stats
type: note
permalink: trainer-day/os-projects/email-automation/backlogs/review-campaign-stats
---

# Review Campaign Stats

## Business Purpose
Enable TrainerDay to track and analyze email campaign performance by retrieving statistics from BigMailer API, providing insights into user engagement and campaign effectiveness.

## Main Sentiment
After successfully sending email campaigns, we need visibility into how our users are engaging with our communications to continuously improve our messaging and timing.

## Key Objectives
1. **Performance Tracking**: Monitor key metrics like open rates, click rates, and unsubscribes
2. **Engagement Analysis**: Understand how users interact with our email updates
3. **Data-Driven Decisions**: Use campaign statistics to optimize future communications
4. **Quick Access**: Retrieve stats with a simple script execution

## Success Criteria
- Ability to fetch statistics for any sent campaign
- Display comprehensive metrics including delivery, engagement, and performance data
- Save statistics for historical analysis
- Clear, formatted output for easy interpretation

## Implementation Details
Created `step4-campaign-stats.js` script that:
- Fetches campaign details from BigMailer API
- Extracts statistics directly from campaign object (no separate stats endpoint needed)
- Calculates performance metrics like click-to-open rate
- Displays formatted statistics in the console
- Saves complete stats to `output/last-campaign-stats.json`

## Current Status
✅ **COMPLETED** - The script is fully functional and tested. It successfully retrieved stats for the July 2025 campaign showing:
- 28,769 recipients
- 24.88% open rate
- 1.65% unsubscribe rate
- 0.01% complaint rate