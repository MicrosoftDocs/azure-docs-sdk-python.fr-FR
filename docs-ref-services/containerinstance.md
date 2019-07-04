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
# <a name="azure-container-instances-libraries-for-python"></a><span data-ttu-id="a2fb2-104">Bibliothèques Azure Container Instances pour Python</span><span class="sxs-lookup"><span data-stu-id="a2fb2-104">Azure Container Instances libraries for Python</span></span>

<span data-ttu-id="a2fb2-105">Utiliser les bibliothèques Azure Container Instances pour Python pour créer et gérer des instances de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-105">Use the Microsoft Azure Container Instances libraries for Python to create and manage Azure container instances.</span></span> <span data-ttu-id="a2fb2-106">Pour en savoir plus, consultez [Vue d’ensemble d’Azure Container Instances](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="a2fb2-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-apis"></a><span data-ttu-id="a2fb2-107">API de gestion</span><span class="sxs-lookup"><span data-stu-id="a2fb2-107">Management APIs</span></span>

<span data-ttu-id="a2fb2-108">Utilisez la bibliothèque de gestion pour créer et gérer des instances de conteneurs Azure dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="a2fb2-109">Installez le package de gestion via pip :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-109">Install the management package via pip:</span></span>

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a><span data-ttu-id="a2fb2-110">Exemple de source</span><span class="sxs-lookup"><span data-stu-id="a2fb2-110">Example source</span></span>

