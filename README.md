# Movie-Revenue-and-Rating-Prediction

For this project, I use the tmbd movie dataset from Kaggle and mainly use the **"tmdb_5000_movies.csv"** (https://www.kaggle.com/tmdb/tmdb-movie-metadata). The goal is to predict two variables **revenue** (a regression problem) and whether the **vote_average** is greater than 7 (a classification problem). And they are not used as one of the covariates to predict each other.

I use all odd **id** as training data and even **id** as testing data. Any information after the release date is not allowed to use, for example, **popularity** and **vote_count**.

