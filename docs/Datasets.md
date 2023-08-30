# Datasets

Datasets identify data within different data stores, such as tables, files, folders, and documents. For example, an Azure Blob dataset specifies the blob container and folder in Blob Storage from which the activity should read the data



Steps:  

1. Azure Data Factory -> Author -> Datasets -> New Dataset
2. Select the type you want, for example ```HTTP``` (you will also need to select a format if you choose http, e.g - ```DelimitedTest```)
3. Give your dataset a name
4. Select the ```Linked Service``` you created previously  
5. If using ```HTTP```, provide the relative URL (e.g - everything after the base URL)  
6. You would also then create your ```Sink``` (target) dataset. This is typically an Azure storage object of some kind (e.g - Azure Data Lake Storage Gen2)
7. Provide a name, select your ```Linked Service``` and choose a location for your ```Sink``` under ```File Path```
8. Select ```None``` under ```Schema``` if you dont want to do any mapping