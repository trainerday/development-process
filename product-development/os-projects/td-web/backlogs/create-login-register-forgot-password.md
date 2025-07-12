---
title: session
type: note
permalink: //session
---

# VO2max Duration-Free Algorithm Session

## Problem Statement

We've been working on removing the reliance on asking for duration in the VO2max estimation algorithm, but this has reduced accuracy.

## Current Implementation

The algorithm now uses HR-based duration mapping in `getDurationFromHRPercent()` function:

```javascript
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
```

## Issues Causing Accuracy Reduction

1. **Fixed HR-to-duration mapping**: Uses predetermined duration bands based on HR percentage
2. **Individual variability ignored**: People can sustain different durations at same HR% based on fitness/training
3. **Loss of actual effort information**: Estimating duration instead of using real effort duration loses precision
4. **Cascading errors**: Estimated duration affects HR profile calculations → effort intensity → final VO2max
5. **Arbitrary duration reduction**: Cutting all durations in half with 10-minute max may not reflect real physiology

## Algorithm Flow

1. **HR-based duration estimation**: `getDurationFromHRPercent(hrPercent)`
2. **Fitness level auto-detection**: Calculate 40-min power → determine fitness level
3. **HR profile analysis**: Use fitness-specific k-value for expected HR
4. **Effort intensity calculation**: Compare observed vs expected HR
5. **True power estimation**: Adjust observed power by effort intensity
6. **CP/W' modeling**: Calculate Critical Power and W' from true power
7. **VO2max conversion**: Get 3-minute power from CP/W' model

## Target Validation

- Target VO2max: 33-37 ml/kg/min (Garmin reference)
- Need to improve accuracy while maintaining duration-free approach

## Files Modified

- `vo2max-functions.js`: Core algorithm with HR-based duration mapping
- `test-fitness-levels.js`: Testing the duration-free API

## Next Steps

Need to explore solutions to improve accuracy while keeping the duration-free approach.

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
 * @param {number} hrMax - Maximum heart rate
 * @param {number} profileK - HR Profile decay constant
 * @param {number} durationMinutes - Duration in minutes
 * @returns {number} Expected heart rate for duration
 */
function calculateExpectedHR(hrMax, profileK, durationMinutes) {
    return hrMax - profileK * Math.sqrt(durationMinutes);
}

/**
 * Effort Intensity Analyzer
 * @param {number} observedHR - Actual heart rate achieved
 * @param {number} expectedHR - Expected heart rate for duration
 * @param {number} hrMax - Maximum heart rate
 * @returns {number} Effort intensity (0-1 scale)
 */
function analyzeEffortIntensity(observedHR, expectedHR, hrMax) {
    const observedPercent = (observedHR / hrMax) * 100;
    const expectedPercent = (expectedHR / hrMax) * 100;
    return observedPercent / expectedPercent;
}

/**
 * True Power Estimator
 * @param {number} observedPower - Actual power achieved
 * @param {number} effortIntensity - Effort intensity (0-1)
 * @returns {number} Estimated true power capability
 */
function estimateTruePower(observedPower, effortIntensity) {
    // this uses a linear model which since both intensities are the same duration it linear should be accurate enough
    return observedPower / effortIntensity;
}

/**
 * Calculate W' (anaerobic work capacity) based on phenotype, fitness level, and weight
 * @param {string} phenotype - Power phenotype: 'sprinter', 'punchy', 'pursuiter', 'tt'
 * @param {string} fitnessLevel - Fitness level: 'beginner', 'intermediate', 'advanced', 'elite'
 * @param {number} weightKg - Body weight in kg
 * @returns {number} W' in kilojoules
 */
