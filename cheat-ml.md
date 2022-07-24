
<details><summary>regression sm.OLS - simple linear regression</summary>

- import modules
  ```python
  import numpy as np
  import pandas as pd
  import statmodels.api as sm
  ```

- load data
  ```python
  df = pd.read_csv(datafile)
  df.columns

  df = ISLP.load_data(Dataset)
  df.columns
  ```

- prepare X dataframe

  ```python
  X = pd.DataFrame({'intercept': np.ones(df.shape[0]), 'X1': df.X1})
  X.head()

  y = df.Y
  ```

- fit the model

  ```python
  model = sm.OLS(y, X)
  results = model.fit()
  ```

- look at the results
  ```python
  from ISLP.models import summarize
  summarize(results)
  results.params
  results.summary()
  ```

- predict
  ```python
  newX = pd.DataFrame({'X1': [100, 200, 300]})
  estimatedY = results.get_predictions(newX)
  estimatedY.predicted_mean()
  ```
</details>

<details><summary>regression sm.OLS - multiple linear regression</summary>

- model with 3 variables, 1 of them not associated with the response

  ```python
  Adv = ISLP.load_data('/content/drive/MyDrive/Colab Notebooks/ISLP_Data/Advertising')

  design = MS(['TV', 'radio', 'newspaper'])
  X = design.fit_transform(Adv)
  model = sm.OLS(Adv.sales, X)   # sales ~ intercept, TV, radio, newspaper
  results = model.fit()

  estimates = results.get_prediction(X)
  yhat = estimates.predicted_mean

  n, p = Adv.shape[0], 3
  RSE = np.sqrt(np.sum((Adv.sales - y1.predicted_mean)**2)/(n-p-1))
  results.summary()
  RSE
  ```

- with interaction between variables

  ```python
  Adv = ISLP.load_data('/content/drive/MyDrive/Colab Notebooks/ISLP_Data/Advertising')

  design = MS(['TV', 'radio', ('TV', 'radio')])
  X = design.fit_transform(Adv)
  model = sm.OLS(Adv.sales, X)   # sales ~ intercept, TV, radio, TV x radio
  results = model.fit()

  estimates = results.get_prediction(X)
  yhat = estimates.predicted_mean
  conf_interval = estimates.conf_int(alpha=0.05)            # 95% CI
  pred_interval = estimates.conf_int(obs=True, alpha=0.05)  # 95% PI

  n, p = Adv.shape[0], 3
  RSE = np.sqrt(np.sum((Adv.sales - y1.predicted_mean)**2)/(n-p-1))
  results.summary()
  RSE

  R2 = results.rsquared
  RSE = np.sqrt(results.scale)
  # collinearity effect, VIF
  from statsmodels.stats.outliers_influence import variance_inflation_factor as VIF
  vif = VIF(X, col_idx)

  vals = [ VIF(X, i) for i in range(1, X.shape[1]) ]
  vifs = pd.DataFrame({'vif': vals, index=X.columns[1:])
  ```

- with polynomial terms
  ```python
  X = MS([poly('lstat', degree=2), 'age']).fit_transform(Boston)

  fittedvalues = yhat = results.fittedvalues
  residuals = results.resid

  anova_lm(results1, results3)
  ```

- with qualitative predictors
  ```python
  MS(columns) will automatically figure out which columns are categorical, and use dummy variables for them
  ``
</details>
