# DataCleanser
 This program automates basic data cleansing methods, simplifying the process of cleaning and preparing datasets for analysis.

 #### Importing the appropriate libraries
 ```
# Import the Libraries
import pandas as pd
import numpy as np
```

**pandas** is a powerful library used for data manipulation and analysis, particularly for handling structured data in the form of dataframes. It provides a wide range of tools and functions to read, process, and transform data efficiently.
**numpy** is another fundamental library used for numerical computing in Python. It offers support for large, multi-dimensional arrays and matrices, along with a collection of mathematical functions to operate on these arrays. 

#### Importing data
```
df = pd.read_csv(r'LOCATION\prac.csv')
df.head(10) # Print the first 10 rows
```
This step essientally imports the .csv file into the program while printing the first 10 columns to get a grasp of the data
#### Finding datatypes
```
# Find Datatypes:
df.dtypes
```
In this code, df.dtypes is used to find the datatypes of each column in the DataFrame df. It will return a series that contains the datatype of each column in the DataFrame, showing how the data is stored in each column (e.g., int64, float64, object, etc.). We want a general understanindg of the types of data we are working with.

```
# Locate the Float64 and the Object Columns 
floatColumns = df.select_dtypes(include=['float64'])
objectColumns = df.select_dtypes(include = ['O'])
```
floatColumns: This DataFrame contains only the columns with datatype float64. It is used to isolate columns that hold numerical data with decimal points.
objectColumns: This DataFrame contains only the columns with datatype object. It is used to isolate columns that contain text or non-numeric data.
```
# Find the Number of Null Values
float_NULLS = floatColumns.isnull().sum()
object_NULLS = objectColumns.isnull().sum()
```
In this code, the number of null (missing) values in the floatColumns and objectColumns DataFrames is calculated.

```
# Replace the null values in the Objects Columns 
x = floatColumns.mean() # Find the Mean
df[floatColumns.columns] = floatColumns.fillna(x) # Fill Na Vlaues
```
The null values in the floatColumns DataFrame, containing columns with numerical data, are replaced with the mean value calculated using floatColumns.mean(). The line df[floatColumns.columns] = floatColumns.fillna(x) fills the null values in the original DataFrame df for the corresponding columns with the mean value calculated from the floatColumns DataFrame.


```
# Fix the Inconsistency in Spellings
object_columns = df.select_dtypes(include=['object'])
df[object_columns.columns] = object_columns.apply(lambda x: x.str.capitalize())
```


In this code, the DataFrame df is first filtered to contain only columns with object (text) data, and this subset is stored in the object_columns DataFrame. Then, a lambda function is applied to each element in object_columns, converting the text in each cell to capitalize the first letter while making all other letters lowercase. This process standardizes the spelling format and fixes inconsistency in the spellings of text data in the df DataFrame.

```
df.dropna(inplace = True)
df.head()
```
Dropping the values with a NULL value

```
# Dropping Duplicate Names:

duplicates = df.duplicated(subset=df.columns[0])
df.drop_duplicates(subset=df.columns[0], inplace=True)
df.head()
```

In this code, the DataFrame df is checked for duplicate values in its first column. Any duplicate rows based on the first column's values are dropped from the DataFrame, ensuring data consistency and removing redundant data entries.
```
# Sorting by Year
if 'Year' in df:
    df.sort_values(by='Year', inplace=True)
df
```
If there is a year column in the data, we may sort the values in order to have the values ascending or descending in a clean fashion. 
