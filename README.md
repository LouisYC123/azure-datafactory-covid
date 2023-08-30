# Covid-19 Data Pipeline

![azure-covid-proj drawio](https://github.com/LouisYC123/azure-datafactory-covid/assets/97873724/50ef968d-01c2-4354-be3e-c74096448df1)

## Dashboard

![dash1](https://github.com/LouisYC123/azure-datafactory-covid/assets/97873724/e01551b8-18bb-4be7-a627-48cc8e62bdeb)  

![dash3](https://github.com/LouisYC123/azure-datafactory-covid/assets/97873724/5755f081-2d69-48c8-b893-1eda2bcb2ee3)

## Prerequisites
- Create blob storage container for raw data from Eurostat
- Create a container name ```raw``` in the Data Lake

### Naming Standards
```<nameOfService>_<typeOfStorageAccount>_<nameOfStorageAccount>```  

e.g:  
```
ls_ablob_covidreportingsa     # linkedService_blobStorage_StorageName
```

## Extract
 - Eurostat data that provides the population of each EU country
 - This has been downloaded from the EuroStat website and saved in a blob storage container.
 - ADF Copy Activity will copy this from blob storage into the Data Lake
    - Copy Activity
        - Copy Data
        - Copy metadata including: name, type and structure of file
    - Uses a Linked Service
    - Control Flow includes: validation activity, If conditions, web activity, get metadata activity, delete activity, trigger
- Another ADF Activity will download a CSV file from the ECDC website and copy across to the data lake.

## Transform
 - Data Flows

## Data Lake

Contains the following data:

- Confirmed Cases
- Mortality
- Hospitilisation / ICU Cases
- Testing Numbers
- Countrys population by age group


## Build

1. HTTP Connector + Parametrized CopyActivity to get data and load to Data Lake
2. Data Flow to transform the `Cases & Deaths` Data:
    - Filter out non-EU countries
    - Create a 'standard' country code using name
    - pivot the `indicator` and `daily count` columns
    - drop the `rate_14_day` column
    - rename `date` as `reported_data`