---
title: Bibliothèques Azure Scheduler pour Python
description: Références sur les bibliothèques Azure Scheduler pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Scheduler
author: lisawong19
ms.author: routlaw
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 73c33ff808212fade192ca7c7c05a8e64d3fafda
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534211"
---
# <a name="azure-scheduler-libraries-for-python"></a><span data-ttu-id="91917-104">Bibliothèques Azure Scheduler pour Python</span><span class="sxs-lookup"><span data-stu-id="91917-104">Azure Scheduler libraries for python</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="91917-105">Installer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="91917-105">Install the libraries</span></span>

## <a name="management"></a><span data-ttu-id="91917-106">gestion</span><span class="sxs-lookup"><span data-stu-id="91917-106">Management</span></span>

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a><span data-ttu-id="91917-107">Exemples</span><span class="sxs-lookup"><span data-stu-id="91917-107">Example</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="91917-108">Créer le client de gestion</span><span class="sxs-lookup"><span data-stu-id="91917-108">Create the management client</span></span>

<span data-ttu-id="91917-109">Le code suivant permet de créer une instance du client de gestion.</span><span class="sxs-lookup"><span data-stu-id="91917-109">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="91917-110">Vous devrez fournir votre identifiant ``subscription_id``, qui peut être récupéré à partir de votre [liste d’abonnements](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="91917-110">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="91917-111">Consultez la section relative à [l’authentification de la gestion de ressources](/python/azure/python-sdk-azure-authenticate) pour en savoir plus sur la gestion de l’authentification d’Azure Active Directory avec le Kit de développement logiciel (SDK) Python et la création d’une instance ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="91917-111">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.scheduler import SchedulerManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

scheduler_client = SchedulerManagementClient(
    credentials,
    subscription_id
)
```

### <a name="create-a-job-collection"></a><span data-ttu-id="91917-112">Créer une collection de travaux</span><span class="sxs-lookup"><span data-stu-id="91917-112">Create a job collection</span></span>

<span data-ttu-id="91917-113">Le code suivant crée une collection de travaux sous un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="91917-113">The following code creates a job collection under an existing resource group.</span></span>
<span data-ttu-id="91917-114">Pour créer ou gérer des groupes de ressources, consultez la section relative à la [gestion des ressources](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="91917-114">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.scheduler.models import JobCollectionDefinition, JobCollectionProperties, Sku

group_name = 'myresourcegroup'
job_collection_name = "myjobcollection"
scheduler_client.job_collections.create_or_update(
    group_name,
    job_collection_name,
    JobCollectionDefinition(
        location = "West US",
        properties = JobCollectionProperties(
            sku = Sku(
                name="Free"
            )
        )
    )
)
# scheduler_client is a JobCollectionDefinition instance
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="91917-115">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="91917-115">Explore the Management APIs</span></span>](/python/api/overview/azure/scheduler/management)