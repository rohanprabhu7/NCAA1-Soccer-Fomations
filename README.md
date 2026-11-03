# NCAA1-Soccer-Fomations
# NCAA Division 1 Soccer Formations Analysis

## Overview
This project analyzes multi-season NCAA soccer match datasets to evaluate team tactical structures and performance. By processing match events, formation data, and league data, this analysis quantifies formation efficiency, win rates, and expected goals (xG) to illustrate tactical effectiveness across varying match scenarios.

## Technologies Used
* **Python**
* **Polars:** Used for memory-efficient lazy evaluation (`scan_parquet`) and fast data manipulation.
* **Matplotlib & Seaborn:** Used for rendering custom data visualizations.
* **Google Colab:** Used as the primary compute environment, leveraging Google Drive mounting for large dataset storage.

## Datasets
The analysis processes several .parquet files:
* all_events.parquet: Contains high-granularity play-by-play actions (passes, shots, duels, infractions).
* matches.parquet: Contains match-level metadata (teams, scores, dates).
* leagues.parquet: Contains division and competition details.
* formations.parquet: Contains team tactical setups and structures.

## Key Features & Methodology

### 1. Data Engineering & Lazy Evaluation
* Loaded and joined multiple large datasets using Polars' lazy execution pipeline to optimize memory usage. 
* Merged event data with match and formation data using corresponding match and team IDs.

### 2. Tactical & Performance Metrics
* **Win Rate Analysis:** Grouped data by team_formation to calculate total games played, total wins, and overall win rates for each tactical setup.
* **Expected Goals (xG):** Aggregated `shot_xg` and actual goals (shot_isGoal) within specific time windows to account for mid-game formation switches. 

### 3. Custom Play Sentiment Analysis
* Implemented a custom weighted scoring system to evaluate team performance beyond standard goals.
* **High/Mid-Impact Positives:** Awarded positive weights for goals, shots on target, accurate progression passes, and successful duels.
* **High/Low-Impact Negatives:** Applied penalty weights for red cards, yellow cards, and stopped progress.
* Aggregated these weighted actions to generate an `overall_play_rating` for each formation.

### 4. Filtering and Visualization
* Filtered out statistically insignificant data by applying a sample-size threshold (e.g., formations used in at least 30 matches).
* Visualized the "Formation Usage Frequency & Selected Cutoff Threshold" using Matplotlib and Seaborn, applying a cutoff line to isolate the top 10 most frequently used formations for deep-dive analysis.
