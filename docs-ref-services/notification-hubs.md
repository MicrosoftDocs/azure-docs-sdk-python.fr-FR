---
title: Bibliothèques Azure Notification Hubs pour Python
description: Références sur les bibliothèques Azure Notification Hubs pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Notification Hubs
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f600b28c347cdbffc16342da25a72e4de8e83c5f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534245"
---
# <a name="azure-notification-hubs-libraries-for-python"></a><span data-ttu-id="c3f70-104">Bibliothèques Azure Notification Hubs pour Python</span><span class="sxs-lookup"><span data-stu-id="c3f70-104">Azure Notification Hubs libraries for python</span></span>

## <a name="management-apipythonapioverviewazurenotificationhubsmanagement"></a>[<span data-ttu-id="c3f70-105">API de gestion</span><span class="sxs-lookup"><span data-stu-id="c3f70-105">Management API</span></span>](/python/api/overview/azure/notificationhubs/management)

```bash
pip install azure-mgmt-notificationhubs
```

## <a name="create-the-management-client"></a><span data-ttu-id="c3f70-106">Créer le client de gestion</span><span class="sxs-lookup"><span data-stu-id="c3f70-106">Create the management client</span></span>

<span data-ttu-id="c3f70-107">Le code suivant permet de créer une instance du client de gestion.</span><span class="sxs-lookup"><span data-stu-id="c3f70-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="c3f70-108">Vous devrez fournir votre identifiant ``subscription_id``, qui peut être récupéré à partir de votre [liste d’abonnements](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="c3f70-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="c3f70-109">Consultez la section relative à [l’authentification de la gestion de ressources](/python/azure/python-sdk-azure-authenticate) pour en savoir plus sur la gestion de l’authentification d’Azure Active Directory avec le Kit de développement logiciel (SDK) Python et la création d’une instance ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="c3f70-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.notificationhubs import NotificationHubsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

redis_client = NotificationHubsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="check-namespace-availability"></a><span data-ttu-id="c3f70-110">Vérifier la disponibilité de l’espace de noms</span><span class="sxs-lookup"><span data-stu-id="c3f70-110">Check namespace availability</span></span>

<span data-ttu-id="c3f70-111">Le code suivant permet de vérifier la disponibilité d’un espace de noms associé à un hub de notifications.</span><span class="sxs-lookup"><span data-stu-id="c3f70-111">The following code check namespace availability of a notification hub.</span></span>

```python
from azure.mgmt.notificationhubs.models import CheckAvailabilityParameters

account_name = 'mynotificationhub'
output = notificationhubs_client.namespaces.check_availability(
    azure.mgmt.notificationhubs.models.CheckAvailabilityParameters(
        name = account_name
    )
)
# output is a CheckAvailibilityResource instance
print(output.is_availiable) # Yes, it's 'availiable', it's a typo in the REST API
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3f70-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="c3f70-112">Explore the Management APIs</span></span>](/python/api/overview/azure/notificationhubs/management)
