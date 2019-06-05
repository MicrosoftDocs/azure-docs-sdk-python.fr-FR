---
title: Bibliothèques Azure Web Apps pour Python
description: ''
keywords: Azure, Python, Kit de développement logiciel (SDK), API, web apps, App Service
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 4870394c6ee39cde546d090fa1a0d136609851b3
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376692"
---
# <a name="azure-web-apps-libraries-for-python"></a>Bibliothèques Azure Web Apps pour Python

## <a name="overview"></a>Vue d'ensemble

Déployez et mettez à l’échelle des sites web, des applications web, des services et des API REST avec [Azure App Service](/azure/app-service).

Pour découvrir Azure App Service, consultez la section [Créer une application web Python dans Azure](/azure/app-service-web/app-service-web-get-started-python).

## <a name="management-api"></a>API de gestion

Déployez, gérez et mettez à l’échelle des éléments hébergés dans Azure App Service avec l’API de gestion.

Installez la bibliothèque via pip.

```bash
pip install azure-mgmt-web
```

### <a name="example"></a>Exemples

Déployer une application web à partir d’un référentiel GitHub dans Azure Web Apps.

```python
siteConfiguration = SiteConfig(
    python_version='3.4'
)

# create a web app
web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=SERVICE_PLAN_ID,
        site_config=siteConfiguration
    )
)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url='https://github.com/lisawong19/python-docs-hello-world',
        branch='master'
    )
)
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/python/api/overview/azure/webapps/management)

## <a name="samples"></a>Exemples

* [Gérer des sites web Azure avec Python][1]
* [Créer un flux de travail d’application logique][2]

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=web-app) des exemples d’application web.

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md
