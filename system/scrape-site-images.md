---
title: scrape-site-images
type: note
permalink: claude-code-os/system/scrape-site-images
---

# Link/Popup Loop

## Overview
This process discovers all unique pages and popups on the UAT site through intelligent clicking and deduplication.

## Implementation Details

### Authentication
- Use cookie page: `http://trainerday.com/f8e7d6c5-b4a3-4928-8716-5a4b3c2d1e0f.html`
- Wait 1000ms after loading for cookie to set

### Repeating Element Definition
If you count 20+ similar elements (same basic structure tags and classes) with the same parent/grandparent structure and CSS classes, consider them repeating elements.

### Step 1: Initial URL Discovery
Start with these URLs:
- https://app.uat.trainerday.com/
- https://app.uat.trainerday.com/coach-jack

For each page:
- Find all href links pointing to pages in this domain
- Create a unique list of URLs (without query strings)

### Step 2: Recursive Link Discovery
- Visit each discovered link from Step 1
- Repeat the link discovery process
- Create a unique list from all discovered links

### Step 3: Apply Deduplication Rules
- From all discovered URLs, keep only:
  - All main pages (/, /activities, /library, etc.)
  - Only ONE example from `/workouts/*` paths
  - Only ONE example from `/plans/*` paths
- This reduces testing time while still covering all page types

### Step 4: Two-Level Popup Discovery
Visit all pages from Step 3 (deduplicated list) and find popups:

#### Level 1 - Dropdown Triggers
- Find all `<a>` tags with `href="#"` or blank href
- Exclude repeating elements (except the first one)
- Click each trigger and:
  - Store any redirect URLs
  - Create a hash of the new DOM patterns (HTML tags + CSS classes) for deduplication
  - Save both the hash AND the selector/index to recreate this state:
    - Example: `{hash: "abc123", selector: "button.dropdown:nth-child(3)", pageUrl: "/library"}`
    - The hash prevents duplicate clicks, the selector lets us click it again later

#### Level 2 - Dropdown Items
With the new DOM from Level 1:
- Find any new links
- Check for further DOM expansion by clicking elements
- Save the complete path to recreate states:
  - Example: `{level1: "button.dropdown:nth-child(3)", level2: "a.menu-item:nth-child(2)", pageUrl: "/library", hash: "def456"}`

### Step 5: Screenshot Collection
After collecting all links and popup states:
- Revisit each page and take a screenshot
- Recreate each unique popup state and take a screenshot
- Wait 0.5 seconds after clicking to ensure popups are fully loaded

### Step 6: Screenshot Analysis & Deduplication

**Part 1: Visibility Detection**
- Compare each popup screenshot with its base page screenshot
- Use pixel sampling (1% of pixels) to detect visual differences
- Mark screenshots with "no_visible_change" if < 2% pixels are different
- Mark screenshots with "visible_popup" if ≥ 2% pixels are different

**Part 2: Popup Identification (for visible changes)**
- Use GPT-4 Vision (gpt-4o-mini model) to identify and classify popups
- Detect popup types: modal, dropdown, tooltip, notification
- Extract popup names and descriptions for grouping

**Part 3: Center-Overlay Modal Detection & Cropping**
- Specialized detection for white modals on dark overlays (centered)
- Dynamic boundary detection scanning from center outward
- Automatic cropping with padding (20px top, 15px sides) to avoid clipping
- Only works for specific popup style pattern

**Part 4: Cross-Page Deduplication**
- Group identical popups by name across different pages
- Identify which popups are reused throughout the site
- Generate recommendations for which screenshots to keep/delete

**Output:** `data/step6-consolidated-analysis.json` containing:
- Visibility results for all screenshots
- Popup analysis with names and types
- Grouped popups showing cross-page usage
- Recommendations for deletion

**Known Issues:**
- Some L1/L2 screenshots may not show actual popups due to Step 5 bug where elements aren't being clicked properly before screenshots
- Center-Overlay Modal detection is limited to specific visual pattern

### Step 7: Compare Sitemaps
- Load previous sitemap from `data/sitemap.json`
- Compare with current sitemap to identify:
  - New pages added
  - Pages removed
  - Popup changes (new/removed)
- Generate change report

### Step 8: Update Sitemap
- Update `data/sitemap.json` with the new sitemap
- Include timestamp and version information
- Preserve history of changes for tracking
	