---
title: 3 Testing Process
type: note
permalink: product-development/system/workflows/automated-development/3-testing-process
---

# Testing Process

## Local Testing (Dev Testing)

*Instructions for Claude Code on how to test implementations locally during development*

### When to Run Local Testing
- After completing development work in `3-in-progress`
- Before moving items to `4-staging`

### Local Testing Steps

0. **Install Testing Dependencies (if needed)**
   - Check if Puppeteer is installed: `npm list puppeteer`
   - If not installed, run: `npm install --save-dev puppeteer`
   - This will also download Chromium for headless testing

1. **Start Local Server**
   - Check if server is already running (test localhost connection)
   - If server is not running, execute: `npm run dev` or `npm start`
   - Verify server starts without errors
   - Note the local URL (typically `http://localhost:3000` or similar)
   - Wait for server to be fully ready before proceeding

2. **Screenshot Capture & AI Analysis**
   - Create automated test file in project's `testing/` folder
   - Use Puppeteer for screenshot capture and testing
   - **Create test file**: `testing/[feature-name]-visual-test.js`
   - **For home page**: Run standard visual tests on the home page (`testing/index-visual-test.js`)
   - Test should:
     - Launch headless Chrome with Puppeteer
     - Navigate to the implemented feature
     - Take screenshots of key pages/features
     - Capture both desktop (1920x1080) and mobile (375x667) viewports
     - Save screenshots to `testing/screenshots/` folder
     - Check for console errors
     - Check for network 404s
     - Verify key elements are present
   - **Send screenshots to OpenAI Vision API for analysis**
     - Use API key from environment variable
     - **Reference visual standards template** (trainer-day/templates/visual-standards-template.md)
     - Ask specific validation questions:
       * "Are there any broken images, missing assets, or 404 placeholders visible?"
       * "Does the layout look professional and properly aligned?"
       * "Are all UI elements rendering correctly (buttons, forms, text, navigation)?"
       * "Does this page match modern web design standards?"
       * "Are there any obvious visual bugs or styling issues?"
       * "Is the content readable and properly formatted?"
       * **"Does this follow our visual standards: Poppins font, TrainerDay logo present, consistent input heights?"**
       * **"Does this implementation match the task specifications and requirements?"**
       * **"Are all the features/elements mentioned in the task requirements actually present and visible?"**
       * **"Are all text input boxes the same height?"**
       * **"Are all dropdown/select boxes the same height as the text inputs?"**
       * **"Do all form elements have consistent visual styling and alignment?"**
     - Get AI assessment: Pass/Fail with specific issues noted

3. **Visual Validation**
   - Review OpenAI vision analysis results
   - If AI reports any issues, investigate and fix before proceeding
   - Manual verification of AI findings:
     - Missing or broken images/assets (like logos)
     - Layout issues or misaligned elements
     - Correct fonts and styling
     - Responsive design working properly

4. **Console & Network Error Checking**
   - Open browser developer tools (F12)
   - Check Console tab for JavaScript errors:
     - Red error messages
     - Uncaught exceptions
     - Failed function calls
   - Check Network tab for failed requests:
     - 404 errors (missing files)
     - 500 server errors
     - Failed CSS/JS/image loads
     - Any red entries indicating failed requests
   - Document all errors found with details
   - **Critical**: No JavaScript errors or 404s should exist for basic functionality

5. **Basic Functional Testing**
   - Test key interactions (clicks, form submissions, navigation)
   - Verify all links work and don't produce console errors
   - Check that JavaScript functionality works as expected
   - Test core functionality of the feature

6. **Generate Test Report**
   - Document what was tested
   - Note any issues found
   - Mark as "Passed Local Testing" or "Failed - needs fixes"
   - **Save test report in project's `testing/` folder**
   - **File name should match the backlog item name** (e.g., `design-main-ui-ux-and-power-to-speed-calculator-test-report.md`)
   - Include screenshots and OpenAI analysis results in the report

### Success Criteria
- All screenshots show expected visual results
- OpenAI vision analysis reports no critical issues
- **Zero JavaScript errors in browser console**
- **Zero 404 errors or failed network requests**
- Core functionality works as intended
- Feature meets basic requirements

---

## Staging Testing (Future)
*More comprehensive integration testing will be documented here later*

