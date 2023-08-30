# Integration Runtimes

The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory and Azure Synapse pipelines to provide the following data integration capabilities across different network environments:
- Data Flow: Execute a Data Flow in a managed Azure compute environment.
- Data movement: Copy data across data stores in a public or private networks (for both on-premises or virtual private networks). The service provides support for built-in connectors, format conversion, column mapping, and performant and scalable data transfer.
- Activity dispatch: Dispatch and monitor transformation activities running on a variety of compute services such as Azure Databricks, Azure HDInsight, ML Studio (classic), Azure SQL Database, SQL Server, and more.
- SSIS package execution: Natively execute SQL Server Integration Services (SSIS) packages in a managed Azure compute environment.
In Data Factory and Synapse pipelines, an activity defines the action to be performed. A linked service defines a target data store or a compute service. An integration runtime provides the bridge between activities and linked services. It's referenced by the linked service or activity, and provides the compute environment where the activity is either run directly or dispatched. This allows the activity to be performed in the closest possible region to the target data store or compute service to maximize performance while also allowing flexibility to meet security and compliance requirements.
Integration runtimes can be created in the Azure Data Factory and Azure Synapse UI via the management hub directly, as well as from any activities, datasets, or data flows that reference them.

### Integration runtime types
Data Factory offers three types of Integration Runtime (IR), and you should choose the type that best serves your data integration capabilities and network environment requirements. The three types of 

IR are:
- Azure
- Self-hosted
- Azure-SSIS

Integration Runtimes can be created in a number of ways. 

For example, in ADF -> Manage -> Integration Runtimes -> New