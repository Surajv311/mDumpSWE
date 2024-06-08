
# Data_transformation_info

### Pandas infos: 
- What is the max data that can be loaded in pandas df?
  - Pandas loads datasets onto the memory, so the data size should not be bigger than the RAM you have.
  - However, even when your data only occupies, for example, 1 GB of your hard disk, it may take up, e.g. 2 GB of your memory when being loaded by Pandas.
  - The reason is data representation techniques are different. On your hard disk, your data may be compressed to take up less space, then Pandas has to uncompress it to easier and faster processing, resulting in a bigger size on the memory.
  - Another reason may be because of data types. If you save your data as a CSV file, a number, e.g. 0 is saved as a character, i.e. 1 byte in size. However, when Pandas loads it, that number is recognized as an integer, which takes up 4 or 8 bytes.
  - Loading is one story, processing is another. Pandas may be able to load your data, yet doing complex computation may fail. This is why I said “handle” is hard to define.
  - In conclusion, Pandas is optimized to work with data on the memory, so if your dataset is bigger than your memory, don’t use Pandas (or use Pandas on each chunk of your data separately, Pandas supports this).
- [Pandas SQL chunksize _al](https://stackoverflow.com/questions/31837979/pandas-sql-chunksize/31839639#31839639)
  - chunksize is None(default value):
    - pandas passes query to database; database executes query; pandas checks and sees that chunksize is None; pandas tells database that it wants to receive all rows of the result table at once; database returns all rows of the result table; pandas stores the result table in memory and wraps it into a data frame; now you can use the data frame
  - chunksize in not None:
    - pandas passes query to database; database executes query; pandas checks and sees that chunksize has some value; pandas creates a query iterator(usual 'while True' loop which breaks when database says that there is no more data left) and iterates over it each time you want the next chunk of the result table; pandas tells database that it wants to receive chunksize rows; database returns the next chunksize rows from the result table; pandas stores the next chunksize rows in memory and wraps it into a data frame; now you can use the data frame
  - Though understand that (in one of comments to the linked page): For many databases, the entire dataset will still be read into memory whole, before an iterator is returned, essentially meaning it pulls down the whole table and then chunks it.

```
Eg: 
sql = "SELECT * FROM My_Table"
for chunk in pd.read_sql_query(sql , engine, chunksize=5):
    print(chunk)
```

- 

#### JSON explode vs JSON normalize  

JSON explode creates more rows by expanding a column with lists, while JSON normalize creates more columns by flattening nested JSON objects within a column.

```
Consider the df: 
   id   name       scores
0   1  Alice  [90, 95, 88]
1   2    Bob      [85, 92]

df_exploded = df.explode('scores')

The df_exploded DataFrame after applying JSON explode:
   id   name scores
0   1  Alice     90
0   1  Alice     95
0   1  Alice     88
1   2    Bob     85
1   2    Bob     92

df_normalized = pd.json_normalize(df, 'scores', ['id', 'name'], sep='_')

The df_normalized DataFrame after applying JSON normalize:
   id   name  scores_0  scores_1  scores_2
0   1  Alice        90        95        88
1   2    Bob        85        92       NaN
```

Sidenote: When you use json_normalize to flatten a nested column in a DataFrame, the non-nested columns are not automatically included in the flattened result. json_normalize only operates on the specified nested column and doesn't consider the other columns in the original DataFrame. That's why there is a need to add them back to the flattened DataFrame if you want to retain all the columns from the original DataFrame. In many cases, especially when working with nested JSON data, you might want to perform operations on specific nested columns separately, and you may not need all columns in every operation. Adding the non-nested columns back gives you the flexibility to choose which columns to include in your final DataFrame based on your analysis or processing needs. It allows you to control which columns are present in the flattened DataFrame, which can be especially useful when working with large or complex datasets. In summary, json_normalize focuses on flattening the specified nested column, and if you want to retain non-nested columns, you need to add them back manually to the resulting DataFrame to have a complete view of your data. Eg this code:

```
for col in ist_all_tickets_df.columns.difference(['custom_fields']):
		list_all_tickets_df_normalized[col] = list_all_tickets_df[col]
```

[JSON Flattening _al](https://stackoverflow.com/questions/49822874/i-want-to-flatten-json-column-in-a-pandas-dataframe)

#### Dataframe Index   

In a DataFrame, the "index" refers to the row labels or identifiers that uniquely identify each row of data. It is essentially an ordered set of labels or integers that allows you to access and retrieve rows by their labels.In this example, the index consists of the integers 0, 1, 2, and 3, which correspond to the row positions in the DataFrame. Each row has a unique index label.

```
      Name  Age
0    Alice   25
1      Bob   30
2  Charlie   22
3    David   28

Note:
# Specify a custom index with duplicates

custom_index = ['A', 'B', 'A', 'D']
df = pd.DataFrame(data, index=custom_index)
      Name  Age
A    Alice   25
B      Bob   30
A  Charlie   22
D    David   28
```

In the example, the index labels 'A' are duplicated, as they appear more than once. This is what is meant by a "duplicate index." Duplicate index labels can lead to issues when performing certain operations or transformations on a DataFrame.

#### Dataframe Reset Index   

If you encounter issues related to duplicate indices in your DataFrame, it's often a good practice to reset the index to ensure that it is unique and continuous. 

You can do this using `df.reset_index(drop=True, inplace=True)` as shown in the previous code examples. If you don't use `df.reset_index()` after exploding and flattening the DataFrame, the output would include the old index as a new column in the DataFrame. 

```
   id   name      street         city
0   1  Alice  123 Main St     New York
1   1  Alice    456 Elm St  Los Angeles
0   2    Bob    789 Oak St      Chicago
As you can see, the old index column (0, 1, etc.) is retained as a new column in the DataFrame. This can sometimes lead to confusion, especially if you want to work with a clean DataFrame that starts with an index of 0 and increments sequentially.
```

#### Others

- Polars was built from the ground up to be blazingly fast and can do common operations around 5–10 times faster than pandas. Polars is that it is written in Rust, a low-level language that is almost as fast as C and C++. In contrast, pandas is built on top of Python libraries, one of these being NumPy. While NumPy’s core is written in C, it is still hamstrung by inherent problems with the way Python handles certain types in memory, such as strings for categorical data, leading to poor performance when handling these types. Another factor that contributes to Polars’ impressive performance is Apache Arrow, a language-independent memory format. Arrow was actually co-created by Wes McKinney in response to many of the issues he saw with pandas as the size of data exploded. It is also the backend for pandas 2.0, a more performant version of pandas. One of the other cores of Polars’ performance is how it evaluates code. Pandas, by default, uses eager execution, carrying out operations in the order you’ve written them. In contrast, Polars has the ability to do both eager and lazy execution, where a query optimizer will evaluate all of the required operations and map out the most efficient way of executing the code.


----------------------------------------------------------------------





