<span data-ttu-id="a2fb2-111">Si vous souhaitez voir les exemples de code suivants en contexte, vous pouvez les trouver dans le référentiel GitHub suivant :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="a2fb2-112">Azure-Samples/aci-docs-sample-python</span><span class="sxs-lookup"><span data-stu-id="a2fb2-112">Azure-Samples/aci-docs-sample-python</span></span>](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a><span data-ttu-id="a2fb2-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="a2fb2-113">Authentication</span></span>

<span data-ttu-id="a2fb2-114">Une des méthodes plus simples pour authentifier les clients Kit de développement logiciel (comme les clients Azure Container Instances et Gestionnaire des ressources dans l’exemple suivant) est [l’authentification basée sur un fichier](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span><span class="sxs-lookup"><span data-stu-id="a2fb2-114">One of the easiest ways to authenticate SDK clients (like the Azure Container Instances and Resource Manager clients in the following example) is with [file-based authentication](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span></span> <span data-ttu-id="a2fb2-115">L’authentification basée sur un fichier interroge la variable d’environnement `AZURE_AUTH_LOCATION` en quête d’un accès à un fichier de données d’identification.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-115">File-based authentication queries the `AZURE_AUTH_LOCATION` environment variable for the path to a credentials file.</span></span> <span data-ttu-id="a2fb2-116">Pour utiliser l’authentification basée sur un fichier :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="a2fb2-117">Créer un fichier d’informations d’identification avec [Azure CLI](/cli/azure) ou [Cloud Shell](https://shell.azure.com/) :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="a2fb2-118">Si vous utilisez [Cloud Shell](https://shell.azure.com/) pour générer le fichier d’informations d’identification, copiez son contenu dans un fichier local auquel votre application Python peut accéder.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your Python application can access.</span></span>

2. <span data-ttu-id="a2fb2-119">Définissez la `AZURE_AUTH_LOCATION` variable d’environnement sur le chemin d’accès complet au fichier d’informations d’identification généré.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="a2fb2-120">Par exemple (dans Bash) :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-120">For example (in Bash):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="a2fb2-121">Une fois que vous avez créé le fichier d’informations d’identification et renseigné la variable d’environnement `AZURE_AUTH_LOCATION`, utilisez la méthode `get_client_from_auth_file` des objets [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] et [ContainerInstanceManagementClient][ContainerInstanceManagementClient].</span><span class="sxs-lookup"><span data-stu-id="a2fb2-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the `get_client_from_auth_file` method of the [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] and [ContainerInstanceManagementClient][ContainerInstanceManagementClient] objects.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

<span data-ttu-id="a2fb2-122">Pour plus d’informations sur les méthodes d’authentification disponibles dans les bibliothèques de gestion Python pour Azure, consultez [S’authentifier avec les bibliothèques de gestion Azure pour Python](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="a2fb2-122">For more details about the available authentication methods in the Python management libraries for Azure, see [Authenticate with the Azure Management Libraries for Python](/python/azure/python-sdk-azure-authenticate).</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="a2fb2-123">Créer un groupe de conteneurs : conteneur unique</span><span class="sxs-lookup"><span data-stu-id="a2fb2-123">Create container group - single container</span></span>

<span data-ttu-id="a2fb2-124">Cet exemple crée un groupe de conteneurs à un seul conteneur</span><span class="sxs-lookup"><span data-stu-id="a2fb2-124">This example creates a container group with a single container</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L141 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="a2fb2-125">Créer un groupe de conteneurs : plusieurs conteneurs</span><span class="sxs-lookup"><span data-stu-id="a2fb2-125">Create container group - multiple containers</span></span>

<span data-ttu-id="a2fb2-126">Cet exemple crée un groupe de conteneurs avec deux conteneurs : un conteneur d’application et un conteneur side-car.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-126">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L144-L197 "Create multi-container group")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="a2fb2-127">Créer un groupe de conteneurs basé sur des tâches</span><span class="sxs-lookup"><span data-stu-id="a2fb2-127">Create task-based container group</span></span>

<span data-ttu-id="a2fb2-128">Cet exemple crée un groupe de conteneurs à un seul conteneur basé sur des tâches.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-128">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="a2fb2-129">Cet exemple montre plusieurs fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-129">This example demonstrates several features:</span></span>

* <span data-ttu-id="a2fb2-130">[Command line override](/azure/container-instances/container-instances-start-command) : une ligne de commande personnalisée, différente de celle spécifiée dans la ligne `CMD` du fichier Docker du conteneur est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-130">[Command line override](/azure/container-instances/container-instances-start-command) - A custom command line, different from that which is specified in the container's Dockerfile `CMD` line, is specified.</span></span> <span data-ttu-id="a2fb2-131">Command line override vous permet de spécifier une ligne de commande personnalisée à exécuter au démarrage du conteneur remplaçant la ligne de commande par défaut intégrée dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-131">Command line override allows you to specify a custom command line to execute at container startup, overriding the default command line baked-in to the container.</span></span> <span data-ttu-id="a2fb2-132">En ce qui concerne l’exécution de plusieurs commandes au démarrage du conteneur, ce qui suit s’applique :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-132">Regarding executing multiple commands at container startup, the following applies:</span></span>

   <span data-ttu-id="a2fb2-133">Si vous souhaitez exécuter une **commande unique** avec plusieurs arguments de ligne de commande, par exemple `echo FOO BAR`, vous devez les fournir sous forme de liste de chaînes à la propriété `command` du [Conteneur][Container].</span><span class="sxs-lookup"><span data-stu-id="a2fb2-133">If you want to run a **single command** with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string list to the `command` property of the [Container][Container].</span></span> <span data-ttu-id="a2fb2-134">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-134">For example:</span></span>

   `command = ['echo', 'FOO', 'BAR']`

   <span data-ttu-id="a2fb2-135">Si, toutefois, vous souhaitez exécuter **plusieurs commandes** avec (éventuellement) plusieurs arguments, vous devez exécuter un interpréteur de commandes et passer les commandes en chaînes en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-135">If, however, you want to run **multiple commands** with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="a2fb2-136">Par exemple, cela exécute à la fois une commande `echo` et une commande `tail` :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-136">For example, this executes both an `echo` and a `tail` command:</span></span>

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* <span data-ttu-id="a2fb2-137">[Variables d’environnement](/azure/container-instances/container-instances-environment-variables) : deux variables d’environnement sont spécifiées pour le conteneur du groupe de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-137">[Environment variables](/azure/container-instances/container-instances-environment-variables) - Two environment variables are specified for the container in the container group.</span></span> <span data-ttu-id="a2fb2-138">Utilisez des variables d’environnement pour modifier le comportement du script ou d’une application lors de l’exécution, ou transmettre des informations dynamiques à une application s’exécutant dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-138">Use environment variables to modify script or application behavior at runtime, or otherwise pass dynamic information to an application running in the container.</span></span>
* <span data-ttu-id="a2fb2-139">[Restart policy](/azure/container-instances/container-instances-restart-policy) : le conteneur est configuré à l’aide d’une stratégie de redémarrage « Never », utile pour les conteneurs basés sur des tâches exécutés dans le cadre d’un programme de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-139">[Restart policy](/azure/container-instances/container-instances-restart-policy) - The container is configured with a restart policy of "Never," useful for task-based containers that are executed as part of a batch job.</span></span>
* <span data-ttu-id="a2fb2-140">Interrogation des opérations avec [AzureOperationPoller][AzureOperationPoller] : une fois la méthode create appelée, l’opération est interrogée pour déterminer quand elle est terminée et à quel moment les journaux du groupe de conteneurs peuvent être obtenus.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-140">Operation polling with [AzureOperationPoller][AzureOperationPoller] - After the create method is invoked, the operation is polled to determine when it has completed and the container group's logs can be obtained.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L200-L276 "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="a2fb2-141">Répertorier des groupes de conteneurs</span><span class="sxs-lookup"><span data-stu-id="a2fb2-141">List container groups</span></span>

<span data-ttu-id="a2fb2-142">Cet exemple répertorie les groupes de conteneurs dans un groupe de ressources, puis imprime certaines de leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-142">This example lists the container groups in a resource group and then prints a few of their properties.</span></span>

<span data-ttu-id="a2fb2-143">Lorsque vous listez les groupes de conteneurs, l’[instance_view][instance_view] de chaque groupe retourné est `None`.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-143">When you list container groups,the [instance_view][instance_view] of each returned group is `None`.</span></span> <span data-ttu-id="a2fb2-144">Pour obtenir les détails des conteneurs d’un groupe de conteneurs, vous devez ensuite [obtenir][containergroupoperations_get] le groupe de conteneurs, qui retourne le groupe avec sa propriété `instance_view` renseignée.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-144">To get the details of the containers within a container group, you must then [get][containergroupoperations_get] the container group, which returns the group with its `instance_view` property populated.</span></span> <span data-ttu-id="a2fb2-145">Consultez la section [Obtenir un groupe de conteneurs existant](#get-an-existing-container-group) suivant, pour obtenir un exemple d’itération sur les conteneurs d’un groupe de conteneurs dans son `instance_view`.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-145">See the next section, [Get an existing container group](#get-an-existing-container-group), for an example of iterating over a container group's containers in its `instance_view`.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L279-L293 "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="a2fb2-146">Obtenir un groupe de conteneurs existant</span><span class="sxs-lookup"><span data-stu-id="a2fb2-146">Get an existing container group</span></span>

<span data-ttu-id="a2fb2-147">Cet exemple obtient un groupe de conteneurs spécifique à partir d’un groupe de ressources, puis imprime certaines de ses propriétés (y compris ses conteneurs) et ses valeurs.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-147">This example gets a specific container group from a resource group, and then prints a few of its properties (including its containers) and their values.</span></span>

<span data-ttu-id="a2fb2-148">L’[opération get][containergroupoperations_get] returns a container group with its [instance_view][instance_view] est renseignée, ce qui vous permet d’itérer sur chaque conteneur du groupe.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-148">The [get operation][containergroupoperations_get] returns a container group with its [instance_view][instance_view] populated, which allows you to iterate over each container in the group.</span></span> <span data-ttu-id="a2fb2-149">Seule l’opération `get` remplit la propriété `instance_vew` du groupe de conteneurs. Le fait de répertorier les groupes de conteneurs dans un abonnement ou un groupe de ressources n’a pas pour effet d’alimenter la vue d’instance en raison de la nature potentiellement onéreuse de l’opération (par exemple, lorsque vous répertoriez des centaines de groupes de conteneurs contenant potentiellement plusieurs conteneurs).</span><span class="sxs-lookup"><span data-stu-id="a2fb2-149">Only the `get` operation populates the `instance_vew` property of the container group--listing the container groups in a subscription or resource group doesn't populate the instance view due to the potentially expensive nature of the operation (for example, when listing hundreds of container groups, each potentially containing multiple containers).</span></span> <span data-ttu-id="a2fb2-150">Comme mentionné précédemment dans la section [Répertorier des groupes de conteneurs](#list-container-groups), après un `list`, vous devez `get` un groupe de conteneurs spécifique pour obtenir les détails relatifs à l’instance de conteneur s’y rapportant.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-150">As mentioned previously in the [List container groups](#list-container-groups) section, after a `list`, you must subsequently `get` a specific container group to obtain its container instance details.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L296-L325 "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="a2fb2-151">Supprimer un groupe de conteneurs</span><span class="sxs-lookup"><span data-stu-id="a2fb2-151">Delete a container group</span></span>

<span data-ttu-id="a2fb2-152">Cet exemple supprime plusieurs groupes de conteneurs à partir d’un groupe de ressources, ainsi que le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-152">This example deletes several container groups from a resource group, as well as the resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a><span data-ttu-id="a2fb2-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2fb2-153">Next steps</span></span>

* <span data-ttu-id="a2fb2-154">Le code source pour les exemples précédents est accessible sur GitHub :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-154">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="a2fb2-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span><span class="sxs-lookup"><span data-stu-id="a2fb2-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span></span>

* <span data-ttu-id="a2fb2-156">Plus d’exemples de code Azure Container Instances :</span><span class="sxs-lookup"><span data-stu-id="a2fb2-156">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="a2fb2-157">[Exemples de code Azure][samples-aci]</span><span class="sxs-lookup"><span data-stu-id="a2fb2-157">[Azure Code Samples][samples-aci]</span></span>

* <span data-ttu-id="a2fb2-158">Découvrez d’autres [exemples de code Python][samples-python] à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="a2fb2-158">Explore more [sample Python code][samples-python] you can use in your apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a2fb2-159">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="a2fb2-159">Explore the management APIs</span></span>](/python/api/overview/azure/containerinstance/management)

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