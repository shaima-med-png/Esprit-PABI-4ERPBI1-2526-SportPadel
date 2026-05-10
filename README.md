# 🎾 Padel Analytics Platform
> **TEAM SPORT — ESPRIT, 4ER PBI 2025/2026**

---

## 📌 Project Overview

The **Padel Analytics Platform** is an end-to-end Business Intelligence and Machine Learning solution built around professional Padel circuit data. It combines a **Power BI dashboard** for interactive exploration, **ML models** for predictive and descriptive analytics, a **FastAPI REST API** for model serving, a **web application** for stakeholder interaction, and a **MLOps monitoring stack** — supporting strategic decisions for sponsors, tournament organizers, and player management teams.

The platform is aligned with key **Sustainable Development Goals (SDGs)**:
- 💚 **SDG 3** — Good Health & Well-Being *(tracking player win rates, match performance, and physical consistency across countries and genders)*
- 🌍 **SDG 8** — Decent Work & Economic Growth *(sponsor targeting, prize money analysis)*
- 🏗️ **SDG 9** — Industry, Innovation & Infrastructure *(data-driven sport analytics)*
- 🤝 **SDG 17** — Partnerships for the Goals *(sponsor-player matching)*

---

## 🗂️ Data Source

- **Source:** Padel professional circuit dataset (FIP / Premier Padel)
- **Architecture:** Star Schema (Fact + Dimension tables)
- **Database:** PostgreSQL (`DW_Padel` schema)

| Table | Type | Key Fields |
|-------|------|------------|
| `padel Dim_Country` | Dimension | `country`, `country_name`, `pk_location` |
| `padel Dim_date` | Dimension | `date`, `Année`, `Trimestre`, `Mois`, `Jour`, `month`, `year`, `PK_id` |
| `padel Dim_Players` | Dimension | `gender`, `move`, `PK_Pl` *(+ more player profile fields)* |
| `padel Dim_Tournament` | Dimension | `Tournament Name`, `categorie`, `country`, `Player Name`, `Round Reached`, `Pk_Tournament`, `Matches Played`, `Matches Won`, `Points Earned`, `PrizePoll` |
| `padel Dim_Equipments` | Dimension | Racket and equipment profile details |
| `padel Fact_Player_Performance` | Fact | `Consistency`, `Joueurs Par Tournoi`, `matches_lost_calc`, `matches_played_calc`, `matches_won_calc`, `Matchs Gagnés`, `Matchs Joués`, `Matchs Par Mois`, `Matchs Perdus`, `Men Players`, `Women Players`, `Players Growth %`, `Points Gagnés`, `points_earned_calc`, `Pts Par Match ratio`, `Top 10 Matchs Gagnés`, `Top 10 Matchs Joués`, `Top 10 Points`, `Top 3 Periods Matches`, `Total Players 2024`, `Total Players 2025`, `Total Players per Tournament`, `Win Loss Ratio`, `Win Rate %`, `appearance_flag_calc`, `fk_date_id`, `fk_location_id`, `fk_players`, `fk_tournament_id`, `pk_fact_id` |
| `padel Fact_Tournament_Event` | Fact | `Brand Visibility`, `Nombre Tournois`, `fk_date_id`, `fk_location_id`, `fk_tournament_id`, `pk_fact_tour_id`, `Prize Money Total`, `Taux de Win`, `Total Players`, `total_matches_calc`, `total_players_calc`, `total_points_calc`, `Tournaments Played` |
| `padel Fact_Equipment_Usage` | Fact | `Active Players Count`, `fk_equipment_id`, `fk_player_id`, `matches_with_equipment`, `Performance Gap`, `Performance Status`, `pk_fact_eq_id`, `Player Count per Equipment`, `Players per Vendor`, `Price Tier`, `Revenue 2023`, `Revenue 2024`, `Revenue 2025`, `Revenue by Product Type`, `Revenue Change 2023 to 2024`, `Revenue Change 2024 to 2025`, `Rolling 3M Wins`, `Total Equipment Market Value`, `usage_count`, `Win Rate Eq%`, `Win Target`, `wins_with_equipment` |

