---
title: Bibliothèques Azure Cosmos DB pour Python
description: Consulter la documentation sur les bibliothèques de client Python pour Azure Cosmos DB
keywords: Azure, Python, Kit de développement logiciel (SDK), API, SQL, base de données, Postgres, Cosmos DB, NoSQL
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: bb5e2af6a28d9543cce0c1e80fab1575b78f8cfa
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534313"
---
# <a name="azure-cosmos-db-libraries-for-python"></a><span data-ttu-id="b1e7a-104">Bibliothèques Azure Cosmos DB pour Python</span><span class="sxs-lookup"><span data-stu-id="b1e7a-104">Azure Cosmos DB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="b1e7a-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b1e7a-105">Overview</span></span>

<span data-ttu-id="b1e7a-106">Utilisez Azure Cosmos DB dans vos applications Python pour stocker et interroger des documents JSON dans un magasin de données NoSQL.</span><span class="sxs-lookup"><span data-stu-id="b1e7a-106">Use Azure Cosmos DB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="b1e7a-107">Apprenez-en davantage sur [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="b1e7a-107">Learn more about [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="b1e7a-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="b1e7a-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="b1e7a-109">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="b1e7a-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="b1e7a-110">Exemples</span><span class="sxs-lookup"><span data-stu-id="b1e7a-110">Example</span></span>

<span data-ttu-id="b1e7a-111">Trouver des documents correspondants dans Azure Cosmos DB à l’aide d’une interface de requête de type SQL :</span><span class="sxs-lookup"><span data-stu-id="b1e7a-111">Find matching documents in Azure CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python Azure Cosmos DB client
client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
# Create a database
db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })

# Create collection options
options = {
    'offerEnableRUPerMinuteThroughput': True,
    'offerVersion': "V2",
    'offerThroughput': 400
}

# Create a collection
collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)

# Create some documents
document1 = client.CreateDocument(collection['_self'],
    { 
        'id': 'server1',
        'Web Site': 0,
        'Cloud Service': 0,
        'Virtual Machine': 0,
        'name': 'some' 
    })

# Query them in SQL
query = { 'query': 'SELECT * FROM server s' }    

options = {} 
options['enableCrossPartitionQuery'] = True
options['maxItemCount'] = 2

result_iterable = client.QueryDocuments(collection['_self'], query, options)
results = list(result_iterable)

print(results)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="b1e7a-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="b1e7a-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="b1e7a-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="b1e7a-113">Samples</span></span>

* [<span data-ttu-id="b1e7a-114">Développer une application Python pour accéder à des données stockées dans un compte d’API SQL Azure Cosmos DB et les gérer</span><span class="sxs-lookup"><span data-stu-id="b1e7a-114">Develop a Python app to access and manage data stored in Azure Cosmos DB SQL API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [<span data-ttu-id="b1e7a-115">Développer une application Python pour accéder à des données stockées dans un compte d’API MongoDB Azure Cosmos DB et les gérer</span><span class="sxs-lookup"><span data-stu-id="b1e7a-115">Develop a Python app to access and manage data stored in Azure Cosmos DB MongoDB API account</span></span>](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [<span data-ttu-id="b1e7a-116">Développer une application Python pour accéder à des données stockées dans un compte d’API Gremlin Azure Cosmos DB et les gérer</span><span class="sxs-lookup"><span data-stu-id="b1e7a-116">Develop a Python app to access and manage data stored in Azure Cosmos DB Gremlin API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [<span data-ttu-id="b1e7a-117">Développer une application Python pour accéder à des données stockées dans un compte d’API Cassandra Azure Cosmos DB et les gérer</span><span class="sxs-lookup"><span data-stu-id="b1e7a-117">Develop a Python app to access and manage data stored in Azure Cosmos DB Cassandra API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [<span data-ttu-id="b1e7a-118">Développer une application Python pour accéder à des données stockées dans un compte d’API Table Azure Cosmos DB et les gérer</span><span class="sxs-lookup"><span data-stu-id="b1e7a-118">Develop a Python app to access and manage data stored in Azure Cosmos DB Table API account</span></span>](https://github.com/Azure-Samples/storage-python-getting-started.git)


