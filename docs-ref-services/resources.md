---
title: Bibliothèques de ressources Azure pour Python
description: Références sur les bibliothèques de ressources Azure pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, ressources
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: cef1f2bad7dcb3ff73aeae9c56000fb949541df9
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534229"
---
# <a name="azure-resources-libraries-for-python"></a>Bibliothèques de ressources Azure pour Python

## <a name="overview"></a>Vue d'ensemble 
Déployez, surveillez et gérez des ressources dans des groupes avec [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de gestion
Utilisez l’API de gestion pour créer des groupes de ressources et déployer des ressources à partir de modèles.

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a>Exemples 
Créer un groupe de ressources dans la région Azure Est des États-Unis.

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a>Exemples
[Manage Azure resources and resource groups with .NET (Gérer des ressources et des groupes de ressources Azure avec .NET)](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) d’exemples Azure Resource Manager.