function calculateWPrime(phenotype, fitnessLevel, weightKg = 80) {
    // Base W' values in kJ for different phenotypes (at 80kg advanced level)
    const basePhenotypeWPrime = {
        'sprinter': 25,      // High anaerobic capacity
        'punchy': 20,        // Moderate-high anaerobic capacity  
        'pursuiter': 15,     // Moderate anaerobic capacity
        'tt': 10             // Low anaerobic capacity (aerobic specialist)
    };
    
    // Fitness level scaling factors (less aggressive)
    const fitnessLevelFactors = {
        'beginner': 0.75,    // helps determine w' 
        'intermediate': 0.85,  
        'advanced': 1.3,     
        'elite': 1.5
    };
    
    const baseWPrime = basePhenotypeWPrime[phenotype] || basePhenotypeWPrime['pursuiter'];
    const fitnessMultiplier = fitnessLevelFactors[fitnessLevel] || fitnessLevelFactors['intermediate'];
    const weightMultiplier = weightKg / 80; // Scale based on 80kg reference
    
    return baseWPrime * fitnessMultiplier * weightMultiplier;
}

/**
 * Iterative solver to find CP from long duration efforts
 * @param {number} knownPower - Known power output in watts
 * @param {number} knownDurationSeconds - Known duration in seconds
 * @param {number} wPrimeJoules - W' in joules
 * @returns {number} Solved CP in watts
 */
function solveCPFromLongEffort(knownPower, knownDurationSeconds, wPrimeJoules) {
    let cp = knownPower; // Initial guess: CP starts at known power
    const tolerance = 0.1; // watts
    const maxIterations = 20;
    
    for (let i = 0; i < maxIterations; i++) {
        // Test current CP: does P(t) = CP + W'/t match known power?
        const predictedPower = cp + wPrimeJoules / knownDurationSeconds;
        const error = predictedPower - knownPower;
        
        // Converged?
        if (Math.abs(error) < tolerance) {
            break;
        }
        
        // Adjust CP (damped to prevent oscillation)
        cp -= error * 0.5;
        
        // Safety bounds: CP should be reasonable
        if (cp < knownPower * 0.5) cp = knownPower * 0.5;
        if (cp > knownPower * 1.5) cp = knownPower * 1.5;
    }
    
    return cp;
}

/**
 * Calculate CP and W' from a known power/duration point
 * @param {number} knownPower - Known power output in watts
 * @param {number} knownDuration - Known duration in minutes
 * @param {string} phenotype - Power phenotype for W' calculation
 * @param {string} fitnessLevel - Fitness level for W' scaling
 * @param {number} weightKg - Body weight for W' scaling
 * @returns {Object} {cp, wPrime} - CP in watts, W' in kJ
 */
function calculateCPWPrime(knownPower, knownDuration, phenotype, fitnessLevel, weightKg = 80) {
    // CP represents ~20-minute power capability
    // We need to solve: knownPower = CP + W'/knownDuration_seconds
    // And we know W' from phenotype, fitness level, and weight
    
    const knownDurationSeconds = knownDuration * 60;
    const wPrime = calculateWPrime(phenotype, fitnessLevel, weightKg);
    const wPrimeJoules = wPrime * 1000;
    
    // Calculate CP using iterative solver for mathematical accuracy
    let cpEstimate;
    
    if (knownDuration <= 20) {
        // For durations ≤ 20min, known power should be higher than CP
        // knownPower = CP + W'/duration, so CP = knownPower - W'/duration
        cpEstimate = knownPower - wPrimeJoules / knownDurationSeconds;
    } else {
        // For durations > 20min, use iterative solver to find CP that satisfies CP/W' model
        cpEstimate = solveCPFromLongEffort(knownPower, knownDurationSeconds, wPrimeJoules);
    }
    
    return { cp: cpEstimate, wPrime };
}

/**
 * Get power at target duration using CP/W' model
 * @param {number} cp - Critical Power in watts
 * @param {number} wPrime - W' in kilojoules
 * @param {number} targetDuration - Target duration in minutes
 * @returns {number} Estimated power at target duration
 */
function getPowerAtDuration(cp, wPrime, targetDuration) {
    // Convert target duration to seconds and W' to joules
    const targetSeconds = targetDuration * 60;
    const wPrimeJoules = wPrime * 1000;
    
    // CP/W' formula: P(t) = CP + W'/t
    return cp + wPrimeJoules / targetSeconds;
}

