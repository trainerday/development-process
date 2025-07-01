---
title: FTP from VO2max Calculator - Spec
type: note
permalink: trainer-day/os-projects/cycling-calculators/backlogs/ftp-from-vo2max-calculator-spec
---

# FTP from VO2max Calculator - Specification

## Purpose
Estimate Functional Threshold Power (FTP) from VO2max measurements, considering individual factors like weight, bike position, and training status.

## Core Functionality
### Input Fields
- **VO2max**: Numeric input in ml/kg/min (30-80 typical range)
- **Body Weight**: Numeric input in kg or lbs
- **Bike Type/Position**: Dropdown selection
- **Training Status**: Dropdown for experience level
- **Age**: Optional numeric input for age-related adjustments

### Bike Position Categories
#### Road Bike Positions
- **Upright/Endurance**: 85% efficiency factor
- **Standard Road**: 90% efficiency factor  
- **Aggressive/Aero**: 92% efficiency factor
- **Time Trial/Triathlon**: 95% efficiency factor

#### Other Bike Types
- **Mountain Bike**: 80% efficiency factor
- **Hybrid/Commuter**: 82% efficiency factor
- **Gravel Bike**: 88% efficiency factor

### Training Status Modifiers
- **Beginner** (< 1 year): 0.85x modifier
- **Recreational** (1-3 years): 0.90x modifier
- **Trained** (3+ years consistent): 1.0x modifier
- **Highly Trained** (competitive): 1.05x modifier

### Calculation Formula
**Base Formula**: FTP = (VO2max × Weight × 16.48) × Efficiency Factor × Training Modifier

Where:
- 16.48 = conversion factor (ml O2 to watts at lactate threshold)
- Efficiency Factor = based on bike position
- Training Modifier = based on training status

### Age Adjustments (Optional)
- **Under 30**: No adjustment
- **30-40**: -2% per decade
- **40-50**: -3% per decade  
- **Over 50**: -4% per decade

### Output Display
- **Estimated FTP**: Primary result in watts
- **FTP/kg Ratio**: Watts per kilogram
- **Confidence Range**: ±10-15% typical variation
- **Comparison Metrics**:
  - Category benchmarks (Cat 5 to Pro levels)
  - Age group percentiles
  - Training recommendations

### Validation Notes
- **Accuracy Disclaimer**: Estimation only, field testing recommended
- **Individual Variation**: Genetics, fiber type, efficiency differences
- **Testing Recommendations**: Suggest proper FTP testing protocols

## Technical Requirements
- Input validation for realistic VO2max values
- Unit conversion (metric/imperial)
- Real-time calculation updates
- Educational content about limitations
- Export functionality

## UI/UX Considerations
- Clear explanation of estimation accuracy
- Links to FTP testing protocols
- Integration with other calculators
- Progress tracking over time
- Educational content about VO2max testing