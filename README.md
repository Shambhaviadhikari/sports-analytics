# NFL Big Data Bowl 2026 — Comprehensive Tracking Analytics
**Theme:** *“The First 0.5 Seconds: Defensive Reaction & Coverage Failure”*  
This repo contains **two full end-to-end scripts** (kept intact conceptually) that perform **tracking analytics + modeling + clustering + broadcast-style visualizations** on Big Data Bowl tracking data.

---

## What this project does (high-level)
We analyze **player tracking data on pass plays** to quantify:
- **Receiver openness** (separation at catch / over time)
- **Coverage matchup performance** (route × coverage)
- **Man vs Zone** differences in space + outcomes
- **Defensive behavior** (reaction time, convergence, pursuit efficiency)
- **Defensive archetypes** (unsupervised clustering)
- **Completion prediction** using early-play features
- **Broadcast-quality visuals** (GIF animation, trails, timelines, heatmaps)

This is useful for:
- **Coaching** (which routes win vs which coverages, when breakdown happens)
- **Scouting** (who reacts fastest, archetype labeling)
- **Broadcast / fan analytics** (animated play visuals)
- **Modeling** (probability of completion using early defensive reaction + separation)

---

## Data
This project assumes Kaggle BDB 2026 file structure:
- `train/input_2023_w01.csv`
- `train/output_2023_w01.csv`
- `supplementary_data.csv`

> **Note:** datasets are not included in this repo due to size + licensing constraints.

---

## Scripts in this repo (what each one adds)

### 1) `ultimate_comprehensive_analysis.py`
**End-to-end analysis pipeline + 8 publication-ready figures + CSV outputs.**

Main analyses:
- Separation at catch point
- Position group analysis (RB vs WR vs TE)
- Route × coverage matchup heatmaps
- Man vs zone comparison
- Defensive convergence + reaction time
- Defensive archetypes clustering
- Temporal separation decay (frame-by-frame)
- Route efficiency index
- Executive dashboard summary

Outputs:
- 8 figures (PNG)
- 6 data exports (CSV)
- A printable terminal report summary

---

### 2) `first_half_second_reaction_model.py`
**Play-level modeling pipeline focused on early reaction & coverage failure.**

Main analyses:
- Defensive reaction time per play (earliest reacting defender)
- Early separation (Frame 2) as “instant openness”
- Coverage breakdown frame (when separation jumps most)
- Logistic regression predicting completion using:
  - reaction_time
  - early_separation
- KMeans clustering of “defensive archetypes” using model features
- AUC + cross validation metrics + ROC curve

Outputs:
- Modeling dataset (`model_df`) + metrics in terminal
- Visualizations for reaction + outcome + ROC + archetypes

---

### 3) `broadcast_visualizations.py`
**Broadcast-quality visual storytelling:**
- `play_animation_broadcast.gif` (animated play)
- `speed_trails.png` (movement trails)
- `separation_timeline.png` (single play separation curve)
- `defensive_heatmap.png` (defender density at ball arrival)

These visuals turn tracking analytics into something immediately understandable.

---

## Key insights (what the analysis is telling us)
### Separation matters
Completed passes show meaningfully higher separation than incomplete passes.  
Separation is a proxy for **throwing window + receiver openness**.

### RB “advantage” is scheme-driven (important nuance)
RBs show much higher separation in this run because RB targets often happen:
- in space (checkdowns, flats)
- after coverage shifts
- on broken plays  
So RB separation is not necessarily “RBs are better,” it’s often **play design + defensive priority**.

### Zone creates space, Man creates tightness
Zone tends to allow more separation on average (by design), while man coverage tightens throwing windows.

### Reaction time + convergence reveal defensive quality
“Quick reactors” (very low reaction frames) are often the defenders who disrupt plays early.  
This supports the theme: **the first 0.5 seconds (few frames) may decide success/failure.**

### Defensive archetypes (clustering)
Clustering on pursuit behavior yields intuitive types like:
- “Ball Hawks” (elite pursuit + fast reaction)
- “Aggressive convergers”
- “Cautious reactors”
- “Zone sitters”  
This turns raw tracking into interpretable defender styles.

