---
title: HR Zone Calculator - Spec
type: note
permalink: trainer-day/os-projects/cycling-calculators/backlogs/hr-zone-calculator-spec
---

# HR Zone Calculator - Specification

## Purpose
Calculate heart rate training zones based on maximum heart rate using various established formulas and methodologies.

## Core Functionality
### Input Fields
- **Maximum Heart Rate**: Numeric input, positive integers (120-220 bpm range)
- **Age**: Optional numeric input for age-based max HR estimation
- **Resting Heart Rate**: Optional numeric input for Karvonen method
- **Calculation Method**: Dropdown selection

### Calculation Methods

#### Direct Percentage (Coggan/TrainingPeaks)
- Zone 1: < 68% HRmax
- Zone 2: 69-83% HRmax
- Zone 3: 84-94% HRmax  
- Zone 4: 95-105% HRmax
- Zone 5: > 106% HRmax

#### Karvonen Method (Heart Rate Reserve)
Uses formula: Target HR = ((HRmax - HRrest) × %Intensity) + HRrest
- Zone 1: 50-60% HRR
- Zone 2: 60-70% HRR
- Zone 3: 70-80% HRR
- Zone 4: 80-90% HRR
- Zone 5: 90-100% HRR

#### Age-Based Max HR Estimation
- **220 - Age** (Traditional)
- **207 - (0.7 × Age)** (Updated formula)
- **208 - (0.7 × Age)** (Tanaka formula)

### Output Display
- Table showing HR zone ranges in BPM
- Color-coded zones matching power zone colors
- Zone descriptions and training intensity
- Comparison between different methods when applicable

## Technical Requirements
- Input validation for realistic HR values
- Real-time calculations
- Optional age-based max HR calculator
- Mobile-responsive design
- Export/print functionality

## UI/UX Considerations
- Clear explanations of different methods
- Educational content about HR zone training
- Visual heart rate zone chart
- Integration suggestions with power zones