## Screenshot Capture & AI Analysis
   - Create automated test file in project's `testing/` folder
   - Use Puppeteer for screenshot capture and testing
   - **Create test file**: `testing/[feature-name]-visual-test.js`
   - **For home page**: Run standard visual tests on the home page (`testing/index-visual-test.js`)
   - Test should:
     - Launch headless Chrome with Puppeteer
     - Navigate to the implemented feature
     - Take screenshots of key pages/features
     - Capture both desktop (1920x1080) and mobile (375x667) viewports
     - Save screenshots to `testing/temp/screenshots/` folder (add temp to .gitignore)
     - Check for console errors
     - Check for network 404s
     - Verify key elements are present
     - **Check form element height consistency** (all inputs/dropdowns should be same height)
     - **Check label alignment across form rows** (labels on same row should have 0px vertical offset)
     - **Handle responsive layouts** (skip row alignment checks for single-column mobile layouts)
   - **Physics/Calculation Accuracy Testing** (for calculator features):
     - If original calculator URL is provided in specifications, test accuracy against it
     - Use test values (e.g., 100W, 250W) to compare results
     - Results should be within acceptable tolerance (typically ±10%)
     - Document any significant calculation differences
   - **Send screenshots to OpenAI Vision API for analysis**
     - Use API key from environment variable  
     - **Use critical visual inspection prompt**:
       ```
       CRITICAL VISUAL INSPECTION: Look very carefully at this [Feature Name] interface screenshot. I need you to identify ANY visual inconsistencies, no matter how small.

       SPECIFIC REQUIREMENTS TO CHECK:
       1. FORM ELEMENT HEIGHTS: Look at ALL input boxes and dropdown boxes. Are they EXACTLY the same height? Even a 1-2 pixel difference is a problem.
       2. ALIGNMENT: Are form elements aligned properly on the same baseline?
       3. VISUAL BUGS: Any broken images, missing assets, or 404 placeholders?
       4. PROFESSIONAL APPEARANCE: Does this look like a polished, production-ready interface?
       5. CONSISTENCY: Do all similar elements (inputs, dropdowns, buttons) have identical styling?

       PAY SPECIAL ATTENTION TO:
       - **LABEL ALIGNMENT**: Are the labels above form fields properly aligned?
       - **ROW ALIGNMENT**: For form fields on the same row, are their labels at the same height/baseline?
       - **LEFT ALIGNMENT**: Are labels on the same row aligned to the left edge consistently?
       - **LABEL HEIGHT**: Do labels take up the same vertical space across a row?

       BE EXTREMELY CRITICAL. If you see ANY visual inconsistencies, report them. Don't overlook height differences, alignment issues, or styling inconsistencies.

       Respond with a JSON object:
       {
         "issues": ["specific description of each visual problem found"],
         "height_consistency": "good/poor - describe any height differences you see",
         "label_alignment": "good/poor - describe any label alignment issues",
         "row_alignment": "good/poor - describe if elements on the same row are properly aligned",
         "overall_assessment": "detailed assessment"
       }
       ```
     - **Reference visual standards template** (trainer-day/templates/visual-standards-template.md)
     - Ask specific validation questions:
       * "Are there any broken images, missing assets, or 404 placeholders visible?"
       * "Does the layout look professional and properly aligned?"
       * "Are all UI elements rendering correctly (buttons, forms, text, navigation)?"
       * "Does this page match modern web design standards?"
       * "Are there any obvious visual bugs or styling issues?"
       * "Is the content readable and properly formatted?"
       * **"Does this follow our visual standards: Poppins font, TrainerDay logo present, consistent input heights?"**
       * **"Does this implementation match the task specifications and requirements?"**
       * **"Are all the features/elements mentioned in the task requirements actually present and visible?"**
     - Get AI assessment: Pass/Fail with specific issues noted

## Enhanced Visual Testing Implementation

### Puppeteer Test Structure Template

**File**: `testing/[feature-name]-visual-test.js`

