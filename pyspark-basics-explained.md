# PySpark Basics: A Comprehensive Guide

This guide provides a detailed explanation of PySpark basics, based on the Jupyter notebook "Basics from the Start". We'll go through each cell, explaining the code and concepts in detail.

## Setting up PySpark

```python
!pip install spark
spark
import spark
```


```python
from pyspark.sql import SparkSession

spark=SparkSession.builder.appName('Practise').getOrCreate()
```

These lines import the necessary PySpark module and create a SparkSession. The SparkSession is the entry point for programming Spark with the Dataset and DataFrame API.

- `from pyspark.sql import SparkSession`: This imports the SparkSession class from PySpark.
- `spark = SparkSession.builder.appName('Dataframe').getOrCreate()`: This creates a new SparkSession or gets an existing one. The `appName` sets a name for our Spark application.

## Loading Data

```python
df_pyspark = spark.read.option('header', 'true').csv('/FileStore/tables/test2.csv', inferSchema=True)
```

This line reads a CSV file and creates a PySpark DataFrame.

- `spark.read`: This is the entry point for reading data into a DataFrame.
- `.option('header', 'true')`: This tells Spark that the CSV file has a header row.
- `.csv('/FileStore/tables/test1.csv')`: This specifies the path to the CSV file.
- `inferSchema=True`: This tells Spark to automatically infer the schema of the DataFrame based on the data.

## Exploring the DataFrame

```python
df_pyspark.printSchema()
```

This prints the schema of the DataFrame, showing the structure and data types of each column.

```python
df_pyspark.show()
```

This displays the first 20 rows of the DataFrame.

```python
type(df_pyspark)
```

This returns the type of `df_pyspark`, which should be `pyspark.sql.dataframe.DataFrame`.

```python
df_pyspark.head(3)
```

This returns the first 3 rows of the DataFrame as a list of Row objects.

## Selecting Columns

```python
df_pyspark.select(['Name', 'Experience']).show()
```

This selects and displays only the 'Name' and 'Experience' columns from the DataFrame.

## DataFrame Statistics

```python
df_pyspark.describe().show()
```

This computes summary statistics for numeric columns in the DataFrame, including count, mean, standard deviation, min, and max.

## Adding a New Column

```python
df_pyspark = df_pyspark.withColumn('Experience After 2 year', df_pyspark['Experience'] + 2)
```

This adds a new column 'Experience After 2 year' to the DataFrame, calculated by adding 2 to the 'Experience' column.

## Handling Missing Data

```python
df_pyspark.na.drop().show()
```

This drops any row that contains null values and shows the result.

```python
df_pyspark.na.drop(how="any", thresh=3).show()
```

This drops rows that have less than 3 non-null values.

```python
df_pyspark.na.fill('Missing Values', ['Experience', 'age']).show()
```

This fills null values in the 'Experience' and 'age' columns with the string 'Missing Values'.

## Using Imputer for Missing Values

```python
from pyspark.ml.feature import Imputer

imputer = Imputer(
    inputCols=['age', 'Experience', 'Salary'], 
    outputCols=["{}_imputed".format(c) for c in ['age', 'Experience', 'Salary']]
    ).setStrategy("median")

imputer.fit(df_pyspark).transform(df_pyspark).show()
```

This uses the Imputer to fill missing values with the median of each column.

## Filtering Data

```python
df_pyspark.filter("Salary <= 20000").show()
```

This filters and shows only the rows where Salary is less than or equal to 20000.

```python
df_pyspark.filter("Salary <= 20000").select(['Name', 'age']).show()
```

This filters on Salary and then selects only the 'Name' and 'age' columns.

```python
df_pyspark.filter((df_pyspark['Salary'] <= 20000) | 
                  (df_pyspark['Salary'] >= 15000)).show()
```

This uses a more complex filter with an OR condition.

## Grouping and Aggregating Data

```python
df_pyspark.groupBy('Name').avg().show()
```

This groups the data by 'Name' and calculates the average of all numeric columns for each group.


## Reading JSON Files

### Single Line JSON

```python
json_file_path = "/FileStore/tables/products_singleline.json"
df = spark.read.json(json_file_path)
```

This code reads a JSON file where each line is a complete JSON object. Spark automatically infers the schema from the JSON structure.

### Multi-line JSON

```python
json_file_path = "/FileStore/tables/products_multiline.json"
df = spark.read.json(json_file_path, multiLine=True)
```

This code reads a JSON file where JSON objects may span multiple lines. The `multiLine=True` option is crucial for correctly parsing this format.

## Writing and Reading Parquet Files

### Writing to Parquet

```python
parquet_file_path = "./data/products.parquet"
df.write.parquet(parquet_file_path)
```

This code writes the DataFrame to a Parquet file. Parquet is a columnar storage format that's highly efficient for analytics workloads.

### Reading from Parquet

```python
df = spark.read.parquet(parquet_file_path)
```

This code reads a Parquet file into a DataFrame. Parquet files include schema information, so Spark can efficiently read them without additional schema specification.

## Utility Operations

Throughout the notebook, these operations are used to inspect the DataFrames:

```python
df.printSchema()  # Displays the schema of the DataFrame
df.show(5)  # Displays the first 5 rows of the DataFrame
```

These are crucial for verifying that the data has been read correctly and understanding its structure.

## Closing the SparkSession

```python
spark.stop()
```

This command stops the SparkSession and releases all associated resources. It's good practice to call this at the end of your Spark applications.
