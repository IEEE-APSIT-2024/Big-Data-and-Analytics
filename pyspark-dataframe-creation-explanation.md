# PySpark DataFrame Creation from Various Data Sources

## Environment Setup

```python
# Set the PySpark environment variables
import os
os.environ['SPARK_HOME'] = "/Users/coder2j/Apps/Spark"
os.environ['PYSPARK_DRIVER_PYTHON'] = 'jupyter'
os.environ['PYSPARK_DRIVER_PYTHON_OPTS'] = 'lab'
os.environ['PYSPARK_PYTHON'] = 'python'
```

This code block sets up the PySpark environment variables. It's crucial for ensuring that PySpark can run properly within the Jupyter environment:
- `SPARK_HOME`: Points to the Spark installation directory
- `PYSPARK_DRIVER_PYTHON`: Specifies Jupyter as the Python driver for PySpark
- `PYSPARK_DRIVER_PYTHON_OPTS`: Sets options for the Python driver (in this case, 'lab' for JupyterLab)
- `PYSPARK_PYTHON`: Specifies the Python executable to use

## Creating a SparkSession

```python
from pyspark.sql import SparkSession

# Create a SparkSession
spark = SparkSession.builder.appName("Create-DataFrame").getOrCreate()
```

This code initializes a SparkSession, which is the entry point for programming Spark with the DataFrame and SQL API. The `appName` sets a name for this Spark application, useful for monitoring in the Spark web UI.

## Reading CSV Files

### Displaying CSV Content

```bash
head -10 ./data/products.csv
```

This bash command displays the first 10 lines of the CSV file, giving us a preview of its structure and content.

### Reading CSV with Header

```python
csv_file_path = "./data/products.csv"
df = spark.read.csv(csv_file_path, header=True)
```

This code reads the CSV file into a DataFrame. The `header=True` option tells Spark that the first row of the CSV file contains column names.

### Reading CSV with Explicit Schema

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType, DoubleType

schema = StructType([
    StructField(name="id", dataType=IntegerType(), nullable=True),
    StructField(name="name", dataType=StringType(), nullable=True),
    StructField(name="category", dataType=StringType(), nullable=True),
    StructField(name="quantity", dataType=IntegerType(), nullable=True),
    StructField(name="price", dataType=DoubleType(), nullable=True)
])

df = spark.read.csv(csv_file_path, header=True, schema=schema)
```

This approach defines an explicit schema for the DataFrame. It gives you more control over the data types of each column and can improve performance by avoiding the need for Spark to infer the schema.

### Reading CSV with Schema Inference

```python
df = spark.read.csv(csv_file_path, header=True, inferSchema=True)
```

This method allows Spark to automatically infer the schema of the CSV file. While convenient, it can be slower for large datasets compared to providing an explicit schema.

## Reading JSON Files

### Single Line JSON

```python
json_file_path = "./data/products_singleline.json"
df = spark.read.json(json_file_path)
```

This code reads a JSON file where each line is a complete JSON object. Spark automatically infers the schema from the JSON structure.

### Multi-line JSON

```python
json_file_path = "./data/products_multiline.json"
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

## Additional Notes

- The notebook demonstrates various methods of reading data into Spark DataFrames, each with its own use cases and advantages.
- CSV and JSON are common formats for data exchange, while Parquet is more efficient for analytics workloads.
- Explicitly defining schemas can improve performance and data quality control.
- Always inspect your data after reading it into a DataFrame to ensure it has been parsed correctly.
- The choice between single-line and multi-line JSON parsing depends on the structure of your JSON files.
- Parquet is a highly efficient format for both reading and writing data in Spark applications.