/**
 * Determine duration from HR percentage based on physiological ranges
 * @param {number} hrPercent - Heart rate as percentage of max HR (0-100)
 * @returns {number} Estimated sustainable duration in minutes
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
 * Calculate 40-minute power from any effort using HR-based duration mapping
 * @param {number} knownPower - Known power output in watts
 * @param {number} knownHr - Known heart rate in bpm
 * @param {string} phenotype - Power phenotype: 'sprinter', 'punchy', 'pursuiter', 'tt'
 * @param {number} maxHr - Maximum heart rate in bpm
 * @param {number} weightKg - Body weight in kg
 * @returns {number} 40-minute power in watts
 */
function calculate40MinPower(knownPower, knownHr, phenotype, maxHr, weightKg = 80) {
    // Step 1: Determine duration from HR percentage
    const hrPercent = (knownHr / maxHr) * 100;
    const estimatedDuration = getDurationFromHRPercent(hrPercent);
    
    // Use intermediate fitness level for initial calculation
    const fitnessLevel = 'intermediate';
    const profileK = 3.0; // intermediate k value
    
    // Step 2: HR Analysis using intermediate fitness and estimated duration
    const expectedHR = calculateExpectedHR(maxHr, profileK, estimatedDuration);
    const effortIntensity = analyzeEffortIntensity(knownHr, expectedHR, maxHr);
    const truePowerAtDuration = estimateTruePower(knownPower, effortIntensity);
    
    // Step 3: Calculate CP/W' from true power at estimated duration
    const { cp, wPrime } = calculateCPWPrime(truePowerAtDuration, estimatedDuration, phenotype, fitnessLevel, weightKg);
    
    // Step 4: Get 40-minute power using CP/W' model
    const power40Min = getPowerAtDuration(cp, wPrime, 40);
    
    return power40Min;
}

/**
 * Determine fitness level from 40-minute w/kg power
 * @param {number} power40Min - 40-minute power in watts
 * @param {number} weightKg - Body weight in kg
 * @returns {string} Fitness level: 'beginner', 'intermediate', 'advanced', 'elite'
 */
function determineFitnessLevel(power40Min, weightKg) {
    const wattsPerKg = power40Min / weightKg;
    
    if (wattsPerKg >= 4.5) {
        return 'elite';
    } else if (wattsPerKg >= 3.5) {
        return 'advanced';
    } else if (wattsPerKg >= 2.5) {
        return 'intermediate';
    } else {
        return 'beginner';
    }
}

/**
 * Get VO2max power (3-minute capability) from any known effort with auto-detected fitness level
 * @param {number} knownPower - Known power output in watts
 * @param {number} knownHr - Known heart rate in bpm
 * @param {string} phenotype - Power phenotype: 'sprinter', 'punchy', 'pursuiter', 'tt'
 * @param {number} maxHr - Maximum heart rate in bpm
 * @param {number} weightKg - Body weight in kg for W' calculation
 * @returns {number} VO2max power in watts
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
    
    // Step 2: Determine duration from HR percentage
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

/**
 * Get VO2max in ml/kg/min from VO2max power (research-based formula)
 * @param {number} wVo2max - VO2max power in watts
 * @param {number} weightKg - Body weight in kg
 * @returns {number} VO2max in ml/kg/min
 */
function getVo2Max(wVo2max, weightKg) {
    // Pure revised ACSM formula from PubMed 1549019 without adjustments
    // Convert watts to kgm/min: 1 watt = 6.12 kgm/min
    const kgmPerMin = wVo2max * 6.12;
    
    // Revised ACSM formula: VO2 = (kgm/min × 1.9) + ((3.5 × kg body weight) + 260)
    // Result is in ml/min, convert to ml/kg/min by dividing by weight
    const vo2MlPerMin = (kgmPerMin * 1.9) + ((3.5 * weightKg) + 260);
    return vo2MlPerMin / weightKg;
}

/**
 * Get detailed calculation breakdown for visualization with auto-detected fitness level and HR-based duration
 * @param {number} knownPower - Known power output in watts
 * @param {number} knownHr - Known heart rate in bpm
 * @param {string} phenotype - Power phenotype: 'sprinter', 'punchy', 'pursuiter', 'tt'
 * @param {number} maxHr - Maximum heart rate in bpm
 * @param {number} weightKg - Body weight in kg
 * @returns {Object} Detailed calculation breakdown
 */
