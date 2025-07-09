---
title: Zone 2 Calculator - Spec
type: note
permalink: product-development/os-projects/cycling-calculators/backlogs/zone-2-calculator-spec
---

# Zone 2 Calculator - Specification

## Purpose
Calculate Zone 2 training ranges using different methodologies for optimal aerobic base building and metabolic efficiency.

## Core Functionality
### Input Fields
- **FTP**: Numeric input (for power-based calculations)
- **Maximum Heart Rate**: Numeric input (for HR-based calculations)
- **Resting Heart Rate**: Optional numeric input (for HRR method)
- **Lactate Threshold HR**: Optional input (if known from testing)
- **Calculation Method**: Dropdown selection

### Zone 2 Definition Methods

#### Power-Based (% of FTP)
- **Coggan Method**: 56-75% FTP
- **Polarized Method**: 55-75% FTP  
- **Seiler Method**: 60-70% FTP
- **Custom Range**: User-defined percentage

#### Heart Rate-Based (% of HRmax)
- **Coggan Method**: 69-83% HRmax
- **Maffetone-Influenced**: 70-80% HRmax
- **Conservative**: 65-75% HRmax

#### Heart Rate Reserve Method
- **Zone 2 HRR**: 60-70% of Heart Rate Reserve
- **Formula**: ((HRmax - HRrest) × 0.60-0.70) + HRrest

#### Lactate-Based (if LT known)
- **Zone 2**: 80-90% of Lactate Threshold HR
- **Alternative**: LT1 (First Lactate Threshold) if available

#### Talk Test Method
- **Subjective Guide**: "Conversational pace" 
- **RPE**: 3-4 out of 10 perceived exertion
- **Nasal Breathing**: Ability to breathe through nose only

### Output Display
- **Primary**: Zone 2 ranges in watts and/or BPM
- **Training Guidelines**:
  - Session duration recommendations (45-90+ minutes)
  - Weekly volume suggestions
  - Progression protocols
- **Metabolic Benefits**: 
  - Mitochondrial adaptations
  - Fat oxidation improvements
  - Aerobic capacity building

### Validation Features
- **Cross-Reference**: Compare power and HR zones for consistency
- **Method Comparison**: Show differences between calculation methods
- **Field Test Suggestions**: How to validate zones through training

## Technical Requirements
- Multiple calculation methods
- Cross-validation between power and HR
- Educational content integration
- Real-time calculations
- Export functionality

## UI/UX Considerations
- Clear explanation of Zone 2 importance
- Training plan integration suggestions
- Progress tracking capabilities
- Visual representation of training zones
- Integration with other calculators