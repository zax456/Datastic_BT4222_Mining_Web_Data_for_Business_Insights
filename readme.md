# BT4222 Datastic Group Project
## Movie recommender System
Group Members: 
 * Ang Kian Hwee (A0150445M)
 * Lee Ying Yang (A0170208N)
 * Zhai Chen (A0156995H)
 * Tang Wen Qian (A0161814J)

## to-do notice
* add code instructions
* store genome_score download somewhere else, as it is too large for GH
* random seed for community generation
* missing plots in EDA

# Insert code instructions here
### EDA


### Community Detection


### Predictive_Modelling
__Processing Data__
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

### Collaborative Filtering
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
