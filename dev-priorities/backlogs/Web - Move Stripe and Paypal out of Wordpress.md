---
title: Web - Move Stripe and Paypal out of Wordpress
type: note
permalink: dev-priorities/backlogs/web-move-stripe-and-paypal-out-of-wordpress
---

# Web - Move Stripe and Paypal out of Wordpress

## Overview
Move the payment processing functionality (Stripe and PayPal) out of the WordPress implementation and integrate it directly into the main TrainerDay web application.

## Background
Currently, payment processing is handled through WordPress, which creates dependencies and potential maintenance issues. Moving this functionality to the main web application will:
- Reduce WordPress dependencies
- Improve payment flow integration
- Simplify maintenance and updates
- Provide better control over the payment experience

## Goals
- Extract Stripe payment processing from WordPress
- Extract PayPal payment processing from WordPress  
- Integrate payment functionality into main web application
- Maintain existing payment workflows and user experience
- Ensure no disruption to current subscribers
- Implement proper error handling and logging

## Technical Requirements
- Migrate Stripe API integration to main web app
- Migrate PayPal API integration to main web app
- Update subscription management workflows
- Implement payment webhooks handling
- Update user account management for payments
- Ensure PCI compliance requirements are met
- Test payment flows thoroughly

## Success Criteria
- [ ] All payment processing moved out of WordPress
- [ ] Existing subscribers continue to work without issues
- [ ] New subscriptions work through new payment system
- [ ] Payment webhooks properly handled
- [ ] Error handling and logging implemented
- [ ] Documentation updated

## Notes
This is a critical infrastructure change that affects revenue, so thorough testing and gradual rollout may be necessary.