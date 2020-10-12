# Clinical Data Exchanges:
## Project Description:
The project is aimed to store, process & manage the huge amount of data in a day to day operations collected from various clinical data sources.
The system establishes the automated exchange of member clinical information with provider and vendor partners to drive increased care coordination and new clinical insights.

## Data architecture
![Image of data architecture](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2018/04/25/overall-ref-arch-1024x581.png)

## ETL Flow
- Data Collected from the API is moved to landing zone s3 buckets.
- ETL job has s3 module which copies data from landing zone to working zone.
- Once the data is moved to working zone, spark job is triggered which reads the data from working zone and apply transformation. Dataset is repartitioned and moved to the Processed Zone.
- Warehouse module of ETL jobs picks up data from processed zone and stages it into the Redshift staging tables.
- Using the Redshift staging tables and UPSERT operation is performed on the Data Warehouse tables to update the dataset.
- ETL job execution is completed once the Data Warehouse is updated.
- Dag execution completes after these Data Quality check.

## Hardware Used
EMR - I used a 3 node cluster with below Instance Types:
m5.xlarge
4 vCore, 16 GiB memory, EBS only storage
EBS Storage:64 GiB
Redshift: For Redshift I used 2 Node cluster with Instance Types dc2.large
