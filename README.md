# pandas
exercise-2
import pandas as pd
import numpy as np
df=pd.DataFrame(np.array([[2,5,4],[10,20,30],[11,12,34]]),index=['a','b','c'],columns=['x','y','z'])
print(df)
    x   y   z
a   2   5   4
b  10  20  30
c  11  12  34
df.loc['c','z']
34
df.loc[['a','b']]
x	y	z
a	2	5	4
b	10	20	30
df.loc['a','z']=15
df
x	y	z
a	2	5	15
b	10	20	30
c	11	12	34
df.loc[df['a']>3]
df
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
~\anaconda3\lib\site-packages\pandas\core\indexes\base.py in get_loc(self, key, method, tolerance)
   3079             try:
-> 3080                 return self._engine.get_loc(casted_key)
   3081             except KeyError as err:

pandas\_libs\index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas\_libs\index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas\_libs\hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()

pandas\_libs\hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()

KeyError: 'a'

The above exception was the direct cause of the following exception:

KeyError                                  Traceback (most recent call last)
<ipython-input-18-f077e348c902> in <module>
----> 1 df.loc[df['a']>3]
      2 df

~\anaconda3\lib\site-packages\pandas\core\frame.py in __getitem__(self, key)
   3022             if self.columns.nlevels > 1:
   3023                 return self._getitem_multilevel(key)
-> 3024             indexer = self.columns.get_loc(key)
   3025             if is_integer(indexer):
   3026                 indexer = [indexer]

~\anaconda3\lib\site-packages\pandas\core\indexes\base.py in get_loc(self, key, method, tolerance)
   3080                 return self._engine.get_loc(casted_key)
   3081             except KeyError as err:
-> 3082                 raise KeyError(key) from err
   3083 
   3084         if tolerance is not None:

KeyError: 'a'
df.at['b','y']
20
df.at['c','x']=20
df
x	y	z
a	2	5	15
b	10	20	30
c	20	12	34
df.iloc[1,2]
30
df.iloc[1,0]=20
df
x	y	z
a	2	5	15
b	20	20	30
c	20	12	34
df.iloc[:-1,:-1]
x	y
a	2	5
b	20	20
df.iat[1,2]
30
df.dtypes
x    int32
y    int32
z    int32
dtype: object
df1=DataFrame({'a':[]})
r=df1.empty
print(r)
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-39-70645693aed3> in <module>
----> 1 df1=DataFrame({'a':[]})
      2 r=df1.empty
      3 print(r)

NameError: name 'DataFrame' is not defined
df.loc[['x','y'],'b']=99
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-31-7bdd5643cfac> in <module>
----> 1 df.loc[['x','y'],'b']=99

~\anaconda3\lib\site-packages\pandas\core\indexing.py in __setitem__(self, key, value)
    686         else:
    687             key = com.apply_if_callable(key, self.obj)
--> 688         indexer = self._get_setitem_indexer(key)
    689         self._has_valid_setitem_indexer(key)
    690 

~\anaconda3\lib\site-packages\pandas\core\indexing.py in _get_setitem_indexer(self, key)
    628         if isinstance(key, tuple):
    629             with suppress(IndexingError):
--> 630                 return self._convert_tuple(key, is_setter=True)
    631 
    632         if isinstance(key, range):

~\anaconda3\lib\site-packages\pandas\core\indexing.py in _convert_tuple(self, key, is_setter)
    752             self._validate_key_length(key)
    753             for i, k in enumerate(key):
--> 754                 idx = self._convert_to_indexer(k, axis=i, is_setter=is_setter)
    755                 keyidx.append(idx)
    756 

~\anaconda3\lib\site-packages\pandas\core\indexing.py in _convert_to_indexer(self, key, axis, is_setter)
   1210             else:
   1211                 # When setting, missing keys are not allowed, even with .loc:
-> 1212                 return self._get_listlike_indexer(key, axis, raise_missing=True)[1]
   1213         else:
   1214             try:

~\anaconda3\lib\site-packages\pandas\core\indexing.py in _get_listlike_indexer(self, key, axis, raise_missing)
   1264             keyarr, indexer, new_indexer = ax._reindex_non_unique(keyarr)
   1265 
-> 1266         self._validate_read_indexer(keyarr, indexer, axis, raise_missing=raise_missing)
   1267         return keyarr, indexer
   1268 

~\anaconda3\lib\site-packages\pandas\core\indexing.py in _validate_read_indexer(self, key, indexer, axis, raise_missing)
   1306             if missing == len(indexer):
   1307                 axis_name = self.obj._get_axis_name(axis)
-> 1308                 raise KeyError(f"None of [{key}] are in the [{axis_name}]")
   1309 
   1310             ax = self.obj._get_axis(axis)

KeyError: "None of [Index(['x', 'y'], dtype='object')] are in the [index]"
df.ndim
2
df.shape
(3, 3)
df.size
9
df.values
array([[ 2,  5, 15],
       [20, 20, 30],
       [20, 12, 34]])
