
<details><summary>regression sm.OLS</summary>

- import modules
  ```python
  import numpy as np
  import pandas as pd
  import statmodels.api as sm
  ```

- simple linear regression
  - load data
    ```python
    df = pd.read_csv(datafile)
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

- multiple linear regression
  ```python
  Adv = ISLP.load_data('/content/drive/MyDrive/Colab Notebooks/ISLP_Data/Advertising')
  X = pd.DataFrame({'intercept': np.ones(Adv.shape[0]), 'TV': Adv.TV, 'radio': Adv.radio, 'newspaper': Adv.newspaper })
  model = sm.OLS(Adv.sales, X)
  results = model.fit()
  design = MS(['TV', 'radio', 'newspaper'])
  X1 = design.fit_transform(X)
  y1 = results.get_prediction(X1)

  n, p = Adv.shape[0], 4
  RSE = np.sqrt(np.sum((Adv.sales - y1.predicted_mean)**2)/(n-p-1))
  results.summary()
  RSE
  ```

</details>
