---
title: session-vo2max
type: note
permalink: sessions/session-vo2max
---

# VO2max Duration-Free Algorithm Session

We've been working on removing the reliance on asking for duration in the VO2max estimation algorithm, but this has reduced accuracy.

The key issue is in the `getDurationFromHRPercent()` function which uses fixed duration bands that don't account for individual variability.

## Complete Code Implementation

### vo2max-functions.js
```javascript
/**
 * VO2max Estimation Functions
 * Clean implementation with only essential functions
 */

/**
 * HR Profile Calculator - Core square root decay formula
 * HR(t) = HRmax - k × √t
 */
function calculateExpectedHR(hrMax, profileK, durationMinutes) {
    return hrMax - profileK * Math.sqrt(durationMinutes);
}

/**
 * Effort Intensity Analyzer
 */
function analyzeEffortIntensity(observedHR, expectedHR, hrMax) {
    const observedPercent = (observedHR / hrMax) * 100;
    const expectedPercent = (expectedHR / hrMax) * 100;
    return observedPercent / expectedPercent;
}

/**
 * True Power Estimator
 */
function estimateTruePower(observedPower, effortIntensity) {
    return observedPower / effortIntensity;
}

/**
 * Calculate W' (anaerobic work capacity) based on phenotype, fitness level, and weight
 */
function calculateWPrime(phenotype, fitnessLevel, weightKg = 80) {
    const basePhenotypeWPrime = {
        'sprinter': 25,      // High anaerobic capacity
        'punchy': 20,        // Moderate-high anaerobic capacity  
        'pursuiter': 15,     // Moderate anaerobic capacity
        'tt': 10             // Low anaerobic capacity (aerobic specialist)
    };
    
    const fitnessLevelFactors = {
        'beginner': 0.75,    
        'intermediate': 0.85,  
        'advanced': 1.3,     
        'elite': 1.5
    };
    
    const baseWPrime = basePhenotypeWPrime[phenotype] || basePhenotypeWPrime['pursuiter'];
    const fitnessMultiplier = fitnessLevelFactors[fitnessLevel] || fitnessLevelFactors['intermediate'];
    const weightMultiplier = weightKg / 80;
    
    return baseWPrime * fitnessMultiplier * weightMultiplier;
}

/**
 * PROBLEMATIC FUNCTION - Determine duration from HR percentage based on physiological ranges
 * THIS IS CAUSING THE ACCURACY REDUCTION
 */
function getDurationFromHRPercent(hrPercent) {
    let baseDuration;
    
    if (hrPercent >= 95) {
        baseDuration = 3;   // >95% = 3 minutes (neuromuscular/anaerobic)
    } else if (hrPercent >= 90) {
        baseDuration = 4;   // 90-95% = 4 minutes (above VO2max)
    } else if (hrPercent >= 85) {
        baseDuration = 6;   // 85-90% = 6 minutes (VO2max range)
    } else if (hrPercent >= 80) {
        baseDuration = 10;  // 80-85% = 10 minutes (threshold-ish)
    } else {
        baseDuration = 20;  // <80% = 20 minutes (aerobic/tempo)
    }
    
    // Cut all durations in half with max of 10 minutes
    const halfDuration = baseDuration / 2;
    return Math.min(halfDuration, 10);
}

/**
 * Get VO2max power (3-minute capability) from any known effort with auto-detected fitness level
 */
function getVo2MaxPower(knownPower, knownHr, phenotype, maxHr, weightKg = 80) {
    // Step 1: Calculate 40-minute power to determine fitness level using HR-based duration
    const power40Min = calculate40MinPower(knownPower, knownHr, phenotype, maxHr, weightKg);
    const autoDetectedFitnessLevel = determineFitnessLevel(power40Min, weightKg);
    
    // Define fitness level k values for HR profile
    const fitnessLevels = {
        'beginner': 4.5,
        'intermediate': 3.0,
        'advanced': 2.0,
        'elite': 1.5
    };
    
    const profileK = fitnessLevels[autoDetectedFitnessLevel] || fitnessLevels['beginner'];
    
    // Step 2: Determine duration from HR percentage - THIS IS THE PROBLEM
    const hrPercent = (knownHr / maxHr) * 100;
    const estimatedDuration = getDurationFromHRPercent(hrPercent);
    
    // Step 3: HR Curve - What should you be able to do for this duration?
    const expectedHR = calculateExpectedHR(maxHr, profileK, estimatedDuration);
    
    // Step 4: Calculate effort intensity and true power capability
    const effortIntensity = analyzeEffortIntensity(knownHr, expectedHR, maxHr);
    const truePowerAtDuration = estimateTruePower(knownPower, effortIntensity);
    
    // Step 5: Calculate CP/W' from true power at estimated duration using auto-detected fitness level
    const { cp, wPrime } = calculateCPWPrime(truePowerAtDuration, estimatedDuration, phenotype, autoDetectedFitnessLevel, weightKg);
    
    // Step 6: Convert to VO2max power (3-minute capability) using CP/W' model
    const vo2maxPower = getPowerAtDuration(cp, wPrime, 3);
    
    return vo2maxPower;
}
```

## Problem Analysis

The accuracy reduction comes from the `getDurationFromHRPercent()` function which:

1. **Uses fixed duration bands** - Same HR% always maps to same duration regardless of individual fitness
2. **Ignores individual variability** - A fit person can sustain higher HR for longer than an unfit person
3. **Arbitrary duration reduction** - Cuts all durations in half with 10-minute max
4. **Loses actual effort information** - We're estimating duration instead of using real duration data

## Potential Solutions

1. **Make duration bands fitness-dependent** - Adjust duration estimates based on detected fitness level
2. **Use power-to-duration relationships** - Estimate duration from power output relative to fitness
3. **Add uncertainty bands** - Accept that estimates will be less precise than actual duration
4. **Hybrid approach** - Ask for duration ranges instead of exact duration

Target: 33-37 ml/kg/min VO2max (Garmin reference)