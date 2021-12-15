# Predicting Win Probabilities for March Madness Games

I entered this project in a Kaggle Competition found here https://www.kaggle.com/c/mens-machine-learning-competition-2019. My submission ended up finishing in 78th place out of 866 submissions with a log loss of 0.45876.

## File Directory

### DataFiles

Data provided by Kaggle for training. Contains data for the 2002-2018 seasons. These files include data on cities, conferences, conference tournament games, NCAA tournament games, NCAA tournament seeds and slots, regular season games, seasons, secondary tournament games, coaches, and teams.

### Stage2DataFiles

Data provided by Kaggle for predicitons. Contains data for the 2002-2018 seasons as well as for the 2019 season. Contains the same files as the original DataFiles folder but also includes 2019 data.

### mydata

This is the data I collected from the web or produced in my notebooks. 

The files collected from the web are free and publicly available efficiency ratings. The files with the prefix "colley" are from http://www.colleyrankings.com/. The files with the prefix "teamrank" are from https://www.teamrankings.com/ncb/. The files with the prefix "trank" are from http://www.barttorvik.com/#. The files with the prefix "summary" are from https://kenpom.com/. 

ranking_data.csv was created in TeamDataCleaning.ipynb. It is a dataset of each team in the 2008 and 2010-2018 seasons (Colley Rankings did not have their 2009 data publicly available) with their efficiency ratings scaled on a 0 to 1 scale. This data was used to create a weighted efficiency rating based on prior tournament results. teamsheets.csv was also created in TeamDataCleaning. It is a dataset of effeciency ratings and season stats for each team in seasons 2008 and 2010-2018. matchups.csv was created in MatchupFeatureEngineering.ipynb. It is a dataset to be used for making predictions. It contains data for every game in NCAA tournaments in the 2008 and 2010-2018 seasons.

### ML.ipynb

Uses the sklearn framework's implementation of Logistic Regression, Random Forest, and K Nearest Neigbors algorithms to find the best model to predict NCAA tournament games through cross validation. Logistic Regression with L1 regularization, Logistic Regression with L2 regularization, and Random Forest had the lowest average log loss in cross validation, but only Logistic Regression with L1 regularization and Logistic Regression with L2 regularization had the lowest log loss on the testing set. Therefore, I decided to use the average predicted probabilities of the two Logistic Regression models for my submissions.

### MatchupFeatureEngineering.ipynb

Uses the teamsheets.csv to create features for each tournament matchup to be used for predictions. The predictor variables were created by using each team's data, the difference between each team's data, the absolute value of each team's data, and/or the average of each team's data for each team statistic.

### Predictions.ipynb

Uses code from TeamDataCleaning.ipynb to create the teamsheets data for 2019. Uses code from RatingLinearRegression.ipynb to create the weighted ratings for 2019 teams. Uses code from MatchupFeatureEngineering.ipynb to create the matchup data to be used for predictions. Uses code from ML.ipynb to predict win probabilities for each possible game in the 2019 NCAA tournament using Logistic Regression with L1 regularization and Logistic Regression with L2 regularization and averaging their predictions. Then creates submission1.csv and submission2.csv to be submitted for the Kaggle competition.

### RatingLinearRegression.ipynb

Creates a weighted efficiency rating for each team in each season. Uses ridge regression to determine the weights because  all of the rating metrics should be included and not left out by using forward selection or LASSO regression. The response variable will be the score differential of NCAA tournament games. The X variables will be the difference of each rating metric scaled from 0 to 1 for each year between the two teams. The ratings were scaled in order for interpretability, it is now easy to see which rating system is more important in predicting the score differential of NCAA tournament games. The weighted ratings should be interpreted by the following rule: the difference in the weighted rating of team 1 versus team 2 is the predicted score differential.

### TeamDataCleaning.ipynb

Creates teamsheets.csv, a file for team stats in each season. Cleans the data from multiple sources using pandas and regular expressions.

### submission1.csv

My predicted win probabilities for each game. Kaggle allows two submissions for this competition, so one of the best ways to achieve a lower log loss is to submit your same predictions twice, but give one team a full 100% chance of winning in one submission and their opponent a full 100% of winning in the other submission. To pick this game, it is optimal to choose a first round game with both teams having around a .5 probability of winning because you are guaranteed that the first round game will occur and turning .5 into 1 decreases log loss more than turning a probability greater than .5 to 1. Therefore, I chose this game to be Oklahoma vs Mississippi. submission1.csv gives Mississippi a probability of beating Oklahoma of 1.

### submission2.csv

My predicted probabilities for each game with Oklahoma given a probability of beating Mississippi of 1.

## Viewing This Project

The order in which you should run the python files is:

1) TeamDataCleaning.ipynb up until needing the weights for the team weighted efficiency rating
2) RatingLinearRegression.ipynb
3) The rest of TeamDataCleaning.ipynb
4) MatchupFeatureEngineering.ipynb
5) ML.ipynb
6) Predictions.ipynb

## Results

My submission2.csv (Oklahoma beat Mississippi) achieved a log loss of 0.45876, which placed me 78th out of 866. The 1st place submission achieved a log loss of 0.41477 and 5th place achieved a log loss of 0.43148.

## Future Improvements

- Find some predictors on consistency, i.e. variance in team stats such as rebounding differential, turnover differential, FT%, eFG%
- Find other efficiency metrics that have pre-tournament data
- Do more feature engineering
- Refit a Logistic Regression model with L2 penalty after using L1 dimension reduction cross validating for best combination of features
