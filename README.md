# Performing ETL by building a workflow using Airflow, streaming data to Kafka and later loading it to a MySQL database

In this project I will be collecting data from different file formats (csv, tsv, fixed width) and consolidating it by building a DAG workflow on Apace Airflow, which then streams the data in real-time to Apache Kafka. From this point, I will create a data pipeline that collects the streaming data and loads it into a database.

A broad overview of the steps I will be performing -

- Using Python to build an Airflow DAG, having tasks dealing with consolidating and transforming data from various file formats
- Using Airflow CLI to submit, unpause, interact with and operate the DAG
- Using Kafka CLI and Kafka Python Driver to create topic, produce and consume streaming data in real time
- Using MySQL for creating a database and storing the data

**About the problem -** 

This is a data engineering problem that aims to de-congest the national highways by analyzing the road traffic data from different toll plazas. Each highway is operated by a different toll operator with different IT setup that use different file formats. The goal is to collect this data, bring it into one form, perform some essential transformation on it and stream the data in real-time, storing it into a database. The problem was a part of IBM's capstone project for the course - ETL and Data Pipelines with Shell, Airflow and Kafka.


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


Now I will submit this DAG (python script named ETL_toll_data.py) using Airflow CLI, and verify if it shows in the dags list.

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/a09f222b-295c-4af6-9d7f-536dc92a9cd5)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/45a86bce-4c59-488d-a2ee-adc4441cc43d)

Then I will unpause the DAG to begin the workflow.

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/306ab6c5-76fe-4605-a308-4d6d790cccf3)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/a3e16bf0-249b-4ba4-8a20-083fa7934f1c)

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/d3dbe11e-efb5-4eb0-aa94-ca814264d50c)

## Kafka for receiving the stream and loading data into MySQL db 

Creating a database tolldata and a table within it called livetolldata to receive the stream.

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/a87b4382-a8dd-497b-9ead-66f80cf0c8e9)

I will be using Kafka CLI, and the Kafka Python driver to work with Kafka server, to create topics, stream data and load it.

**Creating a topic -** 

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/e173e0f7-8dad-4401-be7a-597086721d3f)

**Kafka Producer Python script -**  

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/049daa2d-f644-4667-9862-969d4721a902)

**Output of the Producer -**

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/84c44f21-e4b7-40b5-9278-69f3414c27b5)

**Kafka Consumer Python script -** - 

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/fe97ae19-56f0-45db-811b-57eff8060819)

**Output of the Consumer -**

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/d8ddcaa3-8525-4ffe-b2f3-2a62ab7c3323)

**Verifying if the data is loading into the MySQL database -**

![image](https://github.com/Abhishek-Dxt/ETL_Airflow_Kafka/assets/71979171/263762ee-192f-49bc-8eb3-4927a7bb09e9)



It can be seen that the **data is successfully being loaded into the MySQL DB in real-time**, going first through transformation on the various formats using Airflow dag tasks and later being produced and consumed using Kafka Topic & Python Driver scripts. 
