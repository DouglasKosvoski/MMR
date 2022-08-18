# Pandas
Pandas is a Python library used for working with data sets.

It has functions for analyzing, cleaning, exploring, and manipulating data.

The name "Pandas" has a reference to both "Panel Data", and "Python Data Analysis" and was created by Wes McKinney in 2008.

## Instalation
```bash
pip install pandas
```
## Importing
```python
import pandas as pd
```

<details>
  <summary>Series</summary>

A Pandas Series is like a column in a table.<br>

It is a one-dimensional array holding data of any type.

```python
import pandas as pd

a = [1, 7, 2]

myvar = pd.Series(a)

print(myvar)
```

```
output:
0    1
1    7
2    2
```

> If nothing else is specified, the values are labeled with their index number. First value has index 0, second value has index 1 etc.

```python
a = [1, 7, 2]

myvar = pd.Series(a, index = ["x", "y", "z"])
```

```
output:
x    1
y    7
z    2
```

```python
# using this returns the value of "y"
print(myvar["y"])
```

```
output:
7
```
</details>

<details>
    <summary>Key/Value Objects as Series</summary>
    You can also use a key/value object, like a dictionary, when creating a Series.

```python
import pandas as pd

calories = {"day1": 420, "day2": 380, "day3": 390}

myvar = pd.Series(calories)

print(myvar)
```

> The keys of the dictionary become the labels.

```python
# create a Series using only data from "day1" and "day2"
calories = {"day1": 420, "day2": 380, "day3": 390}

myvar = pd.Series(calories, index = ["day1", "day2"])
```
</details>

<details>
    <summary>DataFrames</summary>
    Data sets in Pandas are usually multi-dimensional tables, called DataFrames. <br>Series is like a column, a DataFrame is the whole table.

```python
# create a DataFrame from two Series
data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}

myvar = pd.DataFrame(data)
```

```
output:
     calories  duration
  0       420        50
  1       380        40
  2       390        45
```

>As you can see from the result above, the DataFrame is like a table with rows and columns.<br> Pandas use the `loc` attribute to return one or more specified row(s).

```python
# refer to the row index
print(df.loc[0])
```
```
output:
  calories    420
  duration     50
  Name: 0, dtype: int64
```

```python
# use a list of indexes
print(df.loc[[0, 1]])
```

>This example returns a Pandas Series

```
output:
     calories  duration
  0       420        50
  1       380        40
```

> When using [], the result is a Pandas DataFrame.

## Named Indexes
With the index argument, you can name your own indexes.

```python
# add a list of names to give each row a name:
df = pd.DataFrame(data, index = ["day1", "day2", "day3"])
```

```
output:
        calories  duration
  day1       420        50
  day2       380        40
  day3       390        45
```

```python
# Use the named index in the loc attribute to return the specified row(s)
print(df.loc["day2"])
```

```
output:
  calories    380
  duration     40
  Name: 0, dtype: int64
```

## Load Files Into a DataFrame
If your data sets are stored in a file, Pandas can load them into a DataFrame.

```python
df = pd.read_csv('data.csv')
```

> If you have a large DataFrame with many rows, Pandas will only return the first 5 rows, and the last 5 rows, use `to_string()` to print the entire DataFrame.
</details>

<details>
<summary>Read JSON</summary>
Big data sets are often stored, or extracted as JSON.

JSON is plain text, but has the format of an object, and is well known in the world of programming, including Pandas.

```python
# load the JSON file into a DataFrame
import pandas as pd

df = pd.read_json('data.json')

print(df.to_string()) 
```

> JSON objects have the same format as Python dictionaries.

</details>

<details>
<summary>Viewing the Data</summary>

One of the most used method for getting a quick overview of the DataFrame, is the `head()` method.

The `head()` method returns the headers and a specified number of rows, starting from the top.
```python
# get a quick overview by printing the first 10 rows of the DataFrame
import pandas as pd

df = pd.read_csv('data.csv')

print(df.head(10)) 
```

