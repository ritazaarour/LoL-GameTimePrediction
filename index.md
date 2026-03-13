# Classifying Player Positions Using Post‑Game Statistics in League of Legends

by: Cameron Hensley, Ritesh Saxena, Angela Watson, Rita Zaarour


## Introduction

This project uses a **League of Legends match dataset at the player level**, where each row represents **one player’s performance in a single game**. The dataset captures in‑game statistics such as combat performance, resource generation, damage output, gold income, and objective participation. Together, these metrics describe how a player contributes to their team during a match.

League of Legends is a **role‑based game**, where each position (Top, Jungle, Mid, Bottom, Support) serves a distinct strategic purpose. While players select a role before the match begins, their **in‑game behavior and statistics** may tell a more nuanced story about the position they actually played.

#### **Our Question:** 
> _Can we classify a player’s position (Top, Jungle, Mid, Bottom, Support) using only their in‑game statistics?_

This question has clear **machine learning relevance**, as it represents a real‑world **multiclass classification problem** using structured numerical data. It allows us to demonstrate **feature engineering, classification techniques, and model evaluation** using a popular game with rich and interpretable data.

For readers of this website, this project illustrates how **raw gameplay data can be transformed into meaningful insights** about player behavior and team dynamics.

#### **Dataset Summary**
> 124,150 rows and 165 columns

### Relevant Coulmns and Their Descriptions.

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

<iframe src="kills_position.html" width="800" height="500" frameborder="0"></iframe>
The distribution of kills per player in League of Legends is right-skewed, with most players recording relatively low kill counts and a small number of high-performing players producing a long right tail of extreme values. The distributions are similar by position, with the exception of the Support position which has a much higher frequency of low kill values. The differences in kills by position indicates that this might be a good feature for our classification problem.

![Win Rate by Region](Win%20Rate%20by%20Region.png)
The plot demonstrates a strong regional imbalance in League of Legends esports, with Korea and China achieving dominant win rates well above 50%, while most minor regions fall significantly below the global average when competing internationally.


---

## Assessment of Missingness

