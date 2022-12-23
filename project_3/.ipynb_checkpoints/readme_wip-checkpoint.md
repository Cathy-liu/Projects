# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

## 01 Problem Statement





## 02 Data Collection





## 03 Data Cleaning & EDA

before removing posts
![](image/stats_summary.PNG)

![](image/word_count.PNG)

![](image/remove_extreme_word_count.PNG)

![](image/distribution_word_count.PNG)

![](image/top_15_uni_stock.PNG)

![](image/top_15_unig_wsb.PNG)

![](image/stock_big.PNG)

![](image/wsb_bi.PNG)



## 04 Preprocessing & Modeling

![](image/confusion_matrix_production_model.PNG)

![](image/AUC_production_model.PNG)



## 05 Evaluation and Conceptual Understanding

|   |               Model                    | Training F1 | Testing F1 | Training Accuracy | Testing Accuracy | Precision | Recall | Specificity|  AUC  |
|:-:|:--------------------------------------:|:-----------:|:----------:|:-----------------:|:----------------:|:---------:|:------:|:----------:|:-----:|
| 0 | Baseline (null model)                  |     0.946   |    0.946   |       0.898       |      0.898       |   0.898   | 1.000  |    0       | 0.50  |
| 1 | TF-IDF + Multinomial NB                |     0.948   |    0.946   |       0.901       |      0.898       |   0.898   | 1.000  |    0.005   | 0.70  |
| 2 | TF-IDF + Random Forest                 |     0.997   |    0.952   |       0.994       |      0.910       |   0.914   | 0.993  |    0.177   | 0.75  |
| 3 | TF-IDF + LinearSVC                     |     0.974   |    0.952   |       0.953       |      0.911       |   0.913   | 0.995  |    0.167   | 0.76  |
| 4 | TF-IDF + VotingClassifier              |     0.961   |    0.951   |       0.926       |      0.909       |   0.915   | 0.990  |    0.191   |  -    |
| 5 | TF-IDF + Multinomial NB (oversample)   |     0.989   |    0.970   |       0.989       |      0.971       |   0.995   | 0.946  |    0.995   | 1.00  |
| 6 | TF-IDF + Random Forest (oversample)    |     0.989   |    0.971   |       0.989       |      0.972       |   0.995   | 0.948  |    0.995   | 1.00  |

Evluation of the model performance: 

As shown in the table above, performance of model 0-4 are characteristic of an imbalanced dataset. Due to the high imbalance (0.9/0.1 ratio), even the null baseline model of predicting everything as the majority class has high F1 score and accuracy as the majority class correct predition rate has overwhelmed the false prediction rates on the minority class. This effect has dominated the metrics of F1, accuracy, precision and recall, hence for these four metrics, Model 1-4 do not provide much room of improvement from the baseline score. However, there is one metric Specificity that is telling of the poor performance on the minority class, which means the models are not good at correctly identifying the negatively labelled - which in this case is the minority class.

Model 2-4 have all incorpurated class_weight='balanced' in their argument inputs to give more penalty to the false preditions on the minority class. The metric Specificity dSpecificity here means the model's ability to correctly identify samples that are denoted as negative (represents r/stock subreddit).es significantly improve from the baseline score and also the NB model (which does not cater for specifying the class_weight parameter) to 0.191 in the case of Model 4, this says that Model 2-4 have a better capability to correctly identify samples that are in the negative labelled class (i.e. belong to r/stock subreddit posts).

In Model 5-6, the dataset have been treated with oversampling of the minority class so that the processed dataset is balanced. The oversampling is done through sampling on the original minority class dataset with replacement. It can be seen that metrics have greatly improved on the metric Specificity to a really high score of 0.995, and there is improvement on the overall performance shown in the other metrics too.

As there are such dramatic improvement in performance in Model 5 and 6, oversampling will be incorporated in the production model. While the Random Forest model outperforms the Multinomical NB model just by a slight amount in its higher Recall scoring, for the benefit of interpretability, we will choose the multinomial NB as the production model.


![](image/interpretation.PNG)

Interpretation of the output of the production model (TF-IDF+Multinomial with oversampling treatment):

1. On the X-axis are the top 15 features from both r/stock and r/wallstreetbet. As there are 7 overlaping features, in total there are 23 features in the plot.

2. The blue bars represents each word's probability of occurance in a Class 0 (r/stock) post; whereas the yellow bars represents each word's probability of occurance in a Class 1 (r/wallstreetbet) post. The y values of the bar plots are on the right side. Based on the Naive Bayes assumption, we can effectively interprete the blue bars as the probabilitistic contribution of the presence of a particular word in a text document to the probabilitity of that document belonging to Class 0 (stock); and likewise, the yellow bars represent the probabilitstic contribution of the presence of a particular word in a text document to the probability of that document belonging to Class 1 (wallstreetbet).

