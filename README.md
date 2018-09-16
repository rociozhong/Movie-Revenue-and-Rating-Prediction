# Movie-Revenue-and-Rating-Prediction

For this project, I use the tmbd movie dataset from Kaggle and mainly use the **"tmdb_5000_movies.csv"** (https://www.kaggle.com/tmdb/tmdb-movie-metadata). The goal is to predict two variables **revenue** (a regression problem) and whether the **vote_average** is greater than 7 (a classification problem). And they are not used as one of the covariates to predict each other. I use all odd **id** as training data and even **id** as testing data. Any information after the release date is not allowed to use, for example, **popularity** and **vote_count**.

The original movie data set has 4801 observations and 21 variables including budget, genres, homepage, movie id, keywords, language, title, overview, popularity, production company, production country, release date, revenue, runtime, status, vote average and vote count.

In order to predict movie’s revenue and vote average, I first clean the data set:

1. First, because not all variables can be used in modeling, I delete the irrelevant variables including popularity, vote count, keywords, homepage, title and tagline. 

2. Second, for purposes of modeling, I apply nature log function on budget and revenue, and delete the corresponding “inf” observations.

3. Third, for several variables like “genres” which is json type, I extract the key words in genres and create additional variables. Specifically, for example, the variable “genres” includes 21 types such as action, adventure and so on. Thus I create addtional 21 genre variables, such as temp_genre_action, temp_genre_adventure. Then I assign 1 to the subject if its original “genres” variable includes that type, otherwise, I assign 0 to it. The same method apply to the “production_countries”, “production company” and “spoken languages”. 

4. Fourth, I convert the release date variable into 3 variables including year, month and date. Then I base upon these information, I create an additional variable “holiday” to represent whether the movie is released during holiday season (especially Thanksgiving during Nov 22-28 and Chrismas during Dec 18-31 ) or summer season (from May to August). If the movie is released during these holiday season, it is assigned to be 1, otherwise 0. 

5. Fifth, I use the extracted production company information, and create a variable named “large_prod”. I use additional information from website and find out the first top 10 production companies which are more likely to produce good movies. Thus the “large_prod” will be 1 if the movie is produced by these top 10 companies, otherwise 0. 

6. Finally, using “original language” and “spoken language”, I create “lang” variable which is 1 if the movie uses English and 0 otherwise. Similarly, a “us” variable is created to check whether the movie is produced in US or not.

I divide the data set into train data and test data. I use all odd id as training data and even id as testing data. Thus, the train data has 1647 observations and test data has 1582 observations.

## Revenue prediction
In order to predict movie revenue, I use linear regression and apply AIC to select variables. According to the “step” function with “both” direction, there are 15 important varibales contributing to the revenue prediction: budget, runtime, genre_action, genre_adventure, genre_comedy, genre_crime, genre_drama, genre_history, genre_thriller, genre_western, large_prod and holiday. And the corresponding prediction MSE is 1.578468.

## Vote average prediction
To classify the vote average, I first categorize the dependent variable as 1 if the vote average is larger than 7, and 0 for the rest. For this classification question, I adopt random forest method. First, I use 5-fold cross-validation to tuning "mtry" variable from 1 to 15. Based on the cross-validation error, I set mtry as 3. The most important variables are runtime, release date, budget, holiday, large production company, whether the language is English, and whether the movies are drama, comedy, thriller or action. Applying the model on the test data, I have the  prediction error rate as 0.1807838, and accuracy rate as 0.8128951.

## Revenue and rating prediction for the movie "Star Wars: The Last Jed"
From the IMDB website, I find the relevent information about the movie "Star Wars: The Last Jed", such as runtime, genres, production company, release date and language. Since there is no information about the movie budget, we use an estimated budget. Becuase the last "star wars" movies budget is about 245 million us dollars, then we use 300 million us dollars as the new one's budget. Therefore, using linear model mentioned above, we have the predicted revenue is about 615,294,502, and the vote average is large than 7. 
