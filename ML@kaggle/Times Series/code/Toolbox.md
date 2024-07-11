### `pd.Dataframe: Group by with mean`
- Raw CSV:
- | id  | date     | store_nbr | family       | sales | onpromotion |
| --- | -------- | --------- | ------------ | ----- | ----------- |
| 0   | 1/1/2013 | 1         | AUTOMOTIVE   | 0     | 0           |
| 1   | 1/1/2013 | 1         | BABY CARE    | 0     | 0           |
| 2   | 1/1/2013 | 1         | BEAUTY       | 0     | 0           |
| 3   | 1/1/2013 | 1         | BEVERAGES    | 0     | 0           |
| 4   | 1/1/2013 | 1         | BOOKS        | 0     | 0           |
| 5   | 1/1/2013 | 1         | BREAD/BAKERY | 0     | 0           |
| 6   | 1/1/2013 | 1         | CELEBRATION  | 0     | 0           |
| 7   | 1/1/2013 | 1         | CLEANING     | 0     | 0           |
| 8   | 1/1/2013 | 1         | DAIRY        | 0     | 0           |
```python
average_sales = store_sales.groupby('date').mean()['sales']
 ```
- |id|store_nbr|family|sales|onpromotion|
|---|---|---|---|---|
|date||||||
|---|---|---|---|---|---|
|2013-01-01|0|1|AUTOMOTIVE|0.000000|0|
|2013-01-01|1|1|BABY CARE|0.000000|0|
|2013-01-01|2|1|BEAUTY|0.000000|0|
|2013-01-01|3|1|BEVERAGES|0.000000|0|
|2013-01-01|4|1|BOOKS|0.000000|0|
|...|...|...|...|...|
---

### `sclearn: model.predict`
```python
model.predict(X) # return np.array

# map it with time and index, same time index as the training data
y_pred = pd.Series(model.predict(X),index=X.index) return np.array
 ```