```javascript
const puppeteer = require('puppeteer');
const fs = require('fs');
const path = require('path');

// Test configuration
const TEST_URL = 'http://localhost:3000/[feature-path]';
const SCREENSHOTS_DIR = path.join(__dirname, 'temp', 'screenshots');

// Ensure temp directory exists and add to .gitignore
if (!fs.existsSync(path.join(__dirname, 'temp'))) {
  fs.mkdirSync(path.join(__dirname, 'temp'), { recursive: true });
}
if (!fs.existsSync(SCREENSHOTS_DIR)) {
  fs.mkdirSync(SCREENSHOTS_DIR, { recursive: true });
}

// Viewport configurations
const VIEWPORTS = {
  desktop: { width: 1920, height: 1080 },
  mobile: { width: 375, height: 667 }
};

// Test results tracking
let testResults = {
  passed: true,
  errors: [],
  warnings: [],
  screenshots: [],
  timestamp: new Date().toISOString()
};

async function runVisualTests() {
  const browser = await puppeteer.launch({ headless: 'new' });
  
  try {
    for (const [device, viewport] of Object.entries(VIEWPORTS)) {
      const page = await browser.newPage();
      await page.setViewport(viewport);
      
      // Error monitoring
      const consoleErrors = [];
      const networkErrors = [];
      
      page.on('console', msg => {
        if (msg.type() === 'error') consoleErrors.push(msg.text());
      });
      
      page.on('response', response => {
        if (response.status() >= 400) {
          networkErrors.push({ url: response.url(), status: response.status() });
        }
      });
      
      // Navigate and screenshot
      await page.goto(TEST_URL, { waitUntil: 'networkidle2' });
      const screenshotPath = path.join(SCREENSHOTS_DIR, `[feature-name]-${device}.png`);
      await page.screenshot({ path: screenshotPath, fullPage: true });
      testResults.screenshots.push(screenshotPath);
      
      // OpenAI Vision Analysis
      const visionAnalysis = await analyzeScreenshotWithOpenAI(screenshotPath, device);
      if (visionAnalysis.issues && visionAnalysis.issues.length > 0) {
        visionAnalysis.issues.forEach(issue => {
          testResults.warnings.push(`OpenAI Vision (${device}): ${issue}`);
        });
      }
      
      // Check required elements
      const elementsToCheck = {
        'Logo': 'img[src*="logo"]',
        'Title': 'h1, h2', 
        // Add feature-specific selectors
      };
      
      for (const [name, selector] of Object.entries(elementsToCheck)) {
        const element = await page.$(selector);
        if (!element) {
          testResults.warnings.push(`Missing element on ${device}: ${name}`);
        }
      }
      
      // Form element height consistency check
      const elementHeights = await page.evaluate(() => {
        const elements = { textInputs: [], selects: [], allHeights: [] };
        
        document.querySelectorAll('input[type="number"], input[type="text"]').forEach(input => {
          const height = window.getComputedStyle(input).height;
          elements.textInputs.push({ id: input.id || 'unnamed', height: height });
          elements.allHeights.push(parseFloat(height));
        });
        
        document.querySelectorAll('select').forEach(select => {
          const height = window.getComputedStyle(select).height;
          elements.selects.push({ id: select.id || 'unnamed', height: height });
          elements.allHeights.push(parseFloat(height));
        });
        
        const uniqueHeights = [...new Set(elements.allHeights)];
        elements.consistent = uniqueHeights.length === 1;
        elements.uniqueHeights = uniqueHeights;
        
        return elements;
      });
      
      if (!elementHeights.consistent) {
        testResults.warnings.push(`Form elements have inconsistent heights on ${device}: ${elementHeights.uniqueHeights.join(', ')}px`);
      }
      
      // Label alignment check (desktop only for multi-column layouts)
      if (device === 'desktop') {
        const labelAlignment = await page.evaluate(() => {
          const formGrid = document.querySelector('.form-grid');
          if (!formGrid) return { overallAlignment: true, message: 'No form grid found' };
          
          const gridColumns = window.getComputedStyle(formGrid).gridTemplateColumns;
          const isSingleColumn = !gridColumns.includes(' ');
          
          if (isSingleColumn) {
            return { overallAlignment: true, isSingleColumn: true, message: 'Single column layout' };
          }
          
          const labels = { leftColumn: [], rightColumn: [], rows: [] };
          const formGroups = document.querySelectorAll('.form-group');
          
          formGroups.forEach((group, index) => {
            const label = group.querySelector('label');
            if (label) {
              const rect = label.getBoundingClientRect();
              const labelInfo = {
                text: label.textContent.trim(),
                top: Math.round(rect.top),
                height: Math.round(rect.height)
              };
              
              if (index % 2 === 0) {
                labels.leftColumn.push(labelInfo);
              } else {
                labels.rightColumn.push(labelInfo);
              }
            }
          });
          
          let alignmentIssues = [];
          const rowCount = Math.min(labels.leftColumn.length, labels.rightColumn.length);
          
          for (let i = 0; i < rowCount; i++) {
            const leftLabel = labels.leftColumn[i];
            const rightLabel = labels.rightColumn[i];
            
            if (leftLabel && rightLabel) {
              const topDifference = Math.abs(leftLabel.top - rightLabel.top);
              
              if (topDifference > 2) {
                alignmentIssues.push(`Row ${i + 1}: "${leftLabel.text}" and "${rightLabel.text}" labels have ${topDifference}px vertical offset`);
              }
            }
          }
          
          return {
            alignmentIssues: alignmentIssues,
            overallAlignment: alignmentIssues.length === 0
          };
        });
        
        if (!labelAlignment.overallAlignment) {
          labelAlignment.alignmentIssues.forEach(issue => {
            testResults.warnings.push(`Label alignment issue on ${device}: ${issue}`);
          });
        }
      }
      
      // Error reporting
      if (consoleErrors.length > 0) {
        testResults.errors.push(`Console errors on ${device}: ${consoleErrors.join(', ')}`);
        testResults.passed = false;
      }
      
      if (networkErrors.length > 0) {
        testResults.errors.push(`Network errors on ${device}: ${networkErrors.map(e => `${e.url} (${e.status})`).join(', ')}`);
        testResults.passed = false;
      }
      
      await page.close();
    }
  } finally {
    await browser.close();
  }
  
  // Generate test report
  generateReport();
}

async function analyzeScreenshotWithOpenAI(screenshotPath, device) {
  const apiKey = process.env.OPENAI_API_KEY;
  if (!apiKey) {
    return { issues: ['OpenAI API key not found'], overall_assessment: 'api_key_missing' };
  }
  
  try {
    const imageBuffer = fs.readFileSync(screenshotPath);
    const base64Image = imageBuffer.toString('base64');
    
    const payload = {
      model: "gpt-4o-mini",
      messages: [{
        role: "user",
        content: [{
          type: "text",
          text: `CRITICAL VISUAL INSPECTION: Look very carefully at this interface screenshot. I need you to identify ANY visual inconsistencies, no matter how small.

SPECIFIC REQUIREMENTS TO CHECK:
1. FORM ELEMENT HEIGHTS: Look at ALL input boxes and dropdown boxes. Are they EXACTLY the same height? Even a 1-2 pixel difference is a problem.
2. ALIGNMENT: Are form elements aligned properly on the same baseline?
3. VISUAL BUGS: Any broken images, missing assets, or 404 placeholders?
4. PROFESSIONAL APPEARANCE: Does this look like a polished, production-ready interface?
5. CONSISTENCY: Do all similar elements (inputs, dropdowns, buttons) have identical styling?

