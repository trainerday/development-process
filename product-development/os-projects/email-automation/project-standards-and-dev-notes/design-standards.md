---
title: Design Standards
type: documentation
permalink: product-development/os-projects/email-automation/project-standards-and-dev-notes/design-standards
---

# Email Automation - Design Standards

## Email Design Principles

### Visual Hierarchy
- Clear subject lines (50 characters or less)
- Prominent call-to-action buttons
- Scannable content with headers and bullet points
- F-pattern layout for readability

### Brand Consistency
- TrainerDay brand colors and fonts
- Consistent header/footer across all emails
- Logo placement and sizing standards
- Tone of voice guidelines

### Responsive Design
- Mobile-first approach
- Single column layout for mobile
- Minimum font size: 14px for body, 22px for headers
- Touch-friendly button sizes (44x44px minimum)

## Email Types & Templates

### Transactional Emails
- Welcome emails
- Password resets
- Order confirmations
- Account notifications

### Marketing Emails
- Newsletters
- Product announcements
- Promotional campaigns
- Event invitations

### Automated Campaigns
- Onboarding sequences
- Re-engagement campaigns
- Birthday/anniversary emails
- Abandoned cart reminders

## Technical Design Standards

### HTML Email Guidelines
- Table-based layouts for compatibility
- Inline CSS only
- Alt text for all images
- Fallback fonts (Arial, Helvetica, sans-serif)

### Image Standards
- Optimize for web (under 100KB per image)
- 2x resolution for retina displays
- Host images on reliable CDN
- Background colors for image-off scenarios

### Accessibility
- Proper heading hierarchy
- Sufficient color contrast (4.5:1 minimum)
- Descriptive link text
- Screen reader compatibility

## Testing Requirements

### Email Clients
- Gmail (Desktop & Mobile)
- Outlook (2016, 2019, 365)
- Apple Mail (Desktop & iOS)
- Yahoo Mail
- Android native client

### Pre-send Checklist
- [ ] Subject line under 50 characters
- [ ] Preheader text optimized
- [ ] All links tested
- [ ] Images have alt text
- [ ] Unsubscribe link present
- [ ] Mobile preview checked
- [ ] Spam score evaluated

## Performance Metrics

### Key Metrics to Track
- Open rate (target: 20-25%)
- Click-through rate (target: 2-5%)
- Conversion rate
- Unsubscribe rate (keep under 0.5%)
- Bounce rate (keep under 2%)

### A/B Testing Elements
- Subject lines
- Send times
- CTA button colors/text
- Email length
- Personalization elements