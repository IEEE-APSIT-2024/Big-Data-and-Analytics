# WHY BIG DATA ANALYTICS ?
![bda](https://github.com/user-attachments/assets/2eae582e-baa8-414e-a219-1d80f63c85dc)


## Vs in Big Data
![image](https://github.com/user-attachments/assets/0f87cb8e-06eb-42bd-9c26-2987c0e5bf4c)

## Big data arch
![image](https://github.com/user-attachments/assets/aa07d47b-468a-4e47-b78c-f1b583bc18e4)

# HADOOP
![hadoop](https://github.com/user-attachments/assets/adfba0f5-9322-4d71-a7b9-a28a72ae71c1)

## hadoop arch: 
![hadooparch](https://github.com/user-attachments/assets/22596a12-0791-41e2-a53a-75680019f507)

## HDFS:
![hdfs](https://github.com/user-attachments/assets/be3e67cc-42e2-48bb-a82b-e296de43025e)

## MapReduce:
![mapreduce](https://github.com/user-attachments/assets/f04a552c-0fa2-4c80-a535-838bdd75eaac)



# Apache Spark

Spark is a unified analytics engine for large-scale data processing. It provides
high-level APIs in Scala, Java, Python, and R, and an optimized engine that
supports general computation graphs for data analysis. It also supports a
rich set of higher-level tools including Spark SQL for SQL and DataFrames,
pandas API on Spark for pandas workloads, MLlib for machine learning, GraphX for graph processing,
and Structured Streaming for stream processing.

<https://spark.apache.org/>

# Why that Spark?

Apache Spark’s main advantage is **speed—it** performs in-memory computations, avoiding disk I/O for intermediate results, unlike Hadoop, which writes to disk between each step of the MapReduce process. Spark is often 100x faster in-memory and 10x faster on disk. Here’s why Spark is a game-changer:

1) In-Memory Computation
2) Unified Data Processing
3) Ease of Use 
4) Fault Tolerance

![image](https://github.com/user-attachments/assets/7c2a36ec-3274-4985-8ef0-fd1b19ec24f6)

The Apache Spark framework uses a **master-slave architecture** 
The architecture of Spark is divided into the following components:

Driver Program: It is the main application entry point that creates SparkContext (the gateway to Spark) and uses this to coordinate with the workers.
Cluster Manager: Manages resource allocation for the Spark application (e.g., YARN, Mesos).
Worker Nodes: They run on the nodes in the cluster and execute tasks assigned by the Driver.

# What is Scala?


# RDD in use?

# Spark Components: Here we go again!

![image](https://github.com/user-attachments/assets/6ca021f6-8f13-4d78-bc61-e8006265d48a)

Spark Core: The foundation that provides distributed task dispatching, scheduling, and basic I/O functionalities.
Spark SQL: Module for working with structured data.
Spark Streaming: For processing real-time streaming data.
MLlib: A distributed machine learning framework.
GraphX: A distributed graph processing framework.

# Spark Big Data Analysis on Databricks

## Project Overview

This project demonstrates a real-world problem solved using Apache Spark for big data processing on the Databricks platform. The solution leverages Spark's distributed data processing capabilities to handle large-scale datasets efficiently. By walking through the problem-solving process, we explore Spark transformations, actions, and data pipelines. The project is designed to be beginner-friendly while demonstrating advanced analytics.

### Problem Statement

The project focuses on solving a [briefly describe the problem here]. The data is processed and analyzed using Spark's core features, including RDDs, DataFrames, and SQL, on the Databricks platform. The analysis leads to insights that help [describe outcome/goals].

### Key Features
- **Data Ingestion**: Efficiently reading large datasets from various sources like CSV, JSON, and databases.
- **Data Cleaning**: Handling missing data, duplicates, and inconsistencies.
- **Data Transformation**: Using Spark's transformations (e.g., map, filter, join) to process the data.
- **Exploratory Data Analysis (EDA)**: Gaining insights through Spark SQL and DataFrames.
- **Visualization**: Basic visualizations using Databricks' built-in charting tools.
- **Performance Optimization**: Partitioning, caching, and other Spark performance enhancements.

### Technologies Used
- **Apache Spark**: Distributed data processing
- **Databricks**: Cloud platform for big data analytics
- **PySpark**: Python API for Spark
- **Delta Lake**: For handling data reliability and performance

## Project Setup

### Prerequisites
- [Databricks Account](https://databricks.com/)
- Python 3.11.5
- Git

### Installation and Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/IEEE-APSIT-2024/Big-Data-and-Analytics.git
   cd Big-Data-and-Analytics
2.**Set up Databricks Workspace**:

 a.**Sign in to your Databricks account**.
 b.**Import the `.ipynb` file** into your Databricks workspace.
 c.**Install necessary libraries**: Ensure you have installed the following libraries within the Databricks environment:

   ```bash
   pip install pyspark delta-spark
```
## Running the Code

1. **Import the notebook** from this repository into your Databricks environment.
2. **Attach the notebook** to a running Databricks cluster.
3. **Run each cell sequentially** to see the analysis results.

- **Read Dataset**:
   ```python
   df = spark.read.format('csv').option('header', 'true').load('/path/to/your/dataset.csv')

**Simple Data Transformation:**:
   ```python
   clean_df = df.filter(df['column_name'].isNotNull())
   ```

**SQL Query on DataFrame**:
   ```python
   df.createOrReplaceTempView("table_name")
   result = spark.sql("SELECT * FROM table_name WHERE condition")
   ```
## Extensions and Future Work

### Additional Features

- **Real-Time Data Processing**:  
  Extend the project to include a real-time data processing pipeline using Spark Streaming.

- **Machine Learning Integration**:  
  Build machine learning models using Spark MLlib for predictive analytics.

- **ETL Pipeline**:  
  Create a robust ETL pipeline with data ingestion, transformation, and storage into Delta Lake.

- **Batch vs. Stream Processing**:  
  Compare batch processing with real-time streaming in terms of performance and use cases.

- **Graph Processing**:  
  Incorporate graph analytics using GraphX for network-based data analysis.


### How to Contribute
If you'd like to contribute to this project, feel free to fork the repository and submit pull requests. Contributions are welcome for improving the codebase, documentation, and adding more advanced features.



