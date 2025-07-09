---
title: Scrape Site Images
type: note
permalink: product-development/os-projects/td-ai-testing/backlogs/scrape-site-images
---

# Scrape Site Images - Link/Popup Loop Implementation

## Overview
This document describes the implementation of the "Link/Popup Loop" process for discovering all unique pages and popups on the TrainerDay UAT site through intelligent clicking and deduplication.

## Implementation Steps

### Step 1: Initial URL Discovery
- Start with seed URLs
- Visit each page and collect all internal links
- Output: `step1-initial-urls.json`

### Step 2: Recursive Link Discovery with Repeating Element Detection
- Visit all URLs from Step 1
- Use `shared/find-repeating-elements.js` to detect repeating patterns
- Only collect first instance from groups of 20+ similar elements
- Prevents collecting hundreds of workout/plan URLs
- Output: `step1-2-all-urls.json`

### Step 3: URL Deduplication
- **IMPORTANT: Contains hardcoded patterns for TrainerDay site structure**
- Patterns:
  - `/workouts/*` - Keeps only first workout URL as example
  - `/plans/*` - Keeps only first plan URL as example
- These patterns are hardcoded in regex form:
  ```javascript
  if (urlPath.match(/^\/workouts\/[^\/]+$/)) { ... }
  else if (urlPath.match(/^\/plans\/[^\/]+$/)) { ... }
  ```
- Assumption: All workout pages and plan pages follow same template
- Deduplication is applied globally across all discovered URLs
- Output: `step1-2-3-deduplicated-urls.json`

### Step 4: First Level Popup Discovery
- Visit each URL from Step 3
- Find all clickable elements (links, buttons)
- Click each element and detect DOM changes
- Use MD5 hashing to avoid duplicate patterns
- Output: `step4-triggers.json`

### Step 5: Second Level Popup Discovery
- For each first-level trigger that caused DOM changes
- Click the trigger to open the popup
- Find clickable elements within the popup
- Test each element for navigation or further DOM changes
- Output: `step5-second-level.json`

### Step 6: Screenshot All Visible Modals
- Capture base page screenshots
- Attempt to trigger each discovered popup
- Take screenshots of triggered popups
- Output: `screenshots/` directory and `step6-screenshots-manifest.json`

### Step 7: Visibility Detection
- Compare popup screenshots with base pages
- Detect if visible changes occurred
- Filter out non-visible popups
- Output: `step7-visibility.json`

### Step 8: Popup Identification (GPT-4 Vision)
- Analyze visible popups with GPT-4 Vision
- Identify popup types (modal, dropdown, tooltip, etc.)
- Group similar popups
- Output: `step8-popup-identification.json`

### Step 9: Modal Detection & Cropping
- Identify center-overlay modals
- Crop modal content from full screenshots
- Save cropped versions
- Output: `screenshots/cropped-popups/` and `step9-modal-cropping.json`

### Step 10: Cross-Page Deduplication
- Remove popups too similar to base pages
- Identify duplicate popups across pages
- Group by popup names
- Move duplicates to separate folder
- Output: `step10-deduplication.json`

### Step 11: Name Normalization (Not implemented)
- Normalize popup names for consistency
- Create final popup catalog

### Step 12: Update Sitemap (Not implemented)
- Update sitemap.json with discovered content
- Include page URLs and popup information

## Shared Modules

### shared/find-repeating-elements.js
```javascript
function findRepeatingElements(elements, options = {}) {
    const { threshold = 20, selector = 'a' } = options;
    // Groups elements by signature (tag, classes, parent structure)
    // Returns filtered list with only first instance from large groups
}
```

### shared/cleanup-helper.js
```javascript
function cleanupAndPrepare(baseDir, outputFiles) {
    // Creates data directory if needed
    // Removes specified output files before running
}
```

## Authentication
- Uses cookie page: `https://trainerday.com/f8e7d6c5-b4a3-4928-8716-5a4b3c2d1e0f.html`
- Wrapped in try-catch to handle timeouts gracefully

## Known Hardcoded Values

1. **Cookie URL**: `https://trainerday.com/f8e7d6c5-b4a3-4928-8716-5a4b3c2d1e0f.html`
2. **Base URL**: `https://app.uat.trainerday.com`
3. **Seed URLs**: 
   - `https://app.uat.trainerday.com/`
   - `https://app.uat.trainerday.com/coach-jack`
4. **URL Patterns (Step 3)**:
   - `/workouts/*` - Deduplication pattern
   - `/plans/*` - Deduplication pattern
5. **Repeating element threshold**: 20 (elements appearing 20+ times are considered repeating)

## Current Status
- All steps run successfully
- Steps 1-5 produce expected results
- Steps 6-10 functional but may need selector updates for popup capture
- System is fully operational and maintainable