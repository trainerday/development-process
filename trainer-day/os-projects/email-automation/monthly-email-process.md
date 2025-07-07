---
title: monthly-email-process
type: note
permalink: trainer-day/os-projects/email-automation/monthly-email-process
---

# Monthly Email Process

## Overview
This project automates the process of sending email updates to TrainerDay users through BigMailer.

## Prerequisites
- Node.js installed
- MongoDB connection configured in `.env`
- BigMailer API key configured in `.env`
- GitHub CLI (`gh`) installed and authenticated

## Complete Email Campaign Workflow

### Overview of Steps
1. **Sync Users** - Ensure BigMailer has all your latest users from MongoDB
2. **Generate Content** - Fetch recent development updates and create email content
3. **Create Campaign** - Build the email campaign in BigMailer with proper formatting
4. **Send Campaign** - Manually review and send via BigMailer web interface
5. **Review Performance** - Analyze campaign statistics and document learnings

### Detailed Step-by-Step Process

#### Step 1: Sync Latest Users from MongoDB to BigMailer
```bash
node step1-sync-users.js
```
**What it does:**
- Connects to MongoDB using credentials from `.env`
- Checks `bigmailer-sync-status.json` for last synced userId
- Finds all users with userId greater than last sync point
- Adds new users to BigMailer's "All Contacts" list
- Updates sync status file with progress
- Rate limited to 2 requests/second to respect API limits

**Alternative for full sync (use rarely):**
```bash
node sync-users-full.js
```
- Syncs ALL users since a specific date
- Can take 3+ hours for large databases
- Use only when setting up or fixing sync issues

#### Step 2: Generate Development Update Content
```bash
node step2-generate-content.js
```
**What it does:**
- Uses GitHub CLI to fetch all merged PRs since September 2024
- Searches across all TrainerDay repositories
- Creates a markdown summary of all updates
- Applies correct team name mappings (fun titles)
- Saves to `output/development-summary-since-sept-2024.md`
- Also saves raw PR data for reference

#### Step 2.5: HUMAN CONTENT REVIEW
**YOU manually:**
- Review the generated markdown content in `output/development-summary-since-sept-2024.md`
- Edit team member names and achievements for accuracy
- Adjust messaging and tone to match brand voice
- Confirm all features/improvements are accurate
- Add any missing major updates or corrections
- Ensure personal note from Alex V is current and relevant

#### Step 3: Create Email Campaign in BigMailer
```bash
node step3-create-campaign.js
```
**What it does:**
- Reads the email template from `email-template.html`
- Reads the markdown summary from Step 2
- Converts markdown to professional HTML email
- Inserts the converted content into the template
- Applies proper formatting (tight spacing, brand colors)
- Creates a draft campaign in BigMailer with:
  - Today's date in the campaign name
  - Eye-catching subject line with emoji
  - Responsive HTML design
  - Plain text version for compatibility
- Saves campaign ID to `output/last-campaign-created.json`

#### Step 4: Send the Campaign (Manual)
**Note:** BigMailer API does not support sending campaigns programmatically.

