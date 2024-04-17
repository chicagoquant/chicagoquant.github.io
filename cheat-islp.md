# Data

| Dataset | Filename |
|---|---|
| NCI60 | labels(Y) = NCI60labs.csv, features(X) = NCI60data.npy |
| Khan | Khan\_xtrain.csv, Khan\_ytrain.csv, Khan\_xtest.csv, Khan\_ytest.csv |
| Hitters | Hitters.csv |
| Carseats | Carseats.csv |
| NYSE | NYSE.csv |
| Publication | Publication.csv |
| BrainCancer | BrainCancer.csv |
| Bikeshare | Bikeshare.csv |
| Wage | Wage.csv |
| Auto | Auto.csv |
| Boston | Boston.csv |
| Caravan | Caravan.csv |
| College | College.csv |
| Credit | Credit.csv |
| Default | Default.csv |
| Fund | Fund.csv |
| OJ | OJ.csv |
| Portfolio | Portfolio.csv |
| Smarket | Smarket.csv |
| Weekly | Weekly.csv |

# Ch 2 -- Statistical Learning

```python
print('fit a model with', 11, 'variables')

print?

3+5

'hello' + ' ' + 'world'

x = [3, 4, 5]
y = [4, 9, 7]
x + y                           # list concat

import numpy as numpy

x = np.array([3,4,5])
y = np.array([4,9,7])
x + y                           # add items

x = np.array([[1, 2], [3, 4]])
x
x.ndim                          # 2
x.dtype                         # dtype('int64')

y = np.array([[1, 2], [3.0, 4]])
y.dtype                         # dtype('float64')

np.array?
x = np.array([[1, 2], [3, 4]], float)
x.dtype                         # dtype('float64')

x.shape                         # (2,2)

x = np.array([1, 2, 3, 4])
x.sum()                         # 10
np.sum(x)

x = np.array([1, 2, 3, 4, 5, 6])
print('beginning x:\n', x)      # 1-d array
x_reshape = x.reshape((2, 3))   # 2 rows, 3 columns
print('reshaped x:\n', x_reshape)

x_reshape[0, 0]                 # 1
x_reshape[1, 2]                 # 6

# reshaped refers to the same space in memory as before
x[0]                            # 1
x_reshape[0, 0] = 10
x[0]                            # changed to 10

x_reshape.shape, x_reshape.ndim, x_reshape.T

np.sqrt(x)
x**0.5

x = np.random.normal(size=50)
x                               # x ~ N(0,1)
y = x + np.random.normal(loc=50, scale=1, size=50)
y                               # y ~ N(50,1) + N(0,1)

np.corrcoef(x, y)

rng = np.random.default_rng(1303)       # to get the same random value, set the seed to constant
print(rng.normal(scale=5, size=2))
rng2 = np.random.default_rng(1303)
print(rng2.normal(scale=5, size=2))     # same values generated as before

rng = np.random.default_rng(3)
y = rng.standard_normal(10)
np.mean(y)
y.mean()

np.var(y), y.var(), np.mean((y - y.mean())**2)

np.sqrt(np.var(y)), np.std(y)

X = rng.standard_normal((10, 3))
X

X.mean(axis=0)
X.mean(0)

# ----------------- graphics ------------------ #
from matplotlib.pyplot import subplots
fig, ax = subplots(figsize=(8, 8))
x = rng.standard_normal(100)
y = rng.standard_normal(100)
ax.plot(x, y);


output = subplots(figsize=(8, 8))
fig = output[0]
ax = output[1]

fig, ax = subplots(figsize=(8, 8))
ax.plot(x, y, 'o');

fig, ax = subplots(figsize=(8, 8))
ax.scatter(x, y, marker='o');

fig, ax = subplots(figsize=(8, 8))
ax.scatter(x, y, marker='o')            # no semicolon at end of line

fig, ax = subplots(figsize=(8, 8))
ax.scatter(x, y, marker='o')
ax.set_xlabel("this is the x-axis")
ax.set_ylabel("this is the y-axis")
ax.set_title("Plot of X vs Y");

fig.set_size_inches(12,3)
fig

fig, axes = subplots(nrows=2,
                     ncols=3,
                     figsize=(15, 5))

axes[0,1].plot(x, y, 'o')
axes[1,2].scatter(x, y, marker='+')
fig

fig.savefig("Figure.png", dpi=400)
fig.savefig("Figure.pdf", dpi=200);

axes[0,1].set_xlim([-1,1])
fig.savefig("Figure_updated.jpg")
fig

fig, ax = subplots(figsize=(8, 8))
x = np.linspace(-np.pi, np.pi, 50)
y = x
f = np.multiply.outer(np.cos(y), 1 / (1 + x**2))
ax.contour(x, y, f);

fig, ax = subplots(figsize=(8, 8))
ax.contour(x, y, f, levels=45);

fig, ax = subplots(figsize=(8, 8))
ax.imshow(f);

seq1 = np.linspace(0, 10, 11)
seq1

seq2 = np.arange(0, 10)
seq2

"hello world"[3:6]
"hello world"[slice(3,6)]

A = np.array(np.arange(16)).reshape((4, 4))
A

A[1,2]
A[[1,3]]
A[:,[0,2]]
A[[1,3],[0,2]]

np.array([A[1,0],A[3,2]])
A[[1,3],[0,2,3]]                    # error, shape mismatch

A[[1,3]][:,[0,2]]

idx = np.ix_([1,3],[0,2,3])
A[idx]

A[1:4:2,0:3:2]

keep_rows = np.zeros(A.shape[0], bool)
keep_rows
keep_rows[[1,3]] = True
keep_rows
np.all(keep_rows == np.array([0,1,0,1]))

A[np.array([0,1,0,1])]
A[keep_rows]

keep_cols = np.zeros(A.shape[1], bool)
keep_cols[[0, 2, 3]] = True
idx_bool = np.ix_(keep_rows, keep_cols)
A[idx_bool]

idx_mixed = np.ix_([1,3], keep_cols)
A[idx_mixed]

# ----------------- loading data ------------------ #
import pandas as pd
Auto = pd.read_csv('Auto.csv')
Auto

Auto = pd.read_csv('Auto.data', delim_whitespace=True)      # same data, but space delimited file (not csv)

Auto['horsepower']                                  # why is everything a string?

np.unique(Auto['horsepower'])                       # because there is a field with '?' in it, replace it

Auto = pd.read_csv('Auto.data',
                   na_values=['?'],
                   delim_whitespace=True)
Auto['horsepower'].sum()


Auto.shape                                          # 397 x 9

Auto_new = Auto.dropna()
Auto_new.shape                                      # 392 x 9


Auto = Auto_new # overwrite the previous value
Auto.columns

Auto[:3]

idx_80 = Auto['year'] > 80
Auto[idx_80]

Auto[['mpg', 'horsepower']]

Auto.index

Auto_re = Auto.set_index('name')
Auto_re

Auto_re.columns

rows = ['amc rebel sst', 'ford torino']
Auto_re.loc[rows]

Auto_re.iloc[[3,4]]
Auto_re.iloc[:,[0,2,3]]

Auto_re.iloc[[3,4],[0,2,3]]
Auto_re.loc['ford galaxie 500', ['mpg', 'origin']]

idx_80 = Auto_re['year'] > 80
Auto_re.loc[idx_80, ['weight', 'origin']]

Auto_re.loc[lambda df: df['year'] > 80, ['weight', 'origin']]

Auto_re.loc[lambda df: (df['year'] > 80) & (df['mpg'] > 30),
            ['weight', 'origin']
           ]

Auto_re.loc[lambda df: (df['displacement'] < 300)
                       & (df.index.str.contains('ford')
                       | df.index.str.contains('datsun')),
            ['weight', 'origin']
           ]

total = 0
for value in [3,2,19]:
    total += value
print('Total is: {0}'.format(total))

total = 0
for value in [2,3,19]:
    for weight in [3, 2, 1]:
        total += value * weight
print('Total is: {0}'.format(total))


total = 0
for value, weight in zip([2,3,19],
                         [0.2,0.3,0.5]):
    total += weight * value
print('Weighted average is: {0}'.format(total))

rng = np.random.default_rng(1)
A = rng.standard_normal((127, 5))
M = rng.choice([0, np.nan], p=[0.8,0.2], size=A.shape)
A += M
D = pd.DataFrame(A, columns=['food',
                             'bar',
                             'pickle',
                             'snack',
                             'popcorn'])
D[:3]


for col in D.columns:
    template = 'Column "{0}" has {1:.2%} missing values'
    print(template.format(col,
          np.isnan(D[col]).mean()))



fig, ax = subplots(figsize=(8, 8))
ax.plot(horsepower, mpg, 'o');                      # error

fig, ax = subplots(figsize=(8, 8))
ax.plot(Auto['horsepower'], Auto['mpg'], 'o');

ax = Auto.plot.scatter('horsepower', 'mpg')
ax.set_title('Horsepower vs. MPG');

fig = ax.figure
fig.savefig('horsepower_mpg.png');

Auto.cylinders = pd.Series(Auto.cylinders, dtype='category')
Auto.cylinders.dtype

fig, ax = subplots(figsize=(8, 8))
Auto.boxplot('mpg', by='cylinders', ax=ax);         # boxplot

fig, ax = subplots(figsize=(8, 8))
Auto.hist('mpg', ax=ax);

fig, ax = subplots(figsize=(8, 8))
Auto.hist('mpg', color='red', bins=12, ax=ax);      # a histogram

pd.plotting.scatter_matrix(Auto);

pd.plotting.scatter_matrix(Auto[['mpg',             # scatterplot matrix, pairwise relationship
                                 'displacement',
                                 'weight']]);

Auto[['mpg', 'weight']].describe()

Auto['cylinders'].describe()
Auto['mpg'].describe()
```

