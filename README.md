# Crowning the GOAT A Data-Driven NBA Basketball Analysis went with this

![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)
![GitHub](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

- [Project Introduction](#project-introduction)
- [:abc: Glossary](#abc-glossary)
- [:dart: Project Goals](#dart-project-goals)
- [:question: Questions to Answer](#question-questions-to-answer)
  - [Player Performance Analysis](#player-performance-analysis)
  - [Era \& Team Comparisons](#era--team-comparisons)
  - [MVP \& Dream Team](#mvp--dream-team)
- [:information\_source: Data Source](#information_source-data-source)
- [:hammer: Tech Stack](#hammer-tech-stack)
- [:broom: Data Cleaning \& Preparation](#broom-data-cleaning--preparation)
- [:microscope: Analysis \& Key Findings](#microscope-analysis--key-findings)
  - [Player Performance Analysis](#player-performance-analysis-1)
  - [Era \& Team Comparisons](#era--team-comparisons-1)
- [:warning: Limitations](#warning-limitations)


## Project Introduction

An argument has plagued the game of Basketball that is as old as the game itself.

**WHO IS THE MVP?** 

Many have laid claim to the throne throughout the years.

However, using SQL, this project casts aside opinion and will crown an MVP based on NBA player performance statistics across 27 seasons (1996-97 to 2022-23).

In addition, performance trends across players, seasons, teams and experience levels will be analyzed to paint a broader picture of performance beyond the MVP.

## :abc: Glossary

|Abbreviation | Full Form | Description |
|---|---|---|
| `draft_year` | N/A | The year the player was picked |
| `draft_round` | N/A | The round in which the player was picked. There are 2 rounds. Round 1 picks are considered more promising. **Pre-1989 draft year, there are more than 2 draft rounds.** |
| `gp` | Games Played | How many games a player participated in that season |
| `pts` | Points | Average points scored per season |
| `reb` | Rebounds | Average times the player grabbed a missed shot per season |
| `ast` | Assists | Average times they passed to someone who scored per game |
| `net_rating` | Net Rating | When this player is on court, does the team outscore opponents or get outscored? Positive = good |
| `oreb_pct` | Offensive Rebound % | Out of all possible offensive rebounds while a player was on court, what % did he grab? |
| `dreb_pct` | Defensive Rebound % | Same idea as `oreb_pct` but for defensive rebounds |
| `usg_pct` | Usage % | How much of the team's plays "go through" this player. high % = ball is in his hands a lot |
| `ts_pct` | True Shooting % | How efficiently does the player score? Accounts for 2-pointers, 3-pointers AND free throws |
| `ast_pct` | Assist % | Out of all teammate baskets while he was on court, what % did he set up? |
| `PG` | Point Guard | Typically the shortest player on the floor and primary ball handler, responsible for setting up plays. In this project, players under 190cm are classified as `PG`. |
| `SG` | Shooting Guard | A perimeter scorer, often the team's go-to shooter. In this project, players between 190cm and 198cm are classified as SG. |
| `SF` | Small Forward | A versatile, all-around position blending scoring, rebounding and defense. In this project, players between 198cm and 205cm are classified as SF. |
| `PF` | Power Forward | A bigger, physical player who scores and rebounds closer to the basket. In this project, players between 205cm and 213cm are classified as PF. |
| `C` | Center | Typically the tallest player on the floor, anchoring the paint on both ends. In this project, players over 213cm are classified as C. |

## :dart: Project Goals
  
- Which players lead their seasons in scoring, rebounding, and playmaking and how efficient are they?

 - How do players from different eras (1990s, 2000s, 2010s, 2020s) compare in size, style, and performance?

 - Which teams, positions, or player types consistently produce top performers?

 - Based on the data, who deserves the MVP crown?

## :question: Questions to Answer

### Player Performance Analysis

 - Rank players in each season by points, rebounds, assists per game.

- Compare efficiency stats (TS% vs usage%) - do volume scorers sacrifice efficiency?

- Identify most improved players across seasons (biggest jump in points/rebounds/assists).

### Era & Team Comparisons

- Compare average player size (height/weight) between 1990s, 2000s, 2010s, and 2020s.

- Identify which teams consistently produce top-performing players.

- Look at rookies vs veterans - how do their contributions differ?

### MVP & Dream Team

- Use a weighted index (e.g., 40% points, 15% rebounds, 15% assists, 30% efficiency) to find an MVP for a given season.

- Build your dream starting 5 (PG, SG, SF, PF, C) using stats across all seasons.

## :information_source: Data Source

[:link:Raw Data](Data\nba_all_seasons_raw_data.csv)

> **Note:** On GitHub, click the link above then click the :arrow_down: **Download** 
> button (or press the download icon) on the top right of the page to save the file.

## :hammer: Tech Stack

- **MySQL 8.0+** - Database creation and querying

- **Magic SQL** - Running SQL queries directly within Jupyter notebooks

- **VS Code** - IDE environment

- **Jupyter Notebooks** - Notebook-based structure for combining SQL, narrative, and findings

## :broom: Data Cleaning & Preparation

*Full query and methodology available in [:link:Data Cleaning Notebook](Notebooks/Cleaning/Data%20Cleaning.ipynb)*

| # | Issue/Observation | Action Taken |
|---|---|---|
| 1 | Unnamed index column and `college` column added no value to the analysis questions. | Excluded both columns from analysis. |
| 2 | `season` was stored as a string range (e.g. `1996-97`), making era-based grouping difficult. | Extracted `season_starting_year` using `SUBSTRING_INDEX()`. |
| 3 | No column existed to group seasons into eras for comparison. | Derived a `decade` column (1990s–2020s) from `season_starting_year` using a `CASE` statement. |
| 4 | `draft_round` contained values from 0 to 8, despite the NBA Draft only having 2 rounds. | Investigated and found pre-1989 drafts had more than 2 rounds. Documented in the Glossary rather than corrected, since `draft_round` was not used in core analysis. |
| 5 | Small sample sizes (e.g. 1 game played) produced misleading statistics, such as a 100% usage rate. | Applied a minimum games played threshold (`gp >= 20`) across efficiency, MVP, and "most improved" analyses. |
| 6 | "Most improved player" rankings were skewed by players with minimal prior playing time, inflating perceived improvement. | Additionally filtered to players averaging more than 5 points in their prior season. |

## :microscope: Analysis & Key Findings

*Full query and methodology available in [:link:Data Analysis Notebook](Notebooks/Analysis/Data%20Analysis.ipynb)*

### Player Performance Analysis

Players were ranked by points, rebounds, and assists across the full dataset (1996-97 to 2022-23), with games played included for context.

**Top Performers (All-Time, 1996-97 to 2022-23, minimum 20 games played)**

*Scoring (pts):*

| Rank | Player | Season | GP | Pts |
|---|---|---|---|---|
| 1 | James Harden | 2018-19 | 78 | 36.1 |
| 2 | Kobe Bryant | 2005-06 | 80 | 35.4 |
| 3 | James Harden | 2019-20 | 68 | 34.3 |
| 4 | Joel Embiid | 2022-23 | 66 | 33.1 |
| 5 | Allen Iverson | 2005-06 | 72 | 33.0 |

*Rebounding (reb):*

| Rank | Player | Season | GP | Reb |
|---|---|---|---|---|
| 1 | Dennis Rodman | 1996-97 | 55 | 16.1 |
| 2 | Andre Drummond | 2017-18 | 78 | 16.0 |
| 3 | Andre Drummond | 2018-19 | 79 | 15.6 |
| 4 | Ben Wallace | 2002-03 | 73 | 15.4 |
| 5 | Andre Drummond | 2019-20 | 57 | 15.2 |
| 5 | Kevin Love | 2010-11 | 73 | 15.2 |
| 5 | DeAndre Jordan | 2017-18 | 77 | 15.2 |

*Playmaking (ast):*

| Rank | Player | Season | GP | Ast |
|---|---|---|---|---|
| 1 | Rajon Rondo | 2011-12 | 53 | 11.7 |
| 1 | Russell Westbrook | 2020-21 | 65 | 11.7 |
| 1 | Rajon Rondo | 2015-16 | 72 | 11.7 |
| 4 | Chris Paul | 2007-08 | 80 | 11.6 |
| 4 | Steve Nash | 2006-07 | 76 | 11.6 |

**Efficiency vs Usage**

A common assumption is that high-usage players (those who handle the ball more) sacrifice shooting efficiency. The data shows the opposite:

| Usage Category | Avg True Shooting % | Total Players |
|---|---|---|
| Low Usage (< 0.20) | 0.53 | 6,823 |
| Medium Usage (0.20–0.30) | 0.53 | 3,679 |
| High Usage (> 0.30) | 0.57 | 218 |

*(Filtered to `gp >= 20` to exclude small sample sizes.)*

High usage players are slightly **more** efficient, not less, suggesting elite players earn the ball more precisely because they're efficient with it, rather than usage causing a drop in quality.

**Most Improved Players**

Using `LAG()` to compare each player's season-over-season stats (filtered to players averaging 5 or more points in the prior season, to exclude bench-to-starter jumps rather than genuine improvement), the biggest single-season point improvements were

  - Paul George (+14.3, 2015)
  
  - CJ McCollum (+14.0, 2015)
  
  - Amar'e Stoudemire (+11.7, 2006)
  
  - Zach Randolph (+11.7, 2003)


### Era & Team Comparisons

**Player Size & Scoring Across Decades**

| Decade | Avg Height (cm) | Avg Weight (kg) | Avg Pts | Total GP |
|---|---|---|---|---|
| 1990s | 200.86 | 100.54 | 7.83 | 86,964 |
| 2000s | 201.04 | 101.36 | 8.10 | 244,989 |
| 2010s | 200.60 | 100.01 | 8.27 | 250,084 |
| 2020s | 198.82 | 97.78 | 8.75 | 74,987 |

NBA players have grown shorter and lighter over time, while average scoring has steadily risen which is consistent with the league's shift toward "pace and space" basketball, prioritizing speed and shooting over size.

*(Note: Total games played for the 2020s is lower than other decades simply because the dataset only covers a few seasons of that decade (2020-21 to 2022-23), not because fewer games were played per season.)*

**Teams Producing Top Performers**

A "top performer" was defined as a player averaging 20 or more points per game across a minimum of 20 games played in a season.

| Team | Seasons w/ Top Performer | Total Appearances |
|---|---|---|
| Minnesota Timberwolves | 25 | 30 |
| Los Angeles Lakers | 23 | 32 |
| Sacramento Kings | 22 | 28 |
| Toronto Raptors | 22 | 26 |
| Golden State Warriors | 22 | 35 |
| Dallas Mavericks | 21 | 26 |
| New York Knicks | 20 | 23 |
| Milwaukee Bucks | 20 | 29 |
| Chicago Bulls | 19 | 23 |
| Cleveland Cavaliers | 19 | 22 |

 - Golden State stands out for total appearances (35) relative to seasons (22), indicating they often fielded *multiple* 20+ point scorers in the same season, rather than relying on a single star.

 - Minnesota's #1 ranking by seasons reflects sustained individual scoring talent rather than historical team success, highlighting the difference between having a star and building a winning team.


**Rookies vs Veterans**

Players were grouped by age into three experience levels: Rookie (under 23), Mid Career (23–29), and Veteran (30+).

| Experience Level | Avg Pts | Avg Reb | Avg Ast |
|---|---|---|---|
| Rookie | 7.75 | 3.40 | 1.56 |
| Mid Career | 8.40 | 3.57 | 1.80 |
| Veteran | 8.05 | 3.61 | 2.02 |

 - Scoring peaks during a player's prime years (Mid Career) before slightly declining as a Veteran

 - Assists and rebounds continue climbing with experience, indicating basketball IQ and positioning compensate for physical decline later in a career.









## :warning: Limitations

