# PySpark GraphFrame Streaming: Vertices and Edges Data Processing

This project demonstrates real-time processing of vertices and edges data using PySpark Streaming. 
The goal is to read streaming data from source directories, apply transformations, and write the processed data to a sink in Parquet format. 
The datasets represent a graph structure where vertices correspond to locations (e.g., cities), and edges represent relationships (e.g., flights between cities).

## Project Overview

The project consists of the following main steps:

### 1- Defining Schemas: Define schemas for both the vertices and edges datasets to ensure the data is structured correctly during streaming.
### 2- Creating Streaming DataFrames:
        - Two streaming DataFrames are created: one for the vertices data and another for the edges data. 
        - Each DataFrame reads from a separate source directory that will stream the respective data in real time.
### 3- Transforming Data:
        - Edges Data: A new column is added to categorize delays into three categories:
            Early: Flights arriving earlier than scheduled (negative delay values).
            Late: Flights arriving later than scheduled (positive delay values).
            On Time: Flights arriving exactly on time (zero delay values).
        - Vertices Data: Rows with empty values in the State field are filtered out to ensure data integrity.
### 4- Writing Data to Parquet:
        - The transformed data from both DataFrames (edges and vertices) is written to two separate sink directories in Parquet format.
        - A checkpointing mechanism is used to ensure fault tolerance and enable stream recovery.
### 5- Starting and Stopping the Streaming Queries:
        - The streaming queries are started for both the edges and vertices DataFrames. 
        - The data is manually copied into the respective streaming source directories, allowing the queries to process the incoming data and write it to the sink.
        - Once the data is fully processed, the queries are stopped.
### 6- Reading the Processed Data:
        - After the streaming process is completed, the Parquet files are read from the sink directories into static DataFrames for further analysis or processing.