3. The blue line represents the ratio between the two probabilities of occurance in Class 0 (r/stock) post versus in Class 1 (r/wallstreetbet) post for a particular word. The y values of the line plot is on the left side. The blue line gives a good indication of a word's relative contribution to classifying documents with the word to r/stock versus to r/wallstreetbet.

4. The words on the X-axis are sorted in decending order in the ratio of the two probabilities as defined in (3). Hence the more towards the left, presence of the words are more biased to contributing to classifying documents with them as r/stock, whereas the more towards the right, presence of these words are more biased to contributing to classifying documents with them as r/wallstreetbet.

5. The dashed horizontal red line denotes y=1, and its intersection with the blue line defined in (3) have seperated the words on the X-axis to two groups: presence of those of the left side have a higher contribution to classifying to r/stock rather than r/wallstreetbet subreddit; presence of those words to the right hand side have a higher contribution classifying into r/wallstreetbet.

6. If we want to identify the top words that distinguish a document as a 'r/stock' post, then we should take from the left hand side, the most prominent five being 'analysis', 'free', 'stock', 'fund' and 'trading'.

7. Likewise, if we want to identify the top words that distinguish a document as a 'r/wallstreetbet' post, we should take from the right hand side, the most prominent five being 'yolo', 'week', 'going', 'call' and 'year'.

8. It can be seen from the bar charts that there are some common top occurance words that have similar probablistic contribution to both classes, such as 'good', 'make' and 'moon'. If there is future analysis on top of this work, these words can be added to the stop_word list, as they do not help much to distinguish between the two classes.



## 06 Conclusion and Recommendations






#### About the API

Pushshift's API is fairly straightforward. For example, if I want the posts from [`/r/boardgames`](https://www.reddit.com/r/boardgames), all I have to do is use the following url: https://api.pushshift.io/reddit/search/submission?subreddit=boardgames

To help you get started, we have a primer video on how to use the API: https://youtu.be/AcrjEWsMi_E

**NOTE:** Pushshift now limits you to 100 posts per request (no longer the 500 in the screencast).

---

### Requirements

- Gather and prepare your data using the `requests` library.
- **Create and compare two models**. One of these must be a Random Forest classifier, however the other can be a classifier of your choosing: logistic regression, KNN, SVM, etc.
- A Jupyter Notebook with your analysis for a peer audience of data scientists.
- An executive summary of your results.
- A short presentation outlining your process and findings for a semi-technical audience.

