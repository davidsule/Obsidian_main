# Scaling

notebook: FYP_imaging_evaluating_features


# Feature Selection

## Variance Threshold

remove low variance

## Univariate feature selection

sklearn: can be a pre-processing stop to an estimator
selecting the best features based on univariate statistical tests
select k best, percentile, based on false poz / fals discovery rate / familiy-wise error rate, or configurable strategy

chi^2 exxample for analyzing how many features are the best: https://scikit-learn.org/stable/auto_examples/svm/plot_svm_anova.html#sphx-glr-auto-examples-svm-plot-svm-anova-py
other info on how to select best nr of features: https://machinelearningmastery.com/feature-selection-with-numerical-input-data/

## mutual_info_classif

Mutual information (MI) [[1]](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.mutual_info_classif.html#r50b872b699c4-1) between two random variables is a non-negative value, which measures the dependency between the variables. It is equal to zero if and only if two random variables are independent, and higher values mean higher dependency.
Measure: mutual information gain: from the whole set of features, how much information do we get out with given param. The distribution/variance of one param might contain info about the other one, this is the mutual information gain. The param with the highest value gives the most info about the featureset in general. (also, entropy stuff)

[Mutual information](https://en.wikipedia.org/wiki/Mutual_information) is calculated between two variables and measures the reduction in uncertainty for one variable given a known value of the other variable.

> A quantity called mutual information measures the amount of information one can obtain from one random variable given another.

Notebook: FYP_imaging_evaluating_features
```python
import matplotlib.pyplot as plt

import numpy as np

import pandas as pd

# Univariate feature selection with mutual information for feature scoring

from sklearn.feature_selection import mutual_info_classif, SelectKBest


selector = SelectKBest(mutual_info_classif, k=2)

selector.fit(X, y)

  
# Show the feature scores

scores = selector.scores_


  

fig, ax = plt.subplots()

ax.bar(np.arange(0,num_total_features-1), scores, width=.2)

ax.set_xlabel('feature index')

ax.set_ylabel('mutual information')
```

```python
# Use the selector to actually only leave the features with the high scores

X_after_selection = selector.transform(X)

print(X_after_selection.shape)
```

### Chi^2

Not applicable: features must be Bool of frequency (I think) (I don't think you can use numerical as feature)

### Anova (f_classif)
Analysis of variance


## Select nr of features

chi^2 exxample for analyzing how many features are the best: https://scikit-learn.org/stable/auto_examples/svm/plot_svm_anova.html#sphx-glr-auto-examples-svm-plot-svm-anova-py
other info on how to select best nr of features: https://machinelearningmastery.com/feature-selection-with-numerical-input-data/


# Classification

- KNN
- Decision tree#
- Logistic Regression


Univariate:
- Anova (f_classif)
- mutual info


RFE is a wrapper type




- logistic regression
- Anova
- mutual info



Automatic selection of nr of features
GridSearch: take a selection algorithms, take a model, put them in a pipeline, then run them in the gridsearch (grid set up to examine nr of features from 1 to all), it test how many is the best by doing the model on each step, then does the cross-validation (that you can also set up -> stratified)
https://machinelearningmastery.com/feature-selection-with-numerical-input-data/
RFECV loop:
1. RFE
2. Cross-validation 
https://machinelearningmastery.com/rfe-feature-selection-in-python/

Cross validation:
- **Stratified:** The splitting of data into folds may be governed by criteria such as ensuring that each fold has the same proportion of observations with a given categorical value, such as the class outcome value. This is called [stratified cross-validation](https://machinelearningmastery.com/cross-validation-for-imbalanced-classification/).
- **Train/Test Split**: Taken to one extreme, k may be set to 2 (not 1) such that a single [train/test split](https://machinelearningmastery.com/train-test-split-for-evaluating-machine-learning-algorithms/) is created to evaluate the model.

https://machinelearningmastery.com/k-fold-cross-validation/


Decision Tree
Random Forest
KNN