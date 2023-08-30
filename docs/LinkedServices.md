# Linked Services

https://learn.microsoft.com/en-us/azure/data-factory/concepts-linked-services?tabs=data-factory  

### HTTP Linked Service

Steps:  

1. ADF -> Manage -> Linked Service -> New  
2. Search for ```HTTP``` and click continue
3. Give the service a name
4. Leave ```Connect via integration runtime``` as default
5. Provide the ```Base URL```. This is the base part of the target URL. e.g - ```https://github.com```
6. ```Authentication``` is set to ```Anonymous``` because we dont need any usernames or passwords for the base URL access
7. Test the connection then click create