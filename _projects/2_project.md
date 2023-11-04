---
layout: page
title: RecSys Challenge
description: Deep funnel optimization for app installations focusing on user privacy. 
img: assets/img/recsys.png
importance: 2
category: Work
---
In this challenge, we are provided a real-world ad dataset from the Sharechat and Moj apps to act as a benchmark for research into deep funnel optimization with a focus on user privacy. As part of the challenge, ShareChat released anonymized dataset corresponds to roughly 10M random users who visited the ShareChat + Moj app over three months.(We do not have the name of the feartures) we are directly given the preprocessed data.

## Dataset
We are provided with the following data:

|Feature | Description|
|----------|---------------|
|`Row ID`| f_0|
|`Date`| f_1|
|`Categorical Features`| f_2 ... f_32|
|`Binary Features`| f_33 ... f_41|
|`Numerical Features`| f_42 ... f_79|
|`Is_click`| [Binary] Did the user clicked on the ad|
|`Is Install`| [Binary] Did the user install the app |

As the data is anonymized, we do not have the name of the features. The data is preprocessed and we are directly given the preprocessed data. Basic Discription of data is given below:

|`Total Rows`| 3485852|
|`Only Installs`| 358645 ~ 10%| 
|`Only Clicks`| 518357 ~ 15%|
|`Both Installed and Clicked`| 247957 ~ 7%| 
|`Unique Dates`| 22|

## Data Exploration

We did some exporation regarding the range of the feautures and no. of classes in categorical features. Along with this we also explored the correlation between features and the target variable. We also explored the class imbalance in the dataset.

## Data Preprocessing

All the data is given in terms of number so intialize steps of standardization and encoding (One hot or Label encoding) is not required. We just have to check for missing values and remove them. We have to check for outliers and remove them. We have to check for correlation between features and remove them. We have to check for class imbalance and use techniques like SMOTE to balance the classes.

#### Imputation

For categorical features we tried mode imputation , Knn based imputation and probabilistic imputation. For numerical features we tried mean imputation. The missing values can also be given a seperate category.

## Models
We tried a lot of models like Logistic Regression, Random Forest, XGBoost, LightGBM, CatBoost, Naive Bayse, etc. We also tried stacking of models. We also tried different techniques like Grid Search, Random Search, Bayesian Optimization, etc. to tune the hyperparameters of the models.

## Results

|          **Model**         | **Val Loss** | **Test Loss** |**Description**|
|:--------------------------:|--------------|---------------|:--------------:|
|`xgb_all_feat`| 5.968 | 6.373| Hyper parameter turing with optuna|
|`f1_xgb_catb_best`|Nan| 6.375|Combined XGB and Catboost with f1 formula|
|`xgb_all_feat_xgb_chain`| 5.99| 6.385|Xgb on top of another Xgb model|
|`catboost_all_feat`| 5.739  | 6.461 |Catboost model with all the feature with optuna|
|`xgb_stacked_kfold_logistic` | Nan| 6.611|XGB Stacked kflod Logistic Regression|
|`xgb_calibrated_logistic`  |Nan| 6.613|Calibrated XGB with logistic regression|
|`xgb_stack_all_cat_num_xgb` |6.026| 6.643|Stack all the above row 1,2 and 3 optuna with xgb|
|`xgb_num_cat_all_avg`|Nan| 6.690|Simple average of all the xgb of row 1|
|`xgb_cat_feat`| 6.248  | 6.927| Hyper parameter turing with optuna while using only Categorical Features|
|`xgb_float_all_feat`| 5.79| 7.254|Converted all the categorical values to probablites|
|`xgb_num_feat`| 6.245  | 7.401|Hyper parameter turing with optuna while using only Numerical Features|
|`xgb_stack_all_cat_num`| 7.685   | 9.910|Stack all the above row 1,2 and 3 optuna with logistice regression model|