PAY SPECIAL ATTENTION TO:
- **LABEL ALIGNMENT**: Are the labels above form fields properly aligned?
- **ROW ALIGNMENT**: For form fields on the same row, are their labels at the same height/baseline?
- **LEFT ALIGNMENT**: Are labels on the same row aligned to the left edge consistently?
- **LABEL HEIGHT**: Do labels take up the same vertical space across a row?

BE EXTREMELY CRITICAL. If you see ANY visual inconsistencies, report them.

Respond with a JSON object:
{
  "issues": ["specific description of each visual problem found"],
  "height_consistency": "good/poor - describe any height differences you see",
  "label_alignment": "good/poor - describe any label alignment issues", 
  "row_alignment": "good/poor - describe if elements on the same row are properly aligned",
  "overall_assessment": "detailed assessment"
}`
        }, {
          type: "image_url",
          image_url: { url: `data:image/png;base64,${base64Image}` }
        }]
      }],
      max_tokens: 500
    };
    
    const response = await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${apiKey}`,
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(payload)
    });
    
    if (!response.ok) {
      return { issues: [`API request failed: ${response.status}`], overall_assessment: 'api_error' };
    }
    
    const data = await response.json();
    const content = data.choices[0].message.content;
    
    try {
      return JSON.parse(content);
    } catch (parseError) {
      return {
        issues: content.includes('issue') || content.includes('problem') ? [content] : [],
        overall_assessment: content.includes('good') || content.includes('excellent') ? 'good' : 'review_needed'
      };
    }
  } catch (error) {
    return { issues: [`Vision analysis failed: ${error.message}`], overall_assessment: 'analysis_failed' };
  }
}

function generateReport() {
  console.log('\\n📊 TEST RESULTS SUMMARY\\n' + '='.repeat(50));
  
  if (testResults.passed) {
    console.log('✅ ALL TESTS PASSED!\\n');
  } else {
    console.log('❌ TESTS FAILED!\\n');
  }
  
  if (testResults.errors.length > 0) {
    console.log('ERRORS:');
    testResults.errors.forEach(error => console.log(`  - ${error}`));
  }
  
  if (testResults.warnings.length > 0) {
    console.log('WARNINGS:');
    testResults.warnings.forEach(warning => console.log(`  - ${warning}`));
  }
  
  console.log('SCREENSHOTS SAVED:');
  testResults.screenshots.forEach(screenshot => console.log(`  - ${screenshot}`));
  
  // Write JSON report
  const reportPath = path.join(__dirname, 'temp', 'test-results.json');
  fs.writeFileSync(reportPath, JSON.stringify(testResults, null, 2));
  console.log(`\\n📄 Detailed report saved to: ${reportPath}`);
}

