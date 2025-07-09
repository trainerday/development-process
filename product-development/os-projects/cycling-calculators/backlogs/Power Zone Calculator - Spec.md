---
title: Power zone calculator   spec
type: note
permalink: product-development/os-projects/cycling-calculators/backlogs/Power Zone Calculator - Spec
---

# Power Zone Calculator - Specification

## Purpose
Calculate cycling power training zones based on FTP (Functional Threshold Power) using different coaching methodologies.

## Core Functionality
### Input Fields
- **FTP (Watts)**: Numeric input, positive integers only
- **Coaching Method**: Dropdown selection
  - Coggan/TrainingPeaks (7 zones)
  - Polarized (3 zones)
  - Sweet Spot (5 zones)
  - Custom (user-defined percentages)

### Zone Methodologies

#### Coggan/TrainingPeaks (7 Zones)
- Zone 1: Active Recovery (< 55% FTP)
- Zone 2: Endurance (56-75% FTP)  
- Zone 3: Tempo (76-90% FTP)
- Zone 4: Lactate Threshold (91-105% FTP)
- Zone 5: VO2max (106-120% FTP)
- Zone 6: Anaerobic Capacity (121-150% FTP)
- Zone 7: Sprint Power (> 150% FTP)

#### Polarized (3 Zones)
- Zone 1: Easy (< 75% FTP)
- Zone 2: Moderate (75-90% FTP)
- Zone 3: Hard (> 90% FTP)

#### Sweet Spot (5 Zones)
- Zone 1: Recovery (< 65% FTP)
- Zone 2: Aerobic (65-80% FTP)
- Zone 3: Sweet Spot (80-95% FTP)
- Zone 4: Threshold (95-105% FTP)
- Zone 5: VO2max+ (> 105% FTP)

### Output Display
- Table showing zone ranges in watts
- Color-coded zones for visual clarity
- Zone descriptions and training purposes
- Percentage ranges alongside watt ranges

## Technical Requirements
- Responsive design for mobile/desktop
- Input validation for FTP values
- Real-time calculation updates
- Export functionality (PDF/print)

## UI/UX Considerations
- Clear zone visualization with color coding
- Educational tooltips for each zone
- Comparison view between methodologies
- Save/bookmark functionality for personal FTP