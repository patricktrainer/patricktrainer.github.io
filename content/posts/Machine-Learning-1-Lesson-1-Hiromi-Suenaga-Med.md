
---
    title: Machine-Learning-1-Lesson-1-Hiromi-Suenaga-Med
    date: 2021-01-01    
    draft: true
    tags: []
---
# Machine-Learning-1-Lesson-1-Hiromi-Suenaga-Med[1*ZzaVXSfj0SCERQUCnQljpw.png](Machine%20Learning%201%20Lesson%201%20-%20Hiromi%20Suenaga%20-%20Med%2054b5bb82ebf4439fb80044ea6105c638/1ZzaVXSfj0SCERQUCnQljpw.png)
# Syllabus in brief
Depending on time and class interests, we’ll cover something like (not necessarily in this order):
Train vs. test
- Effective validation set construction
Trees and ensembles
- Creating random forests
- Interpreting random forests
What is ML?
Ethical considerations
Skip:
- Dimensionality reduction
- Interactions
- Monitoring training
- Collaborative filtering
- Momentum and LR annealing
# Random Forest: Blue Book for Bulldozers
```
%load_ext autoreload%autoreload 2%matplotlib inlinefrom fastai.imports import *from fastai.structured import *from pandas_summary import DataFrameSummaryfrom sklearn.ensemble import RandomForestRegressor, RandomForestClassifierfrom IPython.display import display
```
Data science ≠Software engineering [[08:43](https://youtu.be/CzdWqFTmn0Y?t=8m43s)].
**Unstructured data**: Images
`pandas` is the most important library when you are working with structured data which is usually imported as `pd`.
The variable we want to predict is called **Dependent Variable** in this case our dependent variable is `SalePrice`
**Question**: Should you never look at the data because of the risk of overfit?
- Create an instance of an object for the machine learning model
- Call `fit` by passing in the independent variables (the things you are going to use to predict) and dependent variable (the thing you want to predict).
It is important that validation and test sets will use the same category mappings (in other words, if you used 1 for “high” for a training dataset, then 1 should also be for “high” in validation and test datasets).
```
df, y, nas = proc_df(df_raw, 'SalePrice')
```
proc_df in structured.py
- `df` — data frame
- `y_fld` — name of the dependent variable
- It makes a copy of the data frame, grab the dependent variable values (`y_fld`), and drop the dependent variable from the data frame.
