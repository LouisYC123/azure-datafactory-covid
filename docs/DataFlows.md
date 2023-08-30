# Data Flows

Data Flows is a feature of ADF.  

Data Flows can be used to visually design data transformations without writing any code.  

Once you've created the transformations using the visual tools available within data low,
Data Factory translates them to Spark code that executes on scaled out as your Databricks clusters.  

Data Factory manages the translation of the code, management of the Databricks clusters
and execution of the data flow activities in them.  

Data Flows benefit from the scheduling where it triggers and monitoring capabilities within Data Factory

There are two types of data flow:  
- Mapping Data Flow:  
This is the recommended type of data flow for creating transformations when your schema is fixed and you know the transformation logic upfront.

- Wrangling Data Flow:  
This is recommended for visually exploring and preparing datasets.

### Limitations of Data Flows

- Not yet available in all Regions
- Data flows have got only set of limited connectors available:
 The main support currently is for Azure storages such as ADLS Gen2, Azure Blob Storage,
Azure Sequel Database, Azure Synapse Analytics. Limited support for 3rd party as yet.
- Not suitable for complex logic:
 For complex logic, you are better off writing in spark and executing via ADF 


## Steps

1. ADF -> Author -> Data Flow -> New Data Flow
2. Add Source -> Choose dataset (Every Data Flow needs a `Source` and a `sink`)
3. `Optimize` is where you can performance tune
4. `Inspect` lets you inspect the columns
5. Partitioning is important as the underlying compute is done on Spark:
    - `Use Current Partition`  lets ADF decide the partition
    - `Single Partition` is essentialy single thread-processing
    - `Set Partitioning` lets you choose the partition strategy
6. `Data flow debug` must be turned on to use `Data Preview`, but note, this spins up a spark cluster and so incurs a charge.
7. If you click the plus sign to the right of the transformation you can view the full list of transformations available
8. The data flows themselves are not executable, so you'll have to build a pipeline to execute a data flow. ADF has a specific `Data Flow` activity
9. In the `Data Flow` acitvity in ADF, you specify the settings such as which kind of cluster you wanna run on, which integration run time you want to run your cluster on as well and any parameters you want to send.
10. Back in Data Flow - `Source Type` defines wether you use one of your pre-configure datasets or a Data Flow `Inline` one. The decision on whether to use a data set
or inline is based on a few factors:
    - whether that type is supported
    - whether you want to use that data set in any of my other transformations.If that's the case, it's easier to you create a data set and then reuse it everywhere.
    -  If you have a fixed schema and you know and understand the data set really well, then this should go in a `Dataset`.
11. `Allow Schema drfit` - if you expect your source data to change often, even if there is a new column being added to the data set,data flow will just flow that through to the sync.
12. Alternatively, ticking `Validate Schema` will fail if a dataset does not conform to a specified schema.
13. `Sampling` allows random sampling of records for testing purposes.
14. The `Projection` tab lets you  deal with the actual data types manually  
15. `Inspect` & `Data Preview` shows you what will come out of the source transformation.



https://www.udemy.com/course/learn-azure-data-factory-from-scratch/learn/lecture/23931336#overview