> If the number of rows is not specified, the head() method will return the top 5 rows.

There is also a `tail()` method for viewing the last rows of the DataFrame.

The `tail()` method returns the headers and a specified number of rows, starting from the bottom.

## Info About the Data
The DataFrames object has a method called `info()`, that gives you more information about the data set.

```python
print(df.info()) 
```

```
output:
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 169 entries, 0 to 168
  Data columns (total 4 columns):
   #   Column    Non-Null Count  Dtype  
  ---  ------    --------------  -----  
   0   Duration  169 non-null    int64  
   1   Pulse     169 non-null    int64  
   2   Maxpulse  169 non-null    int64  
   3   Calories  164 non-null    float64
  dtypes: float64(1), int64(3)
  memory usage: 5.4 KB
  None
```

</details>

<details>
<summary>Cleaning Data</summary>
Data cleaning means fixing bad data in your data set.

Bad data could be:
- Empty cells
- Data in wrong format
- Wrong data
- Duplicates

### __Empty Cells__
Empty cells can potentially give you a wrong result when you analyze data.

### __Remove Rows__
One way to deal with empty cells is to remove rows that contain empty cells.

This is usually OK, since data sets can be very big, and removing a few rows will not have a big impact on the result.

```python
# returns a new Data Frame with no empty cells
import pandas as pd

df = pd.read_csv('data.csv')

new_df = df.dropna()

print(new_df.to_string())
```

> By default, the dropna() method returns a new DataFrame, and will not change the original.<br><br>If you want to change the original DataFrame, use the `inplace = True` argument.

### __Replace Empty Values__
```python
# replace NULL values with the number 130
df = pd.read_csv('data.csv')

df.fillna(130, inplace = True) 
```

```python
# replace Only For Specified Columns
df = pd.read_csv('data.csv')

df["Calories"].fillna(130, inplace = True) 
```
</details>

<details>
<summary>Cleaning Data of Wrong Format</summary>
Cells with data of wrong format can make it difficult, or even impossible, to analyze data.

To fix it, you have two options: remove the rows, or convert all cells in the columns into the same format.

### __Convert Into a Correct Format__
```
For example:
      Duration          Date  Pulse  Maxpulse  Calories
  21        60  '2020/12/21'    108       131     364.2
  22        45           NaN    100       119     282.0
  23        60  '2020/12/23'    130       101     300.0
  24        45  '2020/12/24'    105       132     246.0
  25        60  '2020/12/25'    102       126     334.5
  26        60      20201226    100       120     250.0
  27        60  '2020/12/27'     92       118     241.0
```

Let's try to convert all cells in the 'Date' column into dates.

Pandas has a `to_datetime()` method for this:

```python
import pandas as pd

df = pd.read_csv('data.csv')

df['Date'] = pd.to_datetime(df['Date'])

print(df.to_string())
```

```
output:
      Duration          Date  Pulse  Maxpulse  Calories
  21        60  '2020/12/21'    108       131     364.2
  22        45           NaT    100       119     282.0
  23        60  '2020/12/23'    130       101     300.0
  24        45  '2020/12/24'    105       132     246.0
  25        60  '2020/12/25'    102       126     334.5
  26        60  '2020/12/26'    100       120     250.0
  27        60  '2020/12/27'     92       118     241.0
```

> As you can see from the result, the date in row 26 was fixed, but the empty date in row 22 got a NaT (Not a Time) value, in other words an empty value. One way to deal with empty values is simply removing the entire row.

### __Removing Rows__
The result from the converting in the example above gave us a NaT value, which can be handled as a `NULL` value, and we can remove the row by using the `dropna()` method.

```python
# remove rows with a NULL value in the "Date" column
df.dropna(subset=['Date'], inplace = True)
```
</details>

<details>
<summary>Wrong Data</summary>
"Wrong data" does not have to be "empty cells" or "wrong format", it can just be wrong, like if someone registered "199" instead of "1.99".

Sometimes you can spot wrong data by looking at the data set, because you have an expectation of what it should be.

