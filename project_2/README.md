# Project 2 - Ames Housing Data and Kaggle Challenge

### Problem Statement
This project aim to determine which feature variables are most likely to impact the property sale price of a home in Ames. With the defined exploratory features, we can further predict the housing price by using regression model. All these information are intend to provide a guideline to the stakeholder of Ames city housing developer.

### Overview
Based on a United States Census Bureau report in 2010, Ames had a population of approximately 59,000. Also, Ames, Iowa economy and demographics is largely defined by the Iowa State University, a public research university located in the middle of the city. More than 75%  of Ames' population is either studying as a student or working as a faculty at Iowa State University, making Ames one large extended campus. 

Housing prices have steadily increased over the course of the past three decades with the exception of severe economic downturns such as the economic recession of 2008. The housing market is not only a very strong economic indicator but it has a financial impact on anyone looking to own a home themselves.

As a member of the Ames city housing developer, the stakeholder would like to understand the features which are most likely to impact housing price and to make prediction on te price of a house at sale. In order to achieve the targets, Ames Housing Dataset from Kaggle will be used. Furthermore, regression model will be created based on the Ames Housing Dataset. This model will enable us to make prediction on the price of a house at sale.

The Ames Housing Dataset is a public dataset made available by Kaggle. The dataset is a record of houses sold in Ames between the years 2006 and 2010 with each entry being represented by 81 exploratory data variables and the sale price of a house.  

This project covers:
- Background
- Data Import & Cleaning
- Exploratory Data Analysis & Data Visualization
- Creating and iteratively refining a regression model
- Prediction on Test Dataset
- Conclusions and Recommendations

### Datasets

