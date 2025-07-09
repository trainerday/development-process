---
title: create-login-register-forgot-password
type: backlog_item
permalink: product-development/os-projects/td-web/backlogs/create-login-register-forgot-password
---

# Create login, register and forgot password in our site

## Description
Implement native authentication system (login, registration, and password reset) on our main site, moving away from WordPress-based authentication while maintaining compatibility with existing user accounts.

## Details
- Original Trello List: Up Next
- Import Date: 2025-01-03
- Priority: High (Up Next)
- Status: Pending

## Technical Requirements
- Create login page with email/password authentication
- Implement user registration flow
- Add forgot password functionality with email reset
- Use WordPress salt for password hashing to maintain compatibility
- Ensure mobile app compatibility with new auth system
- Maintain session management across web and mobile

## Security Considerations
- Use existing WP salt for backward compatibility
- Implement proper password hashing
- Add rate limiting for login attempts
- Secure password reset tokens
- CSRF protection for forms

## Mobile App Compatibility
- Ensure authentication APIs work with existing mobile apps
- Maintain same authentication tokens/sessions
- Test thoroughly on both iOS and Android apps