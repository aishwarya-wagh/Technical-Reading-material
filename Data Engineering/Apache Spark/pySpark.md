# PySpark Demo Project

## Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Loading Data](#loading-data)
4. [Data Manipulation Scenarios](#data-manipulation-scenarios)
    - [Filtering Data](#filtering-data)
    - [Selecting Columns](#selecting-columns)
    - [Renaming Columns](#renaming-columns)
    - [Adding Columns](#adding-columns)
    - [Dropping Columns](#dropping-columns)
    - [Aggregating Data](#aggregating-data)
    - [Joining DataFrames](#joining-dataframes)
    - [Handling Missing Values](#handling-missing-values)
    - [Sorting Data](#sorting-data)
    - [Window Functions](#window-functions)
    - [GroupBy and Aggregations](#groupby-and-aggregations)
    - [Pivoting and Unpivoting](#pivoting-and-unpivoting)
    - [Handling Dates and Timestamps](#handling-dates-and-timestamps)
    - [User Defined Functions (UDFs)](#user-defined-functions-udfs)
5. [Conclusion](#conclusion)

## 1. Introduction
This demo project showcases various data manipulation techniques using PySpark. It includes examples of filtering, selecting, renaming, adding, and dropping columns, as well as aggregating, joining, and handling missing values. The project aims to provide a comprehensive guide to common PySpark operations.

## 2. Setup
To set up the project, follow these steps:

1. Install Apache Spark and PySpark:
    ```bash
    pip install pyspark
    ```

2. Set up your project directory:
    ```bash
    mkdir pyspark-demo
    cd pyspark-demo
    ```

3. Create a Python script for your demo:
    ```bash
    touch demo.py
    ```

4. (Optional) Download a sample dataset to work with.

## 3. Loading Data
To load data into a PySpark DataFrame, use the following code snippet:

```python
from pyspark.sql import SparkSession

# Initialize Spark session
spark = SparkSession.builder \
    .appName("PySpark Demo") \
    .getOrCreate()

# Load CSV data into DataFrame
df = spark.read.csv("path/to/your/dataset.csv", header=True, inferSchema=True)
```

## 4. Data Manipulation Scenarios

### Filtering Data
Filter rows based on a condition.

```python
# Filter rows where age > 30
filtered_df = df.filter(df.age > 30)
```

### Selecting Columns
Select specific columns from the DataFrame.

```python
# Select columns 'name' and 'age'
selected_df = df.select("name", "age")
```

### Renaming Columns
Rename columns in the DataFrame.

```python
# Rename column 'age' to 'years'
renamed_df = df.withColumnRenamed("age", "years")
```

### Adding Columns
Add a new column to the DataFrame.

```python
# Add a new column 'age_plus_10'
df_with_new_col = df.withColumn("age_plus_10", df.age + 10)
```

### Dropping Columns
Drop a column from the DataFrame.

```python
# Drop the 'age' column
df_dropped_col = df.drop("age")
```

### Aggregating Data
Aggregate data using functions like sum, avg, max, etc.

```python
from pyspark.sql.functions import avg

# Calculate average age
avg_age = df.agg(avg("age")).collect()[0][0]
```

### Joining DataFrames
Join two DataFrames on a common column.

```python
# Sample DataFrame to join
df2 = df.select("name", "salary")

# Join DataFrames on 'name' column
joined_df = df.join(df2, on="name", how="inner")
```

### Handling Missing Values
Handle missing values in the DataFrame.

```python
# Drop rows with any missing values
df_dropped_na = df.dropna()

# Fill missing values in 'age' column with the average age
avg_age = df.select(avg("age")).first()[0]
df_filled_na = df.fillna({"age": avg_age})
```

### Sorting Data
Sort data by a specific column.

```python
# Sort by 'age' in descending order
sorted_df = df.orderBy(df.age.desc())
```

### Window Functions
Apply window functions for advanced analytics.

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import rank

# Define window specification
window_spec = Window.partitionBy("department").orderBy(df.salary.desc())

# Apply rank function
df_with_rank = df.withColumn("rank", rank().over(window_spec))
```

### GroupBy and Aggregations
Group data by a column and perform aggregations.

```python
# Group by 'department' and calculate average salary
grouped_df = df.groupBy("department").agg(avg("salary").alias("avg_salary"))
```

### Pivoting and Unpivoting
Pivot and unpivot data for better analysis.

```python
# Pivot data to get average salary by department
pivoted_df = df.groupBy("department").pivot("gender").agg(avg("salary"))
```

### Handling Dates and Timestamps
Work with date and timestamp columns.

```python
from pyspark.sql.functions import to_date, year, month, dayofmonth

# Convert string to date
df_with_date = df.withColumn("date", to_date(df.date_string, "yyyy-MM-dd"))

# Extract year, month, day
df_with_date_parts = df_with_date.withColumn("year", year(df_with_date.date)) \
    .withColumn("month", month(df_with_date.date)) \
    .withColumn("day", dayofmonth(df_with_date.date))
```

### User Defined Functions (UDFs)
Create and use UDFs for custom transformations.

```python
from pyspark.sql.functions import udf
from pyspark.sql.types import StringType

# Define UDF to convert name to uppercase
def to_uppercase(name):
    return name.upper()

uppercase_udf = udf(to_uppercase, StringType())

# Apply UDF to 'name' column
df_with_uppercase_name = df.withColumn("name_uppercase", uppercase_udf(df.name))
```

## 5. Conclusion
This demo project covers a wide range of data manipulation scenarios using PySpark. By exploring these examples, you will gain a deeper understanding of how to work with PySpark for your data processing and analysis needs. Feel free to extend this project with additional data manipulation techniques and advanced features.

