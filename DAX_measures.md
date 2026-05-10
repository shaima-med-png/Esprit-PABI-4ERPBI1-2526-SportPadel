# DAX Measures Documentation — Padel Analytics Dashboard

---

## Table: padel Fact_Player_Performance

### Consistency
Measures the consistency score of a player across matches.

### Joueurs Par Tournoi (Players Per Tournament)
Counts the number of players participating per tournament.

### Matchs Gagnés (Matches Won)
Total number of matches won by a player.

### Matchs Joués (Matches Played)
Total number of matches played by a player.

### Matchs Par Mois (Matches Per Month)
Total number of matches played per month.

### Matchs Perdus (Matches Lost)
Total number of matches lost by a player.

### Men Players
Total number of male players.

### Women Players
Total number of female players.

### Players Growth %
Percentage growth in the number of players year over year.
> **Formula logic:** (Players Current Year - Players Previous Year) / Players Previous Year × 100

### Total Players 2024
Total distinct players registered in 2024.

### Total Players 2025
Total distinct players registered in 2025.

### Total Players per Tournament
Average number of players per tournament.

### Top 3 Periods Matches
Returns the top 3 time periods (months) with the highest number of matches played.

### Points Gagnés (Points Won)
Total points earned by a player.

### Pts Par Match Ratio (Points Per Match Ratio)
Average points scored per match played.
> **Formula logic:** Total Points / Total Matches Played

### Win Rate %
Percentage of matches won out of total matches played.
> **Formula logic:** Matches Won / Matches Played × 100

### Win Loss Ratio
Ratio of matches won to matches lost.
> **Formula logic:** Matches Won / Matches Lost

### Top 10 Matchs Gagnés (Top 10 Matches Won)
Returns the top 10 players ranked by matches won.

### Top 10 Matchs Joués (Top 10 Matches Played)
Returns the top 10 players ranked by matches played.

### Top 10 Points
Returns the top 10 players ranked by total points earned.

### Total Joueurs Par An (Total Players Per Year)
Total number of distinct players per year.

### appearance_flag_calc
Calculated column flagging whether a player made an appearance.

### matches_lost_calc
Calculated column for total matches lost.

### matches_played_calc
Calculated column for total matches played.

### matches_won_calc
Calculated column for total matches won.

### points_earned_calc
Calculated column for total points earned.

---

## Table: padel Fact_Tournament_Event

### Brand Visibility
Measures the brand visibility score for a tournament event.

### Nombre Tournois (Number of Tournaments)
Total count of tournament events.

### Prize Money Total
Total prize money distributed across all tournaments.

### Taux de Win (Win Rate)
Overall win rate across all tournament events.

### Total Players
Total number of players across all tournament events.

### Tournaments Played
Total number of tournaments played.

### total_matches_calc
Calculated column for total matches in a tournament.

### total_players_calc
Calculated column for total players in a tournament.

### total_points_calc
Calculated column for total points in a tournament.

---

## Table: padel Fact_Equipment_Usage

| Field | Description |
|-------|-------------|
| `Active Players Count` | Number of active players using equipment |
| `league_count` | Number of leagues the equipment was used in |
| `matches_with_equipment` | Matches played using this equipment |
| `usage_count` | Total usage count of the equipment |
| `wins_with_equipment` | Wins achieved while using this equipment |
| `Performance Gap` | Gap between actual and target performance |
| `Performance Status` | Status indicator vs performance target |
| `Player Count per Equipment` | Number of players using each equipment |
| `Players per Vendor` | Number of players per equipment vendor |
| `Price Tier` | Equipment price category |
| `Revenue 2023` | Equipment revenue generated in 2023 |
| `Revenue 2024` | Equipment revenue generated in 2024 |
| `Revenue 2025` | Equipment revenue generated in 2025 |
| `Revenue by Product Type` | Revenue broken down by product type |
| `Revenue Change 2023 to 2024` | Revenue variation between 2023 and 2024 |
| `Revenue Change 2024 to 2025` | Revenue variation between 2024 and 2025 |
| `Rolling 3M Wins` | Rolling 3-month wins with equipment |
| `Total Equipment Market Value` | Total market value of all equipment |
| `Win Rate Eq%` | Win rate percentage when using this equipment |
| `Win Target` | Target win rate for equipment performance |

---

## Dimension Tables

### padel Dim_Players

| Field | Description |
|-------|-------------|
| `gender` | Player gender (Men / Women) |
| `move` | Player movement score |
| `player` | Player name |
| `points` | Player ranking points |
| `position` | Player ranking position |

### padel Dim_Tournament

| Field | Description |
|-------|-------------|
| `Tournament Name` | Name of the tournament |
| `categorie` | Tournament category (P1, P2, Major, Finals) |
| `country` | Tournament host country |
| `Matches Played` | Matches played in tournament |
| `Matches Won` | Matches won in tournament |
| `Player Name` | Name of the player |
| `Points Earned` | Points earned in tournament |
| `PrizePoll` | Prize pool of the tournament |
| `Round Reached` | Furthest round reached |

### padel Dim_Equipments

| Field | Description |
|-------|-------------|
| `handle` | Racket handle type |
| `price` | Equipment price |
| `product_type` | Type of product (Raquettes, Accessoire, Sac, Programme test) |
| `racket_type` | Type of racket (Attaque / Polyvalente) |
| `surface` | Racket surface material |
| `title` | Equipment title/name |

### padel Dim_Country

| Field | Description |
|-------|-------------|
| `country` | Country code |
| `country_name` | Full country name |

### padel Dim_date

| Field | Description |
|-------|-------------|
| `date` | Full date |
| `Année` | Year |
| `Trimestre` | Quarter |
| `Mois` | Month |
| `Jour` | Day |

---

## Author
**TEAM SPORT** — ESPRIT School of Engineering, 4ER PBI 2025/2026
