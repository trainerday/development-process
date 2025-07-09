---
title: Move Paypal Payments From Rcp
type: backlog_item
permalink: product-development/os-projects/td-web/backlogs/move-paypal-payments-from-rcp
---

# Move paypal payments from RCP to our solution

## Description
Migrate PayPal payment processing from Restrict Content Pro (RCP) WordPress plugin to our native billing solution. This follows the same pattern as the Stripe migration.

## Details
- Original Trello List: Up Next
- Import Date: 2025-01-03
- Priority: High (Up Next)
- Status: Pending

## Technical Requirements
- Migrate existing PayPal customer records
- Update PayPal IPN (Instant Payment Notification) endpoints
- Ensure seamless transition for existing subscribers
- Maintain payment history and subscription status
- Handle PayPal-specific requirements (recurring payments, etc.)

## Dependencies
- New billing system must support PayPal
- PayPal API integration in our solution
- Data migration scripts for existing customers
- Coordination with Stripe migration efforts

## Notes
- "Same idea as stripe" - follow similar migration pattern
- Ensure both payment methods work in parallel during transition