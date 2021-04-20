```python
import pandas as pd

df = pd.read_csv('input.txt', sep='\t', header=None)
df2 = df.iloc[:, [1, 0]]
df2.columns = [0, 1]
df = pd.concat([df, df2])
df = df.groupby(df.columns[0]).agg('count').reset_index()
df.columns = ['person', 'links_count']
df = df.sort_values(by=['links_count', 'person'], ascending=[False, True])
print(df.head().to_string(index=False))
```
