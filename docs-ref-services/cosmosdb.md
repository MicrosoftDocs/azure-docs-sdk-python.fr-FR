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
# <a name="azure-cosmos-db-libraries-for-python"></a>Bibliothèques Azure Cosmos DB pour Python

## <a name="overview"></a>Vue d'ensemble

Utilisez Azure Cosmos DB dans vos applications Python pour stocker et interroger des documents JSON dans un magasin de données NoSQL.

Apprenez-en davantage sur [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

## <a name="client-library"></a>Bibliothèque cliente
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Bibliothèque de gestion
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Exemples

Trouver des documents correspondants dans Azure Cosmos DB à l’aide d’une interface de requête de type SQL :

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
> [Explorer les API de gestion](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>Exemples

* [Développer une application Python pour accéder à des données stockées dans un compte d’API SQL Azure Cosmos DB et les gérer](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [Développer une application Python pour accéder à des données stockées dans un compte d’API MongoDB Azure Cosmos DB et les gérer](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [Développer une application Python pour accéder à des données stockées dans un compte d’API Gremlin Azure Cosmos DB et les gérer](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [Développer une application Python pour accéder à des données stockées dans un compte d’API Cassandra Azure Cosmos DB et les gérer](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [Développer une application Python pour accéder à des données stockées dans un compte d’API Table Azure Cosmos DB et les gérer](https://github.com/Azure-Samples/storage-python-getting-started.git)


