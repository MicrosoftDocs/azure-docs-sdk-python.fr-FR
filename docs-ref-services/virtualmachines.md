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
# <a name="azure-virtual-machine-libraries"></a>Bibliothèques de machines virtuelle Azure

## <a name="overview"></a>Vue d'ensemble

Des ressources de calcul à la demande et évolutives s’exécutant sous Linux et Windows.

Pour découvrir les machines virtuelles Azure, consultez la section [Créer une machine virtuelle Linux avec le portail Azure](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API de gestion

Créez, configurez et mettez à l’échelle des machines virtuelles Windows et Linux dans Azure à partir de votre code avec l’API de gestion.

Installez la bibliothèque via pip.

```bash
pip install azure-mgmt-compute
```

### <a name="example"></a>Exemples

Créez une machine virtuelle Linux dans un groupe de ressources Azure existant avec l’authentification Managed Service Identity (MSI).

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
> [Explorer les API de gestion](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a>Exemples

* [Gestion des machines virtuelles][1]
* [Authentifier avec Managed Service Identity][2]
* [Créer une machine virtuelle avec l’extension Managed Service Identity][3]
* [Gérer un équilibreur de charge][4]
* [Créer et configurer des disques managés][5]
* [Lister des images][6] 
* [Surveiller les machines virtuelles][7]

Afficher la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) des exemples de machines virtuelles.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md
