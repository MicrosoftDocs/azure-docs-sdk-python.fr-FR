---
title: Bibliothèques Azure Batch pour Python
description: Références sur les bibliothèques Batch pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Batch, traitement, planification, longue durée
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: bbc691a8db6597c77575900b4e2a06f34ebb179c
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534352"
---
# <a name="azure-batch-libraries-for-python"></a><span data-ttu-id="80325-104">Bibliothèques Azure Batch pour Python</span><span class="sxs-lookup"><span data-stu-id="80325-104">Azure Batch libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="80325-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="80325-105">Overview</span></span>

<span data-ttu-id="80325-106">Exécutez efficacement des applications de calcul haute performance en parallèle et à grande échelle dans le cloud avec [Azure Batch](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="80325-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>

<span data-ttu-id="80325-107">Pour découvrir Azure Batch, consultez [Créer un compte Batch avec le portail Azure](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="80325-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="80325-108">Installer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="80325-108">Install the libraries</span></span>

## <a name="client-library"></a><span data-ttu-id="80325-109">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="80325-109">Client library</span></span>
<span data-ttu-id="80325-110">Les bibliothèques de client Azure Batch vous permettent de configurer des nœuds et des pools de calcul, de définir des tâches et de les configurer pour s’exécuter dans les travaux. Vous pouvez configurer un gestionnaire de travaux pour contrôler et surveiller l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="80325-110">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="80325-111">[En savoir plus](/azure/batch/batch-api-basics) sur l’utilisation de ces objets pour exécuter des solutions de calcul parallèles à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="80325-111">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

```bash
pip install azure-batch
```
### <a name="example"></a><span data-ttu-id="80325-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="80325-112">Example</span></span>

<span data-ttu-id="80325-113">Configurez un pool de nœuds de calcul Linux dans un compte Batch :</span><span class="sxs-lookup"><span data-stu-id="80325-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```python
# create the batch client for an account using its URI and keys
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

## <a name="management-api"></a><span data-ttu-id="80325-114">API de gestion</span><span class="sxs-lookup"><span data-stu-id="80325-114">Management API</span></span>
<span data-ttu-id="80325-115">Utilisez les bibliothèques de gestion Azure Batch pour créer et supprimer des comptes Batch, lire et régénérer les clés de compte Batch, et gérer le stockage de comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="80325-115">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="80325-116">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="80325-116">Explore the Client APIs</span></span>](/python/api/overview/azure/batch/client)

### <a name="example"></a><span data-ttu-id="80325-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="80325-117">Example</span></span>
<span data-ttu-id="80325-118">Créez un compte Azure Batch, puis configurez pour ce compte une nouvelle application et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="80325-118">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```python
from azure.mgmt.batch import BatchManagementClient
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.storage import StorageManagementClient

LOCATION ='eastus'
GROUP_NAME ='batchresourcegroup'
STORAGE_ACCOUNT_NAME ='batchstorageaccount'

# Create Resource group
print('Create Resource Group')
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})

# Create a storage account
storage_async_operation = storage_client.storage_accounts.create(
    GROUP_NAME,
    STORAGE_ACCOUNT_NAME,
    StorageAccountCreateParameters(
        sku=Sku(SkuName.standard_ragrs),
        kind=Kind.storage,
        location=LOCATION
    )
)
storage_account = storage_async_operation.result()

# Create a Batch Account, specifying the storage account we want to link
storage_resource = storage_account.id
batch_account = azure.mgmt.batch.models.BatchAccountCreateParameters(
    location=LOCATION,
    auto_storage=azure.mgmt.batch.models.AutoStorageBaseProperties(storage_resource)
)
creating = batch_client.account.create('MyBatchAccount', LOCATION, batch_account)
creating.wait()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="80325-119">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="80325-119">Explore the Management APIs</span></span>](/python/api/overview/azure/batch/management)
