---
title: Disques managés
description: Création, redimensionnement et mise à jour d’un disque géré.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: routlaw
ms.openlocfilehash: 8618b42a545e2e36ccca8944ef1dc6cf49966b00
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534416"
---
# <a name="managed-disks"></a>Disques managés

Le service Disques managés Azure offre une gestion de disques simplifiée et améliorent la scalabilité, la sécurité et l’échelle. Managed Disks fait disparaître la notion de compte de stockage pour disques, permettant ainsi aux clients de mettre à l’échelle sans avoir à se soucier des limites associées aux comptes de stockage. Cet article fournit une introduction rapide et des références sur l’utilisation du service avec Python.

Du point de vue du développeur, l’expérience de la fonctionnalité Disques managés dans Azure CLI est idiomatique à l’expérience CLI rencontrée dans d’autres outils multiplateformes. Vous pouvez utiliser le Kit de développement logiciel (SDK) [Azure Python](https://azure.microsoft.com/develop/python/) et le [package azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) pour administrer la fonctionnalité Disques managés. Vous pouvez créer un client de calcul à l’aide de ce [didacticiel](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).

## <a name="standalone-managed-disks"></a>Disques managés autonomes

Vous pouvez facilement créer des disques managés autonomes de plusieurs façons.

### <a name="create-an-empty-managed-disk"></a>Créer un disque managé vide

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'disk_size_gb': 20,
        'creation_data': {
            'create_option': DiskCreateOption.empty
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-blob-storage"></a>Créer un disque managé à partir du Stockage Blob

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.import_enum,
            'source_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd'
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-an-image-from-blob-storage"></a>Créer une image à partir du stockage Blob

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.images.create_or_update(
    'my_resource_group',
    'my_image_name',
    {
        'location': 'eastus',
        'storage_profile': {
           'os_disk': {
              'os_type': 'Linux',
              'os_state': "Generalized",
              'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
              'caching': "ReadWrite",
           }
        }        
    }
)
image_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-your-own-image"></a>Créer un disque managé à partir de votre propre image

```python
from azure.mgmt.compute.models import DiskCreateOption

# If you don't know the id, do a 'get' like this to obtain it
managed_disk = compute_client.disks.get(self.group_name, 'myImageDisk')
async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.copy,
            'source_resource_id': managed_disk.id
        }
    }
)

disk_resource = async_creation.result()
```

## <a name="virtual-machine-with-managed-disks"></a>Machines virtuelles avec disques managés

Vous pouvez créer une machine virtuelle avec disque géré implicite pour une image de disque spécifique. La création est simplifiée avec la création implicite de disques managés, car il n’y a pas besoin de fournir toutes les informations du disque. Vous n’avez pas à vous soucier de la création et de la gestion des comptes de stockage.

Un disque géré est créé implicitement lors de la création d’une machine virtuelle à partir d’une image du système d’exploitation dans Azure. Dans le paramètre ``storage_profile``, ``os_disk`` est maintenant facultatif. Vous n’avez pas besoin de créer un compte de stockage pour créer une machine virtuelle.

```python
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        publisher='Canonical',
        offer='UbuntuServer',
        sku='16.04-LTS',
        version='latest'
    )
)
```

Le paramètre ``storage_profile`` est maintenant valide. Pour avoir un exemple complet de la procédure à suivre pour créer une machine virtuelle dans Python (réseau y compris), consultez l’ensemble du [didacticiel sur les machines virtuelles dans Python](https://github.com/Azure-Samples/virtual-machines-python-manage).

Vous pouvez également créer un ``storage_profile`` à partir de votre propre image :

```python
# If you don't know the id, do a 'get' like this to obtain it
image = compute_client.images.get(self.group_name, 'myImageDisk')
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        id = image.id
    )
)
```

Vous pouvez facilement attacher un disque géré déjà mis en service.

```python
vm = compute.virtual_machines.get(
    'my_resource_group',
    'my_vm'
)
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
vm.storage_profile.data_disks.append({
    'lun': 12, # You choose the value, depending of what is available for you
    'name': managed_disk.name,
    'create_option': DiskCreateOptionTypes.attach,
    'managed_disk': {
        'id': managed_disk.id
    }
})
async_update = compute_client.virtual_machines.create_or_update(
    'my_resource_group',
    vm.name,
    vm,
)
async_update.wait()
```

## <a name="virtual-machine-scale-sets-with-managed-disks"></a>Groupes de machines virtuelles identiques avec disques managés

Avant la fonctionnalité Disques managés, il fallait créer un compte de stockage manuellement pour chaque machine virtuelle que vous vouliez placer dans votre groupe identique. Il fallait ensuite utiliser le paramètre de liste ``vhd_containers`` afin de fournir tous les noms de comptes de stockage à l’API REST du groupe identique. Le guide de transition officiel est disponible dans cet article `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.

Dorénavant, avec Managed Disks, vous n’avez plus à gérer aucun compte de stockage. Si vous êtes habitué au Kit de développement Python VMSS, vous pouvez maintenant utiliser le même ``storage_profile`` que celui utilisé lors de la création d’une machine virtuelle :

```python
'storage_profile': {
    'image_reference': {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "16.04-LTS",
        "version": "latest"
    }
},
```

Voici l’exemple complet :

```python
naming_infix = "PyTestInfix"
vmss_parameters = {
    'location': self.region,
    "overprovision": True,
    "upgrade_policy": {
        "mode": "Manual"
    },
    'sku': {
        'name': 'Standard_A1',
        'tier': 'Standard',
        'capacity': 5
    },
    'virtual_machine_profile': {
        'storage_profile': {
            'image_reference': {
                "publisher": "Canonical",
                "offer": "UbuntuServer",
                "sku": "16.04-LTS",
                "version": "latest"
            }
        },
        'os_profile': {
            'computer_name_prefix': naming_infix,
            'admin_username': 'Foo12',
            'admin_password': 'BaR@123!!!!',
        },
        'network_profile': {
            'network_interface_configurations' : [{
                'name': naming_infix + 'nic',
                "primary": True,
                'ip_configurations': [{
                    'name': naming_infix + 'ipconfig',
                    'subnet': {
                        'id': subnet.id
                    } 
                }]
            }]
        }
    }
}

# Create VMSS test
result_create = compute_client.virtual_machine_scale_sets.create_or_update(
    'my_resource_group',
    'my_scale_set',
    vmss_parameters,
)
vmss_result = result_create.result()
```

## <a name="other-operations-with-managed-disks"></a>Autres opérations avec disques managés

### <a name="resizing-a-managed-disk"></a>Redimensionnement d’un disque managé

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.disk_size_gb = 25
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="update-the-storage-account-type-of-the-managed-disks"></a>Mettre à jour le type de compte de stockage des disques managés

```python
from azure.mgmt.compute.models import StorageAccountTypes

managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.account_type = StorageAccountTypes.standard_lrs
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="create-an-image-from-nlob-storage"></a>Créer une image à partir du Stockage Blob

```python
async_create_image = compute_client.images.create_or_update(
    'my_resource_group',
    'myImage',
    {
        'location': 'westus',
        'storage_profile': {
            'os_disk': {
                'os_type': 'Linux',
                'os_state': "Generalized",
                'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
                'caching': "ReadWrite",
            }
        }
    }
)
image = async_create_image.result()
```

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a>Créer une capture instantanée d’un disque managé actuellement attaché à une machine virtuelle

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
async_snapshot_creation = self.compute_client.snapshots.create_or_update(
        'my_resource_group',
        'mySnapshot',
        {
            'location': 'westus',
            'creation_data': {
                'create_option': 'Copy',
                'source_uri': managed_disk.id
            }
        }
    )
snapshot = async_snapshot_creation.result()
```