// Run the tests
runVisualTests().catch(error => {
  console.error('Test runner failed:', error);
  process.exit(1);
});
```

### Calculator Accuracy Testing Template

For calculator features, add accuracy validation:

```javascript
// Add to test after basic functionality tests
async function testCalculatorAccuracy(page) {
  console.log('🧮 Testing calculator accuracy...');
  
  const testCases = [
    { power: 100, expectedSpeed: null }, // Will be filled from original calculator
    { power: 250, expectedSpeed: null }
  ];
  
  // If original calculator URL provided, test against it first
  const originalCalculatorURL = '[ORIGINAL_CALCULATOR_URL]'; // From specifications
  
  if (originalCalculatorURL) {
    console.log('📊 Comparing against original calculator...');
    
    for (const testCase of testCases) {
      // Test our calculator
      await page.evaluate((power) => {
        document.querySelector('#powerOutput').value = power;
        // Trigger calculation
        document.querySelector('#powerOutput').dispatchEvent(new Event('input'));
      }, testCase.power);
      
      await page.waitForTimeout(500); // Allow calculation
      const ourResult = await page.$eval('#speedResult', el => parseFloat(el.textContent));
      
      // Test original calculator (if accessible)
      try {
        const originalPage = await browser.newPage();
        await originalPage.goto(originalCalculatorURL);
        // Set values and get result from original calculator
        // This will vary based on original calculator's interface
        const originalResult = await getOriginalCalculatorResult(originalPage, testCase.power);
        
        const difference = Math.abs(ourResult - originalResult);
        const percentDifference = (difference / originalResult) * 100;
        
        console.log(`  Power ${testCase.power}W: Our result: ${ourResult}, Original: ${originalResult}, Difference: ${percentDifference.toFixed(1)}%`);
        
        if (percentDifference > 10) { // Allow 10% tolerance
          testResults.warnings.push(`Calculator accuracy issue: ${testCase.power}W shows ${percentDifference.toFixed(1)}% difference from original`);
        }
        
        await originalPage.close();
      } catch (error) {
        testResults.warnings.push(`Could not test against original calculator: ${error.message}`);
      }
    }
  }
}
```

### Key Testing Requirements Checklist

✅ **Visual Consistency**
- All form elements (inputs, selects) exactly same height
- Labels on same row have 0px vertical offset (desktop)
- No broken images or 404 placeholders
- Professional appearance matching visual standards

✅ **Technical Validation**  
- Zero console errors
- Zero network 404s
- All required elements present
- Basic functionality working

✅ **Responsive Design**
- Desktop (1920x1080) and mobile (375x667) viewports
- Single column mobile layouts skip row alignment checks
- All elements render properly on both screen sizes

✅ **Calculator Accuracy** (when applicable)
- Test against original calculator if URL provided
- Results within ±10% tolerance acceptable
- Test multiple power levels (e.g., 100W, 250W)
- Document any significant calculation differences

✅ **Critical OpenAI Vision Analysis**
- Use enhanced prompt for maximum sensitivity
- JSON response format for structured feedback
- Focus on height consistency and label alignment
- Report all visual inconsistencies, no matter how minor

## Enhanced Layout Testing with Overlap Detection

### Overlap Detection Requirements
All visual tests must include specific overlap detection to catch layout issues:

#### JavaScript-Based Overlap Detection
```javascript
// Add to Puppeteer tests
async function checkForOverlaps(page, device) {
  return await page.evaluate(() => {
    const overlaps = [];
    
    // Get all visible elements with significant size
    const elements = Array.from(document.querySelectorAll('*')).filter(el => {
      const rect = el.getBoundingClientRect();
      return rect.width > 10 && rect.height > 10 && 
             getComputedStyle(el).visibility !== 'hidden' &&
             getComputedStyle(el).display !== 'none';
    });
    
    // Check for overlaps between elements
    for (let i = 0; i < elements.length; i++) {
      for (let j = i + 1; j < elements.length; j++) {
        const el1 = elements[i];
        const el2 = elements[j];
        
        // Skip if one element contains the other
        if (el1.contains(el2) || el2.contains(el1)) continue;
        
        const rect1 = el1.getBoundingClientRect();
        const rect2 = el2.getBoundingClientRect();
        
        // Check for overlap
        const overlap = !(rect1.right <= rect2.left || 
                         rect2.right <= rect1.left || 
                         rect1.bottom <= rect2.top || 
                         rect2.bottom <= rect1.top);
        
        if (overlap) {
          const overlapWidth = Math.min(rect1.right, rect2.right) - Math.max(rect1.left, rect2.left);
          const overlapHeight = Math.min(rect1.bottom, rect2.bottom) - Math.max(rect1.top, rect2.top);
          const overlapArea = overlapWidth * overlapHeight;
          
          // Only report significant overlaps (> 100 square pixels)
          if (overlapArea > 100) {
            overlaps.push({
              element1: el1.tagName + (el1.id ? '#' + el1.id : ''),
              element2: el2.tagName + (el2.id ? '#' + el2.id : ''),
              overlapArea: Math.round(overlapArea)
            });
          }
        }
      }
    }
    
    return { overlaps };
  });
}
```

#### Enhanced OpenAI Vision Prompt for Overlap Detection
```
CRITICAL LAYOUT INSPECTION: Examine this [Feature Name] interface screenshot for ANY layout issues, especially overlapping elements.

SPECIFIC OVERLAP DETECTION REQUIREMENTS:
1. **OVERLAPPING ELEMENTS**: Look for ANY elements that overlap, cover, or obstruct other elements
2. **TEXT OVERLAP**: Check if any text overlaps with other text, buttons, or form elements
3. **BUTTON OVERLAP**: Verify buttons don't overlap with each other or other UI elements
4. **FORM OVERLAP**: Ensure form inputs, labels, and dropdowns don't overlap
5. **NAVIGATION OVERLAP**: Check if navigation overlaps with main content
6. **CONTENT OVERFLOW**: Look for any content extending beyond its container boundaries

CRITICAL VISUAL ISSUES TO DETECT:
- Elements positioned on top of each other incorrectly
- Text that runs into other text or elements
- Buttons that cover or are covered by other elements
- Form elements that overlap with labels or other inputs
- Any UI element that appears "cut off" or partially hidden
- Misaligned elements that create visual conflicts

LAYOUT CONSISTENCY CHECKS:
1. FORM ELEMENT HEIGHTS: Are all input boxes and dropdown boxes exactly the same height?
2. ALIGNMENT: Are form elements aligned properly on the same baseline?
3. VISUAL BUGS: Any broken images, missing assets, or 404 placeholders?
4. PROFESSIONAL APPEARANCE: Does this look polished and production-ready?
5. CONSISTENCY: Do all similar elements have identical styling and proper spacing?

BE EXTREMELY DETAILED about any overlapping elements. If elements are overlapping, describe:
- Which specific elements are overlapping
- Where the overlap occurs (top, bottom, left, right)
- How severe the overlap is

Respond with a JSON object:
{
  "issues": ["specific description of each overlap or layout problem found"],
  "overlap_detected": true/false,
  "overlap_details": ["detailed description of each overlap found"],
  "height_consistency": "good/poor - describe any height differences",
  "label_alignment": "good/poor - describe any label alignment issues",
  "layout_assessment": "good/poor - describe overall layout quality",
  "critical_issues": ["any critical layout problems that must be fixed"],
  "overall_assessment": "detailed assessment focusing on overlaps and layout"
}
```

### Overlap Testing Requirements

✅ **Mandatory Overlap Checks**
- JavaScript-based geometric overlap detection
- OpenAI vision analysis focusing on visual overlaps
- Multi-device testing (desktop, tablet, mobile)
- Element boundary validation
- Content overflow detection

✅ **Overlap Reporting**
- Document all overlaps > 100 square pixels
- Identify specific elements involved
- Calculate overlap area and severity
- Generate visual evidence via screenshots
- Create actionable fix recommendations

✅ **Acceptable vs Critical Overlaps**
- **Acceptable**: Intentional overlays (modals, tooltips, dropdowns)
- **Critical**: Unintentional overlaps affecting usability
- **Blocking**: Any overlap that obscures interactive elements
- **Minor**: Small overlaps (<50px²) that don't affect function

This enhanced testing catches layout issues early and ensures professional, polished interfaces.

## Enhanced GPT Instructions for Layout Issue Detection

### Critical Visual Inspection Prompt Template

When analyzing screenshots with OpenAI Vision API, use this enhanced prompt to catch layout width issues:

```
CRITICAL LAYOUT INSPECTION: Examine this [Feature Name] interface screenshot for ANY layout issues, especially width and container problems.

