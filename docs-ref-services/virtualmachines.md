---
title: Bibliothèques de machines virtuelles Azure pour Python
description: ''
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Calcul, Machines virtuelles
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: e09ffed98f3f6050e34ca2cb39e645e30f8bdb15
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534186"
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="31378-103">Bibliothèques de machines virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="31378-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="31378-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="31378-104">Overview</span></span>

<span data-ttu-id="31378-105">Des ressources de calcul à la demande et évolutives s’exécutant sous Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="31378-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="31378-106">Pour découvrir les machines virtuelles Azure, consultez la section [Créer une machine virtuelle Linux avec le portail Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="31378-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="31378-107">API de gestion</span><span class="sxs-lookup"><span data-stu-id="31378-107">Management API</span></span>

<span data-ttu-id="31378-108">Créez, configurez et mettez à l’échelle des machines virtuelles Windows et Linux dans Azure à partir de votre code avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="31378-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="31378-109">Installez la bibliothèque via pip.</span><span class="sxs-lookup"><span data-stu-id="31378-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute
```

### <a name="example"></a><span data-ttu-id="31378-110">Exemples</span><span class="sxs-lookup"><span data-stu-id="31378-110">Example</span></span>

<span data-ttu-id="31378-111">Créez une machine virtuelle Linux dans un groupe de ressources Azure existant avec l’authentification Managed Service Identity (MSI).</span><span class="sxs-lookup"><span data-stu-id="31378-111">Create a new Linux virtual machine in an existing Azure resource group with Managed Service Identity(MSI) authentication.</span></span>

```python
VM_PARAMETERS={
        'location': 'LOCATION',
        'os_profile': {
            'computer_name': 'VM_NAME',
            'admin_username': 'USERNAME',
            'admin_password': 'PASSWORD'
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': 'Canonical',
                'offer': 'UbuntuServer',
                'sku': '16.04.0-LTS',
                'version': 'latest'
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': 'NIC_ID',
            }]
        },
    }

def create_vm()
    compute_client.virtual_machines.create_or_update(
        'RESOURCE_GROUP_NAME', 'VM_NAME', VM_PARAMETERS)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="31378-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="31378-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a><span data-ttu-id="31378-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="31378-113">Samples</span></span>

* <span data-ttu-id="31378-114">[Gestion des machines virtuelles][1]</span><span class="sxs-lookup"><span data-stu-id="31378-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="31378-115">[Authentifier avec Managed Service Identity][2]</span><span class="sxs-lookup"><span data-stu-id="31378-115">[Authenticate with Managed Service Identity][2]</span></span>
* <span data-ttu-id="31378-116">[Créer une machine virtuelle avec l’extension Managed Service Identity][3]</span><span class="sxs-lookup"><span data-stu-id="31378-116">[Create a virtual machine with Managed Service Identity Extension][3]</span></span>
* <span data-ttu-id="31378-117">[Gérer un équilibreur de charge][4]</span><span class="sxs-lookup"><span data-stu-id="31378-117">[Manage a load balancer][4]</span></span>
* <span data-ttu-id="31378-118">[Créer et configurer des disques managés][5]</span><span class="sxs-lookup"><span data-stu-id="31378-118">[Create and configure managed disks][5]</span></span>
* <span data-ttu-id="31378-119">[Lister des images][6]</span><span class="sxs-lookup"><span data-stu-id="31378-119">[List images][6]</span></span> 
* <span data-ttu-id="31378-120">[Surveiller les machines virtuelles][7]</span><span class="sxs-lookup"><span data-stu-id="31378-120">[Monitor virtual machines][7]</span></span>

<span data-ttu-id="31378-121">Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) des exemples de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="31378-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md
