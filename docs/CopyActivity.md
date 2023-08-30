# Copy Activity

In Azure Data Factory and Synapse pipelines, you can use the Copy activity to copy data among data stores located on-premises and in the cloud. After you copy the data, you can use other activities to further transform and analyze it. You can also use the Copy activity to publish transformation and analysis results for business intelligence (BI) and application consumption.  

The Copy activity is executed on an integration runtime.   
The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory and Azure Synapse pipelines to provide the following data integration capabilities across different network environments:
- Data Flow: Execute a Data Flow in a managed Azure compute environment.
- Data movement: Copy data across data stores in a public or private networks (for both on-premises or virtual private networks). The service provides support for built-in connectors, format conversion, column mapping, and performant and scalable data transfer.
- Activity dispatch: Dispatch and monitor transformation activities running on a variety of compute services such as Azure Databricks, Azure HDInsight, ML Studio (classic), Azure SQL Database, SQL Server, and more.
- SSIS package execution: Natively execute SQL Server Integration Services (SSIS) packages in a managed Azure compute environment.

In Data Factory and Synapse pipelines, an activity defines the action to be performed. A linked service defines a target data store or a compute service. **An integration runtime provides the bridge between activities and linked services.** It's referenced by the linked service or activity, and provides the compute environment where the activity is either run directly or dispatched.  

An integration runtime needs to be associated with each source and sink data store.  

To copy data from a source to a sink, the service that runs the Copy activity performs these steps:
1. Reads data from a source data store.
2. Performs serialization/deserialization, compression/decompression, column mapping, and so on. It performs these operations based on the configuration of the input dataset, output dataset, and Copy activity.
3. Writes data to the sink/destination data store.

Azure Data Factory supports the following file formats:
- Avro format
- Binary format
- Delimited text format
- Excel format
- JSON format
- ORC format
- Parquet format
- XML format


You can use the Copy activity to copy files as-is between two file-based data stores, in which case the data is copied efficiently without any serialization or deserialization. In addition, you can also parse or generate files of a given format, for example, you can perform the following:
- Copy data from a SQL Server database and write to Azure Data Lake Storage Gen2 in Parquet format.
- Copy files in text (CSV) format from an on-premises file system and write to Azure Blob storage in Avro format.
- Copy zipped files from an on-premises file system, decompress them on-the-fly, and write extracted files to Azure Data Lake Storage Gen2.
- Copy data in Gzip compressed-text (CSV) format from Azure Blob storage and write it to Azure SQL Database.
- Many more activities that require serialization/deserialization or compression/decompression.


https://learn.microsoft.com/en-us/azure/data-factory/copy-activity-overview  


A use case might be: Ingesting data from Azure blob storage to Azure Data Lake using copy activity in ADF.  
When using a Copy, we need connection details. For example, the connection details between a blob storage and Azure Data Lake.  
In Data factory, these connection details are represented by ```Link Services```  
The copy activity itself is not executable, so we need a pipeline to wrap all of this up so that it can be executed.


### Steps

In general, to use the Copy activity in Azure Data Factory or Synapse pipelines, you need to:
1. Create linked services for the source data store and the sink data store.  
2. Create datasets for the source and sink. 
3. Create a pipeline with the Copy activity. 


#### Detailed Steps


1. Open up Azure Data Factory Studio
2. -> Manage
3. -> Linked Services
4. Create a linked service for both source and target
5. Then create a ```Dataset```: click the pencil ```Author``` icon.
6. Choose the right settings for your data set type (Delimited Text in our case)
7. Provide the path to the file saved in the blob storage
8. We are just doing a straight copy so we can select ``` None ``` for the schema infer options
9. Specify the compression (gzip in our case) , compression level and the column delimiter
10. Create a new pipeline and add a ```Copy data``` task
11. ```Secure output``` annd ```Secure input``` - prevents seneitive data from being written to log files
12. Select your ```Source``` and ```Sink``` (target)
13. Mapping is for column source-to-target mapping
14. You can use ```Validate All``` to check for errors and ```Debug``` to test

