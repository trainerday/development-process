---
title: delete-account-does-not-work-new-delete-api
type: note
permalink: trainer-day/os-projects/td-mobile/backlogs/delete-account-does-not-work-new-delete-api
---

# Delete Account Does Not Work + New Delete API

## Overview
The current delete account functionality is not working properly. There is also a better delete method available in a different project (ManageUsers) that should be reviewed and potentially deployed.

## Priority
High - Account deletion is a critical user privacy feature

## Current Issue
Current delete account process is not functioning correctly.

## Proposed Solution
Review and potentially deploy the improved delete API from the ManageUsers project. The new REST API method may need additional security measures.

## Acceptance Criteria
- [ ] Fix current delete account functionality
- [ ] Review ManageUsers project delete API
- [ ] Implement improved delete method
- [ ] Add appropriate security measures to new API
- [ ] Test delete functionality thoroughly
- [ ] Ensure compliance with data privacy regulations

## Technical Notes
- ManageUsers project contains a better delete method
- Current implementation shown in attached image
- Need to add security to the REST API method

## Related Links
- Trello Card ID: #22