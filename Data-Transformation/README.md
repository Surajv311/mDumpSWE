
# Data_transformation_info

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

----------------------------------------------------------------------





