The url column (missing ~87% of rows) contains links to match VODs. While its missingness correlates with league (some leagues have urls more than others), this correlation alone does not make it MAR. The missingness is ultimately driven by an unobserved variable — whether a league or tournament organizer has a VOD publication policy — which is not captured anywhere in the dataset. The absence of a url is informative about the value itself: a match without a url is one that was never recorded or published, and that fact is tied to something inherent about the match (its league's media infrastructure), not just to observed columns. This makes url NMAR.

To make this MAR, additional data that could explain the missingness includes:

- League media policy data — a column indicating whether each league officially publishes VODs (yes/no). If missingness is fully explained by this flag, it becomes MAR.
- Tournament tier/region — a structured classification of leagues by region and competitive tier (e.g., major vs. minor region), which may proxy for VOD availability.
- Broadcast platform — knowing whether a match was streamed on Twitch, YouTube, or a regional platform (or not at all) would directly explain why no url exists.

If any of these variables were added to the dataset and fully accounted for the missingness pattern in url, the mechanism would shift from NMAR to MAR — because the missingness would then be explainable by observed data rather than the unrecorded value itself.  

From our permutation test, we found that the missing values in the url column do not appear to occur completely at random. When we compared the distribution of game length for matches where the url value is missing versus when it is present, we noticed that the two groups show different patterns. The observed difference in our test statistic was larger than what we typically saw in the permutation distribution under the null hypothesis. Because of this, the resulting p-value was small, which led us to reject the null hypothesis that missingness in the url column is independent of game characteristics.

In simpler terms, this suggests that whether the url value is missing may be related to other variables in the dataset rather than happening randomly. This means the missingness is likely closer to Missing at Random (MAR) instead of Missing Completely at Random (MCAR). This is important for our project because it tells us that we should be careful when handling missing values. If we simply drop rows with missing values, we might unintentionally introduce bias into our analysis. Understanding the pattern of missingness helps us make better decisions about how to handle the data as we continue exploring regional performance and building our prediction models.

<img src="missingness.png" alt="Regional Recall Gap by Position" width="700">

---

## Hypothesis Testing
#### **Question of Interest**
> **Which competitive region has the highest win rate against teams outside their region?**

In the professional **League of Legends** ecosystem, regional identity is a source of pride and often cited by fans and players alike as a real driver of competitive success on the world stage. This analysis seeks to move beyond anecdotal "power rankings" by determining if a team's **home region** is a statistically significant predictor of their win rate in cross-region matches.

By isolating **535 international clashes** from the 2022 season, we test the null hypothesis that all regions possess an **equal probability of victory**. Establishing whether these performance gaps are statistically **"real"** allows us to identify the true hierarchy of global play and determine if the **"gap"** between the East and West (or maybe even between powerhouse regions like China and Korea) is supported by the data.

#### **Hypothesis Framework**

* **Null Hypothesis:** The probability of winning a cross-region match is independent of a team's home region.
* **Alternative Hypothesis:** The probability of winning a cross-region match depends on a team's home region.
* **Test-Statistic:** **Chi-Square Statistic**
    * *Rationale:* We are testing the association between two **categorical variables** (Home Region and Match Result).

Our Chi-Square test returned a p-value below 0.05, indicating that we should reject the null hypothesis and conclude that region does influence win rate.
P-value: 0.00

## Bonferroni‑Adjusted Chi‑Square Results

- **Number of pairs:** 78  
- **Bonferroni‑Adjusted Alpha:** **0.000641**

### Statistically Significant Regional Gaps (Post‑Adjustment)

| Pair | p‑value | Status |
|---|---:|---|
| CIS vs China | 1.534821e‑10 | Significant |
| CIS vs Korea | 6.812126e‑10 | Significant |
| Japan vs China | 4.768216e‑09 | Significant |
| Korea vs Japan | 8.627102e‑09 | Significant |
| CIS vs North America | 4.928379e‑08 | Significant |
| North America vs Japan | 4.745566e‑07 | Significant |
| Oceania vs China | 1.143509e‑06 | Significant |
| Korea vs Oceania | 1.283050e‑06 | Significant |
| Latin America vs China | 4.461116e‑06 | Significant |
| Korea vs Latin America | 5.051276e‑06 | Significant |
| North America vs Oceania | 3.009339e‑05 | Significant |
| Turkey vs China | 3.493086e‑05 | Significant |
| Korea vs Turkey | 3.605527e‑05 | Significant |
| Vietnam vs China | 1.127433e‑04 | Significant |
| North America vs Latin America | 1.181047e‑04 | Significant |
| Korea vs Vietnam | 1.330259e‑04 | Significant |
| Asia‑Pacific vs Japan | 1.446733e‑04 | Significant |
| Asia‑Pacific vs China | 1.508209e‑04 | Significant |
| Asia‑Pacific vs CIS | 1.724185e‑04 | Significant |
| Asia‑Pacific vs Korea | 2.525619e‑04 | Significant |
| Japan vs Europe | 4.029402e‑04 | Significant |
| North America vs Turkey | 5.611446e‑04 | Significant |

> **Note:** All listed comparisons meet the Bonferroni‑adjusted significance threshold (*p* < 0.000641).


---

## Framing a Prediction Problem
We are solving a **multiclass classification** task where we predict a player's position (top, jng, mid, bot, sup) based on their post-game statistics. We chose **position** as our target variable because each position has a relatively different gaming style that is reflected in their post-game stats.

We evaluate our model using **accuracy, precision, recall, and F1-score** together. _Accuracy_ gives us an overall measure of correctness and is appropriate here since the five positions are perfectly balanced in the dataset. We also report _precision, recall, and F1-score_ on a per-role basis. This allows us to identify which specific positions the model struggles to classify and where it performs well, giving us a more complete picture of model performance than any single metric alone.

---

## Baseline Model
Our baseline model is a **Logistic Regression classifier** implemented in a single sklearn Pipeline. Missing values were filled with the column mean before training. We used 85 quantitative features and 1 nominal feature ['side'] out of 165 features total. We did not use any ordinal features. A StandardScaler was applied to the quantitative features and the nominal feature was OneHotEncoded. 

The model achieved **93.52% accuracy** on the test set. Per-role, jungle and support were classified nearly perfectly (F1 ≈ 1.00) due to their highly distinct stat profiles, while bot was also classified strongly (F1 ≈ 0.96). Mid and top were the hardest to distinguish (F1 ≈ 0.86) as they share similar statistics. We believe this is a strong baseline given the natural statistical separation between roles, though there is still room for improvement in distinguishing mid from top. 

---

## Final Model
For our final model we switched to a **Random Forest Classifier** and engineered two new features on top of the existing 85 quantitative and 1 nominal features:

* **['kda_ratio']** = (kills + assists) / (deaths + 1): This captures a player's combat contribution relative to their deaths. Bot and mid laners tend to have high KDA ratios since they are expected to deal damage while avoiding death, whereas top laners have lower ratios since they often absorb damage for the team.
* **['damage_taken_ratio']** = damagetakenperminute / (dpm + 1): This captures how much damage a player absorbs relative to how much they deal. Top laners playing tanks and fighters take significantly more damage relative to their output compared to mid laners who deal high damage while avoiding hits.

These features were chosen to specifically target the mid/top confusion observed in the baseline model, where both roles had the lowest F1-scores (≈ 0.86).

We tuned two hyperparameters using **GridSearchCV** with 5-fold cross validation:

> * **n_estimators** (100, 200): Controls the number of trees in the forest. More trees improves stability and reduces variance in predictions.
> * **max_depth** (None, 10, 20): Controls how deep each tree can grow. Unlimited depth allows the model to learn complex patterns while fixed depths act as regularization against overfitting.

The best parameters were n_estimators = 200 and max_depth = None. The final model achieved **93.08% accuracy**. While overall accuracy is comparable to the baseline, the Random Forest showed some improvement in bot recall (0.96 → 0.97) and maintained perfect classification for jungle and support (F1 ≈ 1.00). 

---

## Fairness Analysis

#### **Fairness Question**
> Does the model perform equally well for players from different regions?

### Performance Metrics by Region

The table below displays the Accuracy, Macro Recall and Macro Precision by Region, giving us an indication of how well our model performs on the whole at a Region level.

| Region           | Accuracy | Macro Recall | Macro Precision |
|------------------|----------|--------------|-----------------|
| China            | 0.834281 | 0.835914     | 0.833810        |
| International    | 0.922314 | 0.924671     | 0.924221        |
| Oceania          | 0.922907 | 0.922845     | 0.928986        |
| CIS              | 0.925272 | 0.926887     | 0.925752        |
| Asia-Pacific     | 0.943631 | 0.945978     | 0.945328        |
| Latin America    | 0.950761 | 0.950258     | 0.950831        |
| Brazil           | 0.955255 | 0.955981     | 0.957214        |
| Europe           | 0.957059 | 0.957202     | 0.957389        |
| Turkey           | 0.957659 | 0.956691     | 0.956607        |
| Vietnam          | 0.957831 | 0.957303     | 0.957523        |
| North America    | 0.961654 | 0.960980     | 0.960985        |
| Korea            | 0.963050 | 0.962087     | 0.963492        |
| Japan            | 0.964876 | 0.964290     | 0.964149        |

Accuracy gap: 0.1306
Macro Recall gap: 0.1284

The Accuracy gap of 0.1306 and Macro Recall gap of 0.1284 indicate that the model performs differently depending on region.

This is further demonstrated at a position level in the following graph, where we can see the recall gap is particularly large for the Mid position.

<img src="regional_recall_gap_by_position.png" alt="Regional Recall Gap by Position" width="700">

### Testing for Fairness

To validate that the difference in model performance by region is statistically significant, we tested two sets of hypotheses.

* **Null Hypothesis:** The Accuracy of our model is consistent across regions.
* **Alternative Hypothesis:** The accuracy of our model is inconsistent for at least one region.
* **Test-Statistic:** **Chi-Square Statistic**

Chi-square statistic: 765.77; p-value: 0.00

* **Null Hypothesis:** The Accuracy of our model is consistent across regions for the Mid position in particular.
* **Alternative Hypothesis:** The accuracy of our model is inconsistent at predicting the Mid position for at least one region.
* **Test-Statistic:** **Chi-Square Statistic**

Mid Recall Chi-square: 523.38; Mid Recall p-value: 0.00

Both p-values are well below a threshold of 0.05, so we reject both null hypotheses. This means that there is a difference in model performance by region and we reject the null hypothsis. We also see a signficant difference in predictions for the Mid position, so we reject that null hypothesis and conclude that our model performs differently across regions for the Mid position.

#### Fairness Conclusion
Although overall regional performance disparities exist, the fairness issue is highly concentrated in the Mid role, which exhibits a recall disparity of 36.8 percentage points across regions. In contrast, Jungle and Support are relatively stable, suggesting that the model’s fairness issues are role-specific rather than universally distributed. The differences in overall recall and recall for the Mid position are statistically significant.

---
