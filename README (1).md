# 🎾 Padel Analytics Platform
> **TEAM SPORT — ESPRIT, 4ER PBI 2025/2026**

---

## 📌 Project Overview

The **Padel Analytics Platform** is an end-to-end Business Intelligence and Machine Learning solution built around professional Padel circuit data. It combines a **Power BI dashboard** for interactive exploration with **ML models** for predictive and descriptive analytics — supporting strategic decisions for sponsors, tournament organizers, and player management teams.

The platform is aligned with key **Sustainable Development Goals (SDGs)**:
- 🌍 **SDG 8** — Decent Work & Economic Growth *(sponsor targeting, prize money analysis)*
- 🏗️ **SDG 9** — Industry, Innovation & Infrastructure *(data-driven sport analytics)*
- 🤝 **SDG 17** — Partnerships for the Goals *(sponsor-player matching)*

---

## 🗂️ Data Source

- **Source:** Padel professional circuit dataset (FIP)
- **Architecture:** Star Schema (Fact + Dimension tables)

| Table | Type | Description |
|-------|------|-------------|
| `Dim_Country` | Dimension | Player & tournament country info |
| `Dim_date` | Dimension | Date hierarchy for time-based analysis |
| `Dim_Players` | Dimension | Player profiles and ranking data |
| `Dim_Tournaments` | Dimension | Tournament metadata (name, category, location) |
| `Dim_Equipments` | Dimension | Racket and equipment details |
| `Fact_Player_Performance` | Fact | Match results, win rates, points per match |
| `Fact_Tournament` | Fact | Prize money, participation, round results |
| `Fact_Equipment` | Fact | Equipment usage linked to performance |

---

## 📊 Power BI Dashboard

The dashboard is structured around **4 interactive report pages**, each targeting a specific analytical perspective. It features a consistent teal & purple design theme, a side navigation bar with icon-based routing, and dynamic filters (Gender, Year, Player, Category) applied across all pages.

---

### 📈 Page 1 — Competition Stats

> Provides a high-level overview of player competition performance, match outcomes over time, and geographic distribution of players worldwide.

![Competition Stats](screenshots/competition_stats.png)

**Key KPIs:**
| Metric | Value |
|--------|-------|
| Points / Match | 73.28 |
| Number of Appearances | 1.027K |
| Match Played | 13 |
| Match Wins | 8 |
| Win Rate % | 63.49% |

**Visuals:**
- 📉 Line chart: Match Outcomes Over Time (Won / Lost / Played)
- 🍩 Donut chart: Players per Tournament by Category (P1, Major, P2, Finals)
- 🎯 Gauge chart: Win Rate %
- 🌍 World Map: Player geographic distribution

**Filters:** Gender · Player search

---

### 🏆 Page 2 — Performance & Analytics

> Deep-dives into individual player performance, ranking trends, and gender-based participation breakdown — ideal for scouting and sponsorship targeting.

![Performance Analytics](screenshots/performance_analytics.png)

**Key KPIs:**
| Metric | Value |
|--------|-------|
| Players Growth % | 215.87% |
| Men Players | 2.418K |
| Women Players | 1.411K |
| Total Players 2025 | 199 |
| Total Players 2024 | 63 |

**Visuals:**
- 📊 Horizontal bar chart: Top 10 Matchs Joués & Gagnés by player (Men & Women)
- 🍩 Donut chart: Women vs Men Players distribution (63.15% vs 36.85%)
- 📋 Detailed stats table: Win Rate %, Pts Par Match ratio per player

**Filters:** Gender · Year (2024–2025)

**Featured Players:** Agustin Tapia, Arturo Coello, Alejandro Galan, Federico Chingotto, Veronica Virseda, Franco Stupaczuk...

---

### 🎾 Page 3 — Equipment Insights

> Analyzes equipment market performance, racket types, vendor revenues, and the relationship between equipment price and player win rate.

![Equipment Insights](screenshots/equipment_insights.png)

**Key KPIs:**
| Metric | Value |
|--------|-------|
| Performance Status | ✅ Exceeds Target |
| Total Equipment Market Value | 129.24K |
| Revenue by Product Type | 92.30M |
| Active Players Count | 27 |

**Visuals:**
- 📊 Waterfall chart: Revenue Changes by Product Type & Vendor (Bullpadel, Head, Adidas, Siux)
- 📏 Bullet chart: Racket Performance vs Target (Polyvalente vs Attaque types)
- 🔵 Scatter plot: Equipment Performance by Price (Win Rate % vs Price per product type)

