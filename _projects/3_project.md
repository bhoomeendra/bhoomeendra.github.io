---
layout: page
title: Microsoft Malware Detection
description: a project that redirects to another website
img: assets/img/microsoft.jpg
importance: 3
category: Work
---

The project is about classifing malware we are provided with a dataset of contaning 9 classes of malaware. The dataset is provided by Microsoft and is available on [Kaggle](https://www.kaggle.com/c/malware-classification/data). The dataset is huge and contains 10,868 files.

## Dataset

For each malware we are provided with a file containing the assembly code and a file containing the byte code. The dataset is divided into 9 classes. The classes are as follows:
1. Ramnit
2. Lollipop
3. Kelihos_ver3
4. Vundo
5. Simda
6. Tracur
7. Kelihos_ver1
8. Obfuscator.ACY
9. Gatak

The challenging part of the problem is to extract features out of the dataset.

## Data Exploration

1. Data is imbalanced as the no. of samples in each class are significantly different.<img src="/assets/img/distribution.png" width="400" height="300">
2. Distribution of the size of the files in the dataset.


## Data Preprocessing

1. The data is in the form of assembly code and byte code. We need to extract features out of it. For that we used bag of words approach. We extracted uni-grams, bi-grams from the binary files and assembly files. We also extracted the frequency of the uni-grams and bi-grams.

2. Image features: We also extracted image features from the binary files so each binary number in the file is represented as a pixel in the image. We extracted first 800 pixels of the images formed from the binary files. This is has been shown to work in one of the best solutions to the problem.

3. We also extracted the size of the files as a feature.

## Model

For the model part we used xgboost classifier and trained it on the features extracted from the dataset. We achieved an log loss of 0.0203 on the test split of the dataset.

