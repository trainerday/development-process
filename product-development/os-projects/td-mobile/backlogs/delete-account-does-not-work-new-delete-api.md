---
title: delete-account-does-not-work-new-delete-api
type: note
permalink: product-development/os-projects/td-mobile/backlogs/delete-account-does-not-work-new-delete-api
---

# Delete Account Does Not Work + New Delete API

## Overview
The current delete account functionality is not working properly. There is also a better delete method available in a different github project (ManageUsers) that should be reviewed and deployed to production

Right now I do it like the attached image but there is also a rest api method in there. Maybe we should add some security to it.  The mobile app should call this method.  Make sure to tell them this can't be undone and will not stop their billing.

![[Pasted image 20250707153740.png]]

