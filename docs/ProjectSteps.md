# Detailed Steps


### HTTPS Activity
1. Create ```Linked Service``` for HTTP target (Github in this case)
2. Create a Source dataset
3. Create a Sink Dataset
4. Create Pipeline to download file from HTTP target
    4.1. Add a CopyActivity
    4.2. Select `Source` and `Sink`
    4.3. Pass filenames as parameters to the Pipeline

### Data Flow Activity
1. ADF -> Author -> New Data Flow
2. Give your Data Flow a name
3. click `Add Source`
4. add a `filter` step
    - ```continent == 'Europe' && not(isNull(country_code))```
5. drop and rename columns using a `Select` transformation
6. prefix incoming column names using a rule-based mapping
7. pivot the `indicator` and `daily_count` using the `pivot` transformation
8. Lookup 2-digit country code using `Lookup` activity

## Create a managed Identity for HDInsight
1. Create a managed identity 
2. Provide access to the Data Lake for their managed identity.
3. Assign to our HDInsight cluster.

## Create an HDInsight Cluster
(Not done due to limitations of free subscription)

## Create a Databricks service & Cluster
1. Create a Databricks service
2. 




Databricks Workspace

Please create the workspace in the region UK South. If you have already created a workspace in another region, please delete that and create in the UK South Region.

Databricks Cluster

Please use the following configuration for the databricks cluster.

Cluster Type - Single Node

Node Type - Standard_D4a_v4