#### Provided Data
There are 3 datasets included in the [`datasets`](./datasets/) project for Ames Iowa Housing analysis.
* [`train.csv`](./datasets/train.csv): Ames Housing Train Dataset ([source](https://www.kaggle.com/datasets/marcopale/housing?select=test.csv))
* [`test.csv`](./datasets/test8.csv): Ames Housing Test Dataset ([source](https://www.kaggle.com/datasets/marcopale/housing?select=test.csv))
* [`sample_sub.csv`](./datasets/sample_sub.csv): Kaggle Submission Sample ([source](https://www.kaggle.com/datasets/marcopale/housing?select=test.csv))

 
### Data Dictionary
The data has 81 columns which include 23 nominal, 23 ordinal, 14 discrete, and 20 continuous variables (and 1 additional observation identifiers). The test dataset have same data dictionary as train dataset except SalePrice. 

|Column|Type|Description|
|---|---|---|
|**Id**|*integer*|Identification number|
|**PID**|*integer*|Parcel identification number|
|**MS SubClass**|*integer*|Identifies the type of dwelling involved in the sale|
|**MS Zoning**|*object*|Identifies the general zoning classification of the sale|
|**Lot Frontage**|*float*|Linear feet of street connected to property|
|**Lot Area**|*integer*|Lot size in square feet|
|**Street**|*object*|Type of road access to property|
|**Alley**|*object*|Type of alley access to property|
|**Lot Shape**|*object*|General shape of property|
|**Land Contour**|*object*|Flatness of the property|
|**Utilities**|*object*|Type of utilities available|
|**Lot Config**|*object*|Lot configuration|
|**Land Slope**|*object*|Slope of property|
|**Neighborhood**|*object*|Physical locations within Ames city limits|
|**Condition 1**|*object*|Proximity to various conditions|
|**Condition 2**|*object*|Proximity to various conditions (if more than one is present)|
|**Bldg Type**|* object*|Type of dwelling|
|**House Style**|*object*|Style of dwelling|
|**Overall Qual**|*integer*|Rates the overall material and finish of the house|
|**Overall Cond**|*integer*|Rates the overall condition of the house|
|**Year Built**|*integer*|Original construction date|
|**Year Remod/Add**|*integer*|Remodel date (same as construction date if no remodeling or additions)| 
|**Roof Style**|*object*|Type of roof|
|**Roof Matl**|*object*|Roof material|
|**Exterior 1st**|*object*|Exterior covering on house|
|**Exterior 2nd**|*object*|Exterior covering on house (if more than one material)|
|**Mas Vnr Type**|*object*|Masonry veneer type|
|**Mas Vnr Area**|*float*|Masonry veneer area in square feet|
|**Exter Qual**|*object*|Evaluates the quality of the material on the exterior|
|**Exter Cond**|*object*|Evaluates the present condition of the material on the exterior|
|**Foundation**|*object*|Type of foundation|
|**Bsmt Qual**|*object*|Evaluates the height of the basement|
|**Bsmt Cond**|*object*|Evaluates the general condition of the basement|
|**Bsmt Exposure**|*object*|Refers to walkout or garden level walls|
|**BsmtFin Type 1**|*object*|Rating of basement finished area|
|**BsmtFin SF 1**|*float*|Type 1 finished square feet|
|**BsmtFin Type 2**|*object*|Rating of basement finished area (if multiple types)|
|**BsmtFin SF 2**|*float*|Type 2 finished square feet|
|**Bsmt Unf SF**|*float*|Unfinished square feet of basement area|
|**Total Bsmt SF**|*float*|Total square feet of basement area|
|**Heating**|*object*|Type of heating|
|**Heating QC**|*object*|Heating quality and condition|
|**Central Air**|*object*|Central air conditioning|
|**Electrical**|*object*|Electrical system|
|**1st Flr SF**|*integer*|First Floor square feet|
|**2nd Flr SF**|*integer*|Second floor square feet|
|**Low Qual Fin SF**|*integer*|Low quality finished square feet (all floors)|
|**Gr Liv Area**|*integer*|Above grade (ground) living area square feet|
|**Bsmt Full Bath**|*float*|Basement full bathrooms|
|**Bsmt Half Bath**|*float*|Basement half bathrooms|
|**Full Bath**|*integer*|Full bathrooms above grade|
|**Half Bath**|*integer*|Half baths above grade|
|**Bedroom AbvGr**|*integer*|Bedrooms above grade (does NOT include basement bedrooms)|
|**Kitchen AbvGr**|*integer*|Kitchens above grade|
|**Kitchen Qual**|*object*|Kitchen quality|
|**TotRms AbvGrd**|*integer*|Total rooms above grade (does not include bathrooms)|
|**Functional**|*object*|Home functionality (Assume typical unless deductions are warranted)|
|**Fireplaces**|*integer*|Number of fireplaces|
|**Fireplace Qu**|* object*|Fireplace quality|
|**Garage Type**|*object*|Garage location|
|**Garage Yr Blt**|*float*|Year garage was built|
|**Garage Finish**|*object*|Interior finish of the garage|
|**Garage Cars**|*float*|Size of garage in car capacity|
|**Garage Area**|*float*|Size of garage in square feet|
|**Garage Qual**|*object*|Garage quality|
|**Garage Cond**|*object*|Garage condition|
|**Paved Drive**|*object*|Paved driveway|
|**Wood Deck SF**|*integer*|Wood deck area in square feet|
|**Open Porch SF**|*integer*|Open porch area in square feet|
|**Enclosed Porch**|*integer*|Enclosed porch area in square feet|
|**3Ssn Porch**|*integer*|Three season porch area in square feet|
|**Screen Porch**|*integer*|Screen porch area in square feet|
|**Pool Area**|*integer*|Pool area in square feet|
|**Pool QC**|*object*|Pool quality|
|**Fence**|*object*|Fence quality|
|**Misc Feature**|*object*|Miscellaneous feature not covered in other categories|
|**Misc Val**|*integer*|Value of miscellaneous feature|
|**Mo Sold**|*integer*|Month Sold (MM)|
|**Yr Sold**|*integer*|Year Sold (YYYY)|
|**Sale Type**|*object*|Condition of sale|
|**SalePrice**|*integer*|Condition of sale|


## Exploratory Data Analysis & Visualisation
- The distribution of the Sale Price data appeared to have a slightly right skew.  Majority of property living space sizes fall between about ($)100,000 to 200,000. 
- The properties of FV -- Floating Village Residential have a higher median over all the others. On the other hand, C(all) -- Commercial properties have the lowest.
- Some neighborhoods have a much higher price tag associated with their houses (e.g. StoneBr). Some neighborhood (e.g. StoneBr) can share similar characteristics with another (e.g. NridgHt), resulting in them having nearly similar median price values that do not exceed each others' interquartile ranges.
- Upward linear regression are observed for 'Gr Liv Area', 'Year Built' and 'Overall Qual' against `SalePrice`.
- 29 features are selected for modelling based on the EDA. 
- For categorical columns, 14 features - 'MS Zoning', 'Land Contour', 'Lot Config','Neighborhood', 'Condition 1', 'Bldg Type', 'House Style', 'Exterior 1st', 'Exterior 2nd', 'Mas Vnr Type', 'Foundation', 'Garage Type', 'Garage Qual', 'Sale Type' are selected as they do not show severely skewed distribution. 
- For numberic columns, another 15 features -- 'Overall Qual', 'Year Built', 'Year Remod/Add', 'Mas Vnr Area', 'Exter Qual', 'Bsmt Qual', 'Total Bsmt SF', '1st Flr SF', 'Gr Liv Area', 'Full Bath', 'Kitchen Qual', 'TotRms AbvGrd','Fireplace Qu', 'Garage Finish', 'Garage Area' are selected due the strong correlationship shown between numeric features vs saleprice. 

## The Modeling Process
1. 29 features selected as X_train: 'Overall Qual', 'Year Built', 'Year Remod/Add', 'Mas Vnr Area', 'Exter Qual', 'Bsmt Qual', 
                                    'Total Bsmt SF', '1st Flr SF', 'Gr Liv Area', 'Full Bath', 'Kitchen Qual', 'TotRms AbvGrd',
                                    'Fireplace Qu', 'Garage Finish', 'Garage Area', 'MS Zoning', 'Land Contour', 'Lot Config',
                                    'Neighborhood', 'Condition 1', 'Bldg Type', 'House Style', 'Exterior 1st', 'Exterior 2nd', 
                                    'Mas Vnr Type', 'Foundation', 'Garage Type', 'Garage Qual', 'Sale Type'
2. `SalePrice` is our target prediction, which is set as y_train.
2. Dummifying 149 columns in total.
3. Using `train-test split` to generate training data for regression model.
4. Model used:
    - Linear regression
    - RidgeCV Regression
    - LassoCV Regression
    - ElasticNet Regression
5. Evaluate your models:
In general, the features do a good job passing the test. However, R-squared value shows negative score in the linear regression, which means the chosen model does not follow the trend of the data. Although the model is giving quite good performamce, it is due to over-fitting. Therefore,  linear model with regularization feature are used. Regularization is a method for "constraining" or "regularizing" the size of the coefficients, thus "shrinking" them towards zero. It reduces model variance and thus minimizes overfitting. If the model is too complex, it tends to reduce variance more than it increases bias, resulting in a model that is more likely to generalize. In this case, we are exploring RidgeCV, LassoCV and ElaticNet model. Out of these 3 models, it seems like our LassoCV model is the most successful in predicting housing sale prices. The LassoCV demostrate R-squared value of 0.87 in train dataset and 0.86 in test dataset.

Therefore, we use LassoCV to further fit on our testing dataset. This allow us to make prediction of the housing sale price on the testing dataset.
    
## Kaggle Submission Score
Score: 25167.84381
Public score: 35055.22681

## Conclusions and Recommendations
It is clear that regression algorithms can be used to quite accurately (about 86% accurancy) predict the price of houses in Ames, Iowa based on the variables recorded in this dataset.  Additionally there are 29 identified features that greatly impact the price of a house. All these inforamtion would be important for housing developer to take into consideration before developing any housing project in Ames, Iowa as they are helpful to maximize the earning profit as a developer.

From the above analysis, the key takeaways are:
- The distribution of the Sale Price data appeared to have a slightly right skew.  Majority of property living space sizes fall between about ($)100,000 to 200,000. The baseline score are calculated based on the mean of the housing sale price, which are ($)178,601.37. This is in alignment with our observation from the distribution of the Sale Price. 
- 29 features -- 'Overall Qual', 'Year Built', 'Year Remod/Add', 'Mas Vnr Area', 'Exter Qual', 'Bsmt Qual', 'Total Bsmt SF', '1st Flr SF', 'Gr Liv Area', 'Full Bath', 'Kitchen Qual', 'TotRms AbvGrd', 'Fireplace Qu', 'Garage Finish', 'Garage Area', 'MS Zoning', 'Land Contour', 'Lot Config', 'Neighborhood', 'Condition 1', 'Bldg Type', 'House Style', 'Roof Matl', 'Exterior 1st', 'Exterior 2nd', 'Mas Vnr Type', 'Foundation', 'Garage Type', 'Garage Qual', 'Sale Type' are most likely impact the property sale price of a home in Ames Iowa based on our evaluation.
- LassoCV model is the most successful in predicting housing sale prices out of three regularization models -- RidgeCV, LassoCV and ElaticNet model as it overcomes the over-fitting found in linear regression.

Recommendation:
- Explore using more features for modelling to check model improvement. 
- Explore the use of non-linear regression models for sale price prediction.
- Make use of available features to further identify features such as housing age or to collect other features such as homebuyer pay-scale.