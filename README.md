# NBA Winning Strategy: A Data-Driven Framework for Front-Office Decisions

**Author:** Karim Elawadi

## Project Overview

This project analyzes NBA team and player data to answer a single guiding question: *if you were running an NBA franchise, what decisions are actually supported by the data — and which common assumptions are not?*

Rather than producing a general overview of the league, the analysis is structured around specific front-office decisions: how to allocate payroll, how to evaluate contracts, how to weigh draft position, how to use physical attributes in scouting, and how to plan around structural factors such as home-court advantage and referee assignment. Every conclusion in this project is tied directly to a result produced by a SQL query, a correlation calculation, or a chart in the notebook — not to general basketball opinion.

## Tools and Technologies

- **Python** — core language for data processing and analysis
- **SQLite (via `sqlite3`)** — querying the relational basketball database
- **Pandas** — data manipulation and aggregation
- **Seaborn / Matplotlib** — statistical visualizations (correlation heatmaps)
- **Plotly (Express and Graph Objects)** — interactive charts (bar charts, scatter plots, dual-axis line plots, heatmaps)

## Data Source

The analysis uses a relational NBA database (SQLite) containing the following tables: `Player`, `Team`, `Team_Attributes`, `Team_History`, `Player_Attributes`, `Game_Officials`, `Game_Inactive_Players`, `Team_Salary`, `Player_Salary`, `Draft`, `Draft_Combine`, `Player_Photos`, `Player_Bios`, and `Game`.

## Methodology

1. **Data exploration** — inspected all available tables and their schemas via direct SQL queries.
2. **Data cleaning** — identified and corrected several data-quality issues before analysis (see below).
3. **SQL-based aggregation** — computed team-level win rates (using `UNION ALL` to combine home and away games correctly), payroll figures, and roster demographics.
4. **Correlation analysis** — measured the strength of relationships between variables such as salary, win rate, roster age, physical attributes, and draft position.
5. **Feature engineering** — built rolling "recent form" features (last 10 games), context-specific home/away form, and a rest-days feature to evaluate their predictive value for game outcomes.
6. **Exploratory data analysis** — examined feature distributions, checked for outliers using the IQR method, and verified class balance of the target variable.
7. **Visualization** — produced correlation heatmaps, scatter plots, bar charts, and dual-axis comparisons to communicate findings clearly.

## Data Quality Issues Identified and Fixed

- **Win rate miscalculation**: the original approach counted only home games, which was corrected using a `UNION ALL` query to include both home and away games.
- **Placeholder salary values**: an identical salary figure was found to repeat exactly across 14 unrelated players on Two-Way contracts in the 2020-21 season, indicating placeholder rather than genuine data. These rows were excluded from salary-based analysis.
- **Missing All-Star data**: `ALL_STAR_APPEARANCES` returned `NaN` for most players instead of `0`, which was corrected before use in correlation calculations.
- **Season-filtering bias**: filtering strictly to the 2023-24 season shrank the usable sample too much; the analysis instead uses each player's most recently recorded salary to preserve a representative sample.

## Key Findings

1. **Spending does not reliably predict winning.** The correlation between total team payroll and win rate across all 30 teams was only 0.31. The highest-spending team had a middling win rate, while the league's best win rate belonged to a mid-payroll team.
2. **Roster experience matters more than payroll.** Win rate and average roster age tended to move together, while salary rank showed no consistent relationship with either win rate or age.
3. **Value contracts exist and are identifiable.** Several of the best value-for-money contracts (points, assists, and rebounds relative to salary) belonged to role players on minimum or near-minimum salaries.
4. **Draft position predicts average performance, not star potential.** Draft pick position showed a moderate negative correlation (-0.41) with overall performance, but almost no relationship (0.022) with All-Star selection specifically.
5. **Physical attributes matter for rebounding only.** Height, weight, and wingspan showed a moderate positive correlation with rebounding (approximately 0.42-0.43), but a weak, slightly negative correlation with points and assists.
6. **Home-court advantage is real, consistent, and not referee-driven.** Across 101 referees with at least 100 officiated games, home teams won 58.8% of games on average, with almost no variation attributable to individual officials.
7. **Team form should be evaluated by context.** Splitting a team's recent form into home-specific and away-specific components improved its correlation with game outcomes (from approximately 0.28-0.31 to 0.33-0.34), compared to a single blended form metric.
8. **A simple rest-days count was not a useful signal** in this dataset (correlation of 0.021 with game outcome), suggesting that fatigue would need to be modeled differently (e.g., flagging true back-to-back games) to be useful.

## Limitations

This is a correlational analysis of a single dataset, not a causal study. It does not account for coaching quality, team chemistry, in-season trades, scouting depth, or any factor outside the underlying database. The relationships reported here are moderate at best and should be read as directional evidence rather than guarantees.

## Repository Contents

- `Basketball.ipynb` — full analysis notebook, including SQL queries, data cleaning steps, correlation analysis, feature engineering, exploratory data analysis, and all visualizations.

## Contact

**Karim Elawadi**

- **Email:** [hamedkarim343@gmail.com](mailto:hamedkarim343@gmail.com)
- **LinkedIn:** [linkedin.com/in/karim-elawadi](https://www.linkedin.com/in/karim-elawadi)
- **HackerRank:** [hackerrank.com/profile/hamedkarim343](https://www.hackerrank.com/profile/hamedkarim343)
