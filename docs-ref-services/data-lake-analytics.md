---
title: Bibliothèques Azure Data Lake Analytics pour Python
description: Références sur les bibliothèques Azure Data Lake Analytics pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Data Lake Analytics
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/04/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f1bba0556baf7c373a3584c2dae922e04fa76fc8
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52279262"
---
# <a name="azure-data-lake-analytics-libraries-for-python"></a><span data-ttu-id="34eb9-104">Bibliothèques Azure Data Lake Analytics pour Python</span><span class="sxs-lookup"><span data-stu-id="34eb9-104">Azure Data Lake Analytics libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="34eb9-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="34eb9-105">Overview</span></span>
<span data-ttu-id="34eb9-106">Exécutez des travaux d’analyse Big Data mis à l’échelle de manière à obtenir des jeux de données conséquents avec [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span><span class="sxs-lookup"><span data-stu-id="34eb9-106">Run big data analysis jobs that scale to massive data sets with [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="34eb9-107">Installer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="34eb9-107">Install the libraries</span></span>

## <a name="management-api"></a><span data-ttu-id="34eb9-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="34eb9-108">Management API</span></span>
<span data-ttu-id="34eb9-109">Utilisez l’API de gestion pour gérer les comptes, les travaux, les stratégies et les catalogues Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="34eb9-109">Use the management API to manage Data Lake Analytics accounts, jobs, policies, and catalogs.</span></span>

```bash
pip install azure-mgmt-datalake-analytics
```

### <a name="example"></a><span data-ttu-id="34eb9-110">Exemples</span><span class="sxs-lookup"><span data-stu-id="34eb9-110">Example</span></span>
<span data-ttu-id="34eb9-111">Il s’agit d’un exemple de la création d’un compte Data Lake Analytics et de l’envoi d’un travail.</span><span class="sxs-lookup"><span data-stu-id="34eb9-111">This is an example of how to create a Data Lake Analytics account and submit a job.</span></span> 

```python
## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adls = '<Azure Data Lake Analytics Account Name>'

# Create the clients
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')

# Create resource group
armGroupResult = resourceClient.resource_groups.create_or_update(rg, ResourceGroup(location=location))

# Create a store account
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()

# Create an ADLA account
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()

# Submit a job
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="34eb9-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="34eb9-112">Explore the Management APIs</span></span>](/python/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a><span data-ttu-id="34eb9-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="34eb9-113">Samples</span></span>
[<span data-ttu-id="34eb9-114">Gérer Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="34eb9-114">Manage Azure Data Lake Anyalytics</span></span>](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-python-sdk)