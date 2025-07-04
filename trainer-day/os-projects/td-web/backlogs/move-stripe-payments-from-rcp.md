---
title: move-stripe-payments-from-rcp
type: backlog_item
permalink: trainer-day/os-projects/td-web/backlogs/move-stripe-payments-from-rcp
---

# Move stripe payments from RCP to our solution

## Description
Migrate Stripe payment processing from Restrict Content Pro (RCP) WordPress plugin to our native billing solution. This is part of the larger initiative to move away from WordPress-based billing.

## Details
- Original Trello List: Up Next
- Import Date: 2025-01-03
- Priority: High (Up Next)
- Status: Pending

## Technical Requirements
- Migrate existing Stripe customer records
- Update all Stripe webhooks to point to new endpoints
- Ensure seamless transition for existing subscribers
- Maintain payment history and subscription status
- Test thoroughly with sandbox environment first

## Dependencies
- New billing system must be fully functional
- Stripe API integration in our solution
- Data migration scripts for existing customers

## Impact
- Reduces dependency on WordPress/RCP
- Improves billing system reliability
- Enables better control over payment processing