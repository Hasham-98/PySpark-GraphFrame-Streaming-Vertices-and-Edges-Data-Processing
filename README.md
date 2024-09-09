# PySpark Streaming and GraphFrame Processing for Vertices and Edges Data


## Project Overview

This project demonstrates the processing of streaming data using Apache Spark and GraphFrames. 
It involves two dataframes for vertices and edges, which are streamed, transformed, and written to storage. 
The processed data is then used to create a graph and apply the PageRank algorithm to find the most important vertices. 
Additionally, a machine learning pipeline is built to predict flight delays based on edge data.


## Project Steps



## 1. Initial Setup

#### Schemas Definition:
        Schemas for both vertices and edges data are defined using the StructType and StructField classes from PySpark.
#### Data Sources:
        The data consists of two folders:
            VertFinalExam: Contains the vertices data.
            EdgesFinalExam: Contains the edges data.
        These represent the vertices and edges of a graph for use with the GraphFrame API.



## 2. Streaming Data Input

#### Streaming Readers:
        A streaming reader is set up for both vertices and edges data from the two respective folders.
        The data from each folder is read into separate streaming DataFrames.



## 3. Data Transformation

#### Edges Data:
        A new column, delay_category, is created based on the delay values in the edges dataframe. The delay categories are defined as:
            - Early: For negative delay values (flights that arrive earlier than expected).
            - Late: For positive delay values (flights that arrive later than expected).
            - OnTime: For flights that arrive on time (0 delay values).
#### Vertices Data:
        The vertices dataframe is filtered to remove rows where the State column is empty.



## 4. Data Writing

#### Streaming Writers:
        Both transformed edges and vertices dataframes are written to disk in csv format.
        The process is checkpointed to ensure data consistency and fault tolerance.



## 5. Read Data

#### Static DataFrames:
        After writing the streaming data, the parquet files are read into static dataframes:
            Vertices Data: Read from the folder containing the vertices CSV files.
            Edges Data: Read from the folder containing the edges CSV files.
        These static dataframes will be used to construct the GraphFrame for further analysis and ml models.



## 6. Graph Creation and Analysis

#### GraphFrame Creation:
        A GraphFrame is created using the processed vertices and edges data.

#### PageRank Algorithm:
        The PageRank algorithm is applied to the graph to find the most important vertices.
        The top 10 vertices based on their PageRank score are selected and displayed.



## 7. Machine Learning

#### Task:
        The goal is to predict the delay category (Early, Late, OnTime) for flights using a classification model.

#### Data Preparation:
        The categorical delay_category column is converted into integer labels (0 for Early, 1 for Late, 2 for OnTime).

#### Data Splitting:
        The data is split into 80% training and 20% testing sets for model training and evaluation.

#### Feature Engineering:
        The selected features are delay and distance, which are combined into a single feature vector using the VectorAssembler transformation.

#### Classifier:
        A Logistic Regression classifier is used to predict the delay category.



## 8. Model Pipeline

#### Pipeline Setup:
        A PySpark pipeline is created with the following stages:
            VectorAssembler: To combine the features into a single vector.
            Logistic Regression Classifier: To predict the delay category.
#### Model Training:
        The pipeline is fit on the training data to produce the classification model.


## 9. Model Evaluation

#### Predictions:
        The trained model is applied to the test data to make predictions.
#### Evaluation Metrics:
        The performance of the model is evaluated using two metrics:
            F1 Score: A measure of precision and recall.
            Accuracy: The percentage of correct predictions.
       The expected model performance should achieve at least a 0.5 F1 score and 0.6 accuracy.


## Requirements

    - PySpark
    - GraphFrames
    - IPython for displaying HTML content
    - Python Libraries:
        findspark, pyspark.sql, pyspark.ml


## Conclusion

This project showcases how to process streaming data, create a graph using GraphFrames, apply the PageRank algorithm, 
and build a machine learning pipeline for predicting flight delays. 
It is a great demonstration of integrating multiple techniques such as graph analysis and machine learning in a real-world scenario.
