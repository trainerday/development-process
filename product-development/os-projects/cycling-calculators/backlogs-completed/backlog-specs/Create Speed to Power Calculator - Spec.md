---
title: Create Speed to Power Calculator - Spec
type: note
permalink: product-development/os-projects/cycling-calculators/backlogs-completed/backlog-specs/create-speed-to-power-calculator-spec
---

# Create Speed to Power Calculator - Technical Specification

## ✅ HIGH CONFIDENCE (Claude is sure)
- **Reuse existing physics engine**: Use same `calculateForces()` method from PowerCalculator
- **Direct power calculation**: `Power = Force × Speed / (1 - drivetrain_loss)` - no iteration needed
- **Route structure**: `/speed-calculator` following existing pattern in `routes/index.js`
- **Template structure**: Mirror `power-calculator.ejs` layout with speed input instead of power input
- **JavaScript class**: `SpeedCalculator` class following same patterns as `PowerCalculator`
- **Form inputs**: Same weight, slope, position, surface inputs as existing calculator
- **CSS styling**: Reuse existing 48px form height consistency and blue theme
- **Navigation integration**: Add to existing shared navigation component
- **Testing framework**: Use existing Puppeteer + OpenAI Vision testing approach
- **Physics validation**: Cross-validate against existing Power→Speed calculator for accuracy

## ❓ NEEDS CLARIFICATION (Claude needs input)  
- **Icon choice**: Should Speed→Power use 🚀 icon or different icon for navigation?
- **Default speed value**: What should be the default target speed (e.g., 30 km/h)?
- **Speed input range**: What min/max values for speed input (e.g., 5-80 km/h)?
- **Home page positioning**: Should Speed→Power calculator card appear before or after "More Calculators" placeholder?
- **URL preference**: Is `/speed-calculator` the preferred URL or would you prefer `/speed-to-power`?

## ⚠️ ASSUMPTIONS (Claude is guessing)
- **Primary input prominence**: Assuming speed input should have same visual prominence as power input (blue section)
- **Unit defaults**: Assuming metric (km/h) as default, imperial (mph) as alternative
- **Result display**: Assuming power result should be displayed in same blue result section style
- **Navigation label**: Assuming "Speed to Power" as navigation text (vs "Speed Calculator")
- **Page title**: Assuming "Speed to Power Calculator" as main page heading
- **Form layout**: Assuming same two-column grid layout for secondary parameters

## 🎯 CRITICAL DECISIONS NEEDED
- **Calculator relationship**: Should there be cross-links between Power→Speed and Speed→Power calculators?
- **Data persistence**: Should input values persist when switching between calculators?
- **URL strategy**: Do you want both calculators accessible from same base path or separate paths?
- **Future expansion**: Are there plans for additional calculators that would affect navigation structure?