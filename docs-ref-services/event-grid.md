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
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="aa0ea-103">Bibliothèques Event Grid pour Python</span><span class="sxs-lookup"><span data-stu-id="aa0ea-103">Event Grid libraries for Python</span></span>


<span data-ttu-id="aa0ea-104">Azure Event Grid est un service de routage d’événement intelligent et entièrement géré qui permet une consommation d’événements uniforme à l’aide d’un modèle publication-abonnement.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-104">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

<span data-ttu-id="aa0ea-105">[En savoir plus](/azure/event-grid/overview) sur Azure Event Grid et la prise en main avec le [didacticiel des événements de stockage d’objets Blob Azure](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="aa0ea-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="aa0ea-106">Kit de développement logiciel de publication</span><span class="sxs-lookup"><span data-stu-id="aa0ea-106">Publish SDK</span></span>

<span data-ttu-id="aa0ea-107">Authentifiez, créez et gérez et publiez des événements dans des rubriques à l’aide du kit de développement logiciel de publication de Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-107">Authenticate, create, handle, and publish events to topics using the Azure Event Grid publish SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="aa0ea-108">Installation</span><span class="sxs-lookup"><span data-stu-id="aa0ea-108">Installation</span></span> 

<span data-ttu-id="aa0ea-109">Installez le package avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="aa0ea-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-eventgrid
```

### <a name="example"></a><span data-ttu-id="aa0ea-110">Exemples</span><span class="sxs-lookup"><span data-stu-id="aa0ea-110">Example</span></span> 

<span data-ttu-id="aa0ea-111">Le code suivant publie un événement dans une rubrique.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-111">The following code publishes an event to a topic.</span></span> <span data-ttu-id="aa0ea-112">Vous pouvez récupérer la clé de la rubrique et le point de terminaison à partir du portail Azure ou via Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="aa0ea-112">You can retrieve the topic key and endpoint through the Azure Portal or through the Azure CLI:</span></span>

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
> [<span data-ttu-id="aa0ea-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="aa0ea-113">Explore the Client APIs</span></span>](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="aa0ea-114">Kit de développement logiciel (SDK) de gestion</span><span class="sxs-lookup"><span data-stu-id="aa0ea-114">Management SDK</span></span>

<span data-ttu-id="aa0ea-115">Créez, mettez à jour et supprimez des instances, des rubriques et des abonnements Event Grid avec le kit de développement logiciel de gestion.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="aa0ea-116">Installation</span><span class="sxs-lookup"><span data-stu-id="aa0ea-116">Installation</span></span> 

<span data-ttu-id="aa0ea-117">Installez le package avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="aa0ea-117">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="aa0ea-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="aa0ea-118">Example</span></span>

<span data-ttu-id="aa0ea-119">La commande suivante crée une rubrique personnalisée et abonne un point de terminaison à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-119">The following creates a custom topic and subscribes an endpoint to the topic.</span></span> <span data-ttu-id="aa0ea-120">Le code envoie ensuite un événement à la rubrique via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-120">The code then sends an event to the topic through HTTPS.</span></span>
<span data-ttu-id="aa0ea-121">RequestBin est un outil tiers en open-source qui vous permet de créer un point de terminaison et d’afficher les requêtes qui lui sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-121">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="aa0ea-122">Accédez à [RequestBin](https://requestbin.com), puis cliquez sur **Créer un RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-122">Go to [RequestBin](https://requestbin.com), and click **Create a RequestBin**.</span></span> <span data-ttu-id="aa0ea-123">Copiez l’URL du fichier bin, dont vous avez besoin pour vous abonner à la rubrique.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-123">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="aa0ea-124">Accédez à l’URL RequestBin créée précédemment pour voir l’événement envoyé.</span><span class="sxs-lookup"><span data-stu-id="aa0ea-124">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="aa0ea-125">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="aa0ea-125">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="aa0ea-126">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="aa0ea-126">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="aa0ea-127">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="aa0ea-127">Learn more</span></span>

[<span data-ttu-id="aa0ea-128">Recevoir des événements avec le kit de développement logiciel Event Grid</span><span class="sxs-lookup"><span data-stu-id="aa0ea-128">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)
