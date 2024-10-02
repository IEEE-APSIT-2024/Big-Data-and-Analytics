# ML Ops with Spark

This project demonstrates the use of PySpark for a machine learning workflow, specifically for predicting total bill amounts based on various features from a restaurant tips dataset.

## Table of Contents

1. [Introduction](#introduction)
2. [Setup](#setup)
3. [Data Loading and Exploration](#data-loading-and-exploration)
4. [Data Preprocessing](#data-preprocessing)
5. [Feature Engineering](#feature-engineering)
6. [Model Training](#model-training)
7. [Model Evaluation](#model-evaluation)
8. [Conclusion](#conclusion)

## Introduction

This project uses PySpark to perform a simple machine learning task. We use a dataset containing information about restaurant bills and tips to predict the total bill amount based on various features such as tip amount, party size, and categorical variables like sex, smoker status, day of the week, and time of day.

## Setup

The project uses PySpark, which should be set up in your environment. The following imports are used:

```python
from pyspark.ml.feature import StringIndexer
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.regression import LinearRegression
```

## Data Loading and Exploration

The data is loaded from a CSV file:

```python
file_location = "/FileStore/tables/tips.csv"
file_type = "csv"

df = spark.read.csv(file_location, header=True, inferSchema=True)
df.show()
```

The dataset contains the following columns:
- total_bill
- tip
- sex
- smoker
- day
- time
- size

## Data Preprocessing

### Handling Categorical Features

We use StringIndexer to convert categorical variables into numerical indices:

```python
indexer = StringIndexer(inputCol="sex", outputCol="sex_indexed")
df_r = indexer.fit(df).transform(df)

indexer = StringIndexer(inputCols=["smoker", "day", "time"], 
                        outputCols=["smoker_indexed", "day_indexed", "time_index"])
df_r = indexer.fit(df_r).transform(df_r)
```

## Feature Engineering

We use VectorAssembler to combine our features into a single vector column:

```python
featureassembler = VectorAssembler(
    inputCols=['tip', 'size', 'sex_indexed', 'smoker_indexed', 'day_indexed', 'time_index'],
    outputCol="Independent Features"
)
output = featureassembler.transform(df_r)
```

## Model Training

We split our data into training and test sets, then train a Linear Regression model:

```python
train_data, test_data = finalized_data.randomSplit([0.75, 0.25])
regressor = LinearRegression(featuresCol='Independent Features', labelCol='total_bill')
regressor = regressor.fit(train_data)
```

The model coefficients and intercept are:

```python
print("Coefficients:", regressor.coefficients)
print("Intercept:", regressor.intercept)
```

## Model Evaluation

We evaluate our model on the test data:

```python
pred_results = regressor.evaluate(test_data)
pred_results.predictions.show()
```

The performance metrics are:

```python
print("R-squared:", pred_results.r2)
print("Mean Absolute Error:", pred_results.meanAbsoluteError)
print("Mean Squared Error:", pred_results.meanSquaredError)
```

## Conclusion

This project demonstrates a basic machine learning workflow using PySpark, including data loading, preprocessing, feature engineering, model training, and evaluation. The Linear Regression model achieved an R-squared value of approximately 0.56, indicating that there's room for improvement in predicting total bill amounts.

Future work could include:
- Feature selection to identify the most important predictors
- Trying different regression algorithms (e.g., Random Forest, Gradient Boosting)
- Hyperparameter tuning to optimize model performance
- Handling potential outliers or influential points in the dataset

