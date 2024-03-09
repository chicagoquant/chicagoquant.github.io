
<details><summary>regression sm.OLS</summary>

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
```

- prepare X dataframe
```python
X = pd.DataFrame({'intercept': np.ones(df.shape[0]),
                 'X1': df.X1})
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
