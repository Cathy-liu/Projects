# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NPL on Intermittent Fasting and Keto Diet


## Problem Statement

We are part of the nutritional/weight loss company helping stakeholder to identify which are the current trend to promote weight loss strategy. Therefore, the purpose of our study include:
1.	Using Pushshift's API to collect posts from subreddits of intermittent fasting and keto diet.
2.	We'll then use NLP to train a classifier on which subreddit a given post came from.

## Background

Weight loss is nowadays trend, not only benefit in maintaining good body figure but also associate with health advantages. Intermittent fasting and the keto diet are both popular weight loss options that boast plenty of success stories. Some people have seen fantastic results with keto, while others advocate intermittent fasting. 

The keto diet is a high-protein, low-carbohydrate, and fat-rich diet that can be too restrictive for some people. Intermittent fasting is an eating pattern that involves alternating periods of not eating with periods of regular food consumption.

When it comes to intermittent fasting vs keto for weight loss, both prove effective. However, the differences come into play with the long-term effects of pounds lost, and the health advantages that are associated. 

[Check here to read Review Article on Advantages and Disadvantages of the Ketogenic Diet.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7480775/)

[Check here for the study on Intermittent Fasting and Metabolic Health.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8839325/)

## Contents

Part 1: 
- Importing Libraries & Reddit Scrapping

Part 2:
- Loading the data set & Exploratory Data Analysis(EDA)
- EDA before Text pre-processing
- Text pre-processing
- EDA after Text pre-processing
- Sentiment Analysis
- Export Dataset for Modeling

Part 3: 
- Baseline Model
- Modelling
- Evaluation and Conceptual Understanding
- Conclusion and Recommendations

---
# Part 1: Importing Libraries & Reddit Scrapping

We managed to extract total of 10290 posts which consist of 5602 posts from keto subreddit and 4688 posts from intermittent fasting subreddit. Out of 80 columns, we export 4 columns -- 'title','selftext','subreddit','created_utc' for our further EDA and text processing in Part 2.

---
# Part 2

## EDA
- Class distribution: There are more intermittent fasting posts with class 0 than keto diet posts with class 1. We can say that the dataset is relatively balanced with 46% of intermittent fasting posts and 56% of keto diet posts. Since the data is balanced, we won’t be applying data-balancing techniques like SMOTE while building the model
- Missing values: There are no missing values in the selftext column.
- Number of words in subreddit: The average number of words in intermittent fasting is 118 as compared to an average of 132 words in a keto reddit.
- Number of characters in subreddit: The average number of character length in intermittent fasting is 626 as compared to an average of 721 characters in a keto subreddit. 
- Both subreddits have quite similar word count and charater length.

## Text EDA Before Pre-processing
Before text pre-processing, we realised that our top 15 words contain words such as 'www reddit', 'reddit com', 'https www', com keto', 'amp 200b', 've' and etc. Those words do not help us in term on understanding the content of the posts and also for model to learn the key information. Therefore, before we move to model building, we need to preprocess our text. 

## Text Pre-processing
We preprocess our text dataset by removing punctuations & special characters, cleaning texts, removing stop words, and applying lemmatization/stemming.

## Text EDA After Pre-processing
After lemmatizating, the top keyword that we get for class 0 (intermittent fasting) are 'day' and 'fast', while we get the most keyword of 'keto' and 'weight loss' for class 1 (keto diet). 

After stemming, the top keyword that we get for class 0 (intermittent fasting) are 'fast' and 'intermittent fast', while we get most keyword of 'keto' and 'start keto' for class 1 (keto diet). 

In the analysis, we extract post that consist of word of 'keto' and 'intermittent fast' as these keywords appear as the most frequent after lemmatizing and stemming. 

My impression after reading fews posts that contain words of 'keto' and 'interminttent fast' are many posters are actually on reddit to seek for advices or suggestions to help on their process on interminttent fasting of keto. Few people share their sucess and health improvement during the process while some other people actually face health issue during the process of weight loss. 

## Sentiment Analysis
In sentiment analysis, we select text after lemmatization for analysis as lemmatization reduce the similar words into its base word which have meaning.

Generally, the sentiment in the comments are positive, which possess 75.1% from the whole data we collected. There are 22.1% are negative comments and only 2.8% are neutral comments.

