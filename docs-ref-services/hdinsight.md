---
title: Kit SDK Azure HDInsight pour Python
description: Informations de référence pour le kit SDK Azure HDInsight pour Python. Le kit SDK HDInsight pour Python fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 04/10/2019
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 3b0799dd77f7ff447ef997b2d142a6744c4a6858
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534267"
---
# <a name="hdinsight-sdk-for-python"></a><span data-ttu-id="5ce91-104">Kit SDK HDInsight pour Python</span><span class="sxs-lookup"><span data-stu-id="5ce91-104">HDInsight SDK for Python</span></span>

## <a name="overview"></a><span data-ttu-id="5ce91-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5ce91-105">Overview</span></span>

<span data-ttu-id="5ce91-106">Le kit SDK HDInsight pour Python fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ce91-106">The HDInsight SDK for Python provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="5ce91-107">Il inclut des opérations permettant de créer, supprimer, mettre à jour, répertorier, mettre à l’échelle, exécuter des actions de script, surveiller, obtenir des propriétés des clusters HDInsight, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="5ce91-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ce91-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="5ce91-108">Prerequisites</span></span>

* <span data-ttu-id="5ce91-109">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5ce91-109">An Azure account.</span></span> <span data-ttu-id="5ce91-110">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5ce91-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="5ce91-111">Python</span><span class="sxs-lookup"><span data-stu-id="5ce91-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="5ce91-112">pip</span><span class="sxs-lookup"><span data-stu-id="5ce91-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="5ce91-113">Installation du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="5ce91-113">SDK Installation</span></span>

