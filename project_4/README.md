# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) West Nile Virus Prediction

## Background

The West Nile Virus (WNV) has been a worrying disease for the United States since 1999. West Nile virus is most commonly spread to humans through infected mosquitos.The [CDC](https://www.cdc.gov/westnile/index.html) has acknowledged it as the leading cause of mosquito-borne disease feeding on infected birds [(*source*)](https://parasitesandvectors.biomedcentral.com/articles/10.1186/1756-3305-3-19#citeas) in the continental United States. Now, there are still no vaccines to prevent or medications to cure WNV patients -- statistics data from the CDC, West Nile fever (WNF) is a potentially serious illness for humans and approximately 1 in 150 infected people develop a serious illness with symptoms that might last for several weeks. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death. Approximately 4/5 show no symptoms at all [(*source*)](http://www.cdc.gov/westnile/faq/genQuestions.html).

In Illinois, [West Nile virus was first identified in September 2001](https://www.dph.illinois.gov/topics-services/diseases-and-conditions/west-nile-virus) when laboratory tests confirmed its presence in two dead crows found in the Chicago area. In 2002, the first human cases of West Nile virus were reported in Chicago and death from West Nile disease were recorded and all but two of the state's 102 counties eventually reported a positive human, bird, mosquito or horse. By the end of 2002, Illinois had counted more human cases (884) and deaths (64) than any other state in the United States. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today. Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus.

Since then, Illinois and more specifically Chicago, has continued to suffer from multiple outbreaks of the WNV. From 2005 to 2016, a total of 1,371 human WNV cases were [reported](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0227160) within Illinois. Out of these total reported cases, 906 cases (66%) were from the Chicago region (Cook and DuPage Counties).  

Dataset used in thie project is included as `train.csv, test.csv, spray.cvs` and `weather.csv`. Datasets were provided by Kaggle.


## Problem Statement

As data scientists in the Division of Societal Cures in Epidemiology & New Creative Engineering (DATA-SCEINCE), we want to **understand the factors driving the spread of Wnv** by leveraging on data collected by Chicago's weather stations and the surveillance system set up by the Chicago Department of Public Health (CDPH) . We also want to **develop a classfication model that could predict the outbreaks of Wnv** within the area of Windy City. Through these studies, we hope to help the City of Chicago and the Chicago Department of Public Health more efficiently and effectively allocate resources toward preventing the transmission of this potentially deadly virus. Our aim is to determine the best strategy for controlling the spread of the WNV

## Datasets

- `train.csv` : the training set consists of data from 2007, 2009, 2011, and 2013.
- `test.csv`  : the test set is used to predict the test results for 2008, 2010, 2012, and 2014.
- `weather.csv`: weather data from 2007 to 2014.
- `spray.csv` : GIS data of spraying efforts in 2011 and 2013

Every year from late-May to early-October, public health workers in Chicago setup mosquito traps scattered across the city. Every week from Monday through Wednesday, these traps collect mosquitos, and the mosquitos are tested for the presence of West Nile virus before the end of the week. The test results include the number of mosquitos, the mosquitos species, and whether or not West Nile virus is present in the cohort.

<u>`train` & `test` dataset </u>

These test results are organized in such a way that when the number of mosquitos exceed 50, they are split into another record (another row in the dataset), such that the number of mosquitos are capped at 50. The location of the traps are described by the block number and street name. These attributes have been mapped into Longitude and Latitude in the dataset and are derived locations. For example, Block=79, and Street= "W FOSTER AVE" gives us an approximate address of "7900 W FOSTER AVE, Chicago, IL", which translates to (41.974089,-87.824812) on the map.

Some traps are "satellite traps". These are traps that are set up near (usually within 6 blocks) an established trap to enhance surveillance efforts. Satellite traps are postfixed with letters. For example, T220A is a satellite trap to T220. Not all the locations are tested at all times. Also, records exist only when a particular species of mosquitos is found at a certain trap at a certain time.

<u>`spray` dataset</u>

The City of Chicago also does spraying to kill mosquitos. Spraying can reduce the number of mosquitos in the area, and therefore might eliminate the appearance of West Nile virus.

<u>`weather` dataset</u>

It is believed that hot and dry conditions after wetter condition are more favorable for West Nile virus than cold and wet. The dataset is from National Oceanic and Atmospheric Administration (NOAA) of the weather conditions of 2007 to 2014, during the months of the tests.

Station 1: CHICAGO O'HARE INTERNATIONAL AIRPORT Lat: 41.995 Lon: -87.933 Elev: 662 ft. above sea level

Station 2: CHICAGO MIDWAY INTL ARPT Lat: 41.786 Lon: -87.752 Elev: 612 ft. above sea level

## Data Dictionary

| **Columns** | **Type** | **Dataset** | **Description** |
|---|---|---|---|
| **Id** | *integer* | test | The id of the record |
| **Date** | *datetime* | train/ test | Date that the WNV test is performed (YYYY-MM-DD) |
| **Address** | *object* | train/ test | Approximate address of the location of trap. This is used to send to the GeoCoder. | 
| **Species** | *object* | train/ test | The species of mosquitos |
| **Block** | *integer* | train/ test | Block number of address | 
| **Street** | *object* | train/ test | Street name |
| **Trap** | *object* | train/ test | Id of the trap |
| **AddressNumberAndStreet** | *object* | train/ test | Approximate address returned from GeoCoder |
| **Latitude, Longitude** | *float* | train/ test | Latitude and Longitude returned from GeoCoder |
| **AddressAccuracy** | *integer* | train/ test | Accuracy returned from GeoCoder |
| **NumMosquitos** | *integer* | train/ test | Number of mosquitoes caught in this trap |
| **WnvPresent** | *integer* | train/ test | Whether West Nile Virus was present in these mosquitos. (1 means WNV is present, while 0 means WNV is absent.) 
| **Date** | *datetime* | spray | The date of the spray (YYYY-MM-DD) |
| **Time** | *object* | spray | The time of the spray |
| **Latitude, Longitude** | *float* | spray | The Latitude and Longitude of the spray |
| **Station** | *integer* | weather | Weather station (1 or 2) |
| **Date** | *datetime* | weather | Date of measurement (YYYY-MM-DD)|
| **Tmax** | *integer* | weather | Maximum daily temperature (in Degrees Fahrenheit, F) |
| **Tmin** | *integer* | weather | Minimum daily temperature (in Degrees Fahrenheit, F) |
| **Tavg** | *object* | weather | Average daily temperature (in Degrees Fahrenheit, F) |
| **Depart** | *object* | weather | Departure from normal temperature (in Degrees Fahrenheit, F) |
| **DewPoint** | *integer* | weather | Average Dew Point temperature (in Degrees Fahrenheit, F) |
| **WetBulb** | *object* | weather | Average Wet Bulb temperature (in Degrees Fahrenheit, F) |
| **Heat** | *object* | weather | Heating Degree Days (season begins with July) |
| **Cool** | *object* | weather | Cooling Degree Days (season begins with January) |
| **Sunrise** | *object* | weather | Time of sunrise (calculated) |
| **Sunset** | *object* | weather | Time of sunset (calculated) |
| **CodeSum** | *object* | weather | Code of significant weather phenomena |
| **Depth** | *object* | weather | Snow/ice depth on the ground in inches, measured at 1200 UTC |
| **Water1** | *object* | weather | Water equivalent in inches, measured at 1800 UTC |
| **SnowFall** | *object* | weather | Total snowfall precipitation for the day (in inches and tenths) |
| **PrecipTotal** | *object* | weather | Total water equivalent precipitation for the day (in inches and tenths).  |
| **StnPressure** | *object* | weather | Average station pressure (in inches of hg) |
| **SeaLevel** | *object* | weather | Average sea level pressure (in inches of hg) |
| **ResultSpeed** | *float* | weather | Resultant wind speed (mph) |
| **ResultDir** | *integer* | weather | Resultant wind direction (degrees) |
| **AvgSpeed** | *object* | weather | Average wind speed (mph) |

# Objective
This is a supervised learning task, since the labels are provided (the expected output, i.e., binary representation of whether WNV was present within mosquito traps). 

We will be predicting two discrete class labels. More specifically, this is a binary classification problem with the ultimate goal -- to build a classifier to distinguish between just two classes, whether WNV was present in these mosquitos. 1 means WNV is present, and 0 means not present.

We will evaluate the performance of our model **using AUC (Area Under Curve) score as the North Star metric**. AUC score can be obtained by measuring the area under the receiver operating characteristic(ROC) curve. The ROC curve plots the true positive rate (TPR) against the false positive rate (FPR).  Our motivation is to increase the correct prediction (TP, TN) out of all the prediction, to detect correctly. The closer the AUC score to 1, the better the model is performing. 

# Data Cleaning
With the given 4 datasets, we have carried out initial analysis on each of them and produced the summary and list of cleaning works to be done.
These include 
- dropping duplicate rows, 
- imputing missing and zero values, 
- splitting strings and replace with correct format, 
- converting to right data types,
- dropping columns with high missing values
- creating more interpretable features

# EDA Summary
- The WNV incidences were highest in August.
- Species that are tested positive for West Nile Virus:Restuans or Pipiens species.
- From map visualisation, the occurences of West Nile virus is more prevalent near bodies of water and O’Hare airport.
- There are 136 traps. T900 (at Ohare airport) is sampled the most.
-  From the scatter plot, we can see that the occurences of West Nile Virus are more prevalent during days with hotter temperatures.
- From the scatter plot, we can see that the occurences of West Nile Virus are more prevalent during days with high humidity.
- Spraying is only effective in keeping the mosquito population under control on certain days.
- From map visualisation, We can see that spray area fails to fully overlap with the virus outbreak.
- Based on the heatmaps above, the existing features seem to have low correlation with the target. Therefore, we will have to perform feature engineering to extract more information from our data and improve the correlation scores.











Welcome to your first week of work at the Disease And Treatment Agency, division of Societal Cures In Epidemiology and New Creative Engineering (DATA-SCIENCE). Time to get to work!

Due to the recent epidemic of West Nile Virus in the Windy City, we've had the Department of Public Health set up a surveillance and control system. We're hoping it will let us learn something from the mosquito population as we collect data over time. Pesticides are a necessary evil in the fight for public health and safety, not to mention expensive! We need to derive an effective plan to deploy pesticides throughout the city, and that is **exactly** where you come in!

## Dataset

The dataset, along with description, can be found here: [https://www.kaggle.com/c/predict-west-nile-virus/](https://www.kaggle.com/c/predict-west-nile-virus/).

**This is also where you will be submitting your code for evaluation**. The public leaderboard uses roughly 30% of the dataset to score an AUC (Area Under Curve) metric.

> If you do not already have a Kaggle account, you will need to sign up on the website.  Also note that you will be submitting a "Late Submission" on Kaggle because the official competition has ended.  You can use the leaderboard to see how your results compare against roughly 1300 other data science teams!

You can submit predictions as many times as you want to Kaggle, but there is a limit of 5 submissions per day.  Be intentional with your submissions!


#### Navigating Group Work

This project will be executed as a group.  To make your team as effective and efficient as possible you should do the create a shared GitHub repo and project planning document as described in the deliverables section below.

## Deliverables

**GitHub Repo**

1. Create a GitHub repository for the group. Each member should be added as a contributor.
2. Retrieve the dataset and upload it into a directory named `assets`.
3. Generate a .py or .ipynb file that imports the available data.

**Project Planning**

1. Define your deliverable - what is the end result?
2. Break that deliverable up into its components, and then go further down the rabbit hole until you have actionable items. Document these using a project managment tool to track things getting done.  The tool you use is up to you; it could be Trello, a spreadsheet, GitHub issues, etc.
3. Begin deciding priorities for each task. These are subject to change, but it's good to get an initial consensus. Order these priorities however you would like.
4. You planning documentation (or a link to it) should be included in your GitHub repo.

**EDA**

1. Describe the data. What does it represent? What types are present? What does each data points' distribution look like? Discuss these questions, and your own, with your partners. Document your conclusions.
2. What kind of cleaning is needed? Document any potential issues that will need to be resolved.

**Note:** As you know, EDA is the single most important part of data science. This is where you should be spending most of your time. Knowing your data, and understanding the status of its integrity, is what makes or breaks a project.

**Modeling**

1. The goal is of course to build a model and make predictions that the city of Chicago can use when it decides where to spray pesticides! Your team should have a clean Jupyter Notebook that shows your EDA process, your modeling and predictions.
2. Conduct a cost-benefit analysis. This should include annual cost projections for various levels of pesticide coverage (cost) and the effect of these various levels of pesticide coverage (benefit). *(Hint: How would we quantify the benefit of pesticide spraying? To get "maximum benefit," what does that look like and how much does that cost? What if we cover less and therefore get a lower level of benefit?)*
3. Your final submission CSV should be in your GitHub repo.

**Presentation**
* Audience: You are presenting to members of the CDC. Some members of the audience will be biostatisticians and epidemiologists who will understand your models and metrics and will want more information. Others will be decision-makers, focusing almost exclusively on your cost-benefit analysis. Your job is to convince both groups of the best course of action in the same meeting and be able to answer questions that either group may ask.
* The length of your presentation should be about 10 minutes (a rough guideline: 1 minute intro, 5 minutes on model, 2 minutes on cost-benefit analysis, 2 minute recommendations/conclusion).  Touch base with your local instructor... er, manager... for specific logistic requirements!

---

It is recommended that this project is submitted through a link to a **public** repository on your personal (not GA) GitHub. This is so you can use the work done on this project to boost your portfolio for hiring. But students who prefer to submit from your GA Github account, may also do so. 

If project submission is done through your **personal GitHub** **public** repository, ensure that your technical report will be hosted on your **personal GitHub** (not **git.generalassemb.ly**).

---

### Project Feedback + Evaluation

For all projects, students will be evaluated on a simple 4 point scale (0-3 inclusive). Instructors will use this rubric when scoring student performance on each of the core project requirements:

Score | Expectations
----- | ------------
**0** | _Does not meet expectations. Try again._
**1** | _Approaching expectations. Getting there..._
**2** | _Meets expectations. Great job._
**3** | _Surpasses expectations. Brilliant!_

### Rubric

Your final assessment ("grade" if you will) will be calculated based on a topical rubric (see below).  For each category, you will receive a score of 0-3.  From the rubric you can see descriptions of each score and what is needed to attain those scores.

For Project 3 the evaluation categories are as follows:
- [Organization](#organization)
- [Data Structures](#data-structures)
- [Python Syntax and Control Flow](#python-syntax-and-control-flow)
- [Probability and Statistics](#probability-and-statistics)
- [Modeling](#modeling)
- [Presentation](#presentation)

#### Organization

Clearly commented, annotated and sectioned Jupyter notebook or Python script.  Comments and annotations add clarity, explanation and intent to the work.  Notebook is well-structured with title, author and sections. Assumptions are stated and justified.


| Score | Status                     | Examples                                                                                                                                                                                                                                         |
|-------|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0     | Does not Meet Expectations | 1. Comments and annotations are **absent** <br> 2. There is no clear notebook structure <br> 3. Assumptions are not stated                                                                                                                                       |
| 1     | Approaching Expectations   | 1. Comments are present but generally unclear or uninformative (e.g., comments do not clarify, explain or interpret the code) <br> 2. There are some structural components like section/subsection headings <br> 3. Assumptions are stated but not justified |
| 2     | Meets Expectations         | 1. Comments and annotations are clear and informative <br> 2. There is a clear structure to the notebook with title and appropriate sectioning <br> 3. Assumptions are both stated and justified                                                             |
| 3     | Exceeds Expectations       | 1. Comments and annotations are clear, informative and insightful <br> 2. There is a helpful and cogent structure to the notebook that clarifies the analysis flow <br> 3. Assumptions are stated, justified and backed by evidence or insight               |

#### Data Structures

Python data structures including lists, dictionaries and imported structures (e.g. DataFrames), are created and used correctly.  The appropriate data structures are used in context.  Data structures are created and accessed using appropriate mechanisms such as comprehensions, slices, filters and copies.

| Score | Status | Examples |
|-------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0 | Does not Meet Expectations | 1. Appropriate data structures are not identified or implemented <br> 2. Data structures are not created appropriately <br> 3. Data structures are not accessed or used effectively |
| 1 | Approaching Expectations | 1. Contextually appropriate data structures are identified in some but not all instances <br> 2. Data structures are created successfully but lacked efficiency or generality (e.g., structures were hard-coded with values that limits generalization; brute-force vs automatic creation/population of data) <br> 3. Data structures are accessed or used but best practices are not adopted |
| 2 | Meets Expectations | 1. Contextually appropriate data structures are identified and implemented given the context of the problem <br> 2. Data structures are created in an effective manner <br> 3. Data structures are accessed and used following general programming and Pythonic best practices |
| 3 | Exceeds Expectations | 1. Use or creation of data structures is clever and insightful <br> 2. Data structures are created in a way that reveals significant Pythonic understanding <br> 3. Data structures are used or applied in clever or insightful ways |


#### Python Syntax and Control Flow

Python code is written correctly and follows standard style guidelines and best practices.  There are no runtime errors.  The code is expressive while being reasonably concise.

| Score | Status | Examples |
|-------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0 | Does not Meet Expectations | 1. Code has systemic syntactical issues <br> 2. Code generates incorrect results <br> 3. Code is disorganized and needlessly difficult |
| 1 | Approaching Expectations | 1. Code is generally correct with some runtime errors <br> 2. Code logic is generally correct but does not produce the desired outcome <br> 3. Code is somewhat organized and follows some stylistic conventions |
| 2 | Meets Expectations | 1. Code is syntactically correct (no runtime errors) <br> 2. Code generates desired results (logically correct) <br> 3. Code follows general best practices and style guidelines |
| 3 | Exceeds Expectations | 1. Code adopts clever or advanced syntax <br> 2. Code generates desired results in an easily consumable manner (e.g., results are written to screen, file, pipeline, etc, as appropriate within the flow of the analysis) <br> 3. Code is exceptionally expressive, well formed and organized |


#### Probability and Statistics

Descriptive and inferential statistics are calculated and applied where appropriate.  Probabilistic reasoning is demonstrated.  There is a clear understanding of how probability and statistics affects the analysis being performed.

| Score | Status | Examples |
|-------|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0 | Does not Meet Expectations | 1. Descriptive statistical calculations are absent <br> 2. Inferential statistical calculations are absent <br> 3. Probabilities or statistics are not relevant given the context of the analysis |
| 1 | Approaching Expectations | 1. Descriptive statistics are present in some cases <br> 2. Inferential statistics are present in some cases <br> 3. Probabilities or statistics are somewhat relevant to the analysis context |
| 2 | Meets Expectations | 1. Descriptive statistics are calculated in all relevant situations <br> 2. Inferential statistics are calculated in all relevant situations <br> 3. Probabilities or statistics are relevant to the analysis |
| 3 | Exceeds Expectations | 1. Descriptive statistics are calculated, interpreted and visualized (where appropriate) <br> 2. Inferential statistics are calculated, interpreted and visualized (where appropriate) <br> 3. Probabilities or statistics are leveraged to draw meaningful or insightful conclusions |

#### Modeling

Data is appropriately prepared for modeling.  Model choice matches the context of the data and the analysis.  Model hyperparameters are optimized.  Model evaluation is robust.  Model results are extracted and explained either visually, numerically or narratively.

| Score | Status | Examples |
|-------|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0 | Does not Meet Expectations | 1. Data is not prepared for modeling.<br>2. Models are not implemented or not implemented fully.<br>3. Model hyperparameters are not considered.<br>4. Model evaluation is not performed.<br>5. Model results are unavailable or not extracted. |
| 1 | Approaching Expectations | 1. Data has some null values, inappropriate types and/or improper handling of categorical labels.<br>2. Model choice is questionable given the objective of the analysis.<br>3. Model hyperparameters are insufficiently or not optimized.<br>4. Model evaluation is performed but the evaluation is not generalizable.<br>5. Model results are extracted but not explained or interpreted. |
| 2 | Meets Expectations | 1. Data is free from nulls and correctly typed for the given model.<br>2. Model choice is appropriate to the analysis.<br>3. Model hyperparameters are optimally selected.<br>4. Model evaluation reflects generalizeable performance.<br>5. Model results are extracted and explained either visually, numerically or naratively. |
| 3 | Exceeds Expectations | 1. Data is pristinely prepared with creative or useful feature engineering.<br>2. Model selection is justified and demonstrates an awareness of tradeoffs.<br>3. Model hyperparameters are optimized and the optimization is demonstrated/justified.<br>4. Model evaluation reflects generalizable performance and is interpreted in the context of the analysis.<br>5. Model results are explained, interpreted and related to the overarching analysis goals. |


#### Presentation

The goal, methodology and results of your work are presented in a clear, concise and thorough manner.  The presentation is appropriate for the specified audience, and includes relevant and enlightening visual aides as appropriate.

| Score | Status | Examples |
|-------|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0 | Does not Meet Expectations | 1. The problem was not well explained or ambiguous. <br> 2. The level of technicality was far above or below the target audience. <br> 3. The presentation went substantially over or under time. <br> 4. The speaker's voice was difficult to hear of unclear. <br> 5. The presentation visuals did not seem to support the talk. |
| 1 | Approaching Expectations | 1. The problem was stated but was not 100% clear. <br> 2. The level of technicality was was good at times, but too low or too high at other times given the target audience. <br> 3. The presentation was given went slightly over or under time. <br> 4. The speaker's voice was at times difficult to understand. <br> 5. The presentation visuals were generally helpful, but some of them were either too complex or disconnected from the narrative. |
| 2 | Meets Expectations | 1. The problem was framed appropriately for the audience. <br> 2. The level of technicality was appropriate to the target audience. <br> 3. The presentation was given within the allocated timeframe. <br> 4. The speaker's voice had volume and clarity. <br> 5. The presentation visuals were helpful and supportive. |
| 3 | Exceeds Expectations | 1. The problem was expertly stated and compelling. <br> 2. The level of technicality was perfect for the target audience. <br> 3. The presentation was given within the allocated timeframe and paced evenly throughout. <br> 4. The speaker's voice was clear, understandable and consistent. <br> 5. The presentation visuals provided distinct insight, supported the speaker from the background, and were not distracting. |