## Export Dataset for Modeling
Lemmatization and stemming did not make much differences in the top occurring unigram and bigrams. Stemming tend to return some words that do not convey much meaning while lemmatizing is usually the more correct and precise way of handling things from a grammatical point of view.  In the industry, generally, stemming is preferred over lemmatization because of the benefit of streamlining number of columns for our downstream modeling task. Therefore, we will remain 'cleantext_stem' for our downsream modeling process.

---

# Part 3

## Baseline Model
Given that we have quite balanced data between both classes, our baseline model accuracy is the probability from our majority subreddit -- Keto diet. Our baseline accuracy is 54.4%. Hopefully we can models that score better than this score during our modeling.

## Modeling
We instantiated 6 classification models -- Logistic Regression, KNeighbors Classifier, Multinomial NB, Random Forest Classifier, AdaBoost Classifier and Gradient Boosting Classifier by using TF-IDF Vectorizer and Count Vectorizer. Total there were 12 models being fit.

### Feature Importance
Feature Importance is a score assigned to the features of a Machine Learning model that defines how “important” is a feature to the model’s prediction. By applying our best model -- Random Forest Classifier model with TF-IDF Vectorizer, we got the feature importance of 'keto' as the most important features and followed by 'fast' as the second most important feature.

## Evaluation and Conceptual Understanding

Overall our models performed quite well. As compared to the baseline model, our model are outperformed. Our train and test scores for each model are very similar, indicating that our models are not overfit. The accuracy overall are quite high for basic model evaluation except KNN model with Count Vectorizer where the accurancy score is only 62%.

Generally, TF-IDF transformation works better than Count Vectorizer in model fitting. In Count Vectorizer we only count the number of times a word appears in the document which results in biasing in favour of most frequent words. this ends up in ignoring rare words which could have helped is in processing our data more efficiently. However, in TF-IDF Vectorizer we consider overall document weightage of a word. It helps us in dealing with most frequent words. Using it we can penalize them. TfidfVectorizer weights the word counts by a measure of how often they appear in the documents.

From the dataframe above, we can see that the Random Forest model tops the other models in 4 of the 6 metrics we evaluate, except precision and specificity. A score greater than 90% suggests that the model is highly accurate when predicting subreddit. Confusion Matrix from Random Forest shows that there are total 225 false subreddits when running through our test model.

As our problem statement do not focus on capturing either positive predictions or negative predicitions, we should use F1 metric to eveluate our model in this case. Simply stated the F1 score sort of maintains a balance between the precision and recall for your classifier. If our precision is low, the F1 is low and if the recall is low again our F1 score is low ([Reference](https://towardsdatascience.com/the-5-classification-evaluation-metrics-you-must-know-aa97784ff226)). By taking F1 metric from our Random Forest model, the interpretation of this value is that on a scale from 0 (worst) to 1 (best), the model’s ability to both capture positive cases and be accurate with the cases it does capture is 0.92, which is very good value.

## Conclusion and Recommendations
In conclusion, Random Forest is the most accurate model tested, sporting about an 91% accuracy. Susequent models that we can use for the subreddits classification are Logistic Regeression and Gradient Boosting Classifier. Furtherore, TF-IDF transformation works better than Count Vectorizer in model fitting.

From our EDA, majority of the subrredits are about 'Keto Diet'. This could indicate that more people are actually interested on keto way. Besides that, we also found that many people are actually on the reddits to seek advices or suggestions to help on their process on interminttent fasting of keto. By refering to scietific article, we realised that both intermittent fasting and keto diet have its advantages and disadvantages. Also, from Dr Anson's article, his advice is to experiment with the dietary plans and see if one works best for you ([Reference](https://drstephenanton.com/keto-vs-intermittent-fasting/)). Therefore, instead of advocating particular way of diet, we could provide professional consultation service toward people who need help throughout their weightloss/health improvement journey via either intermittent fasting or keto diet.

Besides that, sentiment analysis allow us to understand that majority of the posts are positive comments, which possess 75.1%. 

Last but not least, by moving forward with this project, I could do far more exploration with setting different model parameters to check for the improvement. I'd recommend adding more features to the API and to models to strengthen accuracy as well as potential for modeling. Furthermore, I'd explore data drift prevention as surredits post can be updated very soon. It might cause model performance degradation when we use current model to apply on updated posts.

