## Scaling

notebook: FYP_imaging_evaluating_features


## Feature Selection

### Univariate feature selection, mutual_info_classif

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