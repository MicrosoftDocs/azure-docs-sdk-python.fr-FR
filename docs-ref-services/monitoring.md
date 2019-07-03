---
title: Bibliothèques de surveillance Azure pour Python
description: Référence sur les bibliothèques de surveillance Azure pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, surveillance
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 6408854e48378c27da56185899db5e1cc7f939e5
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534259"
---
# <a name="azure-monitoring-libraries-for-python"></a><span data-ttu-id="6cec5-104">Bibliothèques de surveillance Azure pour Python</span><span class="sxs-lookup"><span data-stu-id="6cec5-104">Azure Monitoring libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="6cec5-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6cec5-105">Overview</span></span> 
<span data-ttu-id="6cec5-106">L’analyse fournit des données visant à garantir que votre application reste opérationnelle et soit exécutée en toute intégrité.</span><span class="sxs-lookup"><span data-stu-id="6cec5-106">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="6cec5-107">Elle vous permet également de parer à des problèmes potentiels ou de résoudre des problèmes déjà survenus.</span><span class="sxs-lookup"><span data-stu-id="6cec5-107">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="6cec5-108">En outre, vous pouvez utiliser les données d’analyse pour obtenir des informations détaillées sur votre application.</span><span class="sxs-lookup"><span data-stu-id="6cec5-108">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="6cec5-109">Ces connaissances peuvent vous aider à améliorer les performances de l’application ou sa facilité de gestion, ou à automatiser des actions qui exigeraient normalement une intervention manuelle.</span><span class="sxs-lookup"><span data-stu-id="6cec5-109">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="6cec5-110">En savoir plus sur Azure Monitor [en cliquant ici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="6cec5-110">Learn more about Azure Monitor [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> 

## <a name="installation"></a><span data-ttu-id="6cec5-111">Installation</span><span class="sxs-lookup"><span data-stu-id="6cec5-111">Installation</span></span>
```bash
pip install azure-mgmt-monitor
```

## <a name="example---metrics"></a><span data-ttu-id="6cec5-112">Exemple : métriques</span><span class="sxs-lookup"><span data-stu-id="6cec5-112">Example - Metrics</span></span>
<span data-ttu-id="6cec5-113">Cet exemple obtient les métriques d’une ressource sur Azure (machines virtuelles, etc.).</span><span class="sxs-lookup"><span data-stu-id="6cec5-113">This sample obtains the metrics of a resource on Azure (VMs, etc.).</span></span> <span data-ttu-id="6cec5-114">Cet exemple nécessite au moins la version 0.4.0 du package Python.</span><span class="sxs-lookup"><span data-stu-id="6cec5-114">This sample requires version 0.4.0 of the Python package at least.</span></span>

<span data-ttu-id="6cec5-115">Vous trouverez une liste complète des mots-clés disponibles pour les filtres [à cette adresse](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cec5-115">A complete list of available keywords for filters is available [here](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span></span>

<span data-ttu-id="6cec5-116">Les mesures prises en charge par type de ressource sont disponibles [à cette adresse](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span><span class="sxs-lookup"><span data-stu-id="6cec5-116">Supported metrics per resource type is available [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span></span>

```python
import datetime
from azure.mgmt.monitor import MonitorManagementClient

# Get the ARM id of your resource. You might chose to do a "get"
# using the according management or to build the URL directly
# Example for a ARM VM
resource_id = (
    "subscriptions/{}/"
    "resourceGroups/{}/"
    "providers/Microsoft.Compute/virtualMachines/{}"
).format(subscription_id, resource_group_name, vm_name)

# create client
client = MonitorManagementClient(
    credentials,
    subscription_id
)

# You can get the available metrics of this specific resource
for metric in client.metric_definitions.list(resource_id):
    # azure.monitor.models.MetricDefinition
    print("{}: id={}, unit={}".format(
        metric.name.localized_value,
        metric.name.value,
        metric.unit
    ))

# Example of result for a VM:
# Percentage CPU: id=Percentage CPU, unit=Unit.percent
# Network In: id=Network In, unit=Unit.bytes
# Network Out: id=Network Out, unit=Unit.bytes
# Disk Read Bytes: id=Disk Read Bytes, unit=Unit.bytes
# Disk Write Bytes: id=Disk Write Bytes, unit=Unit.bytes
# Disk Read Operations/Sec: id=Disk Read Operations/Sec, unit=Unit.count_per_second
# Disk Write Operations/Sec: id=Disk Write Operations/Sec, unit=Unit.count_per_second

# Get CPU total of yesterday for this VM, by hour

today = datetime.datetime.now().date()
yesterday = today - datetime.timedelta(days=1)

metrics_data = client.metrics.list(
    resource_id,
    timespan="{}/{}".format(yesterday, today),
    interval='PT1H',
    metricnames='Percentage CPU',
    aggregation='Total'
)

for item in metrics_data.value:
    # azure.mgmt.monitor.models.Metric
    print("{} ({})".format(item.name.localized_value, item.unit.name))
    for timeserie in item.timeseries:
        for data in timeserie.data:
            # azure.mgmt.monitor.models.MetricData
            print("{}: {}".format(data.time_stamp, data.total))

# Example of result:
# Percentage CPU (percent)
# 2016-11-16 00:00:00+00:00: 72.0
# 2016-11-16 01:00:00+00:00: 90.59
# 2016-11-16 02:00:00+00:00: 60.58
# 2016-11-16 03:00:00+00:00: 65.78
# 2016-11-16 04:00:00+00:00: 43.96
# 2016-11-16 05:00:00+00:00: 43.96
# 2016-11-16 06:00:00+00:00: 114.9
# 2016-11-16 07:00:00+00:00: 45.4
```

## <a name="example---alerts"></a><span data-ttu-id="6cec5-117">Exemple : alertes</span><span class="sxs-lookup"><span data-stu-id="6cec5-117">Example - Alerts</span></span>
<span data-ttu-id="6cec5-118">Cet exemple montre comment configurer automatiquement des alertes sur vos ressources lorsqu’elles sont créées pour vous assurer que toutes les ressources sont analysées correctement.</span><span class="sxs-lookup"><span data-stu-id="6cec5-118">This example shows how to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="6cec5-119">Créez une source de données sur une machine virtuelle pour envoyer une alerte en cas d’utilisation du processeur :</span><span class="sxs-lookup"><span data-stu-id="6cec5-119">Create a data source on a VM to alert on CPU usage:</span></span>
```python
from azure.mgmt.monitor import MonitorMgmtClient
from azure.mgmt.monitor.models import RuleMetricDataSource

resource_id = (
    "subscriptions/{}/"
    "resourceGroups/MonitorTestsDoNotDelete/"
    "providers/Microsoft.Compute/virtualMachines/MonitorTest"
).format(self.settings.SUBSCRIPTION_ID)

# create client
client = MonitorMgmtClient(
    credentials,
    subscription_id
)

# I need a subclass of "RuleDataSource"
data_source = RuleMetricDataSource(
    resource_uri = resource_id,
    metric_name = 'Percentage CPU'
)
```
<span data-ttu-id="6cec5-120">Créez une condition de seuil qui se déclenche lorsque l’utilisation moyenne du processeur d’une machine virtuelle au cours des 5 dernières minutes est supérieure à 90 % (à l’aide de la source de données précédente) :</span><span class="sxs-lookup"><span data-stu-id="6cec5-120">Create a threshold condition that triggers when the average CPU usage of a VM for the last 5 minutes is above 90% (using the preceding data source):</span></span>
```python
from azure.mgmt.monitor.models import ThresholdRuleCondition

# I need a subclasses of "RuleCondition"
rule_condition = ThresholdRuleCondition(
    data_source = data_source,
    operator = 'GreaterThanOrEqual',
    threshold = 90,
    window_size = 'PT5M',
    time_aggregation = 'Average'
)
```

<span data-ttu-id="6cec5-121">Créez une action de messagerie :</span><span class="sxs-lookup"><span data-stu-id="6cec5-121">Create an email action:</span></span>
```python
from azure.mgmt.monitor.models import RuleEmailAction

# I need a subclass of "RuleAction"
rule_action = RuleEmailAction(
    send_to_service_owners = True,
    custom_emails = [
        'monitoringemail@microsoft.com'
    ]
)
```

<span data-ttu-id="6cec5-122">Créez l’alerte :</span><span class="sxs-lookup"><span data-stu-id="6cec5-122">Create the alert:</span></span>
```python
rule_name = 'MyPyTestAlertRule'
my_alert = client.alert_rules.create_or_update(
    group_name,
    rule_name,
    {
        'location': 'westus',
        'alert_rule_resource_name': rule_name,
        'description': 'Testing Alert rule creation',
        'is_enabled': True,
        'condition': rule_condition,
        'actions': [
            rule_action
        ]
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="6cec5-123">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="6cec5-123">Explore the Management APIs</span></span>](/python/api/overview/azure/monitoring/management)