**What you need to do:**
1. Log into BigMailer: https://app.bigmailer.io/
2. Navigate to Campaigns > Bulk Campaigns
3. Find your campaign (named with today's date, e.g., "July 2025 Development Update")
4. Click on the campaign to review:
   - Check HTML preview looks correct
   - Verify team names show fun titles
   - Confirm spacing is tight (not too many blank lines)
5. Send a test email to yourself
6. If everything looks good, either:
   - Send immediately to all contacts
   - Schedule for a specific time

#### Step 5: Get Campaign Stats
```bash
node step4-campaign-stats.js
```
**What it does:**
- Fetches campaign statistics from BigMailer API
- Displays delivery, engagement, and performance metrics
- Saves detailed stats to `output/last-campaign-stats.json`

#### Step 5.5: HUMAN CAMPAIGN PERFORMANCE REVIEW
**YOU manually review and analyze:**
- **Open Rate**: Compare to previous campaigns (typical: 20-30%)
- **Click Rate**: Identify which features/topics generated most interest
- **Bounce Rate**: Flag any delivery issues or list hygiene problems
- **Unsubscribe Rate**: Monitor for content issues if unusually high
- **Engagement Patterns**: Note which sections performed best
- **Delivery Issues**: Check for any spam filter problems

**Document learnings for next campaign:**
- What subject lines work best
- Which content formats get more engagement
- Optimal send times and days
- Any technical issues to address

### Quick Reference - What Each Script Does

| Script | Purpose | Typical Runtime |
|--------|---------|----------------|
| `step1-sync-users.js` | Sync new users from MongoDB to BigMailer | 1-5 minutes |
| `step2-generate-content.js` | Fetch PRs and create email content | 30 seconds |
| `step3-create-campaign.js` | Create formatted campaign in BigMailer | 10 seconds |
| `step4-campaign-stats.js` | Fetch campaign performance metrics | 5 seconds |
| Manual review steps | Content review and campaign approval | 10-15 minutes |

## Team Name Mapping
When creating the email content, use these friendly names instead of GitHub usernames:

- **Alex K** - The Pixel Perfectionist ✨ (Developer)
- **Grigory** - Captain Feature Ship 🚢
- **Andrey** - 1,095 Day Running Streak Legend 🏃‍♂️
- **Rodion** - AI's Best Friend 🤖
- **Marek** - Master of Quality Quest 🗡️
- **Dan** - Bug Detection Specialist 🔍

**Note**: Alex V (CEO/Founder) signs the emails personally

## Files Structure
```
email-automation/
├── .env                              # API keys and credentials
├── bigmailer-sync-status.json        # Tracks last sync status
├── email-template.html               # Base HTML email template
├── step1-sync-users.js               # Incremental user sync
├── step2-generate-content.js         # Fetch PRs and generate summary
├── step3-create-campaign.js          # Create email campaign
├── step4-campaign-stats.js           # Get campaign performance data
├── sync-users-full.js                # Full user sync (use cautiously)
├── utilities/
│   ├── bigmailer-list-operations.js # BigMailer API helper functions
│   └── find-user.js                  # MongoDB user search utility
└── output/                           # All generated files go here
    ├── development-summary-since-sept-2024.md  # Email content
    ├── trainerday-users-since-sept-2024.csv   # User export for import
    ├── last-campaign-created.json              # Last campaign details
    └── last-campaign-stats.json                # Campaign performance data
```

## Important Configuration

### BigMailer API Details
- **API Documentation**: https://docs.bigmailer.io/reference/
- **Brand ID**: `55e9e9e3-0564-41c1-ba79-faa7516c009d`
- **List ID (All Contacts)**: `71a953b3-ef1d-4d20-91ba-10e896fe18a5`
- **API Limitations**: Cannot send/schedule campaigns via API (must use web UI)

### Email Campaign Settings
- **Subject Line**: `🚀 285 days, 300+ improvements, and counting...` (update days as needed)
- **Preview Text**: `Your favorite cycling app just got better - see what we've been building for you`
- **From Name**: `Alex V from TrainerDay`
- **From Email**: `support@send.trainerday.com`
- **Reply-To**: `support@trainerday.com`

### Email Content Structure
1. **Feature Updates** - Organized by category (Mobile, Web, Billing, etc.)
2. **Coming Soon** - Future features in development
3. **Dev Team Credits** - With fun titles (see team mapping above)
4. **Personal Note from Alex V** - Styled blockquote with personal message
5. **P.S.** - Pricing reminder ($3.99/month)
6. **Simple Footer** - No social media links, just unsubscribe and address

### Email Formatting Guidelines
- **Spacing**: Use 3px margins between list items for tight layout
- **Headers**: H1=28px, H2=24px, H3=20px with #0068A5 color
- **Lists**: Avoid nested lists for better formatting
- **Strava updates**: Keep on single line, not as sub-list
- **Personal tone**: Email is from Alex V personally, not generic company voice

### Email Template
The base HTML email template is saved as `email-template.html` and includes:
- Responsive design with mobile media queries
- TrainerDay branded header with gradient background
- Content area where markdown is converted and inserted
- Simple footer with unsubscribe link and company info
- Outlook MSO compatibility tags

### Personal Note Styling
The personal note from Alex V uses a styled blockquote for visual distinction:
```html
<blockquote style="border-left: 6px solid #0068A5; margin: 30px 0; padding: 20px 20px 20px 30px; background: linear-gradient(to right, #f0f7fc 0%, #ffffff 100%); font-family: Georgia, serif; font-style: italic;">
  <p style="font-size: 18px; color: #333; margin: 0 0 15px 0;">
    "Your feedback drives everything we build..."
  </p>
  <p style="font-size: 16px; color: #555; margin: 0 0 15px 0; font-style: normal; line-height: 1.6;">
    [Personal message content]
  </p>
  <footer style="font-style: normal;">
    <strong style="font-size: 22px; color: #0068A5;">— Alex V</strong><br>
    <small style="color: #666;">Founder & Chief Cycling Enthusiast 🚴‍♂️</small><br>
    <small style="color: #666;">alex@trainerday.com</small>
  </footer>
</blockquote>
```

### Optional CTA Button HTML
For future use if you want to add a call-to-action button:
```html
<!-- CTA Button -->
<tr>
  <td style="padding: 0 30px 40px 30px; text-align: center;">
    <a href="https://app.trainerday.com" style="display: inline-block; padding: 15px 40px; background-color: #0068A5; color: #ffffff; text-decoration: none; border-radius: 5px; font-weight: 600; font-size: 16px;">Open TrainerDay App</a>
  </td>
</tr>
```

### User Sync Status
The `bigmailer-sync-status.json` file tracks:
- Last userId synced
- Last sync timestamp  
- Total contacts synced
- Last email blast date

### Rate Limiting
- BigMailer API: 2 requests/second
- MongoDB queries are optimized to reduce load

## Script Consolidation

The project has been simplified to main scripts:

1. **step1-sync-users.js** - Syncs new users from MongoDB to BigMailer
2. **step2-generate-content.js** - Fetches GitHub PRs and creates development summary
3. **step3-create-campaign.js** - Creates formatted email campaign in BigMailer
4. **step4-campaign-stats.js** - Retrieves campaign performance metrics

All other scripts are helper utilities and can be ignored for normal workflow.

## Performance Benchmarks

### Typical Campaign Performance
- **Open Rate**: 20-30% (industry average for SaaS)
- **Click Rate**: 3-7% (depends on content quality)
- **Bounce Rate**: <2% (good list hygiene)
- **Unsubscribe Rate**: <0.5% (quality content)

### Campaign Timing
- **Best Send Days**: Tuesday-Thursday
- **Best Send Times**: 10am-2pm EST
- **Frequency**: Monthly or quarterly (avoid over-mailing)

## Troubleshooting

### MongoDB Connection Issues
- Check CA certificate exists: `ca-certificate.crt`
- Verify `.env` credentials are correct
- Ensure MongoDB whitelist includes your IP

### BigMailer API Errors
- Check API key in `.env`
- Monitor rate limit errors (429 errors)
- Campaigns must be sent manually via web UI

### Missing Users
- Check `email` field exists in MongoDB documents
- Verify userId is greater than last sync point

### Poor Campaign Performance
- Review subject line effectiveness
- Check for spam trigger words
- Verify mobile-friendly formatting
- Test send times and days