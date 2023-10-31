# Performing ETL by building a workflow using Airflow, streaming data to Kafka and later loading it to a MySQL database

In this project I will be collecting data from different file formats (csv, tsv, fixed width) and consolidating it by building a DAG workflow on Apace Airflow, which then streams the data in real-time to Apache Kafka. From this point, I will create a data pipeline that collects the streaming data and loads it into a database.

- Using Python to build an Airflow DAG, having tasks dealing with consolidating and transforming data from various file formats
- Using Airflow CLI to unpause, interact and operate the DAG

**About the problem -** 

This is a data engineering problem that aims to de-congest the national highways by analyzing the road traffic data from different toll plazas. Each highway is operated by a different toll operator with different IT setup that use different file formats. The problem was a part of IBM's capstone project for the course - ETL and Data Pipelines with Shell, Airflow and Kafka.


## Data Workflow on Airflow
Data from different file formats will first all be consolidated into a uniform csv format, from where necessary transformations will performed on the data. 

<img width="877" alt="task_pipeline_" src="https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/b2d8060c-81b0-4a94-bdd2-ef9559e55245">

I will first create a DAG on Airflow, importing libraries and defining the deafult arguments, DAG definition, and writing the required tasks.

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/eafc4c1e-ade0-44e9-b247-fa4d2f3a81b6)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/8f4f8fc8-0f14-4da5-bd82-8942cdd7fb6d)

Having defined the DAG and its arguments, the primary tasks will be -
1. Unzip the data (all data comes together in tar file)
2. Extract data from different file sources
3. Consolidate all data together in one csv file
4. Transform the data

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/b88a4eb9-57ac-4100-9242-f9baee088b71)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/18ba8cf8-fc81-4ddf-93cf-5e42ae413894)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/4a18887d-6251-4d63-af00-6cd706862adf)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/797aa254-daa8-411e-92cf-94af2783876b)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/75fe4336-b569-470f-b8d7-dbebc33ee770)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/92c35023-29b8-4682-835f-1de5e333db7a)