# Ch 3 -- Linear Regression

```python
import numpy as np
import pandas as pd
from matplotlib.pyplot import subplots

import statsmodels.api as sm

from statsmodels.stats.outliers_influence \
     import variance_inflation_factor as VIF
from statsmodels.stats.anova import anova_lm

from ISLP import load_data
from ISLP.models import (ModelSpec as MS,
                         summarize,
                         poly)

A = np.array([3,5,11])
dir(A)
A.sum()

Boston = load_data("Boston")
Boston.columns

X = pd.DataFrame({'intercept': np.ones(Boston.shape[0]),
                  'lstat': Boston['lstat']})
X[:4]

y = Boston['medv']
model = sm.OLS(y, X)
results = model.fit()

summarize(results)


design = MS(['lstat'])
design = design.fit(Boston)
X = design.transform(Boston)
X[:4]

design = MS(['lstat'])
X = design.fit_transform(Boston)
X[:4]

results.summary()

results.params

new_df = pd.DataFrame({'lstat':[5, 10, 15]})
newX = design.transform(new_df)
newX

new_predictions = results.get_prediction(newX);
new_predictions.predicted_mean

new_predictions.conf_int(alpha=0.05)

new_predictions.conf_int(obs=True, alpha=0.05)

def abline(ax, b, m):
    "Add a line with slope m and intercept b to ax"
    xlim = ax.get_xlim()
    ylim = [m * xlim[0] + b, m * xlim[1] + b]
    ax.plot(xlim, ylim)


def abline(ax, b, m, *args, **kwargs):
    "Add a line with slope m and intercept b to ax"
    xlim = ax.get_xlim()
    ylim = [m * xlim[0] + b, m * xlim[1] + b]
    ax.plot(xlim, ylim, *args, **kwargs)

# see also
# ax.axline((a0, b0), (a1, b1), linewidth=4, color='r'),
# ax.axline((a0, b0), slope=m, linewidth=4, color='r'),
# ax.axhline(y, color='k', linestyle='--') for horizontal line


ax = Boston.plot.scatter('lstat', 'medv')
abline(ax,
       results.params[0],
       results.params[1],
       'r--',
       linewidth=3)

ax = subplots(figsize=(8,8))[1]
ax.scatter(results.fittedvalues, results.resid)
ax.set_xlabel('Fitted value')
ax.set_ylabel('Residual')
ax.axhline(0, c='k', ls='--');

infl = results.get_influence()
ax = subplots(figsize=(8,8))[1]
ax.scatter(np.arange(X.shape[0]), infl.hat_matrix_diag)
ax.set_xlabel('Index')
ax.set_ylabel('Leverage')
np.argmax(infl.hat_matrix_diag)

# multiple lin reg
X = MS(['lstat', 'age']).fit_transform(Boston)
model1 = sm.OLS(y, X)
results1 = model1.fit()
summarize(results1)
US
terms = Boston.columns.drop('medv')
terms


X = MS(terms).fit_transform(Boston)
model = sm.OLS(y, X)
results = model.fit()
summarize(results)

minus_age = Boston.columns.drop(['medv', 'age'])
Xma = MS(minus_age).fit_transform(Boston)
model1 = sm.OLS(y, Xma)
summarize(model1.fit())

vals = [VIF(X, i)
        for i in range(1, X.shape[1])]
vif = pd.DataFrame({'vif':vals},
                   index=X.columns[1:])
vif

vals = []
for i in range(1, X.values.shape[1]):
    vals.append(VIF(X.values, i))


X = MS(['lstat',
        'age',
        ('lstat', 'age')]).fit_transform(Boston)
model2 = sm.OLS(y, X)
summarize(model2.fit())

X = MS([poly('lstat', degree=2), 'age']).fit_transform(Boston)
model3 = sm.OLS(y, X)
results3 = model3.fit()
summarize(results3)


anova_lm(results1, results3)

ax = subplots(figsize=(8,8))[1]
ax.scatter(results3.fittedvalues, results3.resid)
ax.set_xlabel('Fitted value')
ax.set_ylabel('Residual')
ax.axhline(0, c='k', ls='--')

Carseats = load_data('Carseats')
Carseats.columns

allvars = list(Carseats.columns.drop('Sales'))
y = Carseats['Sales']
final = allvars + [('Income', 'Advertising'),
                   ('Price', 'Age')]
X = MS(final).fit_transform(Carseats)
model = sm.OLS(y, X)
summarize(model.fit())


```

# Ch 4 -- Classification

# Ch 5 -- Resampling Methods

# Ch 6 -- Linear Model Selection and Regularization

# Ch 7 -- Moving Beyond Linearity

# Ch 8 -- Tree Based Methods

# Ch 9 -- SVM

# Ch 10 -- Deep Learning

# Ch 11 -- Survival Analysis and Censored Data

# Ch 12 -- Unsupervised Learning

# Ch 13 -- Multiple Testing