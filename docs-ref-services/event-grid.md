---
title: Bibliothèques Azure Event Grid pour Python
description: ''
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Event Grid
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: e5df1078116f13f959923eac3e0c7b5789545278
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534299"
---
# <a name="event-grid-libraries-for-python"></a>Bibliothèques Event Grid pour Python


Azure Event Grid est un service de routage d’événement intelligent et entièrement géré qui permet une consommation d’événements uniforme à l’aide d’un modèle publication-abonnement.

[En savoir plus](/azure/event-grid/overview) sur Azure Event Grid et la prise en main avec le [didacticiel des événements de stockage d’objets Blob Azure](/azure/storage/blobs/storage-blob-event-quickstart). 

## <a name="publish-sdk"></a>Kit de développement logiciel de publication

Authentifiez, créez et gérez et publiez des événements dans des rubriques à l’aide du kit de développement logiciel de publication de Azure Event Grid.

### <a name="installation"></a>Installation 

Installez le package avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```bash
pip install azure-eventgrid
```

### <a name="example"></a>Exemples 

Le code suivant publie un événement dans une rubrique. Vous pouvez récupérer la clé de la rubrique et le point de terminaison à partir du portail Azure ou via Azure CLI :

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

```python
from datetime import datetime
from azure.eventgrid import EventGridClient
from msrest.authentication import TopicCredentials

def publish_event(self):

        credentials = TopicCredentials(
            self.settings.EVENT_GRID_KEY
        )
        event_grid_client = EventGridClient(credentials)
        event_grid_client.publish_events(
            "your-endpoint-here",
            events=[{
                'id' : "dbf93d79-3859-4cac-8055-51e3b6b54bea",
                'subject' : "Sample subject",
                'data': {
                    'key': 'Sample Data'
                },
                'event_type': 'SampleEventType',
                'event_time': datetime(2018, 5, 2),
                'data_version': 1
            }]
        )
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>Kit de développement logiciel (SDK) de gestion

Créez, mettez à jour et supprimez des instances, des rubriques et des abonnements Event Grid avec le kit de développement logiciel de gestion.

### <a name="installation"></a>Installation 

Installez le package avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>Exemples

La commande suivante crée une rubrique personnalisée et abonne un point de terminaison à la rubrique. Le code envoie ensuite un événement à la rubrique via le protocole HTTPS.
RequestBin est un outil tiers en open-source qui vous permet de créer un point de terminaison et d’afficher les requêtes qui lui sont envoyées. Accédez à [RequestBin](https://requestbin.com), puis cliquez sur **Créer un RequestBin**. Copiez l’URL du fichier bin, dont vous avez besoin pour vous abonner à la rubrique.

```python
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.eventgrid import EventGridManagementClient
import requests

RESOURCE_GROUP_NAME = 'gridResourceGroup'
TOPIC_NAME = 'gridTopic1234'
LOCATION = 'westus2'
SUBSCRIPTION_ID = 'YOUR_SUBSCRIPTION_ID'
SUBSCRIPTION_NAME = 'gridSubscription'
REQUEST_BIN_URL = 'YOUR_REQUEST_BIN_URL'

# create resource group
resource_client = ResourceManagementClient(credentials, SUBSCRIPTION_ID)
resource_client.resource_groups.create_or_update(
    RESOURCE_GROUP_NAME,
    {
        'location': LOCATION
    }
)

event_client = EventGridManagementClient(credentials, SUBSCRIPTION_ID)

# create a custom topic
event_client.topics.create_or_update(RESOURCE_GROUP_NAME, TOPIC_NAME, LOCATION)

# subscribe to a topic
scope = '/subscriptions/'+SUBSCRIPTION_ID+'/resourceGroups/'+RESOURCE_GROUP_NAME+'/providers/Microsoft.EventGrid/topics/'+TOPIC_NAME
event_client.event_subscriptions.create(scope, SUBSCRIPTION_NAME,
    {
        'destination': {
            'endpoint_url': REQUEST_BIN_URL
        }
    }
)

# send an event to topic
# get endpoint url
url = event_client.event_subscriptions.get_full_url(scope, SUBSCRIPTION_NAME).endpoint_url
# get key
key = event_client.topics.list_shared_access_keys(RESOURCE_GROUP_NAME,TOPIC_NAME).key1
headers = {'aeg-sas-key': key}
s = requests.get('https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json')
r = requests.post(url, data=s, headers=headers)
print(r.status_code)
print(r.content)
```
Accédez à l’URL RequestBin créée précédemment pour voir l’événement envoyé.

Supprimer des ressources
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>En savoir plus

[Recevoir des événements avec le kit de développement logiciel Event Grid](/azure/event-grid/receive-events)
