---
title: Create Route Speed Calculator - Spec
type: note
permalink: claude-code-os/os-projects/cycling-calculators/backlog-details/create-route-speed-calculator-spec
---

# Create Route Speed Calculator (Alex's design with Claudes help :)

## Overview
Create a finishing time prediction tool that analyzes GPX/TCX route files and estimates realistic completion times based on rider behavior, not just all-out racing performance. This fills the gap between basic power calculators and race-focused tools like Best Bike Split.

## Core Problem
- Current tools predict race times (all-out effort)
- No tools predict realistic finishing times for recreational rides, group rides, or endurance events
- Need behavioral modeling for how people actually ride vs. theoretical maximum performance

## User Interface Design
**Must match existing calculator styling and UX patterns** from the current cycling calculators suite:
- Consistent visual design language
- Same input field styling and layout patterns
- Matching dropdown styles and behavior
- Consistent color scheme and typography
- Same responsive design approach
- Follow existing error handling and validation patterns

### File Input
- **Upload GPX/TCX file** (drag & drop or file picker)
- Parse elevation profile, distance, and gradient data

### Basic Inputs
- **FTP** (Functional Threshold Power in watts)
- **Weight** (rider + bike combined weight in lbs/kg)
- **Ride Intensity** (Overall ride target intensity):
  - **Pure Zone 2** - Endurance pace throughout
  - **Zone 2/3 Mix** - Mostly easy with some tempo
  - **Zone 3 Tempo** - Steady tempo ride
  - **Zone 3/4 Mix** - Tempo with threshold efforts
  - **Race Pace** - Mixed high intensity

### Behavioral Dropdowns (4 total)

#### 1. Drafting/Group Style
- **Solo Ride** (0% drafting)
- **Aggressive Drafting** (35-40% power savings) - Wheel sucker, maximizes time in draft
- **Moderate Drafting** (25-30% power savings) - Shares work, rotates through paceline  
- **Minimal Drafting** (15-20% power savings) - Often in poor position, edge of group
- **Loose Group/Social** (10-15% power savings) - Frequent regrouping, spread out riding

#### 2. Descent Style
- **Cautious**: 20-25 mph / 30-40 kph
- **Conservative**: 25-30 mph / 40-50 kph  
- **Moderate**: 30-35 mph / 50-55 kph
- **Aggressive**: 35+ mph / 55+ kph

#### 3. Climbing Behavior
- **Conservative Climber**: Stays in target zone, minimal surges
- **Steady Climber**: One zone higher than ride intensity on climbs
- **Aggressive Climber**: Two zones higher on climbs (when sustainable)
- **Racer**: Maximum sustainable power for climb length

#### 4. Aero Position (reuse from existing power calculator)
- **Upright Position (Touring/Comfort)**
- **Relaxed Position (Recreational)**  
- **Standard Road Position**
- **Aggressive Road Position**
- **Time Trial Position**
- **Full Aero Position**

## Technical Implementation

### Physics Engine
Reuse existing power calculation engine from current power calculator:
- Air resistance calculations
- Rolling resistance 
- Gravitational force (climbing)
- CdA values from aero position selection

### Behavioral Modeling Layer

