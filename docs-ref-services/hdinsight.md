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
# <a name="hdinsight-sdk-for-python"></a>Kit SDK HDInsight pour Python

## <a name="overview"></a>Vue d'ensemble

Le kit SDK HDInsight pour Python fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight. Il inclut des opérations permettant de créer, supprimer, mettre à jour, répertorier, mettre à l’échelle, exécuter des actions de script, surveiller, obtenir des propriétés des clusters HDInsight, et bien plus encore.

## <a name="prerequisites"></a>Prérequis

* Un compte Azure. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/).
* [Python](https://www.python.org/downloads/)
* [pip](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a>Installation du Kit de développement logiciel (SDK)

Le kit SDK HDInsight pour Python se trouve dans [l’index du package Python](https://pypi.org/project/azure-mgmt-hdinsight/) et peut être installé en exécutant : 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a>Authentication

Le kit de développement logiciel (SDK) doit d’abord être authentifié avec votre abonnement Azure.  Suivez l’exemple ci-dessous pour créer un principal de service et l’utiliser pour s’authentifier. Une fois cette opération terminée, vous avez une instance de `HDInsightManagementClient`, qui contient de nombreuses méthodes (décrites dans les sections suivantes) pouvant être utilisées pour effectuer des opérations de gestion.

> [!NOTE]
> Il existe d’autres façons de s’authentifier, en plus de l’exemple suivant, peut-être mieux adaptées à vos besoins. Toutes les méthodes sont décrites ici : [S’authentifier avec les bibliothèques de gestion Azure pour Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)

### <a name="authentication-example-using-a-service-principal"></a>Exemple d’authentification à l’aide d’un principal de service

Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash). Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé. 

```azurecli-interactive
az account show
```

Les informations relatives à votre abonnement sont affichées au format JSON.

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

Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en exécutant : 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Si vous n’avez pas déjà enregistré le fournisseur de ressources HDInsight avec une autre méthode (par exemple, en créant un cluster HDInsight via le portail Azure), vous devez le faire une fois avant de pouvoir vous authentifier. Vous pouvez le faire à partir d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant la commande suivante :
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Ensuite, choisissez un nom pour votre principal de service et créez-le avec la commande suivante :

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Les informations relatives au principal de service sont affichées en tant que JSON.

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
Copiez l’extrait de code Python ci-dessous et remplissez `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` et `SUBSCRIPTION_ID` avec les chaînes du code JSON qui a été renvoyé après l’exécution de la commande pour créer le principal de service.

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


## <a name="cluster-management"></a>Gestion du cluster

> [!NOTE]
> Cette section suppose que vous avez déjà authentifié et construit une instance `HDInsightManagementClient` que vous avez conservée dans une variable appelée `client`. Les instructions relatives à l’authentification et à l’obtention d’un `HDInsightManagementClient` se trouvent dans la section Authentification ci-dessus.

### <a name="create-a-cluster"></a>Créer un cluster

Un nouveau cluster peut être créé en appelant `client.clusters.create()`.

#### <a name="samples"></a>Exemples

Des exemples de code pour la création de plusieurs types courants de clusters HDInsight sont disponibles : [HDInsight Python Samples](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).

#### <a name="example"></a>Exemples

Cet exemple montre comment créer un cluster Spark avec 2 nœuds principaux et un nœud de travail.

> [!NOTE]
> Vous devez d’abord créer un groupe de ressources et un compte de stockage, comme expliqué ci-dessous. Si vous les avez déjà créés, vous pouvez ignorer ces étapes.

##### <a name="creating-a-resource-group"></a>Création d’un groupe de ressources

Vous pouvez créer un groupe de ressources à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Création d’un compte de stockage

Vous pouvez créer un compte de stockage à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant :
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Ensuite, exécutez la commande suivante pour obtenir la clé de votre compte de stockage (vous en aurez besoin pour créer un cluster) :
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
L’extrait de code Python ci-dessous crée un cluster Spark avec 2 nœuds principaux et 1 nœud Worker. Remplissez les variables vides comme expliqué dans les commentaires et n’hésitez pas à modifier d’autres paramètres en fonction de vos besoins.

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

### <a name="get-cluster-details"></a>Obtenir les détails du cluster

Pour obtenir les propriétés d’un cluster donné :

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Exemples

Vous pouvez utiliser `get` pour confirmer que vous avez créé votre cluster avec succès.

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

La sortie doit ressembler à :

```output
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a>Répertorier les clusters

#### <a name="list-clusters-under-the-subscription"></a>Répertorier les clusters dans l’abonnement

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a>Répertorier les clusters par groupe de ressources

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> `list()` et `list_by_resource_group()` retournent un objet `ClusterPaged`. Appeler `advance_page()` renvoie une liste de clusters sur cette page et avance l’objet `ClusterPaged` à la page suivante. Cette opération peut être répétée jusqu’à ce qu’une exception `StopIteration` soit générée, indiquant qu’il n’y a plus d’autres pages.

#### <a name="example"></a>Exemples

L’exemple suivant imprime les propriétés de tous les clusters pour l’abonnement actuel :

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a>Supprimer un cluster

Pour supprimer un cluster :

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a>Mettre à jour les balises de cluster

Vous pouvez mettre à jour les balises d’un cluster donné comme suit :

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a>Exemples

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a>Redimensionner le cluster

Vous pouvez mettre à l’échelle un nombre donné de clusters de nœuds Worker en spécifiant une nouvelle taille comme suit :

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a>Cluster Monitoring (Surveillance des clusters)

Le kit de développement logiciel (SDK) HDInsight Management peut également être utilisé pour gérer la surveillance de vos clusters via Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Activer la surveillance OMS

> [!NOTE]
> Pour activer la supervision OMS, vous devez disposer d’un espace de travail Log Analytics existant. Si vous n’en n’avez pas déjà créé un, vous pouvez apprendre comment le faire ici : [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Pour activer la surveillance OMS sur votre cluster :

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a>Afficher l’état de surveillance OMS

Pour obtenir l’état d’OMS sur votre cluster :

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a>Désactiver la surveillance OMS

Pour désactiver OMS sur votre cluster :

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a>Actions de script

HDInsight fournit une méthode de configuration intitulée actions de script, qui appelle des scripts personnalisés pour personnaliser le cluster.
> [!NOTE]
> Vous trouverez plus d’informations sur l’utilisation des actions de script ici : [Personnaliser des clusters HDInsight Linux avec des actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Exécuter des actions de script
Pour exécuter des actions de script sur un cluster donné :

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Supprimer une action de script

Pour supprimer une action de script persistante spécifiée sur un cluster donné :

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a>Répertorier les actions de script persistantes

> [!NOTE]
> `list()` et `list_persisted_scripts()` renvoient un objet `RuntimeScriptActionDetailPaged`. Appeler `advance_page()` retourne une liste de `RuntimeScriptActionDetail` sur cette page et avance l’objet `RuntimeScriptActionDetailPaged` à la page suivante. Cette opération peut être répétée jusqu’à ce qu’une exception `StopIteration` soit générée, indiquant qu’il n’y a plus d’autres pages. Reportez-vous à l’exemple ci-dessous.

Pour répertorier toutes les actions de script persistantes pour le cluster spécifié :
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Exemples

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a>Répertorier tout l’historique d’exécution des scripts

Pour répertorier tout l’historique d’exécution des scripts pour le cluster spécifié :

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Exemples

Cet exemple imprime tous les détails de toutes les exécutions de script passées.

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
