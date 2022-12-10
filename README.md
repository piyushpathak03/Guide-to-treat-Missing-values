# Guide-to-treat-Missing-values
A complete guide to treat missing values

1. Delete Rows with Missing Values
One way of handling missing values is the deletion of the rows or columns having null values. If any columns have more than half of the values as null then you can drop the entire column. In the same way, rows can also be dropped if having one or more columns values as null. Before using this method one thing we have to keep in mind is that we should not be losing information. Because if the information we are deleting is contributing to the output value then we should not use this method because this will affect our output.

When to delete the rows/column in a dataset?

If a certain column has many missing values then you can choose to drop the entire column.
When you have a huge dataset. Deleting for e.g. 2-3 rows/columns will not make much difference.
Output results do not depend on the Deleted data. 
Note: No doubt it is one of the quick techniques one can use to deal with missing values. But this approach is not recommended. 

2. Replacing With Arbitrary Value
If you can replace the missing value with some arbitrary value using fillna().

Ex. In the below code, we are replacing the missing values with ‘0’.As well you can replace any particular column missing values with some arbitrary value also.

Replacing with previous value – Forward fill
We can impute the values with the previous value by using forward fill. It is mostly used in time series data.

Syntax: df.fillna(method=’ffill’)


Replacing with next value – Backward fill
In backward fill, the missing value is imputed using the next value. It is mostly used in time series data.


3. Interpolation
Missing values can also be imputed using ‘interpolation’. Pandas interpolate method can be used to replace the missing values with different interpolation methods like ‘polynomial’, ‘linear’, ‘quadratic’. The default method is ‘linear’.

Syntax: df.interpolate(method=’linear’)

For the time-series dataset variable, it makes sense to use the interpolation of the variable before and after a timestamp for a missing value. Interpolation in most cases supposed to be the best technique to fill missing values.

Handling missing values: python code:
We have taken dataset titanic.csv which is freely available at kaggle.com.This dataset was taken as it has missing values.

1.Reading the data
import pandas as pd
df = pd.read_csv("data.csv")
df
 
2. Checking if there are missing values
df.isnull().sum()
 
3.Filling missing values with 0
new_df = df.fillna(0)
new_df
 
4. Filling NaN values with forward fill value
new_df = df.fillna(method="ffill")
new_df
 
If we use forward fill that simply means we are forwarding the previous value where ever we have NaN values.

5. Setting forward fill limit to 1 
new_df = df.fillna(method="ffill",limit=1)
new_df

Now we have set the limit of forward fill to 1 which means that only once, the value will be copied below. Like in this case we had three NaN values consecutively in column Survived. But one NaN value was filled only as the limit is set to 1.

6. Filling NaN values in Backward Direction
new_df = df.fillna(method="bfill")new_df    

7. Interpolate of missing values
new_df = df.interpolate() 
df    

In this, we were having two values 22 and 26. And in between value was a NaN value. So that NaN value is computed by getting the mean of 22 and 26 i.e. 24. In the same way, other NaN values were also computed.

8. Deleting the rows having all NaN values
new_df = df.dropna(how='all')
new_df      
Those rows in which all the values are NaN values will be deleted. If the row even has one value even then it will not be dropped.

