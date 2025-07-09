---
title: Vo2max calculation   spec
type: backlog_item
permalink: product-development/os-projects/coach-jack/backlogs/VO2max Calculation - Spec
---

### The "Your Real VO2max" Adaptive Model

This model provides a daily, live fitness estimate by processing ride data through a multi-layered, adaptive system that intelligently accounts for training focus, riding context, and performance breakthroughs.

1. Data Filtering & Preparation

This initial stage creates the "gold-standard" data segments used for all subsequent calculations.

- Warm-up Exclusion: The first 20 minutes of every ride are ignored.
    
- Adaptive Segment Filtering: The system finds stable-effort segments using adaptive criteria based on the intensity zone to ensure high-quality data from all training types:
    

- For Zone 1-3: Requires a 3-minute minimum duration and high stability (HR Standard Deviation < 2.0 bpm).
    
- For Zone 4: Requires only a 90-second minimum duration and has a more lenient stability threshold (HR Standard Deviation < 3.0 bpm).
    

- Threshold Capping: As part of this filtering, any segment where Average Power >= 98% of FTP is excluded from the data sets used for regression.
    
- Data Window: The system operates on a rolling 42-day window of these clean segments.
    

2. Automated Context Classification

This stage solves the "different bikes/surfaces" problem without user tagging.

- Efficiency Factor: The model analyzes the physics (Power vs. Speed/Gradient) of every clean segment to calculate its "Efficiency Factor."
    
- Two-Bucket System: Based on this factor, it automatically groups data into two buckets:
    

- Primary Factor Profile: Data that matches the user's normal, historical efficiency.
    
- High-Efficiency Factor Profile: Outlier data from contexts that are significantly more efficient.
    

3. The Core Engine: Independent Parallel Models

For each of the two context buckets above, the system maintains two separate underlying regression models to understand different aspects of fitness:

- The Base Model: Calculated using all stable segments from Zones 1, 2, and 3. This tracks pure, sub-threshold aerobic efficiency.
    
- The Peak Model: Calculated using all stable segments from Zones 1, 2, 3, and 4. This tracks the complete aerobic performance picture up to the threshold.
    

4. The Daily Calculation: The "Dual-Blending" Process

This produces the single, intelligent pVO2max (in watts) for the day through a two-stage blend.

- Stage A: The Intensity Blend: First, within each context profile (Primary and High-Efficiency), the system blends its Base and Peak models. This blend is determined by a "Peak Focus Factor," a rolling average (with a ~21-day half-life) of Weighted Peak Minutes (Z4 time x1, Z5 time x2, Z6+ time x3). The blend slides from a default of 90% Base / 10% Peak up to a maximum of 50/50 when the user's high-intensity work consistently meets a target equivalent to ~10% of their total training volume.
    
- Stage B: The Context Blend: The system then takes the final estimate from the Primary Profile and the High-Efficiency Profile and blends them. The weighting is determined by the proportion of recent segments in each bucket, ensuring the final number is a fair reflection of the user's current riding habits.
    

5. Daily Updates & User-Facing Display

This final layer manages the daily number the user sees, ensuring it's both responsive and stable.

- Foundation + Bonus System: The final blended pVO2max is composed of two parts: a stable Foundational Power representing long-term fitness and a temporary Peak Form Bonus representing recent sharpness.
    
- Breakthroughs: A breakthrough occurs when a new performance is calculated to be higher than the current pVO2max estimate, including any existing bonus from previous days. The difference is added to the Peak Form Bonus via the "Parallel Shift" method, immediately lifting the score.  We should add the previous bonus segment into the primary and peak mixes and calculate the difference between the new total pVO2max (foundation + new higher bonus) and the new Foundational Power (this would be the new bonus shown.
    
- Decay: Each day, only the Peak Form Bonus decays slightly, protecting the user's hard-earned foundational number.  It should go from 100% weight to 0% over 42 days.
    
- Final Display: The total pVO2max (Foundation + Bonus) is converted to the user-facing VO2max number using the latest body weight. The long-term history chart tracks the trend of the more stable pVO2max (watts).
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewx_6AZHPBMLQ1jbB5HHoQDWXPcb7XaDlg7k3J-2QpVYUcCJ3CZN2IZNT0o7srmvAvBMwAbp9552yHwLpvrC4X2TuYPqtU8DDZUxE58bveQbdRlBpZlkv3EUPhXf2yV-ZKIdl-?key=PTHNIUEKLGell_5nE8dRBQ)