function getDetailedCalculation(knownPower, knownHr, phenotype, maxHr, weightKg) {
    // Step 1: Determine duration from HR percentage
    const hrPercent = (knownHr / maxHr) * 100;
    const estimatedDuration = getDurationFromHRPercent(hrPercent);
    
    // Step 2: Calculate 40-minute power to determine fitness level
    const power40Min = calculate40MinPower(knownPower, knownHr, phenotype, maxHr, weightKg);
    const autoDetectedFitnessLevel = determineFitnessLevel(power40Min, weightKg);
    
    const fitnessLevels = {
        'beginner': 4.5,
        'intermediate': 3.0,
        'advanced': 2.0,
        'elite': 1.5
    };
    
    const profileK = fitnessLevels[autoDetectedFitnessLevel] || fitnessLevels['beginner'];
    
    // Step 3: HR Analysis using estimated duration
    const expectedHR = calculateExpectedHR(maxHr, profileK, estimatedDuration);
    const effortIntensity = analyzeEffortIntensity(knownHr, expectedHR, maxHr);
    const truePowerAtDuration = estimateTruePower(knownPower, effortIntensity);
    
    // Step 4: CP/W' Calculation using auto-detected fitness level
    const { cp, wPrime } = calculateCPWPrime(truePowerAtDuration, estimatedDuration, phenotype, autoDetectedFitnessLevel, weightKg);
    
    // Step 5: VO2max calculations
    const vo2maxPower = getPowerAtDuration(cp, wPrime, 3);
    const vo2max = getVo2Max(vo2maxPower, weightKg);
    
    return {
        input: { knownPower, knownHr, phenotype, maxHr, weightKg },
        hrMapping: {
            hrPercent,
            estimatedDuration
        },
        fitnessDetection: {
            power40Min,
            wattsPerKg: power40Min / weightKg,
            autoDetectedFitnessLevel
        },
        hrAnalysis: {
            expectedHR,
            effortIntensity,
            truePowerAtDuration
        },
        cpModel: {
            cp,
            wPrime
        },
        results: {
            vo2maxPower,
            vo2max
        }
    };
}

// Browser/Node.js exports
if (typeof window !== 'undefined') {
    // Browser environment
    window.getVo2MaxPower = getVo2MaxPower;
    window.getVo2Max = getVo2Max;
    window.getDetailedCalculation = getDetailedCalculation;
    window.calculateCPWPrime = calculateCPWPrime;
    window.getPowerAtDuration = getPowerAtDuration;
    window.getDurationFromHRPercent = getDurationFromHRPercent;
    window.calculate40MinPower = calculate40MinPower;
    window.determineFitnessLevel = determineFitnessLevel;
} else if (typeof module !== 'undefined' && module.exports) {
    // Node.js environment
    module.exports = {
        getVo2MaxPower,
        getVo2Max,
        getDetailedCalculation,
        calculateCPWPrime,
        getPowerAtDuration,
        getDurationFromHRPercent,
        calculate40MinPower,
        determineFitnessLevel
    };
}
```

### test-fitness-levels.js
```javascript
const { getVo2MaxPower, getVo2Max, getDetailedCalculation, calculate40MinPower, determineFitnessLevel, getDurationFromHRPercent } = require('./vo2max-functions.js');

console.log('=== Testing HR-Based Duration Mapping - AlexV ===');
console.log();

// Test AlexV data with HR-based duration mapping (no duration input needed)
const testData = {
    knownPower: 130,      // watts
    knownHr: 125,         // bpm
    phenotype: 'punchy',  
    maxHr: 180,           // bpm
    weightKg: 96,
    name: 'AlexV'
};

