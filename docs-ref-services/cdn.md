---
title: Bibliothèques Azure CDN pour Python
description: Références sur les bibliothèques Azure CDN pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, CDN
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 06e6c8786ebbd88b7d3996b640af96a23cd5689b
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52275533"
---
# <a name="azure-cdn-libraries-for-python"></a><span data-ttu-id="3f61b-104">Bibliothèques Azure CDN pour Python</span><span class="sxs-lookup"><span data-stu-id="3f61b-104">Azure CDN libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="3f61b-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="3f61b-105">Overview</span></span>

<span data-ttu-id="3f61b-106">Le [réseau de distribution de contenu (CDN) Azure](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) vous permet de mettre en cache du contenu web pour garantir une disponibilité de bande passante élevée dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="3f61b-106">[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) allows you to provide web content caches to ensure high-bandwidth availability across the globe.</span></span>

<span data-ttu-id="3f61b-107">Pour découvrir Azure CDN, consultez la section [Prise en main d’Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="3f61b-107">To get started with Azure CDN, see [Getting started with Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-apis"></a><span data-ttu-id="3f61b-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="3f61b-108">Management APIs</span></span>

<span data-ttu-id="3f61b-109">Créez, interrogez et gérez des réseaux de distribution de contenu (CDN) Azure avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="3f61b-109">Create, query, and manage Azure CDNs with the management API.</span></span>

<span data-ttu-id="3f61b-110">Installez le package de gestion via pip.</span><span class="sxs-lookup"><span data-stu-id="3f61b-110">Install the management package via pip.</span></span>

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a><span data-ttu-id="3f61b-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="3f61b-111">Example</span></span>

<span data-ttu-id="3f61b-112">Création d’un profil CDN avec un seul point de terminaison défini :</span><span class="sxs-lookup"><span data-stu-id="3f61b-112">Creating a CDN profile with a single defined endpoint:</span></span>

```python
from azure.mgmt.cdn import CdnManagementClient

cdn_client = CdnManagementClient(credentials, 'your-subscription-id')
profile_poller = cdn_client.profiles.create('my-resource-group',
                                            'cdn-name',
                                            {
                                                "location": "some_region", 
                                                "sku": {
                                                    "name": "sku_tier"
                                                } 
                                            })
profile = profile_poller.result()

endpoint_poller = client.endpoints.create('my-resource-group',
                                          'cdn-name',
                                          'unique-endpoint-name', 
                                          { 
                                              "location": "any_region", 
                                              "origins": [
                                                  {
                                                      "name": "origin_name", 
                                                      "host_name": "url"
                                                  }]
                                          })
endpoint = endpoint_poller.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f61b-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="3f61b-113">Explore the Management APIs</span></span>](/python/api/overview/azure/cdn/management)
