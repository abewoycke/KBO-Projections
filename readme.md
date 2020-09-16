![KBO Logo](https://upload.wikimedia.org/wikipedia/en/thumb/0/09/Korea_Baseball_Organization.png/250px-Korea_Baseball_Organization.png)

# Korean Baseball Organization Player Projections

_As of June 2020, the KBO (Korean Baseball Organization) was one of the few sports leagues currently being broadcast in the US. This sparked my interest in the league overall, and my interest in projecting player performance. These projections predict hitter performance in three categories (RBI, HR, and BA) for the full 2020 season based on player performance over the first ~25 games._

__1. Data__

Data was scraped from the always amazing Baseball Reference:
https://www.baseball-reference.com/register/league.cgi?id=17edbc3b

__2. Data Wrangling/Cleaning__

[Data Wrangling Notebook](https://github.com/abewoycke/KBO-Projections/blob/master/2-Data%20Wrangling/KBO%20Projections%20Data%20Wrangling.ipynb)

I had to deal with a varitety of data quality issues. Missing values were either dropped or filled with iterative imputer. I coerced some data types. Batting stance was indicated by a special character in the Player Name column, so that had to be extracted.

__3. EDA__

[EDA Notebook](https://github.com/abewoycke/KBO-Projections/blob/master/3-EDA/KBO%20Projections%20EDA.ipynb)

I looked for expected or unexpected relationships in the data with a correlation matrix heatmap. Most of the correlations with our response variables were things a baseball fan might suspect, although the exact numerical values of those correlations would be hard to estimate without taking a deeper look at the data.

![SO_rate_vs_BA](https://github.com/abewoycke/KBO-Projections/blob/master/3-EDA/SO_Rate_BA.png)
![Doubles_vs_RBI](https://github.com/abewoycke/KBO-Projections/blob/master/3-EDA/2B_Rate_RBI.png)

__4. Modeling and Tuning__

[Modeling Notebook](https://github.com/abewoycke/KBO-Projections/blob/master/5-Modeling/KBO%20Projections%20Modeling.ipynb)

I used some human judgement to reduce multicollinearity in preprocessing (our model doesn't need to count all three of OPS, OBP, and SLG), and then tried a variety of regressors.

_Ridge Regression_ ultimately performed the best for each of the three targeted response variables. This made sense as a top contender, because despite my best efforts, multicollinearity was ultimately going to be a major part of the dataset. And it deals with that fairly well.

From there, I tuned each independent model based on each of the response variables, to end up with one separate model for each.

__5. Model Predictions__

[Documentation Notebook](https://github.com/abewoycke/KBO-Projections/blob/master/6-Documentation/KBO%20Projections%20Documentation.ipynb)

The model performed fairly well. Its predicted top five performers outperformed naive predictions (assuming 2019's players would maintain their rankings) by 42%. The top performing player at the end of the season had been predicted at #2.

![Projected_vs_Actual_BA](https://github.com/abewoycke/KBO-Projections/blob/master/6-Documentation/2020_BA_Residuals_Candidate_Pool.png)

![Projected_vs_Actual_HR](https://github.com/abewoycke/KBO-Projections/blob/master/6-Documentation/2020_HR_Residuals_Candidate_Pool.png)

![Projected_vs_Actual_RBI](https://github.com/abewoycke/KBO-Projections/blob/master/6-Documentation/2020_RBI_Residuals_Candidate_Pool.png)

__6. Future Improvements__

I would love to work with more detailed data if it's available somewhere. At bat or individual game-by-game statistics would make for a more powerful forecaster. A forecast that took into account a player's performance from past seasons would also improve the forecast's accuracy. Forecasting pitcher performance and/or using pitcher data to inform hitter projections would additionally add value to this project. Ultimately, a forecast that predicted things on a smaller scale would be of more value. Game-by-game forecasts, individual at-bats, or even pitch-by-pitch forecasts could be a possibility with more detailed source data.

__7. Project Writeup:__
[Project Writeup](https://github.com/abewoycke/KBO-Projections/blob/master/6-Documentation/Final%20Project%20Deliverables/KBO%20Projections%20Final%20Project%20Report.pdf)

__8. Credits__

Scikit-learn: Machine Learning in Python, Pedregosa et al., JMLR 12, pp. 2825-2830, 2011.
