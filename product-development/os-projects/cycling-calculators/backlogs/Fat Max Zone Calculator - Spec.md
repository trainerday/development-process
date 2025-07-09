---
title: Fat Max Zone Calculator - Spec
type: note
permalink: product-development/os-projects/cycling-calculators/backlogs/fat-max-zone-calculator-spec
---

# Fat Max Zone Calculator - Specification

## Purpose
Calculate the heart rate and power zones where fat oxidation is maximized, using different scientific methodologies.

## Core Functionality
### Input Fields
- **Age**: Numeric input (required for most formulas)
- **Resting Heart Rate**: Numeric input (optional, improves accuracy)
- **Maximum Heart Rate**: Numeric input (measured or estimated)
- **FTP**: Optional numeric input (for power-based fat max estimation)
- **Calculation Method**: Dropdown selection

### Calculation Methods

#### Maffetone Method (180 Formula)
- **Base**: 180 - Age
- **Adjustments**:
  - Subtract 10: Recovering from illness/injury, on medication
  - Subtract 5: Just starting training, inconsistent training, frequent illness
  - No change: Training consistently for 2+ years, injury-free
  - Add 5: Training consistently for 2+ years, competitive athlete

#### Laursen-Jenkins Formula
- **Fat Max HR** = 202 - (0.55 × Age)

#### Heart Rate Reserve Method
- **Fat Max** = 65-75% of Heart Rate Reserve
- **Formula**: ((HRmax - HRrest) × 0.65-0.75) + HRrest

#### Power-Based Estimation
- **Fat Max Power** = 45-65% of FTP
- **Conversion to HR**: Use known power-HR relationship if available

#### Laboratory-Based Input
- **Direct Entry**: For users with metabolic testing results
- **Custom HR Range**: Manual input of tested fat max zone

### Output Display
- **Primary**: Fat max heart rate range (e.g., 135-145 bpm)
- **Secondary Outputs**:
  - Corresponding power range (if FTP provided)
  - Training recommendations
  - Zone duration guidelines
  - Fuel utilization percentages

### Educational Content
- Explanation of fat oxidation vs carbohydrate utilization
- Benefits of fat max training
- How to conduct field tests
- Limitations of estimation methods

## Technical Requirements
- Multiple calculation methods
- Input validation and realistic ranges
- Educational tooltips and explanations
- Comparison between methods
- Export/save functionality

## UI/UX Considerations
- Clear method explanations
- Visual representation of fat/carb utilization curve
- Training recommendations based on results
- Integration with other zone calculators
- Progress tracking over time