---

## 📊 Power BI Dashboard

The dashboard is structured around **4 interactive report pages**, each targeting a specific analytical perspective. It features a consistent teal & purple design theme, a side navigation bar with icon-based routing, dynamic filters (Gender, Year, Player, Category) applied across all pages, and **Row-Level Security (RLS)** to restrict data access per user role.

### 🏠 Home Page
![dashboard_home](https://github.com/user-attachments/assets/6289f5fc-eaf2-4439-b509-1e925bf82fa8)

### 🔐 Row-Level Security (RLS)

| User Email | Role | Visible Data |
|------------|------|--------------|
| `player@gmail.com` | playerDashboard | Player performance data only |
| `tournament@gmail.com` | tournamentDashboard | Tournament data only |
| `equipments@gmail.com` | equipmentsDashboard | Equipment data only |

---

### 📈 Page 1 — Competition Stats

> Provides a high-level overview of player competition performance, match outcomes over time, and geographic distribution of players worldwide.

![competition_stats](https://github.com/user-attachments/assets/51802522-f94d-43d6-a90a-00d55caa0029)

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

![performance_analytics](https://github.com/user-attachments/assets/a4c982ff-1d1a-4baf-bd29-9ff5b2f3003c)

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

---

### 🎾 Page 3 — Equipment Insights

> Analyzes equipment market performance, racket types, vendor revenues, and the relationship between equipment price and player win rate.

![equipment_insights](https://github.com/user-attachments/assets/cf189940-8faf-4089-b809-66172e7aa3ab)

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

![tournament_insights](https://github.com/user-attachments/assets/529eb31d-af46-41ca-a5ba-ee7ee9583fb6)

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

### 🌱 Page 5 — SDG 3: Good Health & Well-Being

> Dedicated page linking padel performance data to the UN Sustainable Development Goal 3 — tracking player health indicators, match consistency, and participation across countries and genders.

![sdg_page](https://github.com/user-attachments/assets/a03d2032-0519-4671-8dfb-092b3fd2a20d)

**Key KPIs:**
| Metric | Value |
|--------|-------|
| Win Rate % | 63.49% |
| Total Matches | 5K |

**Visuals:**
- 📊 Horizontal bar chart: Matches Played by Country & Gender (Spain, France, UAE, Italy, Saudi Arabia…)
- 📉 Line chart: Win Rate % by Month (seasonal performance trends)

**Filters:** Tournaments · Country · Gender · Year (2024–2025)

---

## 🤖 Machine Learning Models

> ![ml_overview](https://github.com/user-attachments/assets/d45bae87-2205-417e-a8c5-8fa224dec5b7)

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

> ![sponsor_classification](https://github.com/user-attachments/assets/e2661a73-c828-441e-b475-edd86a1c914f)

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

### 4. 📈 Player Ranking Forecasting (Time Series)
**File:** `padel_ranking_forecasting.ipynb`

**Objective:** Forecast player ranking evolution over future seasons using historical performance data, enabling federations and sponsors to anticipate rising talent.

**Models Used & Performance:**

| Model | MAE (↓ better) | RMSE (↓ better) | MAPE (↓ better) | Winner |
|-------|---------------|-----------------|-----------------|--------|
| ARIMA | 228.8 | 259.8 | 48.5% | — |
| Prophet | 230.4 | 266.6 | 49.2% | — |
| XGBoost TS | 328.7 | 348.1 | 63.2% | — |
| **LSTM** | **211.2** | **246.8** | **44.1%** | 🏆 Best |

> LSTM achieved the lowest error across all 3 metrics — MAE, RMSE, and MAPE.

**Methodology:**
- Historical data from Jan 2022 to Jul 2023 used for training
- 3-month future forecast generated (Oct 2023 → Jan 2024)
- Time series feature engineering: lag features, rolling averages, trend indicators
- Seasonal decomposition for tournament calendar effects
- Libraries: `statsmodels`, `prophet`, `xgboost`, `tensorflow/keras`, `pandas`, `numpy`

---

## ⚙️ MLOps & Monitoring

**Stack:** FastAPI + Prometheus + Grafana

**Objective:** Monitor ML models in production, detect performance drift, and maintain platform reliability.

### Infrastructure Components

| Component | Role |
|-----------|------|
| **Prometheus** | Metrics collection & time-series storage |
| **Grafana** | Real-time dashboards & visualization |
| **FastAPI** | API gateway + custom metrics exposition |
| **Alertmanager** | Rule-based alerting & notifications |

### Custom Metrics Tracked
- `prediction_requests_total` — Total API prediction calls
- `model_latency_seconds` — Response time per endpoint
- `prediction_confidence_avg` — Average confidence score per model
- `data_drift_score` — Feature distribution drift vs training baseline
- `error_rate` — Failed predictions per time window

### Alerting Rules
- 🔴 **High latency** alert if `p95 latency > 500ms`
- 🟡 **Data drift** alert if drift score exceeds threshold
- 🔴 **Error spike** alert if error rate > 5% over 5 min
- 🟡 **Model degradation** alert if accuracy drops > 10%

### Load Simulation
- Locust-based load testing scenarios
- Simulated 100 concurrent users hitting prediction endpoints
- Stress test: 500 RPS burst for drift detection validation

---

## 🚀 FastAPI REST API

**File:** `api/main.py`

**Objective:** Serve ML model predictions through a production-ready REST API, exposing endpoints for all ML models.

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Health check & model status |
| `POST` | `/predict/ranking` | Forecast player ranking (ARIMA/Prophet/XGBoost/LSTM) |
| `POST` | `/predict/sponsor-tier` | Classify player sponsorship tier |
| `POST` | `/predict/tournament-winner` | Predict tournament winner |
| `GET` | `/clusters/tournaments` | Get tournament clustering results |
| `GET` | `/metrics` | Prometheus metrics exposition |

### Technical Specs
- **Framework:** FastAPI (Python)
- **Authentication:** JWT Bearer Token
- **Response format:** JSON
- **Average latency:** 150–300ms
- **Model serving:** Joblib-serialized models loaded at startup
- **Docs:** Auto-generated Swagger UI at `/docs`

---

## 🌐 Web Application

**Objective:** Provide a user-friendly web interface for all stakeholders to interact with the platform — access dashboards, explore analytics, and manage data — with role-based access control.

### Tech Stack
- **Frontend:** Angular
- **Backend:** Flask / Django
- **Auth:** JWT authentication with role management (Admin, Player, Tournament, Equipment)
- **Orchestration:** Apache Airflow
- **Automation:** N8N
- **Charts:** Chart.js / embedded analytics visuals
- **Deployment:** Docker + Nginx

### Pages & Features

**🏠 Home Page**
![web_home](https://github.com/user-attachments/assets/c8f48569-49ad-43f4-be6b-bcdb8a27f60c)

> Animated padel court landing page with role-based welcome, live ticker (Top Player, Top Country, Total Players, Matches Played), and navigation to all 4 modules.

---

**📈 Competition Page**
![web_competition](https://github.com/user-attachments/assets/8c7cdcf5-e45e-4824-aff4-86241cf3e53c)

> KPIs: Total Players (3,829) · Revenue 2025 (701.66M) · Revenue 2024 (239.29M) · Total Matches (4,608). Visuals: Match Outcomes Over Last Two Years, Women vs Men Players donut, Top 3 Periods of Matches, Top 5 Countries by Tournaments, Win Rate % (64.15%).

---

**🏆 Performance Page**
![web_performance](https://github.com/user-attachments/assets/d1591b89-90b6-43b1-9212-bb649eda1491)

> KPIs: Total Players (3,829) · Men Players (2,418) · Women Players (1,411) · Players Growth (208.16%). Visuals: Top 10 Players by Match Wins (Arturo Coello, Delfina Brea, Agustin Tapia…), Top 3 Players Overview (Matches/Wins/Losses), Player Match Performance radar, Consistency Score.

---

**🏅 Tournaments Page**
![web_tournaments](https://github.com/user-attachments/assets/c5d20b3b-93cb-4a03-850b-f158316dcdaf)

> KPIs: Avg Players/Tournament (81) · Win Rate % (64.15%) · Total Prize Money (940.95M). Visuals: Prize Money by Category (Major leads), Tournaments by Category donut (P1/P2/Major/Finals), Top 10 Tournaments by Prize Money, Players & Prize by Category.

---

**🎾 Equipments Page**
![web_equipments](https://github.com/user-attachments/assets/bebf797e-80fe-407b-ab4f-d947a245afb8)

> KPIs: Market Revenue (9.23M) · Product Revenue (10.00M) · Active Players (635). Visuals: Revenue by Vendor 2023–2025 (Adidas, Babolat, Bullpadel, Head, Siux, Starvie…), Equipment Performance by Price scatter (attaque vs polyvalente), Top 5 Vendor Revenue Yearly Growth, Racket Performance vs Target.

---

### Role-Based Access

| Role | Access |
|------|--------|
| 👑 **Admin** | All dashboards — Competition, Performance, Tournaments, Equipments, Users |
| 🎾 **Player** | Performance dashboard only |
| 🏆 **Tournament** | Tournaments dashboard only |
| 🛒 **Equipment** | Equipments dashboard only |

---

## 🎬 Video Deliverables

### 📹 Commercial Video (PI-CDIO)
**Duration:** ~3 minutes  
**Objective:** A promotional pitch video presenting the Padel Analytics Platform to a business audience — sponsors, tournament organizers, and federation stakeholders.

**Structure:**
1. **Hook** — The problem: fragmented padel data costs opportunities
2. **Solution reveal** — Platform demo highlights (dashboards, predictions)
3. **Value proposition** — Impact for each stakeholder (sponsor ROI, tournament planning, player scouting)
4. **Call to action** — Platform access & next steps

**Techniques used:** Storytelling, problem-solution narrative, visual demo clips, background music, motion graphics

> [![Commercial Video](https://via.placeholder.com/900x200.png?text=▶+Click+to+Watch+Commercial+Video)](https://your-video-link-here)

---

### 🎥 Technical Video
**Objective:** A detailed walkthrough of the platform's technical architecture for an academic/engineering audience — professors, jury, and technical reviewers.

**Structure:**
1. **Architecture overview** — Star schema, ETL pipeline, database design
2. **ETL walkthrough** — Talend Studio jobs and data flow
3. **Power BI demo** — Dashboard navigation, DAX measures, RLS setup
4. **ML models walkthrough** — Notebook demos, model evaluation results
5. **FastAPI demo** — Live API calls via Swagger UI
6. **MLOps demo** — Prometheus metrics, Grafana dashboards, alerting
7. **Web app demo** — Frontend walkthrough for each user role

> [![Technical Video](https://via.placeholder.com/900x200.png?text=▶+Click+to+Watch+Technical+Video)](https://your-video-link-here)

---

## 🛠️ Tools & Technologies

| Layer | Tools |
|-------|-------|
| BI & Visualization | Power BI Desktop, DAX |
| Data Modeling | Star Schema (Fact + Dimension tables) |
| ETL Pipeline | Talend Studio |
| Database | PostgreSQL |
| Machine Learning | Python, Scikit-learn, XGBoost, TensorFlow/Keras, Prophet, Statsmodels |
| API | FastAPI, Pydantic, Joblib, JWT |
| Web Frontend | Angular |
| Web Backend | Flask / Django |
| Orchestration | Apache Airflow |
| Automation | N8N |
| MLOps & Monitoring | Prometheus, Grafana, Alertmanager, Locust |
| Development | Jupyter Notebook, VS Code |
| Version Control | GitHub |

---

## 👥 Authors

**TEAM SPORT** — ESPRIT School of Engineering  
4ER PBI — 2025/2026
