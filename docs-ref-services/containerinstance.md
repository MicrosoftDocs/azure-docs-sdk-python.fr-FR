---
title: Bibliothèques Azure Container Instances pour Python
description: Référence pour les bibliothèques Azure Container Instances pour Python
keywords: Azure, python, Kit de développement logiciel (SDK), API, ACI, conteneur, instances
author: dlepow
manager: jeconnoc
ms.date: 04/15/2019
ms.author: danlep
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 19e0e629253462f77d58740857b853d1c94d53cf
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534324"
---
# <a name="azure-container-instances-libraries-for-python"></a>Bibliothèques Azure Container Instances pour Python

Utiliser les bibliothèques Azure Container Instances pour Python pour créer et gérer des instances de conteneurs Azure. Pour en savoir plus, consultez [Vue d’ensemble d’Azure Container Instances](/azure/container-instances/container-instances-overview).

## <a name="management-apis"></a>API de gestion

Utilisez la bibliothèque de gestion pour créer et gérer des instances de conteneurs Azure dans Azure.

Installez le package de gestion via pip :

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a>Exemple de source

Si vous souhaitez voir les exemples de code suivants en contexte, vous pouvez les trouver dans le référentiel GitHub suivant :

[Azure-Samples/aci-docs-sample-python](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a>Authentication

Une des méthodes plus simples pour authentifier les clients Kit de développement logiciel (comme les clients Azure Container Instances et Gestionnaire des ressources dans l’exemple suivant) est [l’authentification basée sur un fichier](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file). L’authentification basée sur un fichier interroge la variable d’environnement `AZURE_AUTH_LOCATION` en quête d’un accès à un fichier de données d’identification. Pour utiliser l’authentification basée sur un fichier :

1. Créer un fichier d’informations d’identification avec [Azure CLI](/cli/azure) ou [Cloud Shell](https://shell.azure.com/) :

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Si vous utilisez [Cloud Shell](https://shell.azure.com/) pour générer le fichier d’informations d’identification, copiez son contenu dans un fichier local auquel votre application Python peut accéder.

2. Définissez la `AZURE_AUTH_LOCATION` variable d’environnement sur le chemin d’accès complet au fichier d’informations d’identification généré. Par exemple (dans Bash) :

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Une fois que vous avez créé le fichier d’informations d’identification et renseigné la variable d’environnement `AZURE_AUTH_LOCATION`, utilisez la méthode `get_client_from_auth_file` des objets [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] et [ContainerInstanceManagementClient][ContainerInstanceManagementClient].

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

Pour plus d’informations sur les méthodes d’authentification disponibles dans les bibliothèques de gestion Python pour Azure, consultez [S’authentifier avec les bibliothèques de gestion Azure pour Python](/python/azure/python-sdk-azure-authenticate).

## <a name="create-container-group---single-container"></a>Créer un groupe de conteneurs : conteneur unique

Cet exemple crée un groupe de conteneurs à un seul conteneur

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L141 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Créer un groupe de conteneurs : plusieurs conteneurs

Cet exemple crée un groupe de conteneurs avec deux conteneurs : un conteneur d’application et un conteneur side-car.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L144-L197 "Create multi-container group")]

## <a name="create-task-based-container-group"></a>Créer un groupe de conteneurs basé sur des tâches

Cet exemple crée un groupe de conteneurs à un seul conteneur basé sur des tâches. Cet exemple montre plusieurs fonctionnalités :

* [Command line override](/azure/container-instances/container-instances-start-command) : une ligne de commande personnalisée, différente de celle spécifiée dans la ligne `CMD` du fichier Docker du conteneur est spécifiée. Command line override vous permet de spécifier une ligne de commande personnalisée à exécuter au démarrage du conteneur remplaçant la ligne de commande par défaut intégrée dans le conteneur. En ce qui concerne l’exécution de plusieurs commandes au démarrage du conteneur, ce qui suit s’applique :

   Si vous souhaitez exécuter une **commande unique** avec plusieurs arguments de ligne de commande, par exemple `echo FOO BAR`, vous devez les fournir sous forme de liste de chaînes à la propriété `command` du [Conteneur][Container]. Par exemple :

   `command = ['echo', 'FOO', 'BAR']`

   Si, toutefois, vous souhaitez exécuter **plusieurs commandes** avec (éventuellement) plusieurs arguments, vous devez exécuter un interpréteur de commandes et passer les commandes en chaînes en tant qu’argument. Par exemple, cela exécute à la fois une commande `echo` et une commande `tail` :

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* [Variables d’environnement](/azure/container-instances/container-instances-environment-variables) : deux variables d’environnement sont spécifiées pour le conteneur du groupe de conteneurs. Utilisez des variables d’environnement pour modifier le comportement du script ou d’une application lors de l’exécution, ou transmettre des informations dynamiques à une application s’exécutant dans le conteneur.
* [Restart policy](/azure/container-instances/container-instances-restart-policy) : le conteneur est configuré à l’aide d’une stratégie de redémarrage « Never », utile pour les conteneurs basés sur des tâches exécutés dans le cadre d’un programme de traitement par lots.
* Interrogation des opérations avec [AzureOperationPoller][AzureOperationPoller] : une fois la méthode create appelée, l’opération est interrogée pour déterminer quand elle est terminée et à quel moment les journaux du groupe de conteneurs peuvent être obtenus.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L200-L276 "Run a task-based container")]

