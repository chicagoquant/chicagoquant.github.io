# Pandas

```python
import numpy as np, pandas as pd
s = pd.Series([1, 3, 5, 6, 8])
dates = pd.date_range('20240101', periods=6)
# [2024-01-01, ..., 2024-01-06]

df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=['A', 'B', 'C', 'D'])
df = pd.DataFrame({
    "A": 1.0,
    "B": pd.Timestamp("20240101"),
    "C": pd.Series(1, index=list(range(4)), dtype='float32'),
    "D": np.array([3]*4, dtype='int32'),
    "E": pd.Categorical(["test", "train", "test", "train"]),
    "F": "foo",
})
df.dtypes

df.head()
df.tail(3)
df.index
df.columns
df.to_numpy()   # np.array([...])
df.describe()
df.T            # transpose
df.sort_index(axis=1, ascending=False)    # columns in decreasing order: 'D', 'C', 'B', 'A'
df.sort_values(by="B")

# selection
df["A"]
df[0:3]
df["20240101":"20240103"]
df.loc[dates[0]]
df.loc[:, ["A","B"]]

df.iloc[3]
df.iloc[3:5, 0:2]

df[df["A"] > 0]
df[df > 0]
df2 = df.copy()
```

# Kaggle Lessons

https://www.kaggle.com/learn/pandas

```python
df = pd.DataFrame({'Col 1': [1, 2, 3]}, index=[100, 200, 300], name='DF1')
df = pd.read_csv(path_to_csv, index_col=0)
s = pd.Series([1, 2, 3], index=[100, 200, 300])
df.to_csv(path_to_csv)

pd.set_option('display.max_rows', 5)

df.iloc[row_index]
df.loc[index_values]
df.loc[selection]

isin(...)
pd.isnull()
pd.notnull()

df.col.unique(), nunique(), value_counts()

describe, mean, median, unique, value_counts()
idxmax()
series.map(lambda_by_value)
df.apply(lambda_by_row, axis='columns')

grouped = df.groupby(col1)
grouped = df.groupby([col1,...])
grouped.size(), count(), mean(), len(), min(), max()
df2 = grouped.colN.mean()
df2 = grouped.colN.agg(mean)
df2 = grouped.colN.agg([len, min, max, mean])
df2 = grouped.apply(lambda_by_df)
grouped.reset_index()
df.sort_values(by='col', ascending=False)
df.sort_values(by=['col1','col2'], ascending=False)
df.sort_index()

df.dtypes
df.col.dtype
df.col.astype('newtype')

df.col.fillna('Unknown')
df.col.replace('oldstr', 'newstr')

df.rename(columns={'oldname':'newname',})
df.rename(index={0:'rownewindex1',1:'rownewindex2',}) # use set_index() instead

df = pd.concat([ df1, df2 ])
df = df1.join(df2, lsuffix='_L', rsuffix='_R') # suffix for columns that have same name
Join is relational join, like SQL/RDBMS

df2 = df.copy()
y = df.pop("colY")

df['categorized'], uniqs = df.categorical_col.factorize()  # gives unique integer value for categories
df2 = pd.get_dummies(df.col)       # creates new columns for each category
```

# Intro to Machine Learning

https://www.kaggle.com/learn/intro-to-machine-learning

```python
from sklearn.tree import DecisionTreeRegressor

model = DecisionTreeRegression(random_state = 1)
model.fit(X, y)
new_y = model.predict(new_X)

from sklearn.metrics import mean_absolute_error
mae = mean_absolute_error(y, new_y)


from sklearn.model_selection import train_test_split
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 1)

model = DecisionTreeRegression(max_leaf_nodes=50, random_state = 1)

def get_mae(max_leaf_nodes, train_X, val_X, train_y, val_y):
    model = DecisionTreeRegressor(max_leaf_nodes=max_leaf_nodes, random_state=0)
    model.fit(train_X, train_y)
    preds_val = model.predict(val_X)
    mae = mean_absolute_error(val_y, preds_val)
    return(mae)


from sklearn.ensemble import RandomForestRegressor
model = RandomForestRegressor(random_state=1)
```

# Intermediate Machine Learning

https://www.kaggle.com/learn/intermediate-machine-learning

```python
train_X, val_X, train_y, val_y = train_test_split(X, y, train_size=0.8, test_size=0.2, random_state = 1)

features = ['LotArea', 'YearBuilt', '1stFlrSF', '2ndFlrSF', 'FullBath', 'BedroomAbvGr', 'TotRmsAbvGrd']

model = RandomForestRegressor(n_estimators=100, random_state=1)
model = RandomForestRegressor(n_estimators=100, criterion='absolute_error', random_state=1)
model = RandomForestRegressor(n_estimators=100, min_samples_split=20, random_state=1)
model = RandomForestRegressor(n_estimators=100, max_depth=7, random_state=1)

def score_model(model, X_t, X_v, y_t, y_v):
    model.fit(X_t, y_t)
    preds = model.predict(X_v)
    return mean_absolute_error(y_v, preds)
```

# Missing Data

```python
df1 = df.drop([col1, col2], axis=1)
df2 = df.select_dtypes(exclude=['object'])    # exclude string columns

# drop columns with null values
cols_with_missing = [col for col in df.columns if df[col].isnull().any()]
reduced_df = df.drop(cols_with_missing, axis=1)

from sklearn.impute import SimpleImputer

my_imputer = SimpleImputer(strategy='mean')   # median, constant, most_frequent
my_imputer.fit(X)                               # figure out column averages
new_X = pd.DataFrame(my_imputer.transform(X))   # fill null values with column average
new_X = pd.DataFrame(my_imputer.fit_transform(X), columns=X.columns)
new_X.columns = X.columns                       # columns got removed

# add a column of whether imputed
for col in cols_with_missing:
    X[col + '_was_missing'] = X[col].isnull()
```

# Categorical Variables

```python
from sklearn.preprocessing import OrdinalEncoder
labeled_X = X.copy()
encoder = OrdinalEncoder()
labeled_X[cols_with_labels] = encoder.fit_transform(X[cols_with_labels])
labeled_X[cols_with_labels] = encoder.transform(X)

from sklearn.preprocessing import OneHotEncoder
labeled_X = X.copy()
encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
labeled_X = pd.DataFrame(encoder.fit_transform(X[cols_with_labels]), index=X.index)
labeled_X = pd.DataFrame(encoder.transform(X[cols_with_labels]), index=X.index)
labeled_X.columns = labeled_X.columns.astype(str)

OH_X_train = pd.concat([numeric_X_train, labeled_X_train], axis=1)
```

# Pipeline

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

X_train_full, X_valid_full, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2, random_state=0)

categorical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and X_train_full[cname].dtype == "object"]
numerical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

my_cols = categorical_cols + numerical_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()

numerical_transformer = SimpleImputer(strategy='constant')
categorical_transformer = Pipeline(
    steps = [
        ( 'imputer', SimpleImputer(strategy='most_frequent') ),
        ( 'onehot', OneHotEncoder(handle_unknown='ignore') ),
    ])

preprocessor = ColumnTransformer(
    transformers = [
        ( 'num', numerical_transformer, numerical_cols ),
        ( 'cat', categorical_transformer, categorical_cols ),
    ])

model = RandomForestRegressor(n_estimators=100, random_state=0)

my_pipeline = Pipeline(
    steps = [
        ( 'preprocessor', preprocessor ),
        ( 'model', model ),
    ])

my_pipeline.fit(X_train, y_train)

predictions = my_pipeline.predict(X_valid)

score = mean_absolute_error(y_valid, predictions)
print("MAE:", score)
```

# Cross-Validation

```python
from sklearn.model_selection import cross_val_score
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
                              scoring='neg_mean_absolute_error')
mae = scores.mean()


def get_score(n_estimators):
    """Return the average MAE over 3 CV folds of random forest model.

    Keyword argument:
    n_estimators -- the number of trees in the forest
    """
    my_pipeline = Pipeline(steps=[
        ('preprocessor', SimpleImputer()),
        ('model', RandomForestRegressor(n_estimators=n_estimators, random_state=0))
    ])
    scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=3,
                              scoring='neg_mean_absolute_error')
    return scores.mean()
