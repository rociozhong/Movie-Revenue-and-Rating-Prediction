# Movie-Revenue-and-Rating-Prediction

For this project, I use the tmbd movie dataset from Kaggle and mainly use the **"tmdb_5000_movies.csv"** (https://www.kaggle.com/tmdb/tmdb-movie-metadata). The goal is to predict two variables **revenue** (a regression problem) and whether the **vote_average** is greater than 7 (a classification problem). And they are not used as one of the covariates to predict each other. I use all odd **id** as training data and even **id** as testing data. Any information after the release date is not allowed to use, for example, **popularity** and **vote_count**.

The original movie data set has 4801 observations and 21 variables including budget, genres, homepage, movie id, keywords, language, title, overview, popularity, production company, production country, release date, revenue, runtime, status, vote average and vote count.

In order to predict movie’s revenue and vote average, we first clean the data set:

1. First, because not all variables can be used in modeling, we delete the irrelevant variables including popularity, vote count, keywords, homepage, title and tagline. 

2. Second, for purposes of modeling, we apply nature log function on budget and revenue, and delete the corresponding “inf” observations.

3. Third, for several variables like “genres” which is json type, we extract the key words in genres and create additional variables. Specifically, for example, the variable “genres” includes 21 types such as action, adventure and so on. Thus we create addtional 21 genre variables, such as temp_genre_action, temp_genre_adventure. Then we assign 1 to the subject if its original “genres” variable includes that type, otherwise, we assign 0 to it. The same method apply to the “production_countries”, “production company” and “spoken languages”. 

4. Fourth, we convert the release date variable into 3 variables including year, month and date. Then we base upon these information, we create an additional variable “holiday” to represent whether the movie is released during holiday season (especially Thanksgiving during Nov 22 - 28 and Chrismas during Dec 18 -31 ) or summer season (from May to August). If the movie is released during these holiday season, it is assigned to be 1, otherwise 0. 

5. Fifth, we use the extracted production company information, and create a variable named “large_prod”. We use additional information from website and find out the first top 10 production companies which are more likely to produce good movies. Thus the “large_prod” will be 1 if the movie is produced by these top 10 companies, otherwise 0. 

6.Finally, using “original language” and “spoken language”, we create “lang” variable which is 1 if the movie uses English and 0 otherwise. Similarly, a “us” variable is created to check whether the movie is produced in US or not.