```
How can we fix wrong values, like the one for "Duration" in row 7?
  5         60  '2020/12/06'    102       127     300.0
  6         60  '2020/12/07'    110       136     374.0
  7        450  '2020/12/08'    104       134     253.3
  8         30  '2020/12/09'    109       133     195.1
  9         60  '2020/12/10'     98       124     269.0
```

### __Replacing Values__
```python
# set "Duration" = 45 in row 7
df.loc[7, 'Duration'] = 45
```

For small data sets you might be able to replace the wrong data one by one, but not for big data sets.

To replace wrong data for larger data sets you can create some rules, e.g. set some boundaries for legal values, and replace any values that are outside of the boundaries.

Loop through all values in the "Duration" column.
```python
# if the value is higher than 120, set it to 120
for x in df.index:
  if df.loc[x, "Duration"] > 120:
    df.loc[x, "Duration"] = 120 
```

### __Removing Rows__
Another way of handling wrong data is to remove the rows that contains wrong data.

```python
# delete rows where "Duration" is higher than 120
for x in df.index:
  if df.loc[x, "Duration"] > 120:
    df.drop(x, inplace = True) 
```
</details>

<details>
<summary>Discovering Duplicates</summary>
Duplicate rows are rows that have been registered more than one time.

```
For example:
  9         60  '2020/12/10'     98       124     269.0
  10        60  '2020/12/11'    103       147     329.3
  11        60  '2020/12/12'    100       120     250.7
  12        60  '2020/12/12'    100       120     250.7
  13        60  '2020/12/13'    106       128     345.3
```

By taking a look at our test data set, we can assume that row 11 and 12 are duplicates.

> To discover duplicates, we can use the `duplicated()` method.

The duplicated() method returns a Boolean values for each row

```python
# returns True for every row that is a duplicate, othwerwise False
print(df.duplicated())
```

```
output:
10    False
11    False
12     True
13    False
14    False
15    False
```

### __Removing Duplicates__

> To remove duplicates, use the `drop_duplicates()` method.

```python
# remove all duplicates
df.drop_duplicates(inplace = True) 
```
</details>

<details>
<summary>Data Correlations</summary>

The `corr()` method calculates the relationship between each column in your data set.

```python
# show the relationship between the columns
df.corr() 
```

```
output:
            Duration     Pulse  Maxpulse  Calories
  Duration  1.000000 -0.155408  0.009403  0.922721
  Pulse    -0.155408  1.000000  0.786535  0.025120
  Maxpulse  0.009403  0.786535  1.000000  0.203814
  Calories  0.922721  0.025120  0.203814  1.000000
```

>  The `corr()` method ignores "not numeric" columns.

Result Explained

The Result of the `corr()` method is a table with a lot of numbers that represents how well the relationship is between two columns.

The number varies from -1 to 1.

1 means that there is a 1 to 1 relationship (a perfect correlation), and for this data set, each time a value went up in the first column, the other one went up as well.

0.9 is also a good relationship, and if you increase one value, the other will probably increase as well.

-0.9 would be just as good relationship as 0.9, but if you increase one value, the other will probably go down.

0.2 means NOT a good relationship, meaning that if one value goes up does not mean that the other will.

> Perfect Correlation: <br>We can see that "Duration" and "Duration" got the number 1.000000, which makes sense, each column always has a perfect relationship with itself.

> Good Correlation: <br>"Duration" and "Calories" got a 0.922721 correlation, which is a very good correlation, and we can predict that the longer you work out, the more calories you burn, and the other way around: if you burned a lot of calories, you probably had a long work out.

> Bad Correlation: <br>"Duration" and "Maxpulse" got a 0.009403 correlation, which is a very bad correlation, meaning that we can not predict the max pulse by just looking at the duration of the work out, and vice versa.

</details>

<details>
<summary>Reference</summary>

[Pandas Dataframe Reference](https://www.w3schools.com/python/pandas/pandas_ref_dataframe.asp)
</details>
