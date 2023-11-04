---
layout: page
title: Donor Choose
description: Application status prediction for DonorChoose.org 
img: assets/img/donor_choose.png
importance: 1
category: Work
---
The goal of the project is to predict whether or not a DonorsChoose.org project proposal submitted by a teacher will be approved, using the text of project descriptions as well as additional metadata about the project, teacher, and school.

## Dataset

The `train.csv` data set provided by DonorsChoose contains the following features:

|Feature | Description|
|----------|---------------|
|**`project_id`** | A unique identifier for the proposed project. **Example:** `p036502`|   
|**`project_title`**| Title of the project. **Examples:**<br> ```Art Will Make You Happy!```| 
|**`project_grade_category`**| Grade level of students for which the project is targeted. One of the following enumerated values: **```Grades PreK-2, Grades 3-5, Grades 6-8, Grades 9-12```**|  
|**`project_subject_categories`**| One or more (comma-separated) subject categories for the project from the following list of values:  **```Applied Learning, Care & Hunger, Health & Sports, History & Civics, Literacy & Language, Math & Science, Music & The Arts, Special Needs, Warmth```**<br> **Examples:** ```Music & The Arts Literacy & Language, Math & Science```|
|**`school_state`** | State where school is located ([Two-letter U.S. postal code](https://en.wikipedia.org/wiki/List_of_U.S._state_abbreviations#Postal_codes)). **Example:** `WY`|
|**`project_subject_subcategories`** | One or more (comma-separated) subject subcategories for the project. **Examples:** ```Literature & Writing, Social Sciences```|
|**`project_resource_summary`** | An explanation of the resources needed for the project. **Example:** My students need hands on literacy materials to manage sensory needs!|
|**`project_essay_1`**    | Introduce us to your classroom|
|**`project_essay_2`**    | Tell us more about your students| 
|**`project_essay_3`**    | Describe how your students will use the materials you're requesting |
|**`project_essay_4`**    | Close by sharing why your project will make a difference|
|**`project_submitted_datetime`** | Datetime when project application was submitted. **Example:** `2016-04-28 12:43:56.245`|   
|**`teacher_id`** | A unique identifier for the teacher of the proposed project. **Example:** `bdf8baa8fedef6bfeec7ae4ff1c15c56`|  
|**`teacher_prefix`** | Teacher's title. One of the following enumerated values: **```nan, Dr. ,Mr., Mrs.  ,Ms. ,Teacher```**.|
|**`teacher_number_of_previously_posted_projects`** | Number of project applications previously submitted by the same teacher. **Example:** `2`|

Additionally, the `resources.csv` data set provides more data about the resources required for each project. Each line in this file represents a resource required by a project:

Feature | Description 
----------|---------------
**`id`** | A `project_id` value from the `train.csv` file.  **Example:** `p036502`   
**`description`** | Desciption of the resource. **Example:** `Tenor Saxophone Reeds, Box of 25`   
**`quantity`** | Quantity of the resource required. **Example:** `3`   
**`price`** | Price of the resource required. **Example:** `9.95`   

**Note:** Many projects require multiple resources. The `id` value corresponds to a `project_id` in train.csv, so you use it as a key to retrieve all resources needed for a project:

The data set contains the following label (the value you will attempt to predict):

Label | Description
----------|---------------
**`project_is_approved`** | A binary flag indicating whether DonorsChoose approved the project. A value of `0` indicates the project was not approved, and a value of `1` indicates the project was approved.



## Exploratory Data Analysis

* Univariate Analysis
  * Distribution of target variable
  * Distribution of categorical variables
    * Distribution of School State with respect to target variable(Acceptance Rate) and number of projects applied: Have a look at the extrem values
    * Distribution of Teacher Prefix with respect to target variable(Acceptance Rate) and number of projects applied: Have a look at the extrem values
    * Distribution of Project Grade Category with respect to target variable(Acceptance Rate) and number of projects applied: Have a look at the extrem values
    * Distribution of Project Subject Categories with respect to target variable(Acceptance Rate) and number of projects applied: Have a look at the extrem values
    * Distribution of Project Subject Subcategories with respect to target variable(Acceptance Rate) and number of projects applied: Have a look at the extrem values
    * Title of the project length vs target variable(Acceptance Rate)
    * Resource summary length vs target variable(Acceptance Rate)
    * Number of previously posted projects by the same teacher vs target variable(Acceptance Rate)
    * Relation between number of previously posted projects by the same teacher and acceptance rate
  * Distribution of numerical variables
    * Cost of the project vs target variable(Acceptance Rate) and distribution of cost of the project

* Bivariate Analysis

## Data Preprocessing

* Preprocessing of Categorical Features
  * School State
  * Teacher Prefix
  * Project Grade Category
  * Project Subject Categories
  * Project Subject Subcategories

The First step is to convert all the features into standard names so that they do not have any spaces in between and one categorie is a single word. Now we have two choices for categorical features conversion.
  * Convert them into ordinal numbers using LabelEncoder. (But inherent order is not present in the categories)
  * Convert them into one hot encoding using OneHotEncoder

These choices are dependent upon the model we select because a model like Naive bayse or decision tree would be able to directly able to use the ordinal values but a model like logistic regression or SVM would be able to use the one hot encoding. So we will try both the approaches and see which one works better.

Here we have to choices for features which are a list of categories:
  * Convert them into a single category by concatenating all the categories
  * Convert them into multiple categories and use them as a bag of words vector

If we have a limited number of categories when concatened then we can use the first approach but if the number of categories is large then we can use the second approach.

* Preprocessing of Numerical Features
  * Teacher Number of Previously Posted Projects
  * Price of the Project
We have to approches for preprocessing numerical features:
  * Standardize the data using StandardScaler
  * MinMax Scaler to scale the data

* Text Preprocessing
  * Project Title
  * Project Essay
  * Project Resource Summary

Text preprocessing can be done is sereveral different manners we have based on how we want to represent the text vectores. For methods like TF-IDF, Bag of Words we do the following steps.

* Lower case the text
* Tokenize the text
* Remove stop words
* Remove words with numbers ( Depend on the problem statement)
* Remove words with special characters (Depend on the problem statement)
* Remove purturations and irregular words.
* Stemming or Lemmatization

Ones we have a clean corpus we can make vectores like TF-IDF, Bag of Words, etc. We have few more considerations when using TF-IDF and Bag of Words. We can use n-grams to capture the context of the words. We can also use the frequency of the words as a feature. We can also use the IDF values as a feature. We can also use the TF-IDF values as a feature. We can also use the TF-IDF weighted word2vec as a feature.


If we are using word2vec kind of method then we do not need to do all the above steps. We can just tokenize the text and use it and and when we encounter a UNK token we can use the word2vec model to get the vector for the word. The summazation of the vectors of all the words in the sentence is the vector for the sentence. These are dense work vectors. This will be same if we are using BERT or any other transformer based model. The vector corresponding to the CLS token is the vector for the sentence.

## Machine Learning Models
This is a classification problem we have follwing models to try.
* Naive Bayes, Decision Tree, Random Forest, XGBoost

  The this can handle ordinal features.

* SVM, Logistic Regression

  These models can handle only one hot encoded features. The oridinal features are not suitable because they have an inherent order in them and we are learning weights for each feature. In both the models.

## Results

Here are only present the results for the best model we have tried different hyperparameters and features engineering techniques to get the best results. Out of all the models we have tried the best model is LSTM + NN and needs some explanation. We used LSTM to get the feature embedding for the text data and then we used embedding matrix for each categorical feature and the numerical features are used as it is. We then concatenated all the features and passed it through a neural network to get the final result.

| Model |Train AUC | Test AUC |
|-------|----------|
|KNN|1.000|0.560|
| Naive Bayes| 0.715 | 0.650 |
| Decision Tree| 0.686 | 0.685 |
| GBDT |0.747 | 0.710 |
| LSTM + NN | 0.844 | 0.754|