---

## Figures (what each picture means)

### 01 — Position Analysis (RB vs WR vs TE)
A 4-panel summary:
- Avg separation
- Completion rate
- Separation distribution
- Avg EPA  
**Interpretation:** RB separation is inflated by scheme/route context; WR/TE separation is more “coverage battle.”

![01 Position Analysis](./figures/01_position_analysis.png)

---

### 02 — Route Coverage Heatmaps
Two heatmaps:
- Avg separation by route × coverage
- Completion rate by route × coverage  
**Interpretation:** identifies which route concepts win/lose against specific coverages.

![02 Route Coverage Heatmaps](./figures/02_route_coverage_heatmaps.png)

---

### 03 — Man vs Zone
4-panel comparison:
- separation
- completion rate
- distribution
- EPA  
**Interpretation:** zone often concedes space; man tightens windows.

![03 Man vs Zone](./figures/03_man_vs_zone.png)

---

### 04 — Defensive Convergence
Shows pursuit behavior:
- convergence rate distribution
- top positions by convergence
- initial distance vs distance closed
- reaction time distribution  
**Interpretation:** reveals “quick reactors” vs slow responders and who closes fastest.

![04 Defensive Convergence](./figures/04_defensive_convergence.png)

---

### 05 — Defensive Archetypes (KMeans)
4-panel clustering summary:
- archetype counts
- clustering scatter
- distance closed by type
- reaction time by type  
**Interpretation:** groups defenders into behavior styles using tracking features.

![05 Defensive Archetypes](./figures/05_defensive_archetypes.png)

---

### 06 — Temporal Separation
2-panel time-series:
- separation over frames with variability band
- frame-to-frame separation change  
**Interpretation:** separation tends to decay as defenders close; spikes often reflect route breaks / coverage switches.

![06 Temporal Separation](./figures/06_temporal_separation.png)

---

### 07 — Route Efficiency
Two charts:
- best routes by “efficiency”
- best routes by wasted yards  
**Interpretation:** compares how directly routes get to the target location vs how much extra distance they travel.

![07 Route Efficiency](./figures/07_route_efficiency.png)

---

### 08 — Executive Dashboard
A one-screen summary of:
- KPI tiles
- separation distribution by position
- man vs zone
- separation decay trend  
**Interpretation:** “one slide” view for portfolio / submission.

![08 Executive Dashboard](./figures/08_executive_dashboard.png)

---

### Defensive Player Heat Map at Ball Arrival
A 2D density map of where defenders end up at ball arrival.
**Interpretation:** shows defensive collapse zones and where defenders most frequently converge.

![Defensive Heatmap](./figures/defensive_heatmap.png)

---

### Broadcast Animation (GIF)
Animated play visualization with offense/defense + target highlight + LOS marker.
**Interpretation:** makes tracking analysis intuitive and explainable.

![Play Animation](./figures/play_animation_broadcast.gif)

---

### Receiver Separation Timeline (single play)
Separation over time for one play with thresholds for tight/contested/open.
**Interpretation:** shows when the receiver got open and whether the window lasted long enough.

![Separation Timeline](./figures/separation_timeline.png)

---

### Speed Trails (single play)
Movement trails show route geometry + pursuit paths.
**Interpretation:** visually explains *how* separation was created, not just the final separation number.

![Speed Trails](./figures/speed_trails.png)

---

## Project quality (brutally honest)
### What’s strong (top-tier)
✅ Combines tracking analytics + stats + ML + clustering + storytelling  
✅ Broadcast-style visuals that make the project memorable  
✅ Insightful framing: reaction time + early frames matter  
✅ Multiple perspectives: macro (league trends) + micro (single play)

### What could be better (to reach “elite”)
- **Sample size stability:** some tables have low counts; enforce minimum play thresholds.
- **Validation:** train/test split by week or game to prove generalization.
- **Route efficiency sanity check:** values > 1 suggest a calculation quirk; fix to keep metric defensible.
- **Archetype validation:** test stability across weeks or compare to known position/role tendencies.

---

## How to run
### Install
```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy pillow
