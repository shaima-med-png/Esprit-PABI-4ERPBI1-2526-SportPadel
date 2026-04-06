# 🎾 Padel Analytics Dashboard

## Project Overview
This project is a Power BI dashboard analyzing professional Padel tournament 
and player performance data. It provides insights into tournament statistics, 
player competition results, and equipment analytics.

## Data Source
- Source: Padel professional circuit dataset
- Tables used:
  - padel Dim_Country
  - padel Dim_date
  - padel Dim_Equipments
  - padel Dim_Players
  - padel Dim_Tournament
  - padel Fact_Equipment
  - padel Fact_Player_Performance
  - padel Fact_Tournament

## Report Pages

### 1. 🏠 Main Page
Navigation hub with links to all dashboard sections:
- Performance & Analytics
- Tournament Insights
- Competition Stats

### 2. 📊 Competition Stats
- Matchs Gagnés (Won): 8
- Nombre d'apparence: 1.027K
- Win Rate %: 63.49%
- Pts Par Match ratio: 73.28
- Matchs Joués: 13
- Visuals: Donut chart (Matchs Gagnés vs Perdus), Gauge chart, Bar chart 
  (Joueurs Par Tournoi by catégorie)
- Filters: Player, Country, Gender

### 3. 🏆 Performance Analytics
- Top 10 Points by player
- Top 10 Matchs Joués and Matchs Gagnés by player
- Radar chart: Matchs Joués, Gagnés, Perdus by player
- Detailed player stats table: Win Rate %, Pts Par Match ratio

### 4. 🎯 Tournament Insights
- Total Points: 42M
- Total Players: 181K
- Total Matches: 490K
- Consistency score: 73.28
- Prize Money Total by Tournament Name (bar chart)
- Prize Money Total by catégorie (line chart)
- Nombre Tournois by catégorie (pie chart)
- Categories: Finals, Major, P1, P2

## Tools Used
- Power BI Desktop
- DAX for calculated measures
- Data modeling with star schema (Fact + Dimension tables)

## Author
TEAM SPORT — ESPRIT, 4ER PBI 2025/2026