## <a name="list-container-groups"></a>Répertorier des groupes de conteneurs

Cet exemple répertorie les groupes de conteneurs dans un groupe de ressources, puis imprime certaines de leurs propriétés.

Lorsque vous listez les groupes de conteneurs, l’[instance_view][instance_view] de chaque groupe retourné est `None`. Pour obtenir les détails des conteneurs d’un groupe de conteneurs, vous devez ensuite [obtenir][containergroupoperations_get] le groupe de conteneurs, qui retourne le groupe avec sa propriété `instance_view` renseignée. Consultez la section [Obtenir un groupe de conteneurs existant](#get-an-existing-container-group) suivant, pour obtenir un exemple d’itération sur les conteneurs d’un groupe de conteneurs dans son `instance_view`.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L279-L293 "List container groups")]

## <a name="get-an-existing-container-group"></a>Obtenir un groupe de conteneurs existant

Cet exemple obtient un groupe de conteneurs spécifique à partir d’un groupe de ressources, puis imprime certaines de ses propriétés (y compris ses conteneurs) et ses valeurs.

L’[opération get][containergroupoperations_get] returns a container group with its [instance_view][instance_view] est renseignée, ce qui vous permet d’itérer sur chaque conteneur du groupe. Seule l’opération `get` remplit la propriété `instance_vew` du groupe de conteneurs. Le fait de répertorier les groupes de conteneurs dans un abonnement ou un groupe de ressources n’a pas pour effet d’alimenter la vue d’instance en raison de la nature potentiellement onéreuse de l’opération (par exemple, lorsque vous répertoriez des centaines de groupes de conteneurs contenant potentiellement plusieurs conteneurs). Comme mentionné précédemment dans la section [Répertorier des groupes de conteneurs](#list-container-groups), après un `list`, vous devez `get` un groupe de conteneurs spécifique pour obtenir les détails relatifs à l’instance de conteneur s’y rapportant.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L296-L325 "Get container group")]

## <a name="delete-a-container-group"></a>Supprimer un groupe de conteneurs

Cet exemple supprime plusieurs groupes de conteneurs à partir d’un groupe de ressources, ainsi que le groupe de ressources.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a>Étapes suivantes

* Le code source pour les exemples précédents est accessible sur GitHub :

  [Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]

* Plus d’exemples de code Azure Container Instances :

  [Exemples de code Azure][samples-aci]

* Découvrez d’autres [exemples de code Python][samples-python] à utiliser dans vos applications.

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get-resource-group-name--container-group-name--custom-headers-none--raw-false----operation-config-
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient