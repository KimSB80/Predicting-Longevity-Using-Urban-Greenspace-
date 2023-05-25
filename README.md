# Predicting Longevity Using Urban Greenspace

## Problem Statement
Access to urban greenspace is becoming increasingly important as cities continue to grow, and studies have linked access to greenspace (e.g. parks, gardens) to mental well-being (Thompson et al. 2016). Over the past few years, London’s local government has been making a push for “greening London”; the London Plan 2021 outlines an integrated environmental strategy for increasing urban greenspace. For this project, I developed a model to predict which factors are most important for longevity within the London wards.

## Data Collection
I used data from the [London Ward Well-Being Scores](https://www.kaggle.com/datasets/jarxrr/london-ward-wellbeing-scores) dataset, collected by the Greater London Authority over the period of 2009-2013. This dataset includes information on life-expectancy, as well as 12 different well-being indicators such as access to greenspace and public transport, childhood obesity rates, crime rates, and unemployment rates. I merged a [second well-being dataset](https://www.data.gov.uk/dataset/ebbc1dc4-55f1-49e4-a969-67f38fa15ef1/better-environment-better-health-guides-for-london-boroughs) from the Greater London Authority that uses a different metric (total area) for urban greenspace so I could assess whether different greenspace metrics affect the model.

## Data Wrangling and Exploratory Data Analysis
I used fuzzy string matching to merge the two datasets, and checked for missing values. I used panda profiling for a first examination of the data, as well as heatmaps and pairplots (seaborn) to visualize relationships between variables.

## Preprocessing and Feature Engineering
I used ColumnTransformer to create a pipeline that performed one-hot-encoding on categorical variables and standard scaler on numerical variables. Since I was interested in the effect of greenspace on well-being, I created a binned ordinal metric for greenspace that designated it as low, medium, or high based on the total area of greenspace in each region (Borough) of London. 

## Modeling
This is a regression problem in supervised machine learning. I tested the following four regression models:

-- Linear Regression<br>
-- Random Forest<br>
-- Gradient Boosting Regressor<br>
-- Support Vector Regressor (SVR)<br>

I used r-squared and MAE to determine that the gradient boosting model performed the best, and then used GridSearchCV to tune hyperparameters using k-fold cross-validation. 

![download](https://github.com/KimSB80/Predicting-Longevity-Using-Urban-Greenspace-/assets/124254338/e01a4835-10f5-4648-82ee-02f3d67f3552)


## Key Findings:
#### 1. The most important predictor of longevity is unemployment rate. 
Unemployment rate indicates the percentage of working-age residents claiming unemployment benefits in that Ward. This, unsurprisingly, suggests that there is a high degree of stress related to being unemployed that negatively impacts longevity. 

#### 2. Unauthorized school absences, the number of dependent children living in an out-of-work household, and incapacity benefit were also important in predicting longevity. 
These correlations make sense intuitively; these metrics are both representative of hardship. Specifically, the "dependent children" metric represents the % of children living in out-of-work households, and "incapacity benefits" represents the disability claimant rate for that Ward.

#### 3. Access to public greenspace areas does provide some positive benefit.
While access to public greenspace was not a strong predictor of longevity, it does show some importance in the model. Looking at the original data, we can see a positive correlation between greenspace access and longevity. This suggests a positive benefit for people living in areas with more access to parks or other green areas; this may be due to the impact on lifestyle that this access affords, or possibly is related to the wealth of that area. 