SPECIFIC WIDTH AND CONTAINER DETECTION REQUIREMENTS:
1. **INPUT BOX WIDTH**: Are input boxes appropriately sized for their containers? Look for:
   - Input boxes that appear too wide for their grid containers
   - Form elements extending beyond their allocated space
   - Inconsistent spacing between form elements
   - Unit labels (like "kg", "watts") being cut off or extending beyond containers

2. **CONTAINER OVERFLOW**: Check for any content extending beyond container boundaries:
   - Text or elements that get cut off at the edges
   - Horizontal scrollbars appearing when they shouldn't
   - Elements extending beyond the visible viewport
   - Form grids that are too wide for their parent containers

3. **RESPONSIVE LAYOUT ISSUES**: Look for:
   - Elements that break layout on smaller screens
   - Mobile layouts where text or elements extend beyond screen width
   - Inconsistent margins or padding causing alignment issues
   - Form elements that don't adapt properly to available space

4. **VISUAL SPACING PROBLEMS**: Identify:
   - Inconsistent gaps between form elements
   - Elements that appear cramped or too spread out
   - Uneven margins around containers
   - Poor utilization of available space

CRITICAL MEASUREMENTS TO ASSESS:
- Do input boxes fit comfortably within their grid cells?
- Are unit labels (kg, watts, mph, etc.) fully visible and not truncated?
- Is there adequate spacing between form elements?
- Does the overall form width make good use of available space?
- Are there any elements that appear "squished" or "stretched"?

WIDTH-SPECIFIC ISSUES TO DETECT:
- Form fields that are too narrow and look cramped
- Form fields that are too wide and break layout
- Grid containers that don't provide adequate space for their contents
- Unit labels extending beyond their designated areas
- Input groups that overflow their parent containers

BE EXTREMELY DETAILED about width and container issues. Report:
- Specific elements with width problems
- Measurements or estimates of how elements extend beyond boundaries
- Whether the overall layout feels appropriately sized
- Any text or labels that appear cut off

