---
title: Bibliothèques de stockage Azure pour Python
description: ''
keywords: Azure, Python, Kit de développement logiciel (SDK), API, stockage
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: 1cafbe5558c49e238182b7efabeae6fcb96d43d8
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534194"
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="8eb48-103">Bibliothèques de stockage Azure pour Python</span><span class="sxs-lookup"><span data-stu-id="8eb48-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="8eb48-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8eb48-104">Overview</span></span>
- <span data-ttu-id="8eb48-105">Lire et écrire des objets et des fichiers à partir du [Stockage Blob Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage)</span><span class="sxs-lookup"><span data-stu-id="8eb48-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="8eb48-106">Envoyer et recevoir des messages entre des applications connectées par le cloud avec le [stockage de files d’attente Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span><span class="sxs-lookup"><span data-stu-id="8eb48-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="8eb48-107">Lire et écrire des données structurées volumineuses avec le [stockage de tables Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span><span class="sxs-lookup"><span data-stu-id="8eb48-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="8eb48-108">Partager le stockage entre des applications avec [stockage de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span><span class="sxs-lookup"><span data-stu-id="8eb48-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="8eb48-109">Créer, mettre à jour et gérer les requêtes et les comptes de stockage Azure et régénérer les clés d’accès à partir de votre code Python avec les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="8eb48-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="8eb48-110">Installer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="8eb48-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="8eb48-111">Client</span><span class="sxs-lookup"><span data-stu-id="8eb48-111">Client</span></span>

<span data-ttu-id="8eb48-112">Les bibliothèques clientes Stockage Azure sont constituées de 4 packages : blob, fichier, file d’attente et table.</span><span class="sxs-lookup"><span data-stu-id="8eb48-112">Azure Storage Client Libraries consist of 4 packages: Blob, File, Queue and Table.</span></span> <span data-ttu-id="8eb48-113">Pour installer le package de l’objet blob, exécutez :</span><span class="sxs-lookup"><span data-stu-id="8eb48-113">To install the blob package, run:</span></span>

```bash
pip install azure-storage-blob
```

### <a name="management"></a><span data-ttu-id="8eb48-114">gestion</span><span class="sxs-lookup"><span data-stu-id="8eb48-114">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="8eb48-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="8eb48-115">Example</span></span>
```python
from azure.storage.blob import BlockBlobService

blob_service = BlockBlobService(account_name, account_key)

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

## <a name="samples"></a><span data-ttu-id="8eb48-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="8eb48-116">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="8eb48-117">Prise en main du stockage Blob Azure dans Python</span><span class="sxs-lookup"><span data-stu-id="8eb48-117">Get started with Azure Blob Storage in Python</span></span>](https://docs.microsoft.com/azure/storage/blobs/storage-python-how-to-use-blob-storage) | <span data-ttu-id="8eb48-118">Créer, lire, mettre à jour, limiter l’accès et supprimer des fichiers et des objets dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb48-118">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="8eb48-119">Prise en main du stockage de file d’attente Azure dans Python</span><span class="sxs-lookup"><span data-stu-id="8eb48-119">Get started with Azure Queue Storage in Python</span></span>](https://docs.microsoft.com/azure/storage/queues/storage-python-how-to-use-queue-storage) | <span data-ttu-id="8eb48-120">Insérez, Affichez un aperçu, récupérez et supprimez des messages à partir du stockage de files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="8eb48-120">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="8eb48-121">Gérer des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8eb48-121">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="8eb48-122">Créer, mettre à jour et supprimer des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="8eb48-122">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="8eb48-123">Récupérer et régénérer des clés d’accès de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8eb48-123">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="8eb48-124">Découvrez d’autres [exemples de code Python](https://azure.microsoft.com/resources/samples/?platform=python) à utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="8eb48-124">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>
