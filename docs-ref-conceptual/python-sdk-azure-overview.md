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
# <a name="azure-libraries-for-python"></a>Bibliothèques Azure pour Python

Les bibliothèques Azure pour Python vous permettent d’utiliser des services Azure et de gérer des ressources Azure à partir du code de votre application. 

## <a name="manage-azure-resources"></a>Gérer des ressources Azure

Créez et gérez des ressources Azure à partir des applications Python à l’aide des bibliothèques Azure pour Python.

Par exemple, vous pouvez utiliser le code suivant pour créer une instance SQL Server :

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

Vérifiez les [instructions d’installation](python-sdk-azure-install.md) pour obtenir une liste complète des bibliothèques et apprendre comment les importer dans vos projets. Consultez ensuite l’[article de prise en main](python-sdk-azure-get-started.yml) pour configurer l’authentification et exécuter l’exemple de code dans votre abonnement Azure.

## <a name="connect-to-azure-services"></a>Se connecter aux services Azure

En plus d’utiliser les bibliothèques Python pour créer et gérer des ressources dans Azure, vous pouvez vous en servir pour vous connecter et utiliser les ressources dans vos applications. Par exemple, vous pouvez mettre à jour une table SQL Database ou stocker des fichiers dans le stockage Azure. Sélectionnez la bibliothèque dont vous avez besoin pour un service particulier à partir de la liste complète des bibliothèques et visitez le centre de développement Python pour trouver des didacticiels et des exemples de code vous aidant à les utiliser dans vos applications.

Par exemple, pour télécharger une page HTML simple sur un objet blob et obtenir l’URL :

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

## <a name="sample-code-and-reference"></a>Exemple de code et référence
Les exemples suivants détaillent les tâches d’automatisation courantes avec les bibliothèques de gestion Azure pour Python et disposent de codes préparés pour vos applications :
- [Machines virtuelles](python-sdk-azure-virtual-machine-samples.md)
- [Applications Web](python-sdk-azure-web-apps-samples.md)
- [Base de données SQL](python-sdk-azure-sql-database-samples.md)

Une [référence](/python/api/overview/azure) est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion. Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration des versions précédentes sont disponibles dans les [notes de publication](python-sdk-azure-release-notes.md). 

## <a name="get-help-and-give-feedback"></a>Obtenir de l’aide et donner son avis

Posez des questions à la communauté sur [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-sdk-python) et découvrez des problèmes en rapport avec le Kit de développement logiciel (SDK) sur le [projet GitHub](https://github.com/Azure/azure-sdk-for-python).