**Filters:** Products · Racket Types · Game Levels · Vendors

---

### 🏅 Page 4 — Tournament Insights

> Explores tournament-level data including prize money distribution, category breakdown, and AI-powered key influencer analysis on match outcomes.

![Tournament Insights](screenshots/tournament_insights.png)

**Key KPIs:**
| Metric | Value |
|--------|-------|
| Consistency Score | 73.28 |
| Total Points | 42M |
| Total Matches | 490K |
| Season | 2026 Padel Tournament Season |
| Tournaments | 21 |
| Participants | 181,242 |

**Visuals:**
- 📊 Bar chart: Top 10 Tournaments by Total Prize Money *(Paris Major & Qatar Major lead)*
- 📉 Line chart: Prize Money Total by Category (Major > Finals > P1 > P2)
- 🥧 Pie chart: Number of Tournaments by Category (P1: 38.1%, Finals: 28.57%, P2: 23.81%, Major: 9.52%)
- 🤖 Key Influencers AI visual: Factors that decrease matches played (by country)

**Filters:** Tournament Names · Year (2024–2025) · Categories (Finals, Major, P1, P2)

---

## 🤖 Machine Learning Models

### 1. 🥇 Sponsor Player Classification
**File:** `padel_sponsor_classification.ipynb`

**Objective:** Classify players into sponsorship tiers to help brands identify and target the right profiles based on competitive performance.

**Approach:** Multi-class supervised classification

**Target Variable:** Sponsorship Tier
| Tier | Criteria | Sponsorship Value |
|------|----------|-------------------|
| 🥇 Premium | Top 33% ranking + strong win rate | High-value deal |
| 🥈 Standard | Mid-tier ranking + average win rate | Mid-range deal |
| 🥉 Basic | Lower ranking + lower performance | Entry-level deal |

**Methodology:**
- Composite score built from: world ranking, ranking points, win rate, title rate
- Tier assignment using percentile-based thresholds (top/mid/bottom 33%)
- Models: XGBoost, Scikit-learn classifiers
- Libraries: `pandas`, `numpy`, `scikit-learn`, `xgboost`, `matplotlib`, `seaborn`

---

### 2. 🏆 Tournament Clustering
**File:** `Padel_Tournament_Clustering.ipynb`

**Objective:** Group tournaments into homogeneous clusters to help sponsors and organizers understand the competition hierarchy and allocate resources effectively.

**Approach:** Unsupervised clustering

**Models Used:** KMeans & Gaussian Mixture Models (GMM)

**Methodology:**
- Data loaded from PostgreSQL (`PIPADEL` database, `padel` schema)
- Full preprocessing pipeline: StandardScaler, OneHotEncoder, SimpleImputer
- Optimal cluster selection via Silhouette Score & Davies-Bouldin Index
- Visualization with Plotly & Seaborn
- Libraries: `scikit-learn`, `pandas`, `plotly`, `sqlalchemy`, `joblib`

---

### 3. 🏓 Tournament Winner Prediction
**File:** `padel_tournament_prediction_fixed.ipynb`

**Objective:** Predict tournament winners based on player performance history, tournament features, and engineered features — enabling data-driven outcome forecasting.

**Approach:** Supervised multi-class classification with data augmentation

**Models Used:** Random Forest, Gradient Boosting, Logistic Regression, Voting Classifier (Ensemble)

**Methodology:**
- Data loaded from PostgreSQL (`PI_padel` database, `DW_Padel` schema)
- Feature engineering: round encoding, win ratios, match history
- Data augmentation to handle class imbalance
- Stratified K-Fold cross-validation
- Libraries: `scikit-learn`, `pandas`, `numpy`, `seaborn`, `sqlalchemy`

---

## 🛠️ Tools & Technologies

| Layer | Tools |
|-------|-------|
| BI & Visualization | Power BI Desktop, DAX |
| Data Modeling | Star Schema (Fact + Dimension tables) |
| Database | PostgreSQL |
| Machine Learning | Python, Scikit-learn, XGBoost |
| Development | Jupyter Notebook |
| Version Control | GitHub |

---

## 👥 Authors

**TEAM SPORT** — ESPRIT School of Engineering  
4ER PBI — 2025/2026
