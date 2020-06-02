Structures
===

Series
---

### Components:

+ ser.index: Labels
+ ser.values: Values

### Series operations:

+ Select can be done via both label (or index) and integer position: `food[['Dean', 'Christina', 'Aaron']]` OR `food[[0, 2, 6]]`

> Slicing fully supported `food[2:4]` OR `food['Niko':'Dean']`, etc.

DataFrames
---

### Components

+ `df.index`: Labels for the Rows. (Type: pandas.core.indexes.base.Index)
+ `df.columns`: Labels for the Columns. (Type: pandas.core.indexes.base.Index)
+ `df.values`: Actual content of the table. (Type: numpy.ndarray)

pandas.core.indexes.base.Index (Used for both row index and column)
---

+ Get all index values: df.index.values (*INDEX is the label of the row*)

### Getting integer position and labels

+ Get row label by providing the integer position: `df.index[0]`
+ Get column integer position by providing the label: `df.columns.get_loc('a')`

DataFrame Read Operations
===

Indexers
---

### Indexing Operator

+ Select single column by label: `df['col_name']`
+ Select multiple columns by label: `df[['col_name1', 'col_name2']]`
+ Select all columns and the 4 first rows: `df[:3]` (With DataFrame, slicing inside of [] slices the rows)

> Slicing automatically target rows: We can select rows using their integer positions `df[3:6]` and labels `df['Aaron':'Christina']`. However, can be ambiguous, especially if you have integers in your index (remember, index is the row label).

> It is also possible to access a column via property, using the dot notation: `df.col_name`. This helps out chaining methods.

### `.loc` Indexer

The `.loc` indexer selects data in a different way than just the indexing operator. 
It can select subsets of rows or columns. It can also simultaneously select subsets of rows and columns. 
Most importantly, it only selects data by the LABEL of the rows and columns.

+ Select single row by label: `df.loc['row_name']`
+ Select multiple rows by label: `df.loc[['row_name1', 'row_name2']]`

> It is possible to ‘slice’ the rows of a DataFrame with .loc by using slice notation. Slice notation uses a colon to separate start, stop and step values.
> e.g.: `df.loc['row_name1':'row_name2']`. Or `df.loc['row_name2':]`
>
> **`.loc` includes the last value with slice notation**

+ Select columns and rows both by label: `df.loc[['row_name1', 'row_name2'], ['col_name1', 'col_name2', 'col_name3']]`

> Row or column selections can be any of the following as we have already seen:
> * A single label
> * A list of labels
> * A slice with labels
> e.g.: `df.loc[['row_name1', 'row_name2'], 'col_name1']` OR `df.loc['row_name1':'row_name2', ['col_name1', 'col_name2']]` OR `df.loc[:'row_name3', 'col_name4':]` OR `df.loc[:, ['col_name2', 'col_name3']]`, etc.

+ Select row by index and column by label: `df.loc[df.index[<ROW_NUMBER>], '<COLUMN_NAME>']`

### `.iloc` Indexer

The `.iloc` indexer is very similar to `.loc` but only uses integer locations to make its selections. The word `.iloc` itself stands for integer location so that should help with remember what it does.

+ Selecting single row by integer position: df.iloc[3]
+ Selecting multiple rows by integer position: df.iloc[[5, 2, 4]]

> Slicing is fully supported: `df.iloc[3:5]`, `df.iloc[3:]`, `df.iloc[3::2]` (select from 4th element to the end, with step of 2), etc.

+ Selecting rows and columns both by integer position: `df.iloc[[2,3], [0, 4]]` (two rows and two columns)

> Slicing also fully possible: `df.iloc[3:6, [1, 4]]` OR `df.iloc[2:5, 2:5]`, etc. Even selecting all rows for a single columns: `df.iloc[:, 5]`

### `.at` Indexer

Access a single value for a row/column label pair. Faster than `.loc`.
Similar to loc, in that both provide label-based lookups. Use at if you only need to get or set a single value in a DataFrame or Series.

+ Get value from DataFrame: `df.at[4, 'B']`
+ Get value from Series: `df.loc[4].at['B']`

### `.iat` Indexer

Access a single value for a row/column pair by integer position. Faster than `.iloc`.
Similar to iloc, in that both provide integer-based lookups. Use iat if you only need to get or set a single value in a DataFrame or Series.

+  Get value from DataFrame: `df.iat[1, 2]`
+  Get value from Series: `df.loc[0].iat[1]`
