---
title: Classification
date: 2020-08-26 17:04:38
categories:
- Book
- Data Mining
tags:
- Machine Learning
- DNN
- Signal Processing
- Statistics
mathjax: true
---
# Classification

> A form of data analysis that extracts models describing important data classes

1. Learning step : A classifier is built describing a predetermined set of data classes or concepts
2. Classification step : The model is used to predict class labels for given data

## Model Evaluation and Selection

|Measure|Formula|
|:-:|:-:|
|accuracy, recognition rate|$\frac{TP+TN}{P+N}$|
|error rate, misclassification|$\frac{FP+FN}{P+N}$|
|sensitivity, true positive rate, recall|$\frac{TP}{P}$|
|specificity, true negative rate|$\frac{TN}{N}$|
|precision|$\frac{TP}{TP+FP}$|

<!-- More -->

+ True positives ($TP$) : 참인 데이터를 참으로 분류
+ True negatives ($TN$) : 거짓인 데이터를 거짓으로 분류
+ False positives ($FP$) : 거짓인 데이터를 참으로 분류
+ False negatives ($FN$) : 참인 데이터를 거짓으로 분류

|Actual class\Predicted class|yes|no|Total|
|:-:|:-:|:-:|:-:|
|yes|$TP$|$FN$|$P$|
|no|$FP$|$TN$|$N$|
|Total|$P'$|$N'$|$P+N$|

$$
accuracy=\frac{TP+TN}{P+N}
$$
$$
error\ rate=\frac{FP+FN}{P+N}
$$

## Techniques to Improve Classification Accuracy

### Bagging

+ $n$크기의 Training set $D$가 주어졌을 때, 배깅은 $m$개의 복원 표본추출 방법과 균등 확률분포를 이용해 각각 $n'$크기를 갖는 새로운 훈련 집합 $D_i$를 생성
+ 복원 표본추출 방법에 의해 일부 관측 데이터는 각 $D_i$에서 반복해서 나타날 수 있음
+ 만약 $n'=n$이라고 하면, 보다 큰 $n$에 대해 집합 $D_i$는 $D$에 대해 고유한 샘플의 비율은 $1-\frac{1}{e}$을 가질 것으로 기대됨
+ 이러한 샘플을 Bootstrap 샘플이라 함
+ $m$개의 모델은 $m$개의 Bootstrap 샘플들을 이용해 만들어지고 결과를 평균(in regression) 또는 투표(in classification)를 통해 결합

### Improving Classification Accuracy of Class-Imbalanced Data

+ Oversampling : 부족한 데이터를 Resampling
+ Undersampling : 많은 데이터를 Decreasing
+ Threshold-moving
+ Ensemble techniques

# Advanced Methods

## Bayesian Belief Networks



## Classification by Backpropagation

### A Multilayer Feed-Forward Neural Network

![Feed-Forward Neural Network](https://user-images.githubusercontent.com/42334717/89788337-f3f95f00-db59-11ea-9b1e-6cf13e2c398a.png)
