# Azure functions

# WebJobs

WebJobs enable you to run a program or script in the same instance as a web app, API app or mobile app.

WebJobs provide a UI for self-service administration. 

WebJobs currently support Python only without the WebJobs SDK. 

WebJobs support triggers by timer, Azure Storage queues and blobs, Azure service bus queues and topics, Azure Cosmos DB, Azure Event Hubs, File system. 

# Data Storage

For easier exploration of Azure storage, download [Azure Storage Explorer][6]

## [Blob storage][1]
* cloud file system
* the cheapest and with the best performance
* recommended for any solution which stores larger datasets
* can be made accessible publicly and easily downloaded and shared
* specific storage -> as a file, e.g. binary serialized pandas dataframe
* images, documents which can be opened directly in the browser
* distributed access
* streaming video and audio
* write log files
* backup and restore, disaster recovery, archiving
* store data for analysis by an on-premises or Azure-hosted service
* can be accessed via HTTPS from anywhere
* client libraries support python

## [Azure Table storage][2]
* simple tabular data
* non-relational structured data (structured NoSQL data)
* data that don't require complex joins, foreign keys, or stored procedures and can be denormalized for fast access
* schemaless design
* every entity must have PartitionKey + RowKey
* allows searching through the data, choose subset of the dataset based on the Keys
* user data for web applications, address books, device information, metadata
* accepts authenticated calls from inside and outside the Azure cloud
* a table is a collection of entities (<1MB for Azure storage, <2MB for Azure Cosmos DB)
* Azure table storage doesn't support array/list/dict data types and thus you cannot have a column which includes only arrays; the workaround is to store JSON with key value pairs containing arrays in a column

[Create Azure Table storage][5]

### Accessing Azure table storage from python
Use [azure-data-tables][7] for easy manipulation of azure storage from python.

The entity (single data entry) is a data type of python dictionary.

When using a NoSQL storage, there is a lot of new ways of thinking about your storage. 

You can store the entire dataframes within a single RowKey. Let's say you set a single market and a day as your partition. You set a stock as your row. Within the data, you can store a price prediction for every minute of that stock for that day. You can then use the partition and row indexes to retrieve specific objects as you need them.

If you are getting Bad request on a valid entity creation, check out the size of the inserted data. When I was inserting dicts >= 33 KB I was getting the Bad request on create_entity.

If you are getting the getaddr error, try to use a different connection string to your Azure storage account.

Check [azure_tables_code_template](../code_templates/azure/azure_tables.py) for a simple how to guide.

Interesting article about costs of data storage in Azure tables on large scale, how to delete them and how to think about the design of your storage to keep deletion in mind.
[Reaching the limits of Azure Table storage ... or trying to][8]

[Azure table storage design guide][9]

## Azure PostgreSQL or CosmosDb
* relational database
* most expensive solution

## [Inserting data into Azure table storage via HTTP POST request][3]
## [Inserting data into Azure blob storage via HTTP POST request][4]


*How to decide?*
1) Data size
2) Data retention (How long to store the data)
3) How often to be used by its consumers?
4) Do we need to choose head, tail, or query the data directly?
5) When are the data created and for how long are they valid?
6) Data access and sensitivity

# Application insights

To view your saved queries go into the query explorer.

[1]: https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction
[2]: https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-overview
[3]: https://docs.microsoft.com/en-us/rest/api/storageservices/insert-entity
[4]: https://docs.microsoft.com/en-us/rest/api/storageservices/put-blob
[5]: https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-quickstart-portal
[6]: https://azure.microsoft.com/en-us/features/storage-explorer/
[7]: https://pypi.org/project/azure-data-tables/
[8]: https://medium.com/clusterreply/azure-table-storage-limits-da039b20510a
[9]: https://docs.microsoft.com/en-us/azure/cosmos-db/table-storage-design-guide