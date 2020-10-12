# Clinical Data Exchanges:
## Project Description:
The project is aimed to store, process & manage the huge amount of data in a day to day operations collected from various clinical data sources.
The system establishes the automated exchange of member clinical information with provider and vendor partners to drive increased care coordination and new clinical insights.

## Data archtecure

## ETL Flow
Data Collected from the API is moved to landing zone s3 buckets.
ETL job has s3 module which copies data from landing zone to working zone.
Once the data is moved to working zone, spark job is triggered which reads the data from working zone and apply transformation. Dataset is repartitioned and moved to the Processed Zone.
Warehouse module of ETL jobs picks up data from processed zone and stages it into the Redshift staging tables.
Using the Redshift staging tables and UPSERT operation is performed on the Data Warehouse tables to update the dataset.
ETL job execution is completed once the Data Warehouse is updated.
Dag execution completes after these Data Quality check.

