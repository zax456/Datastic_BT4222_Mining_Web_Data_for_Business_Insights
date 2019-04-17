# BT4222 Datastic Group Project
<br>This project is meant for the module BT4222 Mining Web Data for Business Insights of National University of Singapore. Movie data provided by [MovieLens](https://grouplens.org/datasets/movielens/) is used. The aim of this project is to discover the characteristics of certain category of audience and create a movie recommender model.<br>

## Movie recommender System
Group Members: 
 * Ang Kian Hwee (A0150445M)
 * Lee Ying Yang (A0170208N)
 * Zhai Chen (A0156995H)
 * Tang Wen Qian (A0161814J)

## to-do notice
* random seed for community generation
* missing plots in EDA

# Instructions to run the various python notebooks
### <ins>1. EDA</ins>
__Setup__
1. pip install the following packages: 
	1. afinn
	2. textblob
	3. colour (for bar chart's bar colour)
	4. prettytable
	5. nltk
2. Download all nltk corpus using nltk.download("popular")
3. Ignore mounting of Google Drive step and changing of path
4. Set file paths for users.csv and user_ratings.csv

__Movie Metadata Cleaning__
<br><br>__This step was ran before hand. Do not run this section as genome-scores.csv is not uploaded due to file size limit on GitHub.__
1. Set file paths for the following files: 
	1. movie_data_merged_v1.csv
	2. genome-scores.csv
	3. genome_tags.csv
2. Delete rubbish column 'Unnamed: 0' after reading in movie_data_merged_v1.csv 
3. Merge both genome tags and genome scores dataframe and keep tags that have a relevance score of 70% and above
4. Merge master_movies_df with the filtered tags from step 3
4. Run Text Cleaning on genres, Casts and Director columns in master_movies_df 
5. Join the first names and last names of both Casts and Director respectively using join_name function

__Datasets Overview & Merging__
1. Run this section of codes to get basic statistics of the Movie, User and Rating dataframes
2. This section is needed to initialise our master_data dataframe which is used for analysis later on 

__Exploratory Data Analysis on the population__ 
1. This section consist of many sub sections that helps to find insights to our problem statement
2. Running these sub sections is straight forward and the user should not meet into problems unless the required variables are not initialised 

### <ins>2. Community Detection</ins>
__Setup__
1. pip install the following packages: 
	1. afinn
	2. textblob
	3. colour (for bar chart's bar colour)
	4. prettytable
	5. community
	6. networkx
2. Ignore mounting of Google Drive step and changing of path
3. Set file paths for the following files: 
	1. users.csv
	2. movie_data_merged_v2.csv 
	3. user_ratings.csv
4. Run Read in Datasets block of code 

__Network Building__
1. Run code blocks 1 to 4 to add the nodes and edges to network 
2. Run ForceAtlas2 algorithm. This might take quite a long to do. 
3. Run the remaining code blocks under Build Network section
4. Run code blocks under Centralities Measures to get various statistics about the network

__Community Formation__
1. First, split the network into clusters using community package (.best_partition) under Community Detection section 
2. Draw out the network with the communities formed using colour coding 
3. Save the community list of users into a json file for usage in Community Study notebook

### <ins>3. Communities Study</ins>
__Setup__
1. pip install the following packages: 
	1. afinn
	2. textblob
	3. colour (for bar chart's bar colour)
	4. prettytable
	5. nltk
2. Download all nltk corpus using nltk.download("popular")
3. Ignore mounting of Google Drive step and changing of path
4. Set file paths for the following files:
	1. users.csv 
	2. movie_data_merged_v2.csv
	3. user_ratings.csv
	4. community_list.json
5. Run Read in Datasets block of code 
6. Run all pre-defined functions and variables to be used for analysis later on
7. A few key functions/variables to take note of:
	1. __plot_ratings_genres_dist__ - plot the distribution of genres for each rating score 
	2. __plot_user_distribution__ - plot the distribution of predictor variable 
	3. __plot_genre_dist_over_var__ - plot distribution of genres over each category of a predictor variable 
	4. __plot_rating_dist_over_var__ - plot distribution of ratings over each category of a predictor variable
	5. __com_movie_var__ - returns a list of genres which the audience has watched
	6. __get_user_rating__ - returns dataframe consisting of user-movieIds who have given a particular rating score 
	7. __com_giant_tags_5stars/com_giant_tags_1stars__ - lists of 4 strings consisting of concatenated genome tags for movies with either rating-5 or rating-1
	8. __get_keywords_community2_tags__ - prints the top 10 tags which has the highest TF-IDF values in that community. These are tags that defines a particular movie given a particular rating.
	9. __get_tfidf_string__ - returns a dataframe of words with their TF-IDF values. Used to plot word clouds. 
	10. __comX_users_movies__ - dataframe consisting of user-movieIds belonging in community X, where X is 1 to 4

__Community Analysis__
1. Run the codes for the different types of study:
	1. Distribution Study 
	2. Sentiment analysis on Genome Tags
	3. Tags Study
	4. Movie Metadata Study (Casts & Director)
2. Each Study section should run without problems provided all pre-defined functions and variables have been initialised 

### <ins>4. Predictive_Modelling</ins>
__Setup__
1. Set file paths for users.dat, movie_data_merged_v2.csv and training_ratings_for_kaggle_comp.csv
2. Run the data merging, rating bucketization, and train validation test split.
3. Run each of the data preprocessing steps that will also fit each of the data transformers
<br>and transforms training data
4. data_pipe function then combines all preprocessing steps and transformers into a function.
<br>Then applied to test and validation datasets

__Modelling__
1. Naive Bayes and logistic regression do not take much training time. <br>
2. However, XGboost does take some time, and therefore not reccomended to rerun.<br>
3. Right after training XGboost, there is a section to save and reload the model.<br>
Depending on whether directly running after training, or loading from a pre-saved model, uncomment and run the corresponding code blocks for each option only.<br>
__Reccomended to use the loaded model from here on instead of rerunning XGBoost__<br>
4. All diagnosing steps should then be possible provided data has been already processed, and model is loaded.<br>
5. Gridsearch logs are at the bottom of notebook, due to it's length. Re-running not recommended.

### <ins>5. Collaborative Filtering</ins>
1. Load data and run the merging similar to predictive modelling
2. Split train validation test, and convert each into model required by surprise package
   * Package used is [surprise](http://surpriselib.com/)
3. The function diagnose_reccomendation is used to check accuracy and F1-score of each model trained.<br>
make sure to load it before proceeding.
4. Each of the modelling steps can be ran without any issues.
   * __SVD++ takes extremely long to run, not reccomended to do so__
   * SVD-tuned does take around a few minutes to run.
   * The rest of the modelling runs relatively quickly.
5. Model saved at the end, using the package's dump module.
   * Trained models can also be loaded from there.
