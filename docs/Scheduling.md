# Scheduling Pipeline Execution

Data Factory provides the scheduling ability in the form of triggers. You can create triggers and attach them to pipelines so that the pipelines are triggered as specified in the trigger.  
There are three types of triggers in ADF at the moment:
- Schedule Triggers
- Tumbling Window Triggers
- Event Base Triggers  

## Schedule Triggers

Schedule Triggers are basically scheduled to run on a calendar.  
It supports periodic and specific times. The time doesn't have to be at regular intervals.  
You can have many-to-many relationships in triggers and pipelines. For example, you can attach all your ingestion pipelines to one trigger
and that link work all the pipelines at the same time every day.  
Similarly, you can invoke the same pipeline from more than one trigger. For example, you might want to run a database maintenance pipeline
during ingestion as well as transformation.  
The Schedule Triggers can only be scheduled to start in the future. You can't run them for a past day or a time and also it doesn't make sense to do it that way. And for that you've got Tumbling Window Triggers.

1. ```Manage``` Tab -> Triggers -> New
2.  Select the type of trigger you want (Schedule)
3. Select your execution times

## Tumbling Window Triggers  

Tumbling Window Triggers can only be scheduled to run at periodic interval from a specified time.  
Tumbling Window Triggers are a series of fixed sized non-overlapping and continuous time intervals.  
They're very useful when dealing with slices of data. For example, you have a requirement to ingest data from a SQL database into our Data Lake every hour and we only want to ingest the data created during that hour. You can attach the pipeline to the tumbling window trigger
and that will invoke the pipeline every hour and pass the window start and the end time to the copy activity which can then use those times to fetch the data for that particular slice.  
You can schedule a Tumbling Window Trigger to run for a past date, so if you want to ingest or process data for a previous slice
you just need to run that slice. So for example, you wanna get the data from 9:00 AM to 10:00 AM yesterday. You just run that slice
and it'll fetch the data that got created during that period.  
Due to the fact that they are tightly coupled with pipelines, you can only have one trigger for a pipeline and vice-versa.
There are significant differences between Tumbling Window Triggers and Schedule Triggers.  

1. ```Manage``` Tab -> Triggers -> New
2.  Select the type of trigger you want (Tumbling Window)
3. You can add dependencies to your trigger if you need them (up to 2)
4. You can set delay, concurrency and retry policies for your trigger


## Event Base Triggers (Storage Event Trigger)

They run pipelines in response to an event such as the arrival or a deletion of a file in a Blob storage or a Data Lake storage.
Similar to Scheduled Triggers, you can have many pipelines attached to one trigger and vice versa.  

In order to use the event trigger, we need to register the Azure Event Grid Resource provider to our subscription. An Azure resource provider is a set of REST operations that enable functionality for a specific Azure service. For example, the Key Vault service consists of a resource provider named Microsoft.KeyVault. The resource provider defines REST operations for managing vaults, secrets, keys, and certificates. The resource provider defines the Azure resources you can deploy to your account.  

https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/resource-providers-and-types



1. ```Manage``` Tab -> Triggers -> New
2.  Select the type of trigger you want (Storage Event Trigger)
3. To register the Azure Event Grid Resource provider to our subscription, go to the portal home page -> all services -> search for ```Subscriptions``` -> select your subscription -> select ```Resource Providers``` -> search for ```EventGrid```
4. Then click ok/create 
5. Navigate to your pipeline and select ```Add Trigger``` and choose your trigger  

https://www.udemy.com/course/learn-azure-data-factory-from-scratch/learn/lecture/23892198#overview


