# Pandas

### Sort columns
* https://stackoverflow.com/questions/11067027/re-ordering-columns-in-pandas-dataframe-based-on-column-name
```python
df = df.reindex( sorted( df.columns ), axis = 1 )
```

### Concatenate horizontal direction
* https://stackoverflow.com/questions/44327999/python-pandas-merge-multiple-dataframes
```python
from functools import reduce
import pandas as pd

# It suppose that the index or record counts are same.
merged = reduce(
    lambda left, right: pd.merge( left, right, axis = 1 )
)
```

### Slice column side ( By index )
* Use iloc
* https://stackoverflow.com/questions/44127742/python-pandas-slice-column
```python
sample = pd.DataFrame( [[1,2,3], [4,5,6], [7,8,9]] )

'''
sample
   0  1  2
0  1  2  3
1  4  5  6
2  7  8  9
'''

sample.iloc[ :, 1 ]
'''
0    2
1    5
2    8
Name: 1, dtype: int64
'''

sample.iloc[ :, 1: ]
'''
   1  2
0  2  3
1  5  6
2  8  9
''' 
```

### Slice column side( By name )
* https://stackoverflow.com/questions/45225841/pandas-data-slicing-by-column-names
```python
'''
              area       pop
California  423967  38332521
Florida     170312  19552860
Illinois    149995  12882135
New York    141297  19651127
Texas       695662  26448193
'''
data.loc[:, 'area':'pop']
```
