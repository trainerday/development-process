---
title: If Power Doubling Is On
type: note
permalink: product-development/os-projects/td-mobile/backlogs/if-power-doubling-is-on
---

# If Power Doubling Is On

## Overview
Add a warning system to detect when power doubling setting is enabled but should not be, based on power readings during workout start.

## Priority
Medium

## Description
If power doubling is enabled in settings and the user is getting >1.5X power from seconds 5-10 average at the beginning of a workout, show a warning that power doubling is on in the settings and seems like it should not be.

## Acceptance Criteria
- [ ] Monitor power readings during first 5-10 seconds of workout
- [ ] Calculate if power is >1.5X expected levels
- [ ] Display warning when power doubling seems incorrectly enabled
- [ ] Warning should clearly explain the issue
- [ ] Provide option to disable power doubling from warning
- [ ] Only show warning once per workout session

## Technical Notes
- Need to implement power monitoring during workout initialization
- Warning should be non-intrusive but clear
- Consider adding setting to disable this warning for advanced users

## Related Links
- Trello Card ID: #21