<span data-ttu-id="5ce91-114">Le kit SDK HDInsight pour Python se trouve dans [l’index du package Python](https://pypi.org/project/azure-mgmt-hdinsight/) et peut être installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="5ce91-114">The HDInsight SDK for Python can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="5ce91-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="5ce91-115">Authentication</span></span>

<span data-ttu-id="5ce91-116">Le kit de développement logiciel (SDK) doit d’abord être authentifié avec votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5ce91-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="5ce91-117">Suivez l’exemple ci-dessous pour créer un principal de service et l’utiliser pour s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="5ce91-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="5ce91-118">Une fois cette opération terminée, vous avez une instance de `HDInsightManagementClient`, qui contient de nombreuses méthodes (décrites dans les sections suivantes) pouvant être utilisées pour effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="5ce91-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce91-119">Il existe d’autres façons de s’authentifier, en plus de l’exemple suivant, peut-être mieux adaptées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="5ce91-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="5ce91-120">Toutes les méthodes sont décrites ici : [S’authentifier avec les bibliothèques de gestion Azure pour Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="5ce91-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="5ce91-121">Exemple d’authentification à l’aide d’un principal de service</span><span class="sxs-lookup"><span data-stu-id="5ce91-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="5ce91-122">Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="5ce91-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="5ce91-123">Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé.</span><span class="sxs-lookup"><span data-stu-id="5ce91-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="5ce91-124">Les informations relatives à votre abonnement sont affichées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="5ce91-124">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="5ce91-125">Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en exécutant :</span><span class="sxs-lookup"><span data-stu-id="5ce91-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="5ce91-126">Si vous n’avez pas déjà enregistré le fournisseur de ressources HDInsight avec une autre méthode (par exemple, en créant un cluster HDInsight via le portail Azure), vous devez le faire une fois avant de pouvoir vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="5ce91-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="5ce91-127">Vous pouvez le faire à partir d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ce91-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="5ce91-128">Ensuite, choisissez un nom pour votre principal de service et créez-le avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5ce91-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="5ce91-129">Les informations relatives au principal de service sont affichées en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="5ce91-129">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="5ce91-130">Copiez l’extrait de code Python ci-dessous et remplissez `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` et `SUBSCRIPTION_ID` avec les chaînes du code JSON qui a été renvoyé après l’exécution de la commande pour créer le principal de service.</span><span class="sxs-lookup"><span data-stu-id="5ce91-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```python
from azure.mgmt.hdinsight import HDInsightManagementClient
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.hdinsight.models import *

# Tenant ID for your Azure Subscription
TENANT_ID = ''
# Your Service Principal App Client ID
CLIENT_ID = ''
# Your Service Principal Client Secret
CLIENT_SECRET = ''
# Your Azure Subscription ID
SUBSCRIPTION_ID = ''

credentials = ServicePrincipalCredentials(
    client_id = CLIENT_ID,
    secret = CLIENT_SECRET,
    tenant = TENANT_ID
)

client = HDInsightManagementClient(credentials, SUBSCRIPTION_ID)
```


## <a name="cluster-management"></a><span data-ttu-id="5ce91-131">Gestion du cluster</span><span class="sxs-lookup"><span data-stu-id="5ce91-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="5ce91-132">Cette section suppose que vous avez déjà authentifié et construit une instance `HDInsightManagementClient` que vous avez conservée dans une variable appelée `client`.</span><span class="sxs-lookup"><span data-stu-id="5ce91-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="5ce91-133">Les instructions relatives à l’authentification et à l’obtention d’un `HDInsightManagementClient` se trouvent dans la section Authentification ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="5ce91-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="5ce91-134">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="5ce91-134">Create a Cluster</span></span>

<span data-ttu-id="5ce91-135">Un nouveau cluster peut être créé en appelant `client.clusters.create()`.</span><span class="sxs-lookup"><span data-stu-id="5ce91-135">A new cluster can be created by calling `client.clusters.create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="5ce91-136">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-136">Samples</span></span>

<span data-ttu-id="5ce91-137">Des exemples de code pour la création de plusieurs types courants de clusters HDInsight sont disponibles : [HDInsight Python Samples](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="5ce91-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight Python Samples](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="5ce91-138">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-138">Example</span></span>

<span data-ttu-id="5ce91-139">Cet exemple montre comment créer un cluster Spark avec 2 nœuds principaux et un nœud de travail.</span><span class="sxs-lookup"><span data-stu-id="5ce91-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce91-140">Vous devez d’abord créer un groupe de ressources et un compte de stockage, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5ce91-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="5ce91-141">Si vous les avez déjà créés, vous pouvez ignorer ces étapes.</span><span class="sxs-lookup"><span data-stu-id="5ce91-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="5ce91-142">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5ce91-142">Creating a Resource Group</span></span>

<span data-ttu-id="5ce91-143">Vous pouvez créer un groupe de ressources à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant</span><span class="sxs-lookup"><span data-stu-id="5ce91-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="5ce91-144">Création d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="5ce91-144">Creating a Storage Account</span></span>

<span data-ttu-id="5ce91-145">Vous pouvez créer un compte de stockage à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant :</span><span class="sxs-lookup"><span data-stu-id="5ce91-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="5ce91-146">Ensuite, exécutez la commande suivante pour obtenir la clé de votre compte de stockage (vous en aurez besoin pour créer un cluster) :</span><span class="sxs-lookup"><span data-stu-id="5ce91-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="5ce91-147">L’extrait de code Python ci-dessous crée un cluster Spark avec 2 nœuds principaux et 1 nœud Worker.</span><span class="sxs-lookup"><span data-stu-id="5ce91-147">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="5ce91-148">Remplissez les variables vides comme expliqué dans les commentaires et n’hésitez pas à modifier d’autres paramètres en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="5ce91-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```python
# The name for the cluster you are creating
cluster_name = ""
# The name of your existing Resource Group
resource_group_name = ""
# Choose a username
username = ""
# Choose a password
password = ""
# Replace <> with the name of your storage account
storage_account = "<>.blob.core.windows.net"
# Storage account key you obtained above
storage_account_key = ""
# Choose a region
location = ""
container = "default"

params = ClusterCreateProperties(
    cluster_version="3.6",
    os_type=OSType.linux,
    tier=Tier.standard,
    cluster_definition=ClusterDefinition(
        kind="spark",
        configurations={
            "gateway": {
                "restAuthCredential.enabled_credential": "True",
                "restAuthCredential.username": username,
                "restAuthCredential.password": password
            }
        }
    ),
    compute_profile=ComputeProfile(
        roles=[
            Role(
                name="headnode",
                target_instance_count=2,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            ),
            Role(
                name="workernode",
                target_instance_count=1,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            )
        ]
    ),
    storage_profile=StorageProfile(
        storageaccounts=[StorageAccount(
            name=storage_account,
            key=storage_account_key,
            container=container,
            is_default=True
        )]
    )
)

client.clusters.create(
    cluster_name=cluster_name,
    resource_group_name=resource_group_name,
    parameters=ClusterCreateParametersExtended(
        location=location,
        tags={},
        properties=params
    ))
```

### <a name="get-cluster-details"></a><span data-ttu-id="5ce91-149">Obtenir les détails du cluster</span><span class="sxs-lookup"><span data-stu-id="5ce91-149">Get Cluster Details</span></span>

<span data-ttu-id="5ce91-150">Pour obtenir les propriétés d’un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="5ce91-150">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="5ce91-151">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-151">Example</span></span>

<span data-ttu-id="5ce91-152">Vous pouvez utiliser `get` pour confirmer que vous avez créé votre cluster avec succès.</span><span class="sxs-lookup"><span data-stu-id="5ce91-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="5ce91-153">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="5ce91-153">The output should look like:</span></span>

```output
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="5ce91-154">Répertorier les clusters</span><span class="sxs-lookup"><span data-stu-id="5ce91-154">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="5ce91-155">Répertorier les clusters dans l’abonnement</span><span class="sxs-lookup"><span data-stu-id="5ce91-155">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="5ce91-156">Répertorier les clusters par groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5ce91-156">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="5ce91-157">`list()` et `list_by_resource_group()` retournent un objet `ClusterPaged`.</span><span class="sxs-lookup"><span data-stu-id="5ce91-157">Both `list()` and `list_by_resource_group()` return a `ClusterPaged` object.</span></span> <span data-ttu-id="5ce91-158">Appeler `advance_page()` renvoie une liste de clusters sur cette page et avance l’objet `ClusterPaged` à la page suivante.</span><span class="sxs-lookup"><span data-stu-id="5ce91-158">Calling `advance_page()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="5ce91-159">Cette opération peut être répétée jusqu’à ce qu’une exception `StopIteration` soit générée, indiquant qu’il n’y a plus d’autres pages.</span><span class="sxs-lookup"><span data-stu-id="5ce91-159">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="5ce91-160">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-160">Example</span></span>

<span data-ttu-id="5ce91-161">L’exemple suivant imprime les propriétés de tous les clusters pour l’abonnement actuel :</span><span class="sxs-lookup"><span data-stu-id="5ce91-161">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="5ce91-162">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="5ce91-162">Delete a Cluster</span></span>

<span data-ttu-id="5ce91-163">Pour supprimer un cluster :</span><span class="sxs-lookup"><span data-stu-id="5ce91-163">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="5ce91-164">Mettre à jour les balises de cluster</span><span class="sxs-lookup"><span data-stu-id="5ce91-164">Update Cluster Tags</span></span>

<span data-ttu-id="5ce91-165">Vous pouvez mettre à jour les balises d’un cluster donné comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ce91-165">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="5ce91-166">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-166">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a><span data-ttu-id="5ce91-167">Redimensionner le cluster</span><span class="sxs-lookup"><span data-stu-id="5ce91-167">Resize Cluster</span></span>

<span data-ttu-id="5ce91-168">Vous pouvez mettre à l’échelle un nombre donné de clusters de nœuds Worker en spécifiant une nouvelle taille comme suit :</span><span class="sxs-lookup"><span data-stu-id="5ce91-168">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="5ce91-169">Cluster Monitoring (Surveillance des clusters)</span><span class="sxs-lookup"><span data-stu-id="5ce91-169">Cluster Monitoring</span></span>

<span data-ttu-id="5ce91-170">Le kit de développement logiciel (SDK) HDInsight Management peut également être utilisé pour gérer la surveillance de vos clusters via Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="5ce91-170">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="5ce91-171">Activer la surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="5ce91-171">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="5ce91-172">Pour activer la supervision OMS, vous devez disposer d’un espace de travail Log Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="5ce91-172">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="5ce91-173">Si vous n’en n’avez pas déjà créé un, vous pouvez apprendre comment le faire ici : [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="5ce91-173">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="5ce91-174">Pour activer la surveillance OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="5ce91-174">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="5ce91-175">Afficher l’état de surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="5ce91-175">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="5ce91-176">Pour obtenir l’état d’OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="5ce91-176">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="5ce91-177">Désactiver la surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="5ce91-177">Disable OMS Monitoring</span></span>

<span data-ttu-id="5ce91-178">Pour désactiver OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="5ce91-178">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="5ce91-179">Actions de script</span><span class="sxs-lookup"><span data-stu-id="5ce91-179">Script Actions</span></span>

<span data-ttu-id="5ce91-180">HDInsight fournit une méthode de configuration intitulée actions de script, qui appelle des scripts personnalisés pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce91-180">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="5ce91-181">Vous trouverez plus d’informations sur l’utilisation des actions de script ici : [Personnaliser des clusters HDInsight Linux avec des actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="5ce91-181">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="5ce91-182">Exécuter des actions de script</span><span class="sxs-lookup"><span data-stu-id="5ce91-182">Execute Script Actions</span></span>
<span data-ttu-id="5ce91-183">Pour exécuter des actions de script sur un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="5ce91-183">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="5ce91-184">Supprimer une action de script</span><span class="sxs-lookup"><span data-stu-id="5ce91-184">Delete Script Action</span></span>

<span data-ttu-id="5ce91-185">Pour supprimer une action de script persistante spécifiée sur un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="5ce91-185">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="5ce91-186">Répertorier les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="5ce91-186">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="5ce91-187">`list()` et `list_persisted_scripts()` renvoient un objet `RuntimeScriptActionDetailPaged`.</span><span class="sxs-lookup"><span data-stu-id="5ce91-187">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="5ce91-188">Appeler `advance_page()` retourne une liste de `RuntimeScriptActionDetail` sur cette page et avance l’objet `RuntimeScriptActionDetailPaged` à la page suivante.</span><span class="sxs-lookup"><span data-stu-id="5ce91-188">Calling `advance_page()` returns a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="5ce91-189">Cette opération peut être répétée jusqu’à ce qu’une exception `StopIteration` soit générée, indiquant qu’il n’y a plus d’autres pages.</span><span class="sxs-lookup"><span data-stu-id="5ce91-189">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="5ce91-190">Reportez-vous à l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5ce91-190">See the example below.</span></span>

<span data-ttu-id="5ce91-191">Pour répertorier toutes les actions de script persistantes pour le cluster spécifié :</span><span class="sxs-lookup"><span data-stu-id="5ce91-191">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="5ce91-192">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-192">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="5ce91-193">Répertorier tout l’historique d’exécution des scripts</span><span class="sxs-lookup"><span data-stu-id="5ce91-193">List All Scripts' Execution History</span></span>

<span data-ttu-id="5ce91-194">Pour répertorier tout l’historique d’exécution des scripts pour le cluster spécifié :</span><span class="sxs-lookup"><span data-stu-id="5ce91-194">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="5ce91-195">Exemples</span><span class="sxs-lookup"><span data-stu-id="5ce91-195">Example</span></span>

<span data-ttu-id="5ce91-196">Cet exemple imprime tous les détails de toutes les exécutions de script passées.</span><span class="sxs-lookup"><span data-stu-id="5ce91-196">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