console.log('TEST INPUT - AlexV (HR-based duration mapping):');
console.log(`  Known effort: ${testData.knownPower}W @ ${testData.knownHr} bpm`);
console.log(`  Max HR: ${testData.maxHr} bpm`);
console.log(`  Phenotype: ${testData.phenotype}`);
console.log(`  Weight: ${testData.weightKg}kg`);
console.log();

// Step 1: Show HR-based duration mapping
const hrPercent = (testData.knownHr / testData.maxHr) * 100;
const estimatedDuration = getDurationFromHRPercent(hrPercent);

console.log('HR-BASED DURATION MAPPING:');
console.log(`  HR percentage: ${hrPercent.toFixed(1)}% of max`);
console.log(`  Estimated duration: ${estimatedDuration} minutes`);
console.log();

console.log('HR PERCENTAGE BANDS:');
console.log('  >95% max HR → 3 minutes (neuromuscular/anaerobic)');
console.log('  90-95% max HR → 4 minutes (above VO2max)');
console.log('  85-90% max HR → 6 minutes (VO2max range)');
console.log('  80-85% max HR → 10 minutes (threshold-ish)');
console.log('  <80% max HR → 20 minutes (aerobic/tempo)');
console.log();

// Step 2: Calculate 40-minute power and determine fitness level
const power40Min = calculate40MinPower(
    testData.knownPower, 
    testData.knownHr, 
    testData.phenotype, 
    testData.maxHr, 
    testData.weightKg
);

const wattsPerKg = power40Min / testData.weightKg;
const autoDetectedFitnessLevel = determineFitnessLevel(power40Min, testData.weightKg);

console.log('FITNESS LEVEL AUTO-DETECTION:');
console.log(`  40-minute power: ${power40Min.toFixed(1)}W`);
console.log(`  40-minute w/kg: ${wattsPerKg.toFixed(2)} w/kg`);
console.log(`  Auto-detected fitness level: ${autoDetectedFitnessLevel}`);
console.log();

console.log('FITNESS LEVEL RANGES:');
console.log('  Beginner: 1.5-2.5 w/kg');
console.log('  Intermediate: 2.5-3.5 w/kg');
console.log('  Advanced: 3.5-4.5 w/kg');
console.log('  Elite: 4.5+ w/kg');
console.log();

// Step 3: Test with new duration-free API
const wVo2maxAuto = getVo2MaxPower(
    testData.knownPower, 
    testData.knownHr, 
    testData.phenotype, 
    testData.maxHr, 
    testData.weightKg
);

const vo2maxAuto = getVo2Max(wVo2maxAuto, testData.weightKg);

console.log('DURATION-FREE RESULTS:');
console.log(`  Estimated duration: ${estimatedDuration} minutes (from ${hrPercent.toFixed(1)}% HR)`);
console.log(`  Auto-detected fitness: ${autoDetectedFitnessLevel}`);
console.log(`  VO2max Power: ${wVo2maxAuto.toFixed(1)}W`);
console.log(`  VO2max: ${vo2maxAuto.toFixed(1)} ml/kg/min`);
console.log();

// Step 4: Get detailed breakdown
const detailed = getDetailedCalculation(
    testData.knownPower,
    testData.knownHr,
    testData.phenotype,
    testData.maxHr,
    testData.weightKg
);

console.log('DETAILED BREAKDOWN:');
console.log(`  Input: ${detailed.input.knownPower}W @ ${detailed.input.knownHr}bpm`);
console.log(`  HR Mapping: ${detailed.hrMapping.hrPercent.toFixed(1)}% → ${detailed.hrMapping.estimatedDuration}min`);
console.log(`  40-min Power: ${detailed.fitnessDetection.power40Min.toFixed(1)}W (${detailed.fitnessDetection.wattsPerKg.toFixed(2)} w/kg)`);
console.log(`  Auto-detected: ${detailed.fitnessDetection.autoDetectedFitnessLevel}`);
console.log(`  Expected HR: ${detailed.hrAnalysis.expectedHR.toFixed(0)}bpm`);
console.log(`  Effort Intensity: ${(detailed.hrAnalysis.effortIntensity * 100).toFixed(1)}%`);
console.log(`  True Power: ${detailed.hrAnalysis.truePowerAtDuration.toFixed(1)}W`);
console.log(`  CP: ${detailed.cpModel.cp.toFixed(1)}W, W': ${detailed.cpModel.wPrime.toFixed(1)}kJ`);
console.log(`  VO2max Power: ${detailed.results.vo2maxPower.toFixed(1)}W`);
console.log(`  VO2max: ${detailed.results.vo2max.toFixed(1)} ml/kg/min`);

