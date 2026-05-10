# 🎾 Padel Analytics Platform
> **TEAM SPORT — ESPRIT, 4ER PBI 2025/2026**

---

## 📌 Project Overview

The **Padel Analytics Platform** is an end-to-end Business Intelligence and Machine Learning solution built around professional Padel circuit data. It combines a **Power BI dashboard** for interactive exploration, **ML models** for predictive and descriptive analytics, a **FastAPI REST API** for model serving, a **web application** for stakeholder interaction, and a **MLOps monitoring stack** — supporting strategic decisions for sponsors, tournament organizers, and player management teams.

The platform is aligned with key **Sustainable Development Goals (SDGs)**:
- 🌍 **SDG 8** — Decent Work & Economic Growth *(sponsor targeting, prize money analysis)*
- 🏗️ **SDG 9** — Industry, Innovation & Infrastructure *(data-driven sport analytics)*
- 🤝 **SDG 17** — Partnerships for the Goals *(sponsor-player matching)*

---

## 🗂️ Data Source

- **Source:** Padel professional circuit dataset (FIP / Premier Padel)
- **Architecture:** Star Schema (Fact + Dimension tables)
- **Database:** PostgreSQL (`DW_Padel` schema)

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

The dashboard is structured around **4 interactive report pages**, each targeting a specific analytical perspective. It features a consistent teal & purple design theme, a side navigation bar with icon-based routing, dynamic filters (Gender, Year, Player, Category) applied across all pages, and **Row-Level Security (RLS)** to restrict data access per user role.

### 🔐 Row-Level Security (RLS)

| User Email | Role | Visible Data |
|------------|------|--------------|
| `player@gmail.com` | playerDashboard | Player performance data only |
| `tournament@gmail.com` | tournamentDashboard | Tournament data only |
| `equipments@gmail.com` | equipmentsDashboard | Equipment data only |

---

### 📈 Page 1 — Competition Stats

> Provides a high-level overview of player competition performance, match outcomes over time, and geographic distribution of players worldwide.

![competition_stats](https://github.com/user-attachments/assets/1181b7f3-69e7-4459-ae17-72d69adeacfe)

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

![performance_analytics](https://github.com/user-attachments/assets/ce782221-b717-4eac-bd5b-874d38688b82)

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

![equipment_insights](https://github.com/user-attachments/assets/1f637e54-c51d-49a7-bf17-500bca7db3c6)

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

![tournament_insights](https://github.com/user-attachments/assets/8788dccb-bc0f-46b1-8ff3-ab6ed318ac44)

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

> ![ml_overview](https://via.placeholder.com/900x300.png?text=Add+ML+Models+Overview+Screenshot+Here)

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

> ![sponsor_classification](https://via.placeholder.com/900x300.png?text=Add+Sponsor+Classification+Screenshot+Here)

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

> ![tournament_clustering](https://via.placeholder.com/900x300.png?text=Add+Tournament+Clustering+Screenshot+Here)

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

> ![winner_prediction](https://via.placeholder.com/900x300.png?text=Add+Winner+Prediction+Screenshot+Here)

---

### 4. 📈 Player Ranking Forecasting (Time Series)
**File:** `padel_ranking_forecasting.ipynb`

**Objective:** Forecast player ranking evolution over future seasons using historical performance data, enabling federations and sponsors to anticipate rising talent.

**Models Used:**

| Model | Type | Best R² |
|-------|------|---------|
| ARIMA | Statistical time series | — |
| Prophet | Seasonal decomposition (Meta) | — |
| XGBoost | Gradient boosting regression | 0.85 |
| LSTM | Deep learning (sequential patterns) | — |

**Methodology:**
- Time series feature engineering: lag features, rolling averages, trend indicators
- Seasonal decomposition for tournament calendar effects
- Ensemble approach combining statistical and deep learning models
- Libraries: `statsmodels`, `prophet`, `xgboost`, `tensorflow/keras`, `pandas`, `numpy`

> ![ranking_forecast](https://via.placeholder.com/900x300.png?text=Add+Ranking+Forecasting+Screenshot+Here)

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

> ![mlops_grafana](https://via.placeholder.com/900x300.png?text=Add+Prometheus+Grafana+Dashboard+Screenshot+Here)

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

> ![fastapi_swagger](https://via.placeholder.com/900x300.png?text=Add+FastAPI+Swagger+UI+Screenshot+Here)

---

## 🌐 Web Application

**Objective:** Provide a user-friendly web interface for non-technical stakeholders to interact with the platform — access dashboards, run predictions, and explore analytics — without requiring Power BI Desktop or direct API access.

### Features

| Module | Description |
|--------|-------------|
| 🏠 **Home Dashboard** | Overview of key KPIs and platform summary |
| 🔍 **Player Explorer** | Search and compare player stats, rankings, win rates |
| 🏆 **Tournament Browser** | Browse tournaments by category, prize money, location |
| 🤖 **Prediction Center** | Submit player data and get ML predictions (ranking, sponsor tier, winner) |
| 📊 **Analytics View** | Embedded Power BI report pages for deep-dive analysis |
| 🔐 **Role-Based Access** | Login with role-restricted views (Player / Tournament / Equipment) |

### Tech Stack
- **Frontend:** React.js + Tailwind CSS
- **Backend:** FastAPI (shared with ML API)
- **Auth:** JWT authentication with role management
- **Charts:** Recharts / Plotly.js for embedded analytics
- **Deployment:** Docker + Nginx

> ![web_app_home](https://via.placeholder.com/900x300.png?text=Add+Web+Application+Screenshot+Here)

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
| Web Application | React.js, Tailwind CSS, Docker, Nginx |
| MLOps & Monitoring | Prometheus, Grafana, Alertmanager, Locust |
| Development | Jupyter Notebook, VS Code |
| Version Control | GitHub |

---

## 👥 Authors

**TEAM SPORT** — ESPRIT School of Engineering  
4ER PBI — 2025/2026

**Supervised by:** Ridha Berrahal · Ines Mhaya · Malek Naghmouchi
