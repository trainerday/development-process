---
title: Let People Know They Must Accept Location Or Bluetooth Wont Work For Android
type: note
permalink: product-development/os-projects/td-mobile/backlogs/let-people-know-they-must-accept-location-or-bluetooth-wont-work-for-android
---

# Let People Know They Must Accept Location or Bluetooth Won't Work for Android

## Overview
Inform Android users that they must accept location permissions or Bluetooth functionality won't work properly.

## Priority
Medium

## Labels
- Android
- Permissions
- User Experience
- Bluetooth

## Acceptance Criteria
- [ ] Add clear messaging about location permission requirement
- [ ] Explain why location is needed for Bluetooth functionality
- [ ] Show permission prompt at appropriate time
- [ ] Provide helpful error messages when permission is denied
- [ ] Add settings link to enable permissions later
- [ ] Test on various Android versions

## Technical Notes
- Android requires location permission for Bluetooth LE scanning
- Need to educate users why this seemingly unrelated permission is needed
- Should handle permission denial gracefully

## Related Links
- Trello Card ID: #30