console.log();

console.log('TARGET COMPARISON (Garmin: 33-37 ml/kg/min):');
const inRange = vo2maxAuto >= 33 && vo2maxAuto <= 37;
console.log(`  Auto-detected result: ${vo2maxAuto.toFixed(1)} ml/kg/min ${inRange ? '✅' : '❌'}`);

console.log();
console.log('NEW USAGE (duration-free API):');
console.log(`wVo2max = getVo2MaxPower(${testData.knownPower}, ${testData.knownHr}, '${testData.phenotype}', ${testData.maxHr}, ${testData.weightKg})`);
console.log(`vo2max = getVo2Max(wVo2max, ${testData.weightKg})`);

console.log();
console.log('=== SECOND TEST - High HR Effort (Duration-Free) ===');
console.log();

// Second test with high HR effort (should map to shorter duration)
const testData2 = {
    knownPower: 250,      // watts
    knownHr: 160,         // bpm (89% of max HR - should map to 6 minutes)
    phenotype: 'punchy',
    maxHr: 180,           // bpm
    weightKg: 96,
    name: 'AlexV'
};

const hrPercent2 = (testData2.knownHr / testData2.maxHr) * 100;
const estimatedDuration2 = getDurationFromHRPercent(hrPercent2);

console.log('TEST INPUT - AlexV high HR effort:');
console.log(`  Known effort: ${testData2.knownPower}W @ ${testData2.knownHr} bpm`);
console.log(`  HR percentage: ${hrPercent2.toFixed(1)}% of max`);
console.log(`  Estimated duration: ${estimatedDuration2} minutes`);
console.log(`  Max HR: ${testData2.maxHr} bpm`);
console.log(`  Phenotype: ${testData2.phenotype}`);
console.log(`  Weight: ${testData2.weightKg}kg`);
console.log();

// Calculate with duration-free API
const power40Min2 = calculate40MinPower(
    testData2.knownPower, 
    testData2.knownHr, 
    testData2.phenotype, 
    testData2.maxHr, 
    testData2.weightKg
);

const wattsPerKg2 = power40Min2 / testData2.weightKg;
const autoDetectedFitnessLevel2 = determineFitnessLevel(power40Min2, testData2.weightKg);

const wVo2max2 = getVo2MaxPower(
    testData2.knownPower, 
    testData2.knownHr, 
    testData2.phenotype, 
    testData2.maxHr, 
    testData2.weightKg
);

const vo2max2 = getVo2Max(wVo2max2, testData2.weightKg);

console.log('DURATION-FREE RESULTS (high HR):');
console.log(`  Estimated duration: ${estimatedDuration2} minutes (from ${hrPercent2.toFixed(1)}% HR)`);
console.log(`  40-minute power: ${power40Min2.toFixed(1)}W (${wattsPerKg2.toFixed(2)} w/kg)`);
console.log(`  Auto-detected fitness: ${autoDetectedFitnessLevel2}`);
console.log(`  VO2max Power: ${wVo2max2.toFixed(1)}W`);
console.log(`  VO2max: ${vo2max2.toFixed(1)} ml/kg/min`);
console.log();

console.log('COMPARISON - AlexV Tests (both duration-free):');
console.log(`  Low HR (${hrPercent.toFixed(1)}%): ${vo2maxAuto.toFixed(1)} ml/kg/min (${autoDetectedFitnessLevel})`);
console.log(`  High HR (${hrPercent2.toFixed(1)}%): ${vo2max2.toFixed(1)} ml/kg/min (${autoDetectedFitnessLevel2})`);
console.log(`  Difference: ${(vo2max2 - vo2maxAuto).toFixed(1)} ml/kg/min`);
```