#### Climbing Behavior Logic
Power on climbs is determined by:
1. **Base ride intensity** (Zone 2, Zone 3, etc.)
2. **Climbing behavior modifier** (+0, +1, +2 zones)
3. **Climb length constraints** (can't sustain Z5+ for long climbs)
4. **Gradient minimums** (steep grades force higher power)

**Conservative Climber:**
- Maintains ride intensity zone on climbs
- Only increases power when gradient demands it
- Maximizes efficiency over performance

**Steady Climber:**
- Climbs one zone higher than base intensity
- Example: Zone 2 ride → Zone 3 climbs
- Sustainable approach for most riders

**Aggressive Climber:**
- Climbs two zones higher when possible
- Example: Zone 2 ride → Zone 4 climbs (if climb is short enough)
- Limited by climb duration sustainability

**Racer:**
- Maximum sustainable power for climb length
- Short climbs: Zone 5+
- Medium climbs: Zone 4
- Long climbs: Zone 3-4
- Ignores base ride intensity on climbs

#### Descent Speed Limits
Apply maximum speed caps based on descent style selection:
- Segment-by-segment speed calculation
- Never exceed rider's comfort level regardless of physics
- Apply appropriate power requirements for maintaining vs. exceeding speeds

#### Drafting Benefits
Apply power reduction percentages based on group style:
- Reduce power requirements for flat/rolling sections
- Climbing benefits minimal (5-10% of flat benefits)
- Descent benefits minimal (mainly comfort level affects speed)

### Route Processing Algorithm

#### 1. Parse GPX/TCX Data
- Extract elevation profile with high resolution
- Calculate gradient for each segment
- Identify climb/descent/flat sections
- Determine segment distances

#### 2. Segment Classification
- **Climbs**: Gradient > 3% for > 100m
- **Descents**: Gradient < -3% for > 100m  
- **Flats**: Everything else
- **Steep sections**: Gradient > 8% (triggers explosive behavior)

#### 3. Segment Consolidation Rules
Merge adjacent segments to reflect real-world riding:

**Climb Consolidation:**
- Short descents (<50m) within climbs are ignored
- Flat sections (<100m) within climbs are included
- Brief dips in gradient (<30 seconds at <3%) don't break a climb
- Example: 500m climb + 20m descent + 500m climb = single 1020m climb

**Descent Consolidation:**
- Short climbs (<30m) within descents are ignored  
- Flat sections (<100m) within descents are included
- Brief rises (<20 seconds) don't break a descent

**Why This Matters:**
- Accurate climb length determines power zone limits
- Riders don't recover on brief descents within climbs
- Pacing strategy based on total climb, not segments

##### Climb Length and Proximity Dynamics
Riders adjust their power output based on:

**Perceived Climb Length** (affects pacing strategy):
- **Short climbs** (< 2 minutes): Explosive/Variable climbers often go harder, Steady/Grinder types maintain consistent effort
- **Medium climbs** (2-10 minutes): Most riders start conservatively, Variable types may surge mid-climb
- **Long climbs** (> 10 minutes): All rider types become more conservative, pacing becomes critical

**Distance to Summit** (affects current power decisions):
- **Bottom third**: Conservative start for Steady/Grinder types, Variable types may start aggressively
- **Middle third**: Variable types often settle into sustainable rhythm, Explosive types may fade if they started too hard
- **Final third**: 
  - Steady types maintain consistent effort
  - Variable/Explosive types often increase power as summit approaches
  - All types may increase effort in final 10% of climb

**Implementation Strategy**:
1. Calculate total climb length from elevation profile
2. Determine current position within each climb (% complete)
3. Apply climber type modifiers based on climb length category and position
4. Adjust base power targets accordingly throughout each climbing segment

#### 4. Power Target Calculation
For each segment:
- Calculate physics-based power requirement
- Apply behavioral modifiers based on climbing style
- Apply drafting benefits if applicable
- Factor in fatigue accumulation over ride duration

#### 5. Speed Calculation
For each segment:
- Calculate speed from power using existing physics engine
- Apply descent speed limits based on descent style
- Account for acceleration/deceleration between segments

#### 6. Time Accumulation
- Sum time for all segments
- Add estimated stop time (food/mechanicals/photos)
- Apply fatigue factor for rides > 2-3 hours

## Output Design

### Visual Design for Output Sections
Each output section will have subtle visual differentiation:
- **Terrain Breakdown**: Earth-tone accent line (brown/green) with mountain icon
- **Performance Analysis**: Energy-tone accent (orange/yellow) with lightning bolt icon
- **Route Intelligence**: Cool-tone accent (blue) with map pin icon
- Headers will have light gradient backgrounds using existing color palette
- Consistent with current calculator aesthetic but with refined visual hierarchy
### Primary Output
- **Predicted Moving Time** (HH:MM format)

### Additional Core Analytics (All Required Features)

#### Terrain Breakdown
- **Time spent climbing** - Shows time and percentage on uphill segments
- **Time spent descending** - Shows time and percentage on downhill segments  
- **Time on flats** - Shows time and percentage on flat/rolling terrain
- **Average speeds by segment type** - Climbing speed, descent speed, flat speed

#### Performance Analysis
- **Power distribution summary** - Average power by terrain type, power variability
- **Effort distribution** - Time spent in different power zones (Z1, Z2, Z3, Z4+)
- **Climb-by-climb breakdown** - Individual climb times, distance, elevation gain, and average power for each major climb
- **Normalized Power** - NP for the entire route

#### Route Intelligence
- **Route statistics** - Total elevation gain, maximum gradient, number of climbs
- **Speed profile** - Visual representation of speed changes throughout the route
- **Difficulty analysis** - Identifies the most challenging segments and their impact on overall time

### Visual Components
- **Elevation profile with speed overlay** - Shows predicted speed at each point along the route
- **Power heat map** - Color-coded route showing where you'll be working hardest
- **Time progression chart** - Cumulative time vs. distance to see pacing throughout ride

## Technical Dependencies

### File Processing
- GPX/TCX parsing library
- Elevation profile processing
- Gradient calculation algorithms

### Existing Code Reuse
- Power calculation engine from current calculator
- CdA values and aero position logic
- Rolling resistance coefficients
- Air density and environmental factors

## Validation Strategy

### Test Cases
- Compare predictions against known Strava segments
- Validate with different rider types and routes
- Test edge cases (very hilly, very flat, long/short routes)

### Iterative Improvement
- Collect user feedback on accuracy
- Refine behavioral models based on real ride data
- Add advanced options for power users

## Future Enhancements (Not MVP)

### Weather Integration
- Wind speed/direction effects
- Temperature impact on performance
- Rain/road condition adjustments

### Advanced Behavioral Options
- Fatigue modeling over very long rides
- Nutrition stop time estimation
- Group ride surge/recovery patterns

### Route Optimization
- Suggest pacing strategies
- Identify challenging sections
- Compare different route options

## Success Metrics
- Finishing time predictions within ±10% of actual times
- User engagement and repeat usage
- Positive feedback on realism vs. existing race-focused tools

---

# Route Speed Calculator - Technical Specification

## ✅ HIGH CONFIDENCE (Claude is sure)
- Can reuse existing power calculation physics engine from power-calculator.js
- Can implement GPX/TCX file parsing using browser's DOMParser
- Can calculate distances between GPS points using Haversine formula
- Can classify segments as climb/descent/flat based on gradient thresholds
- Can consolidate adjacent segments to reflect continuous climbs/descents
- Can apply drafting power reductions and descent speed limits
- Can implement ride intensity and climbing behavior modifiers
- Can match existing UI patterns and styling from current calculators
- Will use Coggan power zones for effort distribution
- Support both GPX and TCX files up to 20MB
- Display "Moving Time" instead of total time with stops

## ❓ NEEDS CLARIFICATION (Claude needs input)
- For results sharing: Create shareable link with encoded route/settings, or download results as PDF/image?  

## ⚠️ ASSUMPTIONS (Claude is guessing)
- File upload will use drag-and-drop interface similar to modern web apps - yes
- Gradient smoothing will use simple moving average to reduce GPS noise- yes
- Fatigue factor will be linear increase after 2 hours (1% per hour) - yes
- Climb classification: >100m distance AND >3% gradient - yes
- No stop time calculations - only show moving time - yes

## 🎯 CRITICAL DECISIONS MADE

### Climbing Power Zones by Behavior:
Base power determined by ride intensity, then modified by climbing behavior:

**Zone Adjustments:**
- **Conservative**: +0 zones (stays in ride intensity zone)
- **Steady**: +1 zone (sustainable increase)
- **Aggressive**: +2 zones (when climb length allows)
- **Racer**: Maximum sustainable for climb duration

**Climb Length Power Limits:**
- **Short climbs (<2 min)**: Up to Zone 5+
- **Medium climbs (2-10 min)**: Up to Zone 4
- **Long climbs (>10 min)**: Up to Zone 3-4
- **Very long climbs (>20 min)**: Zone 2-3 max

### Drafting Power Savings:
- **Solo Ride**: 0% savings
- **Aggressive Drafting**: 38% savings on flats
- **Moderate Drafting**: 28% savings on flats  
- **Minimal Drafting**: 18% savings on flats
- **Loose Group/Social**: 12% savings on flats
- *Note: Only 30% of these benefits apply on climbs*

### Results Sharing Options:
- NO SHARING FOR NOW
- 
## Power and Speed Calculation Details

### For Each Route Segment:

#### 1. Determine Base Target Power
**Flat/Rolling Sections:**
- Use ride intensity to set base power zone
- Zone 2 = 56-75% FTP
- Zone 3 = 76-90% FTP  
- Zone 4 = 91-105% FTP
- Zone 5 = 106-120% FTP

**Climbing Sections:**
1. Start with ride intensity base zone
2. Apply climbing behavior modifier:
   - Conservative: +0 zones
   - Steady: +1 zone
   - Aggressive: +2 zones
   - Racer: Max sustainable for climb length
3. Check climb length constraints:
   - <2 min: Allow up to Zone 5+
   - 2-10 min: Cap at Zone 4
   - >10 min: Cap at Zone 3-4
   - >20 min: Cap at Zone 2-3

#### 2. Apply Drafting Modifier
- Calculate base power requirement using physics engine
- Apply drafting reduction to power:
  - Flats: Full drafting benefit (0-25% reduction)
  - Climbs: 30% of drafting benefit
  - Descents: Minimal benefit

#### 3. Check Minimum Power Requirements
- Use physics engine to calculate minimum power needed for gradient/speed
- If target power is below minimum, use minimum required power
- This ensures realistic speeds on steep climbs

#### 4. Calculate Speed from Power
Using existing physics engine:
```
Total Force = Gravity Force + Rolling Resistance + Air Resistance
Required Power = Total Force × Speed / Drivetrain Efficiency
```
Solve for speed given the power

#### 5. Apply Descent Speed Limits
On descents:
- Calculate theoretical speed from power/physics
- Apply descent style speed cap
- Use lower of calculated vs capped speed

#### 6. Apply Fatigue Factor
For rides >2 hours:
- Reduce available power by 1% per hour after 2 hours
- Example: 4-hour ride = 2% power reduction in final segments

### Example Calculation Flow:
**Scenario: 5km climb (including 20m descent in middle), 6% average grade, Zone 2 ride, Steady climber**
0. Segment consolidation: Treat as single 5km climb despite brief descent
1. Base ride intensity: Zone 2 (65% FTP)
2. Climbing modifier: +1 zone → Zone 3 (83% FTP)
3. Climb length (~15 min): Within Zone 3 limit ✓
4. No drafting on climb (solo ride)
5. Physics check: 83% FTP sufficient for 6% grade ✓
6. Calculate speed: ~12 km/h at 250W (300W FTP rider)
7. Time for segment: 25 minutes