---
title: Does activity auto pairing work
type: note
permalink: trainer-day/os-projects/td-web/backlogs/does-activity-auto-pairing-work
tags:
- '["investigation"'
- '"bug"'
- '"activities"'
- '"later"'
- '"backlog"]'
---

# Does activity auto pairing work?

## Status
- **Priority**: Later
- **Type**: Investigation/Bug
- **Labels**: Bug, Investigation
- **Created**: 2025-01-03
- **Updated**: 2025-01-03

## Description
Investigate whether activity auto pairing is functioning correctly. One user reported it did not work for them.

## Details
- User report indicates auto pairing feature may not be working
- Need to verify current functionality
- Determine if this is a widespread issue or isolated case
- Activity auto pairing should match completed activities with planned workouts

## Technical Notes
- Review auto pairing algorithm and logic
- Check matching criteria (time, duration, power, etc.)
- Verify background job execution
- Review error logs for pairing failures
- Test with various activity types and sources
- Check timezone handling in matching logic

## Acceptance Criteria
- [ ] Confirm current auto pairing functionality status
- [ ] Identify root cause if feature is broken
- [ ] Document expected behavior and matching criteria
- [ ] Fix any identified issues
- [ ] Add monitoring/logging for pairing success rate
- [ ] User receives notification when pairing occurs
- [ ] Manual pairing option available as fallback

## Resources
- User report of non-functioning auto pairing
- Activity pairing documentation
- System logs

## Notes
- May need to gather more user reports
- Consider adding diagnostic tools for troubleshooting
- Feature may work inconsistently across different integrations