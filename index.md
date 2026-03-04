# Predicting Game Time Length on League of Legends Data

by: Cameron Hensley, Ritesh Saxena, Angela Watson, Rita Zaarour


## Introduction

This project uses a **League of Legends match dataset at the player level**, where each row represents **one player’s performance in a single game**. The dataset captures in‑game statistics such as combat performance, resource generation, damage output, gold income, and objective participation. Together, these metrics describe how a player contributes to their team during a match.

League of Legends is a **role‑based game**, where each position (Top, Jungle, Mid, Bottom, Support) serves a distinct strategic purpose. While players select a role before the match begins, their **in‑game behavior and statistics** may tell a more nuanced story about the position they actually played.

**Our Question:** Can we classify a player’s position (Top, Jungle, Mid, Bottom, Support) using only their in‑game statistics?

| Column Name | Description |
|------------|------------|
| `position` | The role played by the user in the match (Top, Jungle, Mid, Bottom, Support). This is the **target variable**. |
| `side` | The side the player or team was on: Blue or Red. |
| `kills` | Number of enemy champions the player personally killed during the match; higher for carry roles. |
| `assists` | Number of enemy champion kills the player assisted with; typically higher for Supports and Junglers. |
| `deaths` | Number of times the player died; frontline roles often have higher death counts. |
| `doublekills` | Number of double kills by this player. |
| `triplekills` | Number of triple kills by this player. |
| `quadrakills` | Number of quadra kills by this player. |
| `pentakills` | Number of penta kills by this player. |
| `firstbloodkill` | Whether this player got the first blood kill. |
| `firstbloodassist` | Whether this player assisted on the first blood kill. |
| `firstbloodvictim` | Whether this player was the first blood victim. |
| `damagetochampions` |Total damage dealt to enemy champions; reflects offensive contribution by role. |
| `dpm` | Damage to champions per minute. |
| `damageshare` | Percentage of the team’s total champion damage contributed by the player. |
| `damagetakenperminute` | Damage received from enemy champions per minute. |
| `damagemitigatedperminute` | Damage mitigated (blocked/reduced) per minute. |
| `damagetotowers` | Total damage dealt to towers by this player. |
| `wardsplaced` | Total wards placed by this player. |
| `wpm`| Wards placed per minute|
| `wardskilled` | Total enemy wards destroyed by this player.| 
| `wcpm` |	Wards cleared per minute. |
| `controlwardsbought` | Number of control wards purchased; strongly associated with the Support role. |
| `visionscore` | Composite metric measuring vision control through wards placed, cleared, and maintained. |
| `vspm` | Vision score per minute. |
| `totalgold` | Total gold earned by this player over the entire game. |
| `earnedgold` | Gold earned excluding starting gold. |
| `earned gpm` | Earned gold per minute. |
| `earnedgoldshare` | This player's share of the team's total earned gold. |
| `goldspent` | Total gold spent on items by this player. |
| `total cs` | Total number of minions and monsters killed; distinguishes farming roles from Supports. |
| `minionkills` | Total lane minions killed. |
| `monsterkills` | Total jungle monsters killed. |
| `monsterkillsownjungle` | Number of jungle monsters killed in the player’s own jungle; primary indicator of the Jungle role. |
| `monsterkillsenemyjungle` | Number of jungle monsters killed in the player’s enemy jungle; primary indicator of the Jungle role. |
| `cspm` | Creep score per minute; normalizes farming behavior across different game lengths. |
| `goldat10` | Total gold earned by the player at 10 minutes; captures early‑game economic differences by role. |
| `xpat10` | Total XP at 10 minutes. |
| `csat10` | Total creep score at 10 minutes; indicates early lane or jungle farming patterns. |
| `opp_goldat10` | Lane opponent's total gold earned by the player at 10 minutes |
| `opp_xpat10` | Lane opponent's total XP at 10 minutes. |
| `opp_ csat10` | Lane opponent's total creep score at 10 minutes; indicates early lane or jungle farming patterns. |
| `killsat10` | Player's kills at 10 minutes. |
| `assistsat10` | Player's assists at 10 minutes. |
| `deathsat10` | Player's deaths at 10 minutes. |
| `opp_killsat10` | Lane opponent's kills at 10 minutes. |
| `opp_assistsat10` | Lane opponent's assists at 10 minutes. |
| `opp_deathsat10` | Lane opponent's deaths at 10 minutes. |
| `goldat15` | Total gold earned by the player at 15 minutes. |
| `xpat15` | Total XP at 15 minutes. |
| `csat15` | Total creep score at 15 minutes. |
| `opp_goldat15` | Lane opponent's total gold earned by the player at 15 minutes |
| `opp_xpat15` | Lane opponent's total XP at 15 minutes. |
| `opp_ csat15` | Lane opponent's total creep score at 15 minutes; indicates early lane or jungle farming patterns. |
| `killsat15` | Player's kills at 15 minutes. |
| `assistsat15` | Player's assists at 15 minutes. |
| `deathsat15` | Player's deaths at 15 minutes. |
| `opp_killsat15` | Lane opponent's kills at 15 minutes. |
| `opp_assistsat15` | Lane opponent's assists at 15 minutes. |
| `opp_deathsat15` | Lane opponent's deaths at 15 minutes. |
| `goldat20` | Total gold earned by the player at 20 minutes. |
| `xpat20` | Total XP at 20 minutes. |
| `csat20` | Total creep score at 20 minutes. |
| `opp_goldat20` | Lane opponent's total gold earned by the player at 20 minutes |
| `opp_xpat20` | Lane opponent's total XP at 20 minutes. |
| `opp_ csat20` | Lane opponent's total creep score at 20 minutes; indicates early lane or jungle farming patterns. |
| `killsat20` | Player's kills at 20 minutes. |
| `assistsat20` | Player's assists at 20 minutes. |
| `deathsat20` | Player's deaths at 20 minutes. |
| `opp_killsat20` | Lane opponent's kills at 20 minutes. |
| `opp_assistsat20` | Lane opponent's assists at 20 minutes. |
| `opp_deathsat20` | Lane opponent's deaths at 20 minutes. |
| `goldat25` | Total gold earned by the player at 25 minutes. |
| `xpat25` | Total XP at 25 minutes. |
| `csat25` | Total creep score at 25 minutes. |
| `opp_goldat25` | Lane opponent's total gold earned by the player at 25 minutes |
| `opp_xpat25` | Lane opponent's total XP at 25 minutes. |
| `opp_ csat25` | Lane opponent's total creep score at 25 minutes; indicates early lane or jungle farming patterns. |
| `killsat25` | Player's kills at 25 minutes. |
| `assistsat25` | Player's assists at 25 minutes. |
| `deathsat25` | Player's deaths at 25 minutes. |
| `opp_killsat25` | Lane opponent's kills at 25 minutes. |
| `opp_assistsat25` | Lane opponent's assists at 25 minutes. |
| `opp_deathsat25` | Lane opponent's deaths at 25 minutes. |

---

## Data Cleaning and EDA


---

## Assessment of Missingness


---

## Hypothesis Testing


---

## Framing a Prediction Problem


---

## Baseline Model


---

## Final Model


---

## Fairness Analysis


---