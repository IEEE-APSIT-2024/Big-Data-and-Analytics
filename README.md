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

1) Driver Program: It is the main application entry point that creates SparkContext (the gateway to Spark) and uses this to coordinate with the workers.
2) Cluster Manager: Manages resource allocation for the Spark application (e.g., YARN, Mesos).
3) Worker Nodes: They run on the nodes in the cluster and execute tasks assigned by the Driver.

# What is Scala?

Scala is the primary language used to develop Apache Spark, and it's one of the best languages to work with Spark because Spark itself is written in Scala (Scaleable Language)

## Example of Scala Syntax

Here's a simple example to illustrate some Scala features:

```scala
// Define a case class
case class Person(name: String, age: Int)

// Create a list of Person objects
val people = List(
  Person("Alice", 25),
  Person("Bob", 30),
  Person("Charlie", 35)
)

// Use functional programming to filter and map the list
val names = people
  .filter(_.age > 28)
  .map(_.name)

// Print the result using string interpolation
println(s"Names of people over 28: ${names.mkString(", ")}")
```

# RDD in use?

Resilient Distributed Datasets (RDDs) are the fundamental building blocks of Apache Spark. They represent a distributed collection of data across a cluster, and the operations you perform on RDDs enable parallel processing. RDDs provide an abstraction to work with data in a distributed, fault-tolerant manner, ensuring both efficiency and reliability.

![image](https://github.com/user-attachments/assets/4a191277-29a0-464e-8ce6-35ab1f4c1bc1)


# Spark Components: Here we go again!

![image](https://github.com/user-attachments/assets/6ca021f6-8f13-4d78-bc61-e8006265d48a)

a) Spark Core: The foundation that provides distributed task dispatching, scheduling, and basic I/O functionalities.
b) Spark SQL: Module for working with structured data.
c) Spark Streaming: For processing real-time streaming data.
d) MLlib: A distributed machine learning framework.
e) GraphX: A distributed graph processing framework.


### How to Contribute
If you'd like to contribute to this project, feel free to fork the repository and submit pull requests. Contributions are welcome for improving the codebase, documentation, and adding more advanced features.



