# Scaling

notebook: FYP_imaging_evaluating_features


# Feature Selection

## Variance Threshold

remove low variance

## Univariate feature selection

sklearn: can be a pre-processing stop to an estimator
selecting the best features based on univariate statistical tests
select k best, percentile, based on false poz / fals discovery rate / familiy-wise error rate, or configurable strategy

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



## Classification

- KNN
- Decision tree