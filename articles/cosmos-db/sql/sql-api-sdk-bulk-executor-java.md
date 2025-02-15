---
title: 'Azure Cosmos DB: Bulk executor Java API, SDK & resources'
description: Learn all about the bulk executor Java API and SDK including release dates, retirement dates, and changes made between each version of the Azure Cosmos DB bulk executor Java SDK.
author: anfeldma-ms
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 04/06/2021
ms.author: anfeldma
ms.custom: devx-track-java
---

# Java bulk executor library: Download information
[!INCLUDE[appliesto-sql-api](../includes/appliesto-sql-api.md)]

> [!div class="op_single_selector"]
> * [.NET SDK v3](sql-api-sdk-dotnet-standard.md)
> * [.NET SDK v2](sql-api-sdk-dotnet.md)
> * [.NET Core SDK v2](sql-api-sdk-dotnet-core.md)
> * [.NET Change Feed SDK v2](sql-api-sdk-dotnet-changefeed.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Java SDK v4](sql-api-sdk-java-v4.md)
> * [Async Java SDK v2](sql-api-sdk-async-java.md)
> * [Sync Java SDK v2](sql-api-sdk-java.md)
> * [Spring Data v2](sql-api-sdk-java-spring-v2.md)
> * [Spring Data v3](sql-api-sdk-java-spring-v3.md)
> * [Spark 3 OLTP Connector](sql-api-sdk-java-spark-v3.md)
> * [Spark 2 OLTP Connector](sql-api-sdk-java-spark.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](/rest/api/cosmos-db/)
> * [REST Resource Provider](/rest/api/cosmos-db-resource-provider/)
> * [SQL](sql-query-getting-started.md)
> * [Bulk executor - .NET v2](sql-api-sdk-bulk-executor-dot-net.md)
> * [Bulk executor - Java](sql-api-sdk-bulk-executor-java.md)

| | Link/notes |
|---|---|
|**Description**|The bulk executor library allows client applications to perform bulk operations in Azure Cosmos DB accounts. bulk executor library provides BulkImport, and BulkUpdate namespaces. The BulkImport module can bulk ingest documents in an optimized way such that the throughput provisioned for a collection is consumed to its maximum extent. The BulkUpdate module can bulk update existing data in Azure Cosmos containers as patches.|
|**SDK download**|[Maven](https://search.maven.org/#search%7Cga%7C1%7Cdocumentdb-bulkexecutor)|
|**Bulk executor library in GitHub**|[GitHub](https://github.com/Azure/azure-cosmosdb-bulkexecutor-java-getting-started)|
| **API documentation**| [Java API reference documentation](/java/api/com.microsoft.azure.documentdb.bulkexecutor)|
|**Get started**|[Get started with the bulk executor library Java SDK](bulk-executor-java.md)|
|**Minimum supported runtime**|[Java Development Kit (JDK) 7+](/java/azure/jdk/)|

## Release notes
### <a name="2.12.3"></a>2.12.3

* Fix retry policy when `GoneException` is wrapped in `IllegalStateException` - this change is necessary to make sure Gateway cache is refreshed on 410 so the Spark connector (for Spark 2.4) can use a custom retry policy to allow queries to succeed during partition splits

### <a name="2.12.2"></a>2.12.2

* Fix an issue resulting in documents not always being imported on transient errors.

### <a name="2.12.1"></a>2.12.1

* Upgrade to use latest Cosmos Core SDK version.

### <a name="2.12.0"></a>2.12.0

* Improve handling of RU budget provided through the Spark Connector for  bulk operation. An initial one-time bulk import is performed from spark connector with a baseBatchSize and the RU consumption for the above batch import is collected.
  A miniBatchSizeAdjustmentFactor is calculated based on the above RU consumption, and the mini-batch size is adjusted based on this. Based on the Elapsed time and the consumed RU for each batch import, a sleep duration is calculated to limit the RU consumption per second and is used to pause the thread prior to the next batch import.

### <a name="2.11.0"></a>2.11.0

* Fix a bug preventing bulk updates when using a nested partition key

### <a name="2.10.0"></a>2.10.0

* Fix for DocumentAnalyzer.java to correctly extract nested partition key values from json.

### <a name="2.9.4"></a>2.9.4

* Add functionality in BulkDelete operations to retry on specific failures and also return a list of failures to the user that could be retried.

### <a name="2.9.3"></a>2.9.3

* Update for Cosmos SDK version 2.4.7.

### <a name="2.9.2"></a>2.9.2

* Fix for 'mergeAll' to continue on 'id' and partition key value so that any patched document properties which are placed after 'id' and partition key value get added to the updated item list.

### <a name="2.9.1"></a>2.9.1

* Update start degree of concurrency to 1 and added debug logs for minibatch.