Respond with a JSON object:
{
  "issues": ["specific description of each width/layout problem found"],
  "width_issues": ["detailed description of any width-related problems"],
  "container_overflow": ["elements extending beyond their containers"],
  "unit_label_cutoff": true/false,
  "form_width_assessment": "too_narrow/appropriate/too_wide",
  "spacing_quality": "poor/good/excellent",
  "mobile_compatibility": "good/poor - describe any mobile layout issues",
  "critical_fixes_needed": ["immediate layout problems that must be addressed"],
  "overall_assessment": "detailed assessment focusing on width and container issues"
}
```

### Container Width Testing Checklist

When implementing visual tests, ensure these width-specific checks are included:

✅ **Form Container Validation**
- Check form-grid width relative to parent container
- Verify input-with-unit groups fit within their allocated space
- Measure unit label positioning and ensure no cutoff
- Test responsive behavior at different screen sizes

✅ **Element Boundary Checks**
- JavaScript measurement of element boundaries vs container boundaries
- Detection of horizontal overflow beyond viewport
- Form element width consistency across different field types
- Grid cell utilization and spacing validation

✅ **Multi-Device Width Testing**
- Desktop layout width optimization
- Tablet breakpoint behavior
- Mobile single-column layout validation
- Responsive scaling of form elements

✅ **Specific GPT Instructions for Width Issues**
- Enhanced prompts focusing on container boundaries
- Detailed width measurement requests
- Unit label visibility verification
- Form spacing and proportion assessment

This enhanced approach ensures GPT can effectively identify and report width-related layout issues that impact user experience.


## Specification-Based Testing Prompt

When Claude Code needs to create comprehensive tests from a specification, use this prompt:

**"Analyze this specification and create tests focusing on the 3 most critical aspects:**

**SPECIFICATION:** [paste specification]

**Requirements:**
1. **Identify the 3 most critical requirements** from the spec and explain why
2. **Create Puppeteer test file** (`testing/[feature-name]-visual-test.js`) that:
   - Screenshots desktop (1920x1080) and mobile (375x667) 
   - Tests all 3 critical requirements with specific validation
   - Checks console errors, 404s, form element height consistency
   - Includes overlap detection for layout issues
3. **OpenAI Vision Analysis** using critical visual inspection prompt focused on the 3 most important visual aspects
4. **Accuracy Testing** (if calculator): Test against original if URL provided, ±10% tolerance
5. **Generate test report** with pass/fail status and actionable recommendations

Output: Complete test file, identified critical areas, and enhanced vision prompts."**

This prompt ensures comprehensive testing focused on what matters most from the specification.

## Mobile Layout Centering Standards

### Mobile-First Design Testing Requirements

When testing any web application interface, mobile centering should be validated as a standard practice:

✅ **Mobile Layout Testing (≤480px screens)**
- Home page content is centered on narrow screens
- Card-based layouts (content grids, feature cards, product cards, dashboard widgets) are properly centered
- Form inputs and buttons are centered and accessible
- CTAs and important headings are centered
- Logo and branding elements are centered
- Navigation is optimized for touch (drawer/hamburger style)
- All interactive elements are thumb-friendly sized (min 44px)

✅ **Content Alignment Standards**
- **Should be centered:** Home page content, card layouts, form inputs, CTAs, headings, logos, navigation, dashboard widgets, product grids
- **Should stay left-aligned:** Long paragraph text, lists, detailed content, navigation links in drawers, article content, documentation

✅ **Enhanced Mobile Testing in Puppeteer**
```javascript
// Add to existing visual tests - Generic for any web application
async function testMobileCentering(page) {
  await page.setViewport({ width: 375, height: 667 }); // Standard mobile
  await page.setViewport({ width: 320, height: 568 }); // Narrow mobile
  
  // Check for proper centering
  const centeringChecks = await page.evaluate(() => {
    const issues = [];
    
    // Check main content grid centering (adaptable selectors)
    const contentGrids = document.querySelectorAll('.grid, .content-grid, .card-grid, .feature-grid, .product-grid');
    contentGrids.forEach((grid, index) => {
      const gridStyle = window.getComputedStyle(grid);
      const justifyItems = gridStyle.justifyItems;
      if (justifyItems !== 'center' && gridStyle.display === 'grid') {
        issues.push(`Content grid ${index + 1} not centered (justify-items should be center)`);
      }
    });
    
    // Check card centering (generic card classes)
    document.querySelectorAll('.card, .feature-card, .product-card, .content-card').forEach((card, index) => {
      const cardStyle = window.getComputedStyle(card);
      const margin = cardStyle.margin;
      if (!margin.includes('auto')) {
        issues.push(`Card ${index + 1} not centered (margin should include auto)`);
      }
    });
    
    // Check main content wrapper centering
    const contentWrappers = document.querySelectorAll('.content-wrapper, .main-content, .container, .wrapper');
    contentWrappers.forEach((wrapper, index) => {
      const wrapperStyle = window.getComputedStyle(wrapper);
      const textAlign = wrapperStyle.textAlign;
      if (textAlign !== 'center' && wrapper.querySelector('.card, .grid')) {
        issues.push(`Content wrapper ${index + 1} not centered on mobile`);
      }
    });
    
    // Check navigation implementation
    const mobileNav = document.querySelector('[class*="mobile-nav"], [class*="hamburger"], [class*="drawer"]');
    if (!mobileNav) {
      issues.push('No mobile navigation detected - may not be mobile-optimized');
    }
    
    return { issues };
  });
  
  return centeringChecks;
}
```

✅ **Enhanced OpenAI Vision Prompt for Mobile Centering**
```
MOBILE LAYOUT CENTERING INSPECTION: Examine this mobile interface screenshot for proper content centering.

MOBILE CENTERING REQUIREMENTS:
1. **HOME PAGE CONTENT**: Is all home page content properly centered on narrow screens?
2. **CARD LAYOUTS**: Are content cards/feature cards/product cards centered with appropriate max-width?
3. **FORM ELEMENTS**: Are form inputs, buttons, and interactive elements centered?
4. **NAVIGATION**: Is mobile navigation properly implemented (hamburger/drawer style)?
5. **VISUAL BALANCE**: Does the overall layout feel balanced and professional on mobile?

SPECIFIC MOBILE ISSUES TO DETECT:
- Content that appears left-aligned when it should be centered
- Cards or elements that extend beyond comfortable mobile viewing width
- Poor utilization of mobile screen space
- Navigation that doesn't work well on mobile devices
- Elements that appear cramped or poorly spaced on narrow screens

MOBILE-SPECIFIC CHECKS:
- Are content cards limited to reasonable width (≤400px) and centered?
- Is text content readable and appropriately sized for mobile?
- Are interactive elements large enough for touch (≥44px)?
- Does the overall layout feel modern and mobile-optimized?
- Are dashboard widgets/content grids properly centered?

