# ADF Pipelines


### Pipeline Parameters
Parameters are external values passed into pipelines, datasets or linked services.  
The value cannot be changed inside a pipeline.    
A pipeline can receive a parameter, send that to a data set and the data set can then send that to a link service.  

Scenario: Passing in target filenames to a ```Copy Activity``` as a `Parameter`  

#### Passing filename parameters to a pipeline via a trigger
Steps:  

1. ADF -> Author -> Select your source dataset -> Parameters -> New
2. Provide a name and type for your parameter
3. -> Connection 
4. Remove the `Relative URL` (or whatever it is you are parameterizing)
5. click `Add dynamic context` (hover over the box to see this)
6. Add the parameter you just created
7. Click Finish
8. Repeat this for your `Sink` (target dataset) if needed.
9. Back in the Pipeline view, select `Parameters`
10. Create and name your parameters
11. Now your pipeline expects these parameters to be passed in at runtime, so we need to get the trigger to pass them in:
12. Manage -> Triggers -> Create your trigger -> ok -> the next window will ask for the parameters
13. Add the parameter values
13. Back in your pipeline select `Add trigger`
14. Choose the trigger you just created

#### Using Lookup and For Each to dynamically add paramter values
We can improve on this further by dynamically adding the parameter values using a `Lookup` activity.  

Lookup activity can retrieve a dataset from any of the data sources supported by data factory and Synapse pipelines. You can use it to dynamically determine which objects to operate on in a subsequent activity, instead of hard coding the object name. Some object examples are files and tables.
Lookup activity reads and returns the content of a configuration file or table. It also returns the result of executing a query or stored procedure. The output can be a singleton value or an array of attributes, which can be consumed in a subsequent copy, transformation, or control flow activities like ForEach activity.  

Lookup Activity: https://learn.microsoft.com/en-us/azure/data-factory/control-flow-lookup-activity 

Steps:  

1. Create a json file that contains your parameter values
2. Upload this json file into blob storage
3. Create a dataset that points to the file you just created
4. select the linked service for your blob storage
5. in your pipeline, create a `Lookup` task.
6. choose the source dataset you just created
7. untick the `First Row Only` box
7. Then create a `ForEach` activity
9. in `Items`, click 'add dynamic content'
10. Select the `Lookup activity output` and add `.value`. e.g - `@activity('Lookup1').output.value`
11. Click ok / finish
12. under the `Activities` tab of the `ForEach` activity, click the pencil icon
13. copy and paste your `Copy Data` activity 
14. Select your Copy Activity and under `Source`, add/edit the values for the parameters 
15. Select `Execute Copy for Every Record` and add your parameter to the item(). e.g - `@item().sourceRelativeURL`
16. Repeat this for your `Sink` if you have paramters for the sink 





https://www.udemy.com/course/learn-azure-data-factory-from-scratch/learn/lecture/23908620#overview


### Pipeline Variables

Variables are internal values that are set inside a pipeline. The value can be changed inside a pipeline using `Set Variable` or `Append Variable Activity`. For example, you can increment the value of variable inside your pipeline using a set variable or an append variable activity. So that comes in handy when you want to iterate over something and you wanna set the initial and the end values for those.

Both `Parameters` and `Variables` can make your pipeline more dynamic, for example, helping it to deal with a different file each time it is called.

