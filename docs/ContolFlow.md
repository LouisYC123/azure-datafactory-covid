# Control Flow Activities

## Handling Common Production Scenarios 

#### Execute Copy Activity when the file becomes available

Scenario: The data is made available daily, and it could become available anytime during the day, and we don't know what time it becomes available. We need to process the data as soon as it's become available. There are multiple ways, including using control flow activity in Data Factory:  
1. Schedule the pipeline to run every day at midnight
2. use a ```Validation``` activity to ensure that the pipeline only continues once the file has arrived.  
3. Under Settings, select the target dataset
4. Set the ```Timeout``` duration to 1 day  (1.00:00:00)
5. Set the ```Sleep``` interval (poke interval) to something sensible like 10 minutes (600)
6. (Optional) ```Minimum size``` lets you specify the mimimum file size before starting to ingest (to avoid ingesting a large file halfway through it being uploaded)  (e.g - 1024 , measured in bytes)


#### Exectute Copy Activity only if the file contents are as expected

Scenario: We want to ensure that the file we've received is as expected before copying the file to the Data Lake.  We expect 13 columns in the input file. So, let's make sure that the file has 13 columns before we copy the data to Data Lake.  
Data Factory gives you two activities to achieve this:
- 'Get Metadata': lets you get the metadata about the file itself.
- 'If Condition Activity': That'll let you make sure that the condition is satisfied. e.g - you can ask If Condition to check
whether the column count is 13 before you call the Copy Data activity.  
  
1. Select the ```Get Metadata``` activity
2. Under Settings, select the target dataset  
3. Next to ```Field list```, select 'New' and choose the type of metadata you want, in this case ```Column Count```, ```Size``` and ```Exists```
4. Select a ```If Condition``` activity.
5. Under the ```Activites``` tab, Click in the ```Expression``` box and then click the ```Add dynamic content``` box that appears
6. In the expression builder window, place a ```equals``` and inside that, place a ```Get File Metadata```
7. Add ```.columnCount, 13```
8. Full expression is: ```@equals(activity('Get File Metadata').output.columnCount, 13)```
9. Click on the pencil that is next to the ```True```
10. You can then chain this with the above ```Validation``` activity so the full pipeline is:  ```Check file exists -> Get Metadata -> Check Metadata is as expected -> Copy files if Metadata is as expected ```
11. For fail conditions, you can use a ```Web``` activity to send an email.


#### Delete the source file on successful copy

1. Select the ```Delete``` Activity
2. Under ```Source``` select the dataset you want to delete



Validation Activity - https://docs.microsoft.com/en-us/azure/data-factory/control-flow-validation-activity

Get Metadata Activity - https://docs.microsoft.com/en-us/azure/data-factory/control-flow-get-metadata-activity

If Condition Activity - https://docs.microsoft.com/en-us/azure/data-factory/control-flow-if-condition-activity

Web Activity - https://docs.microsoft.com/en-us/azure/data-factory/control-flow-web-activity

Delete Activity - https://docs.microsoft.com/en-us/azure/data-factory/delete-activity

Fail Activity - https://learn.microsoft.com/en-us/azure/data-factory/control-flow-fail-activity
