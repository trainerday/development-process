---
title: Gearing Speed Calculator - Spec
type: note
permalink: trainer-day/os-projects/cycling-calculators/backlogs/gearing-speed-calculator-spec
---

# Gearing Speed Calculator - Specification

## Purpose
Calculate cycling speed based on gearing, wheel size, tire dimensions, and pedaling cadence (RPM).

## Core Functionality
### Input Fields
- **Front Chainring Teeth**: Numeric input (28-60 teeth typical range)
- **Rear Cassette/Cog Teeth**: Numeric input (8-50 teeth typical range)
- **Wheel Size**: Dropdown selection
  - 700c (most common road)
  - 650b (27.5")
  - 26" (MTB)
  - 29" (MTB)
  - Custom diameter input
- **Tire Width**: Numeric input in mm (23-60mm typical range)
- **RPM/Cadence**: Numeric input (40-140 RPM typical range)

### Calculation Logic
1. **Gear Ratio** = Front Chainring ÷ Rear Cog
2. **Wheel Circumference** = π × (Wheel Diameter + (2 × Tire Height))
3. **Distance per Revolution** = Gear Ratio × Wheel Circumference  
4. **Speed** = (Distance per Revolution × RPM × 60) ÷ 1000 (for km/h)

### Tire Size Database
Common tire sizes with actual dimensions:
- 700x23c = 622mm + 23mm
- 700x25c = 622mm + 25mm
- 700x28c = 622mm + 28mm
- 650x47b = 584mm + 47mm
- 26x2.0 = 559mm + 50mm
- 29x2.2 = 622mm + 55mm

### Output Display
- **Primary Output**: Speed in km/h and mph
- **Secondary Outputs**:
  - Gear ratio (e.g., 2.5:1)
  - Gear inches (for traditional measurement)
  - Development (meters per pedal revolution)
  - Cadence recommendations for different speeds

### Additional Features
- **Gear Range Analysis**: Calculate all possible gear combinations
- **Optimal Cadence Zones**: Highlight 80-100 RPM sweet spot
- **Speed Range Table**: Show speeds at different cadences (70, 80, 90, 100, 110 RPM)

## Technical Requirements
- Real-time calculation updates
- Input validation for realistic values
- Responsive design
- Unit conversion (metric/imperial)
- Export functionality

## UI/UX Considerations
- Visual gear ratio representation
- Common gear combination presets
- Educational content about gear selection
- Integration with power calculators
- Mobile-friendly input controls