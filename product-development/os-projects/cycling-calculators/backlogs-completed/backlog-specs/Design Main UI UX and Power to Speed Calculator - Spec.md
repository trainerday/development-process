---
title: Design main ui ux and power to speed calculator   spec
type: note
permalink: product-development/os-projects/cycling-calculators/backlogs-completed/backlog-specs/Design Main UI UX and Power to Speed Calculator - Spec
---

# Design Main UI/UX and Power to Speed Calculator - Requirements

## Current State
Currently no cycling calculator website exists. Need to create a small, focused site for hosting multiple cycling calculators with a clean, professional interface.

## Desired Outcome  
A simple, clean website template that hosts multiple cycling calculators with:

- **TrainerDay branding**: Logo positioned top-left similar to TrainerDay.com
- **Color scheme**: Follow TrainerDay's color palette (research shows they use clean blues/grays for reliability and precision)
- **Navigation**: Sidebar navigation (like app.trainerday.com) OR simple top navigation - need to research best practice
- **Calculator layout**: Clean, minimal form design with adequate spacing between inputs
- **Responsive design**: Works seamlessly on desktop, tablet, and mobile
- **Professional appearance**: Builds trust and credibility for cycling community

The end result should be a test HTML page demonstrating the preferred design direction for the cycling calculator site.

## Interaction Mechanism
Research and create examples of:

1. **Best calculator form designs**: Focus on simplicity, consistency, and intuitive layout with clean lines and ample spacing
2. **Navigation patterns**: **Collapsible sidebar with icons** - Hidden left sidebar that shows only icons by default, expands on hover/click to show labels. This keeps the interface super clean and simple while maintaining easy access to different calculators
3. **Layout optimization**: Responsive design that adjusts and optimizes layout depending on the device–smartphone, tablet, or desktop
4. **Color psychology**: Choose shades that invoke precision, reliability, and clarity, such as blues and grays
5. **Typography**: Select typography that enhances legibility with clean lines and ample spacing

## Special Requirements
- Must incorporate TrainerDay logo and follow brand consistency
- **Collapsible icon-based sidebar navigation**: Clean, minimal interface with icons-only sidebar that expands on interaction
- Navigation should be simple and not overwhelming (avoid complex hamburger menus)
- Focus on essential functions with a clean, minimalist layout without wading through extraneous features
- Site should load quickly and be optimized for cycling enthusiasts
- Design should encourage engagement while maintaining professional credibility
- **Super clean, simple look** with maximum screen space for calculator content

## Additional Context
TrainerDay is a cycling training platform focused on simplicity and effectiveness. Research shows they prioritize keeping things simple and avoiding complexity. The calculator site should reflect these values.

**Key design inspirations to research:**
- Clean web form calculator examples (not traditional button calculators)
- Minimalist sports/fitness website templates  
- Modern sidebar navigation patterns
- Professional cycling industry websites

**Visual Examples and Resources:**