```

See also:
```
	Hyperparameter optimization
	Grid search
	GridSearchCV()
```

# Gradient Boosting

```python
from xgboost import XGBRegressor

my_model = XGBRegressor(random_state=0)
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05, n_jobs=4)
my_model.fit(X_train, y_train,
             early_stopping_rounds=5,
             eval_set=[(X_valid, y_valid)],
             verbose=False)
mae = mean_absolute_error(predictions, y_valid)
```

# Feature Engineering

https://www.kaggle.com/code/ryanholbrook/what-is-feature-engineering

## Mutual Information

```python
from sklearn.feature_selection import mutual_info_regression
discrete_features = X.dtypes == int
mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)

def make_mi_scores(X, y):
    X = X.copy()
    for colname in X.select_dtypes(["object", "category"]):
        X[colname], _ = X[colname].factorize()
    # All discrete features should now have integer dtypes
    discrete_features = [pd.api.types.is_integer_dtype(t) for t in X.dtypes]
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features, random_state=0)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores

def plot_mi_scores(scores):
    scores = scores.sort_values(ascending=True)
    width = np.arange(len(scores))
    ticks = list(scores.index)
    plt.barh(width, scores)
    plt.yticks(width, ticks)
    plt.title("Mutual Information Scores")

# Set Matplotlib defaults
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)

# horizontal bars
plt.figure(dpi=100, figsize=(8,5))
plt.barh(width, barvalues)
plt.yticks(width, ticks)
plt.title("Some title")

sns.regplot(x="col1", y="col2", data=df)

features = ["YearBuilt", "MoSold", "ScreenPorch"]
sns.relplot(
    x = "value",
    y = "SalePrice",
    col = "variable",
    data = df.melt( id_vars = "SalePrice", value_vars=features),
    facet_kws=dict(sharex=False),
);

sns.catplot(x="col1", y="col2", data=df, kind="boxen")
```

# Data Visualization
https://www.kaggle.com/learn/data-visualization

```python
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

fifa_data = pd.read_csv(fifa_filepath, index_col="Date", parse_dates=True)
```

## Line Chart
```python
# Set Matplotlib defaults
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)

plt.figure(figsize=(16,6)) # 16 inches wide x 6 inches tall
plt.title("Some title")
sns.lineplot(data=df)
sns.lineplot(data=df[col], label="Some label")
plt.xlabel("x-axis label")
```

## Bar Chart
```python
plt.figure(figsize=(10,6))
plt.title("Some title")
sns.barplot(x=df.index, y=df['Col1'])
sns.barplot(y=df.index, x=df.Col1) # for horizontal bars
plt.ylabel("y-axis label")
plt.xlabel("x-axis label")
```

## Heatmap
```python
sns.heatmap(data=df, annot=True)
```

## Scatter Plot
```python
sns.scatterplot(x=df.col1, y=df.col2)
sns.regplot(x=df.col1, y=df.col2)              # add a regression line

sns.scatterplot(x=df.col1, y=df.col2, hue=df.col3)   # color based on col3, with values like yes, no
sns.lmplot(x="col1", y="col2", hue="col3", data=df)  # 2 different regression lines, for each color
sns.lmplot(x="col1", y="col2", hue="col3", col="col3", data=df, scatter_kws=dict(edgecolor='w'), col_wrap=3, height=4)
```

## Swarm Plot
```python
sns.swarmplot(x=df.col3, y=df.col2)     # x-axis is category, like yes/no
```

## Histogram
```python
sns.histplot(df.col1)
sns.histplot(data=df, x='col1', hue='col2')
```

## Density Plot

```python
sns.kdeplot(data=df.col1, shade=True)
sns.kdeplot(data=df, x='col1', hue='col2', shade=True)

sns.jointplot(x=df.col1, y=df.col2, kind='kde')
```

## Set Style
```python
sns.set_style("dark") # darkgrid, whitegrid, white, dark, ticks
```

https://www.kaggle.com/learn

https://www.kaggle.com/competitions/titanic

https://www.kaggle.com/chicagoquant/code?scroll=true