Respond with focus on mobile-specific centering and layout issues:
{
  "mobile_centering": "good/poor - describe centering quality",
  "card_layout": "good/poor - describe card centering and sizing",
  "mobile_navigation": "good/poor - describe mobile nav quality", 
  "touch_accessibility": "good/poor - describe touch-friendly design",
  "content_grid_centering": "good/poor - describe grid layout centering",
  "mobile_specific_issues": ["any mobile layout problems found"],
  "centering_assessment": "detailed assessment of mobile centering"
}
```

### Standard Mobile Testing Workflow

✅ **Include in Every Test**
1. Test both tablet (768px) and narrow mobile (375px, 320px) viewports
2. Verify proper centering of all major content areas
3. Check touch accessibility (44px minimum touch targets)
4. Validate mobile navigation implementation
5. Ensure content doesn't extend beyond comfortable viewing width
6. Test card-based layouts and content grids for proper centering

✅ **GPT Review Instructions**
Add this to any GPT analysis request:
"Additionally, verify that this interface follows mobile-first design principles with proper content centering, appropriate card sizing (max-width ~400px), and mobile-optimized navigation. Check that all content is properly centered on narrow mobile screens (≤480px) and that interactive elements are touch-friendly. This applies to any card-based layouts, content grids, dashboard widgets, or feature displays."

This ensures mobile centering becomes a standard part of every visual review and testing process for any web application.
### Mobile-First Design Testing Requirements

When testing any interface, mobile centering should be validated as a standard practice:

✅ **Mobile Layout Testing (≤480px screens)**
- Home page content is centered on narrow screens
- Card-based layouts (calculator grid, feature cards) are properly centered
- Form inputs and buttons are centered and accessible
- CTAs and important headings are centered
- Logo and branding elements are centered
- Navigation is optimized for touch (drawer/hamburger style)
- All interactive elements are thumb-friendly sized (min 44px)

✅ **Content Alignment Standards**
- **Should be centered:** Home page content, card layouts, form inputs, CTAs, headings, logos, navigation
- **Should stay left-aligned:** Long paragraph text, lists, detailed content, navigation links in drawers

✅ **Enhanced Mobile Testing in Puppeteer**
```javascript
// Add to existing visual tests
async function testMobileCentering(page) {
  await page.setViewport({ width: 375, height: 667 }); // Standard mobile
  await page.setViewport({ width: 320, height: 568 }); // Narrow mobile
  
  // Check for proper centering
  const centeringChecks = await page.evaluate(() => {
    const issues = [];
    
    // Check calculator grid centering
    const calculatorGrid = document.querySelector('.calculator-grid');
    if (calculatorGrid) {
      const gridStyle = window.getComputedStyle(calculatorGrid);
      const justifyItems = gridStyle.justifyItems;
      if (justifyItems !== 'center') {
        issues.push('Calculator grid not centered (justify-items should be center)');
      }
    }
    
    // Check calculator cards centering
    document.querySelectorAll('.calculator-card').forEach((card, index) => {
      const cardStyle = window.getComputedStyle(card);
      const margin = cardStyle.margin;
      if (!margin.includes('auto')) {
        issues.push(`Calculator card ${index + 1} not centered (margin should include auto)`);
      }
    });
    
    // Check content wrapper centering
    const contentWrapper = document.querySelector('.content-wrapper');
    if (contentWrapper) {
      const wrapperStyle = window.getComputedStyle(contentWrapper);
      const textAlign = wrapperStyle.textAlign;
      if (textAlign !== 'center') {
        issues.push('Content wrapper not centered on mobile');
      }
    }
    
    return { issues };
  });
  
  return centeringChecks;
}
```

✅ **Enhanced OpenAI Vision Prompt for Mobile Centering**
```
MOBILE LAYOUT CENTERING INSPECTION: Examine this mobile interface screenshot for proper content centering.

MOBILE CENTERING REQUIREMENTS:
1. **HOME PAGE CONTENT**: Is all home page content properly centered on narrow screens?
2. **CARD LAYOUTS**: Are calculator cards/feature cards centered with appropriate max-width?
3. **FORM ELEMENTS**: Are form inputs, buttons, and interactive elements centered?
4. **NAVIGATION**: Is mobile navigation properly implemented (hamburger/drawer style)?
5. **VISUAL BALANCE**: Does the overall layout feel balanced and professional on mobile?

SPECIFIC MOBILE ISSUES TO DETECT:
- Content that appears left-aligned when it should be centered
- Cards or elements that extend beyond comfortable mobile viewing width
- Poor utilization of mobile screen space
- Navigation that doesn't work well on mobile devices
- Elements that appear cramped or poorly spaced on narrow screens

MOBILE-SPECIFIC CHECKS:
- Are calculator cards limited to reasonable width (≤400px) and centered?
- Is text content readable and appropriately sized for mobile?
- Are interactive elements large enough for touch (≥44px)?
- Does the overall layout feel modern and mobile-optimized?

Respond with focus on mobile-specific centering and layout issues:
{
  "mobile_centering": "good/poor - describe centering quality",
  "card_layout": "good/poor - describe card centering and sizing",
  "mobile_navigation": "good/poor - describe mobile nav quality",
  "touch_accessibility": "good/poor - describe touch-friendly design",
  "mobile_specific_issues": ["any mobile layout problems found"],
  "centering_assessment": "detailed assessment of mobile centering"
}
```

### Standard Mobile Testing Workflow

✅ **Include in Every Test**
1. Test both tablet (768px) and narrow mobile (375px, 320px) viewports
2. Verify proper centering of all major content areas
3. Check touch accessibility (44px minimum touch targets)
4. Validate mobile navigation implementation
5. Ensure content doesn't extend beyond comfortable viewing width

✅ **GPT Review Instructions**
Add this to any GPT analysis request:
"Additionally, verify that this interface follows mobile-first design principles with proper content centering, appropriate card sizing (max-width ~400px), and mobile-optimized navigation. Check that all content is properly centered on narrow mobile screens (≤480px) and that interactive elements are touch-friendly."

This ensures mobile centering becomes a standard part of every visual review and testing process.