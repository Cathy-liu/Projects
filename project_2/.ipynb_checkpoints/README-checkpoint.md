# Project 2 - Ames Housing Data and Kaggle Challenge

**Summary of the project**
The goal of this project is to train a regression model for predicting housing price on the given data. Metrics are applied to assess the performance of each model; and for the best performing model selected, hyperparameter tuning is carried out to ensure the production model are set with the best set of parameters. After obtaining the production model, analysis of the model coefficients is carried out to highlight the strongest features in predicting the response variable which is the salesprice of a house. Based on this, business insights are given for stakeholders in the real estate business. 


**Problem Statement**
- What are the top 10 strongest features in deciding the price of a house?
- Among the top strongest features, which are more common sense factors and which are not? 
- Based on the findings to the previous question, what business insights can be made?

**Structure of coding** 
There are 6 parts of coding, below is a summary of the process in each. 

***1. Data Cleaning and EDA***
- From reading the data dictionary at https://www.kaggle.com/c/dsir-426-ames-housing-data, there are 14 columns in the training dataset that 'NA' have actual meanings. In order to differentiate these 'NA' cells that actually have meangings from real absent data, a placeholder string is filled for the NA value in these 14 columns. 

- Upon inspection all the other NA values are real missing data and are imputed using most-frequent values for that feature.

- A correlation function was used to find the top 5 strongest features. Since there are both categorical and numerical features among them, to visualize their correlation with the resopnse variable, scatterplots are used to visualize numerical feature vs salesprice correlation, whereas boxplots are used to visualize distributions of the categorical features. 

- From the visualization, the features 'Overall Qual', 'Gr Liv Area','Garage Area' show strong positive correlation with the salesprice, which is understandable. The other two 'Total Bsmt SF' and 'Garage Cars' may have positively correlated to the salesprice due to the fact that larger garage and basement area in this context suggest a larger house which means higher price.

***2. Preprocessing and Modeling***
- Train/Test split is done before imputing for the 'Lot Frontage' and 'Garage Yr Blt' columns to avoid data leakage. The split portion is 80% - 20%. 

- Before dummifying the categorical features, all 'object' type columns are inspected to be sure that they should be categorical, and not numerical values with strings among the values. 

- All the 'object' type columns are all dummified into binary values.

- There are categorical features that are originally in float/int format, these are ordinal features for which the numerical values are actually meaningful, for this reason they are left with their origianl numerical values. 

- As the number of columns for the training and testing datasets have differed after dummification, an outer join operation have been carried out on both of them to include the columns from the other dataset. This is to make sure the regression model trained on the training dataset can perform normally on the testing dataset.

- Finally, StandardScaler transformation is performed on the feature matrix on training dataset, and the same transformation is subsequently performed on the test dataset.

***3. Model Benchmarks***
- The null model using the mean value of saleprice is taken as the baseline model. 

- For OLS model, based on the metrics, the R^2 is 0.95 on the training data and negative on the testing dataset, this says that the OLS model here is a severely overfit model, and it does not explain any of the variations in y by X for the testing dataset.

- For RidgeCV model, the range for alphas as input parameter is chosen based on parametric experiments, in a way such that convergence is guranteed for the Ridge model and also covers the range where the optimal alpha value falls in.
- The results of the RidgeCV model suggests that though the R^2 on the training dataset is quite ok, the 0.77 value on the test dataset suggests that this model is quite a overfit model, and may not generalize well to new data.

- For the LassoCV regression model, from parametric experiments, alpha=10^2.1 is the smallest alpha value that gurantees convergence. Hence the range of list of alphas input here is chosen such that it covers the optimal alpha value and approximates it more and mroe through iterations.
- The R^2 is 0.904 and 0.884 on the training and testing datasets respectively; the closeness between the R^2 on training dataset and on test dataset suggests that this model is well balanced and generalizes well to new data.

***4. Model Tuning***
- As Lasso regression model perform the best for the problem as suggests by its metrics and also because of the large number of features in the problem, hyperparameter tuning is carried out for the Lasso Regression Model.

- When defining the search grid, for each iteration, focus is on shrinking the range of alphas so that through iterations, we will have zoomed in to obtained a more exact approximate to the optimal value of alpha.

- The R^2 values have virtually fixed around a point for the last four iterations as presented in the code Part 4, this suggests that the we have reached the optimal alpha value and the model is saturated here. 

- The closeness between the R^2 on training (0.9045) and test datasets (0.8835) confirmed that the model performs well and generalizes well too.

***5. Production Model and Insights***
- Based on the parametric experiments in Part 3 and the hyperparameter tuning results in Part 4, we can safely conclude that the LassoCV model with alpha at 920.37 is the model that performs the best and generalizes the best; hence this is the model adopted as the production model.

- Top 10 features are identified by the 10 highest coefficients from the trained Lasso model. There are common sense ones such as area and year built, and there are also not so common sense ones such as a specific neighborhood.

- Interpretation of the coefficients for the top 5 strongest features: 

With all the other factors hold constant,

* Per square feet increase in above ground living area will lead to an increase of $45.73 in price on average;

* Every level upgrade in the overall quality scale will lead to an increase of $11,133 in prices on average;

* Prices of houses in the neighborhood of Northridge Heights are $38,111 higher than that of houses in the neighborhood of Bloomington Heights;

* Each year more recently built contribute to a $219 raise in the price on averge;

* Houses with a second garage are $100,062 more expensive than houses with an elevator on average (probably because they are highrise apartments that are smaller than houses with 2 garages).

- As most other features are kind of universal (e.g. total area), the feature neighorhood is further looked into here for the purpose to gain business insights. The top 3 most valuable neighorhoods are identified based on the mean salesprice in each neighorhoods.

***6. Predictin and Kaggel Submission*** 
- For the data imported from the test.csv file, the same cleaning and pre-processing, feature engineering steps are carried out. 
- After dummification, as there are columns that don't exist in the dummified feature matrix of the data from the train.csv file, these columns are dropped as we do not have any information how they are going to affect the response variable. On the other hand, those few columns that exist in the feature matrix of the data from the train.csv file but absent in this dataset, they are filled up with 0 values to the feature matrix, to keep the columns of the feature matrix exactly the same as the model trained on.
- After obtaining the predicted salesprice using the Prodcution Model, mean predicted salesprice of houses in each neighborhood are plotted to highlight the most valuable neighborhoods in real estate market - NoRidge, NridgHt and StoneBr.