1. **Web Form Calculator Platforms (for UX reference):**
   - [Calculoid.com](https://www.calculoid.com/) - Professional web calculator builder with clean form templates
   - [Jotform Calculator Forms](https://www.jotform.com/form-templates/category/calculation-form) - 90+ web form calculation examples
   - [Elfsight Calculator Templates](https://elfsight.com/calculator-form-widget/templates/) - 115+ web form calculator templates
   - [Calconic Calculator Examples](https://www.calconic.com/) - Interactive web form calculators
   - [Formester Calculation Fields](https://formester.com/features/calculating-fields/) - Examples of form calculators with real-time calculations

2. **Fitness/Sports Website Design:**
   - [Personal Trainer Website Examples](https://www.sitebuilderreport.com/inspiration/personal-trainer-websites) - 31 inspiring fitness website designs
   - [Sports & Fitness Templates on Wix](https://www.wix.com/website/templates/html/health-wellness/sports-fitness) - Clean, modern fitness site layouts

3. **Sidebar Navigation Examples:**
   - [Sidebar Design Collection on Pinterest](https://www.pinterest.com/heyjerio/sidebar-navigation/) - 19 sidebar navigation ideas
   - [Shadcn/ui Sidebar Component](https://ui.shadcn.com/docs/components/sidebar) - Modern, customizable sidebar examples

4. **TrainerDay Brand Reference:**
   - [TrainerDay.com](https://trainerday.com/) - Main site for color scheme and logo placement
   - [TrainerDay App Store](https://apps.apple.com/us/app/trainerday/id1500401973) - Shows app interface design

The goal is to create a design that cycling enthusiasts will trust and find easy to use for their training calculations.

## EXACT SPECIFICATIONS FOR POWER VS SPEED CALCULATOR

### Calculator Requirements
Based on https://www.gribble.org/cycling/power_v_speed.html but simplified:

**Input Fields (simplified from original):**
1. **Total Weight** - Single field combining rider + bike weight (was separate fields)
2. **Bike Position/Aerodynamics** - Dropdown with predefined CDA values:
   - Upright Position (Touring/Comfort): 0.40
   - Relaxed Position (Recreational): 0.35  
   - Standard Road Position: 0.30 (default)
   - Aggressive Road Position: 0.25
   - Time Trial Position: 0.22
   - Full Aero Position: 0.20
3. **Road Slope** - Visual slider (-10% to +15%, default 0%, step 0.1%)
4. **Road Surface** - Dropdown for rolling resistance:
   - Excellent Tarmac: 0.002
   - Good Tarmac: 0.004 (default)
   - Average Road: 0.006
   - Poor Road: 0.008
   - Gravel/Dirt: 0.012
5. **Power Output** - Input field in watts

**Hidden/Fixed Parameters:**
- Headwind: Fixed at 1 km/h (don't show to user)
- Air density: 1.225 kg/m³
- Drivetrain loss: 2%

**Output:**
- Speed result prominently displayed
- Support both Imperial and Metric with toggle

### Design Specifications

**Layout Structure:**
```
Header:
- TrainerDay logo (top-left)
- Page title: "Power vs Speed Calculator"
- Subtitle: "Calculate your cycling speed based on power output"

Main Calculator:
- Metric/Imperial toggle buttons at top
- Two-column grid layout for inputs (responsive to single column on mobile)
- Left column: Weight, Bike Position
- Right column: Slope slider, Road Surface
- Full-width Power Input section (highlighted)
- Full-width Speed Result (prominent blue gradient box)
```

**Color Scheme:**
- Primary blue: #2563eb (TrainerDay brand color)
- Secondary blue: #3b82f6
- Background: #f8fafc (light gray)
- Card background: white
- Text: #334155 (dark gray)
- Labels: #374151
- Borders: #d1d5db

**Typography:**
- Font: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif
- Headers: 2rem, weight 600
- Labels: weight 500
- Body: 1rem, line-height 1.6

**Visual Elements:**
- Cards: white background, border-radius 12px, subtle shadow
- Inputs: padding 0.75rem, border-radius 6px, focus states with blue outline
- Slope slider: Custom styled with blue thumb, visual percentage display
- Power input: Larger font (1.5rem), centered, special highlighting
- Result display: Gradient background, white text, large font (2.5rem)

**Responsive Design:**
- Desktop: Two-column grid for inputs
- Mobile: Single column layout
- All inputs remain full-width within their containers
- Touch-friendly targets (minimum 44px)

### Physics Implementation
Use the same formulas as original Gribble calculator:

**Forces:**
- Gravity: F_gravity = 9.8067 × sin(arctan(slope%/100)) × weight_kg
- Rolling: F_rolling = 9.8067 × cos(arctan(slope%/100)) × weight_kg × Crr  
- Aero: F_aero = 0.5 × CdA × rho × (speed_ms + headwind_ms)²

**Power Calculation:**
- Total resistance = gravity + rolling + aero forces
- Required power = total_resistance × speed / (1 - drivetrain_loss)
- Solve iteratively for speed given input power

**Unit Conversions:**
- Metric: weight in kg, speed in km/h
- Imperial: weight in lbs, speed in mph
- Internal calculations always in metric (kg, m/s)

### User Experience
- Real-time calculation updates as inputs change
- Smooth slider interaction with live percentage display
- Clear visual hierarchy with most important elements (power/speed) emphasized
- Intuitive dropdown descriptions that users can understand
- Professional appearance that builds trust with cycling community

---

# GENERATED TECHNICAL SPECIFICATIONS

## Design Specifications:
- **Layout**: TrainerDay-branded header with collapsible icon sidebar navigation
- **Color Scheme**: TrainerDay blues (#2563eb primary, #3b82f6 secondary) with clean gray backgrounds
- **UI Components**: Two-column responsive grid, custom styled slider, prominent result display
- **Typography**: System fonts with clear hierarchy and sufficient spacing

## Technical Implementation:
- **Frontend**: Vanilla JavaScript with real-time calculations
- **Express Views Structure**: Follow existing Express EJS view structure with layout.ejs
- **CSS Architecture**: Shared styles in public/stylesheets/style.css (extend existing file)
- **Logo Implementation**: Use actual TrainerDay logo image file, not text
- **Physics Engine**: Gribble.org formula implementation with simplified inputs
- **Responsive Design**: Desktop two-column → mobile single-column layout
- **User Inputs**: Total weight, bike position dropdown, road slope slider, surface dropdown, power input
- **Output**: Prominent speed result with metric/imperial toggle

## Key Features:
- Real-time calculation updates as users type/adjust inputs
- Visual slope slider with percentage display
- Predefined aerodynamic position values for ease of use
- Professional cycling calculator appearance that builds trust

The specification includes exact color codes, responsive breakpoints, physics formulas, and detailed UX patterns for a production-ready cycling calculator.


## Original Task
Design main UI/UX and Power to speed calculator

## Implementation Summary

### ✅ **Completed Features**
- **Complete Power to Speed Calculator** with accurate physics calculations
- **Professional UI Design** with TrainerDay branding and Poppins font
- **Shared Navigation Component** for consistent design across pages
- **Responsive Design** optimized for desktop and mobile
- **Enhanced Visual Testing Framework** with Puppeteer + OpenAI Vision
- **Form Element Consistency** with pixel-perfect alignment
- **Accuracy Validation** against original Gribble calculator (within 9% tolerance)

### ✅ **Technical Implementation**
- **Physics Engine**: Aerodynamics and rolling resistance calculations
- **Frontend**: Express.js with EJS templating
- **Styling**: Modern CSS with flexbox and consistent 48px form heights
- **Testing**: Automated visual regression testing with AI analysis
- **Deployment**: Live on both staging and production servers

### ✅ **User Experience**
- **Intuitive Interface**: Clean form layout with metric/imperial toggle
- **Real-time Calculations**: Instant speed results as users adjust inputs
- **Professional Branding**: TrainerDay logo and consistent color scheme
- **Mobile Responsive**: Optimized navigation and layout for all screen sizes

### ✅ **Quality Assurance**
- **Visual Testing**: Comprehensive Puppeteer + OpenAI Vision analysis
- **Physics Validation**: Accuracy confirmed against reference calculator
- **Cross-browser Testing**: Verified functionality across devices
- **Performance**: Fast loading and responsive calculations

## Production URLs
- **Production**: http://cycling-calculators.apihost.trainerday.com/power-calculator
- **Production Alt**: http://cycling-calculators.prod.trainerday.com/power-calculator
- **Staging**: http://cycling-calculators.uat.trainerday.com/power-calculator

## Repository
- **GitHub**: https://github.com/trainerday/cycling-calculators

## Next Steps
Task completed successfully. Ready for additional calculator implementations.