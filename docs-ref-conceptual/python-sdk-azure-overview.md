---
title: Bibliothèques Azure pour Python
description: Vue d’ensemble des bibliothèques de gestion et de service Azure pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: ''
ms.openlocfilehash: bb17295de2f0272f0525fda5edab87e840764478
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534464"
---
# <a name="azure-libraries-for-python"></a><span data-ttu-id="4d964-104">Bibliothèques Azure pour Python</span><span class="sxs-lookup"><span data-stu-id="4d964-104">Azure libraries for Python</span></span>

<span data-ttu-id="4d964-105">Les bibliothèques Azure pour Python vous permettent d’utiliser des services Azure et de gérer des ressources Azure à partir du code de votre application.</span><span class="sxs-lookup"><span data-stu-id="4d964-105">The Azure libraries for Python let you use Azure services and manage Azure resources from your application code.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="4d964-106">Gérer des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="4d964-106">Manage Azure resources</span></span>

<span data-ttu-id="4d964-107">Créez et gérez des ressources Azure à partir des applications Python à l’aide des bibliothèques Azure pour Python.</span><span class="sxs-lookup"><span data-stu-id="4d964-107">Create and manage Azure resources from Python applications using the Azure libraries for Python.</span></span>

<span data-ttu-id="4d964-108">Par exemple, vous pouvez utiliser le code suivant pour créer une instance SQL Server :</span><span class="sxs-lookup"><span data-stu-id="4d964-108">For example, to create a SQL Server instance, you can use the following code:</span></span>

```python
sql_client = SqlManagementClient(
    credentials,
    subscription_id
)

server = sql_client.servers.create_or_update(
    'myresourcegroup',
    'myservername',
    {
        'location': 'eastus',
        'version': '12.0', # Required for create
        'administrator_login': 'mysecretname', # Required for create
        'administrator_login_password': 'HusH_Sec4et' # Required for create
    }
)
```

<span data-ttu-id="4d964-109">Vérifiez les [instructions d’installation](python-sdk-azure-install.md) pour obtenir une liste complète des bibliothèques et apprendre comment les importer dans vos projets. Consultez ensuite l’[article de prise en main](python-sdk-azure-get-started.yml) pour configurer l’authentification et exécuter l’exemple de code dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4d964-109">Review the [install instructions](python-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](python-sdk-azure-get-started.yml) to set up your authentication and run sample code against your own Azure subscription.</span></span>

## <a name="connect-to-azure-services"></a><span data-ttu-id="4d964-110">Se connecter aux services Azure</span><span class="sxs-lookup"><span data-stu-id="4d964-110">Connect to Azure services</span></span>

<span data-ttu-id="4d964-111">En plus d’utiliser les bibliothèques Python pour créer et gérer des ressources dans Azure, vous pouvez vous en servir pour vous connecter et utiliser les ressources dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="4d964-111">In addition to using Python libraries to create and manage resources within Azure, you can also use Python libraries to connect and use those resources in your apps.</span></span> <span data-ttu-id="4d964-112">Par exemple, vous pouvez mettre à jour une table SQL Database ou stocker des fichiers dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4d964-112">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="4d964-113">Sélectionnez la bibliothèque dont vous avez besoin pour un service particulier à partir de la liste complète des bibliothèques et visitez le centre de développement Python pour trouver des didacticiels et des exemples de code vous aidant à les utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="4d964-113">Select the library you need for a particular service from the complete list of libraries and visit the Python developer center for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="4d964-114">Par exemple, pour télécharger une page HTML simple sur un objet blob et obtenir l’URL :</span><span class="sxs-lookup"><span data-stu-id="4d964-114">For example, to upload a simple HTML page on a blob and get the Url:</span></span>

```python
storage_client = CloudStorageAccount(storage_account_name, storage_key)
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(
    'mycontainername',
    public_access=PublicAccess.Blob
)

blob_service.create_blob_from_bytes(
    'mycontainername',
    'myblobname',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url('mycontainername', 'myblobname'))
```

## <a name="sample-code-and-reference"></a><span data-ttu-id="4d964-115">Exemple de code et référence</span><span class="sxs-lookup"><span data-stu-id="4d964-115">Sample code and reference</span></span>
<span data-ttu-id="4d964-116">Les exemples suivants détaillent les tâches d’automatisation courantes avec les bibliothèques de gestion Azure pour Python et disposent de codes préparés pour vos applications :</span><span class="sxs-lookup"><span data-stu-id="4d964-116">The following samples cover common automation tasks with the Azure management libraries for Python and have code ready to use in your own apps:</span></span>
- [<span data-ttu-id="4d964-117">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="4d964-117">Virtual Machines</span></span>](python-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="4d964-118">Applications Web</span><span class="sxs-lookup"><span data-stu-id="4d964-118">Web apps</span></span>](python-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="4d964-119">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="4d964-119">SQL Database</span></span>](python-sdk-azure-sql-database-samples.md)

<span data-ttu-id="4d964-120">Une [référence](/python/api/overview/azure) est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="4d964-120">A [reference](/python/api/overview/azure) is available for all packages in both the service an management libraries.</span></span> <span data-ttu-id="4d964-121">Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration des versions précédentes sont disponibles dans les [notes de publication](python-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="4d964-121">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](python-sdk-azure-release-notes.md).</span></span> 

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="4d964-122">Obtenir de l’aide et donner son avis</span><span class="sxs-lookup"><span data-stu-id="4d964-122">Get help and give feedback</span></span>

<span data-ttu-id="4d964-123">Posez des questions à la communauté sur [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-sdk-python) et découvrez des problèmes en rapport avec le Kit de développement logiciel (SDK) sur le [projet GitHub](https://github.com/Azure/azure-sdk-for-python).</span><span class="sxs-lookup"><span data-stu-id="4d964-123">Post questions to the community on [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-sdk-python) and open issues against the SDK on the [project GitHub](https://github.com/Azure/azure-sdk-for-python).</span></span>
