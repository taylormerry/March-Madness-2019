# Predicting Win Probabilities for March Madness Games

I entered this project in a Kaggle Competition found here https://www.kaggle.com/c/mens-machine-learning-competition-2019.

## File Directory

### DataFiles

Data provided by Kaggle for training. Contains data for the 2002-2018 seasons. These files include data on cities, conferences, conference tournament games, NCAA tournament games, NCAA tournament seeds and slots, regular season games, seasons, secondary tournament games, coaches, and teams.

### Stage2DataFiles

Data provided by Kaggle for predicitons. Contains data for the 2002-2018 seasons as well as for the 2019 season. Contains the same files as the original DataFiles folder but also includes 2019 data.

### mydata

This is the data I collected from the web or produced in my notebooks. 

The files collected from the web are free and publicly available efficiency ratings. The files with the prefix "colley" are from http://www.colleyrankings.com/. The files with the prefix "teamrank" are from https://www.teamrankings.com/ncb/. The files with the prefix "trank" are from http://www.barttorvik.com/#. The files with the prefix "summary" are from https://kenpom.com/. 

ranking_data.csv was created in TeamDataCleaning.ipynb. It is a dataset of each team in the 2008 and 2010-2018 seasons (Colley Rankings did not have their 2009 data publicly available) with their efficiency ratings scaled on a 0 to 1 scale. This data was used to create a weighted efficiency rating based on prior tournament results. teamsheets.csv was also created in TeamDataCleaning. It is a dataset of effeciency ratings and season stats for each team in seasons 2008 and 2010-2018. matchups.csv was created in MatchupFeatureEngineering.ipynb. It is a dataset to be used for making predictions. It contains data for every game in NCAA tournaments in the 2008 and 2010-2018 seasons.
