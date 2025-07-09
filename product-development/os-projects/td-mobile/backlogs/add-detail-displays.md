---
title: add-detail-displays
type: note
permalink: product-development/os-projects/td-mobile/backlogs/add-detail-displays
---

# Add Detail Displays

## Overview
Add detailed data displays when clicking on graphs, similar to the website functionality where you can mouse over a graph and see interval details.

## Priority
Medium

## Description
Like on the website, users should be able to interact with graphs to see detailed information about specific intervals. Need to decide implementation approach for different locations:

1. Today tab - clicking on graph shows popup
2. Workouts - clicking to see details  
3. History - workout details view
4. Main workout during training - could click on lower section of graph

## Acceptance Criteria
- [ ] Implement graph interaction for detail viewing
- [ ] Add detail popups/displays for Today tab graphs
- [ ] Add detail viewing for Workouts section
- [ ] Add detail viewing for History/workout details
- [ ] Consider implementation for active workout screen
- [ ] Ensure consistent user experience across all locations
- [ ] Display relevant interval data (power, HR, cadence, etc.)

## Technical Notes
- Should match website functionality where possible
- Need to decide on interaction patterns (tap, long press, etc.)
- Consider screen space limitations on mobile devices
- May need different approaches for different screen sections

## Related Links
- Trello Card ID: #27