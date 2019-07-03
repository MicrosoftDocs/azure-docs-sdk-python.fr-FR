---
title: Bibliothèques d’autorisation Azure pour Python
description: Références sur les bibliothèques d’autorisation Azure pour Python
keywords: Azure, python, Kit de développement logiciel (SDK), API, autorisation
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c7c4af34e82f2baad39635ecd20f1b9c48900b41
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534367"
---
# <a name="azure-authorization-libraries-for-python"></a><span data-ttu-id="98242-104">Bibliothèques d’autorisation Azure pour Python</span><span class="sxs-lookup"><span data-stu-id="98242-104">Azure Authorization libraries for python</span></span>

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[<span data-ttu-id="98242-105">API de gestion</span><span class="sxs-lookup"><span data-stu-id="98242-105">Management API</span></span>](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a><span data-ttu-id="98242-106">Créer le client de gestion</span><span class="sxs-lookup"><span data-stu-id="98242-106">Create the management client</span></span>

<span data-ttu-id="98242-107">Le code suivant permet de créer une instance du client de gestion.</span><span class="sxs-lookup"><span data-stu-id="98242-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="98242-108">Vous devrez fournir votre identifiant ``subscription_id``, qui peut être récupéré à partir de votre [liste d’abonnements](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="98242-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="98242-109">Consultez la section relative à [l’authentification de la gestion de ressources](/python/azure/python-sdk-azure-authenticate) pour en savoir plus sur la gestion de l’authentification d’Azure Active Directory avec le Kit de développement logiciel (SDK) Python et la création d’une instance ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="98242-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password'       # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
```

## <a name="check-permissions-for-a-resource-group"></a><span data-ttu-id="98242-110">Vérifier les autorisations d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="98242-110">Check permissions for a resource group</span></span>

<span data-ttu-id="98242-111">Le code suivant vérifie les autorisations dans un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="98242-111">The following code checks permissions in a given resource group.</span></span> <span data-ttu-id="98242-112">Pour créer ou gérer des groupes de ressources, consultez la section relative à la [gestion des ressources](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="98242-112">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="98242-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="98242-113">Explore the Management APIs</span></span>](/python/api/overview/azure/authorization/management)