**Pro Tip:** You can find a good example executive summary [here](https://www.proposify.biz/blog/executive-summary).

---

### Necessary Deliverables / Submission

- Code must be in at least one clearly commented Jupyter Notebook.
- A readme/executive summary in markdown.
- You must submit your slide deck as a PDF.
- Materials must be submitted by **29 Jan 2022 9AM** through your GitHub account repo shared with the Teaching Team.

---

## Presentation Structure

- **Presentation Time: 15 minutes**
- Use Google Slides or some other visual aid (Keynote, Powerpoint, etc).
- Consider the audience. Assume you are presenting to a non-technical audience.
- Start with the **data science problem**.
- Use visuals that are appropriately scaled and interpretable.
- Talk about your procedure/methodology (high level, **CODE IS ALWAYS INAPPROPRIATE FOR A NON-TECHNICAL AUDIENCE**).
- Talk about your primary findings.
- Make sure you provide **clear recommendations** that follow logically from your analyses and narrative and answer your data science problem.

Be sure to rehearse and time your presentation before class.

---

## Rubric
Teaching team will evaluate your project using the following criteria.  You should make sure that you consider and/or follow most if not all of the considerations/recommendations outlined below **while** working through your project.

**Note:** Presentation will be done as a group while codes will be prepared and submitted by each student.

For Project 3 the evaluation categories are as follows:<br>
**The Data Science Process**
- Problem Statement
- Data Collection
- Data Cleaning & EDA
- Preprocessing & Modeling
- Evaluation and Conceptual Understanding
- Conclusion and Recommendations

**Organization and Professionalism**
- Organization
- Visualizations
- Python Syntax and Control Flow
- Presentation

**Scores will be out of 30 points based on the 10 categories in the rubric.** <br>
*3 points per section*<br>

| Score | Interpretation |
| --- | --- |
| **0** | *Project fails to meet the minimum requirements for this item.* |
| **1** | *Project meets the minimum requirements for this item, but falls significantly short of portfolio-ready expectations.* |
| **2** | *Project exceeds the minimum requirements for this item, but falls short of portfolio-ready expectations.* |
| **3** | *Project meets or exceeds portfolio-ready expectations; demonstrates a thorough understanding of every outlined consideration.* |


### The Data Science Process

**Problem Statement**
- Is it clear what the goal of the project is?
- What type of model will be developed?
- How will success be evaluated?
- Is the scope of the project appropriate?
- Is it clear who cares about this or why this is important to investigate?
- Does the student consider the audience and the primary and secondary stakeholders?

**Data Collection**
- Was enough data gathered to generate a significant result?
- Was data collected that was useful and relevant to the project?
- Was data collection and storage optimized through custom functions, pipelines, and/or automation?
- Was thought given to the server receiving the requests such as considering number of requests per second?

**Data Cleaning and EDA**
- Are missing values imputed/handled appropriately?
- Are distributions examined and described?
- Are outliers identified and addressed?
- Are appropriate summary statistics provided?
- Are steps taken during data cleaning and EDA framed appropriately?
- Does the student address whether or not they are likely to be able to answer their problem statement with the provided data given what they've discovered during EDA?

**Preprocessing and Modeling**
- Is text data successfully converted to a matrix representation?
- Are methods such as stop words, stemming, and lemmatization explored?
- Does the student properly split and/or sample the data for validation/training purposes?
- Does the student test and evaluate a variety of models to identify a production algorithm (**AT MINIMUM:** Random Forest and one other model)?
- Does the student defend their choice of production model relevant to the data at hand and the problem?
- Does the student explain how the model works and evaluate its performance successes/downfalls?

**Evaluation and Conceptual Understanding**
- Does the student accurately identify and explain the baseline score?
- Does the student select and use metrics relevant to the problem objective?
- Does the student interpret the results of their model for purposes of inference?
- Is domain knowledge demonstrated when interpreting results?
- Does the student provide appropriate interpretation with regards to descriptive and inferential statistics?

**Conclusion and Recommendations**
- Does the student provide appropriate context to connect individual steps back to the overall project?
- Is it clear how the final recommendations were reached?
- Are the conclusions/recommendations clearly stated?
- Does the conclusion answer the original problem statement?
- Does the student address how findings of this research can be applied for the benefit of stakeholders?
- Are future steps to move the project forward identified?


### Organization and Professionalism

**Project Organization**
- Are modules imported correctly (using appropriate aliases)?
- Are data imported/saved using relative paths?
- Does the README provide a good executive summary of the project?
- Is markdown formatting used appropriately to structure notebooks?
- Are there an appropriate amount of comments to support the code?
- Are files & directories organized correctly?
- Are there unnecessary files included?
- Do files and directories have well-structured, appropriate, consistent names?

**Visualizations**
- Are sufficient visualizations provided?
- Do plots accurately demonstrate valid relationships?
- Are plots labeled properly?
- Are plots interpreted appropriately?
- Are plots formatted and scaled appropriately for inclusion in a notebook-based technical report?

**Python Syntax and Control Flow**
- Is care taken to write human readable code?
- Is the code syntactically correct (no runtime errors)?
- Does the code generate desired results (logically correct)?
- Does the code follows general best practices and style guidelines?
- Are Pandas functions used appropriately?
- Are `sklearn` and `NLTK` methods used appropriately?

**Presentation**
- Is the problem statement clearly presented?
- Does a strong narrative run through the presentation building toward a final conclusion?
- Are the conclusions/recommendations clearly stated?
- Is the level of technicality appropriate for the intended audience?
- Is the student substantially over or under time?
- Does the student appropriately pace their presentation?
- Does the student deliver their message with clarity and volume?
- Are appropriate visualizations generated for the intended audience?
- Are visualizations necessary and useful for supporting conclusions/explaining findings?


---

### Why did we choose this project for you?
This project covers three of the biggest concepts we cover in the class: Classification Modeling, Natural Language Processing and Data Wrangling/Acquisition.

Part 1 of the project focuses on **Data wrangling/gathering/acquisition**. This is a very important skill as not all the data you will need will be in clean CSVs or a single table in SQL.  There is a good chance that wherever you land you will have to gather some data from some unstructured/semi-structured sources; when possible, requesting information from an API, but often scraping it because they don't have an API (or it's terribly documented).

Part 2 of the project focuses on **Natural Language Processing** and converting standard text data (like Titles and Comments) into a format that allows us to analyze it and use it in modeling.

Part 3 of the project focuses on **Classification Modeling**.  Given that project 2 was a regression focused problem, we needed to give you a classification focused problem to practice the various models, means of assessment and preprocessing associated with classification.   
