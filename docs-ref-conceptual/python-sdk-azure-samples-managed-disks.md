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
ms.author: liwong
ms.openlocfilehash: 733bd0ffce6ddb10219dae40bad6ea54e1efcd70
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33839404"
---
# <a name="managed-disks"></a><span data-ttu-id="3ee5a-103">Disques managés</span><span class="sxs-lookup"><span data-stu-id="3ee5a-103">Managed Disks</span></span>

<span data-ttu-id="3ee5a-104">Azure Disques managés et 1 000 machines virtuelles dans un groupe identique sont [généralement disponibles](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/). Les disques managés Azure offrent une gestion de disque simplifiée, améliorent l’extensibilité et la sécurité.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-104">Azure Managed Disks and 1000 VMs in a Scale Set are now [generally available](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/) Azure Managed Disks provide a simplified disk Management, enhanced Scalability, better Security and Scale.</span></span> <span data-ttu-id="3ee5a-105">Managed Disks fait disparaître la notion de compte de stockage pour disques, permettant ainsi aux clients de mettre à l’échelle sans avoir à se soucier des limites associées aux comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-105">It takes away the notion of storage account for disks, enabling customers to scale without worrying about the limitations associated with storage accounts.</span></span> <span data-ttu-id="3ee5a-106">Cet article fournit une introduction rapide et des références sur l’utilisation du service avec Python.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-106">This post provides a quick introduction and reference on consuming the service from Python.</span></span>



<span data-ttu-id="3ee5a-107">Du point de vue du développeur, l’expérience de la fonctionnalité Disques managés dans Azure CLI est idiomatique à l’expérience CLI rencontrée dans d’autres outils multiplateformes.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-107">From a developer perspective, the Managed Disks experience in Azure CLI is idomatic to the CLI experience in other cross-platform tools.</span></span> <span data-ttu-id="3ee5a-108">Vous pouvez utiliser le Kit de développement logiciel (SDK) [Azure Python](https://azure.microsoft.com/develop/python/) et le [package azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) pour administrer la fonctionnalité Disques managés.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-108">You can use the [Azure Python](https://azure.microsoft.com/develop/python/) SDK and the [azure-mgmt-compute package 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) to administer Managed Disks.</span></span> <span data-ttu-id="3ee5a-109">Vous pouvez créer un client de calcul à l’aide de ce [didacticiel](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="3ee5a-109">You can create a compute client using this [tutorial](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).</span></span>


## <a name="standalone-managed-disks"></a><span data-ttu-id="3ee5a-110">Disques managés autonomes</span><span class="sxs-lookup"><span data-stu-id="3ee5a-110">Standalone Managed Disks</span></span>

<span data-ttu-id="3ee5a-111">Vous pouvez facilement créer des disques managés autonomes de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-111">You can easily create standalone Managed Disks in a variety of ways.</span></span>

### <a name="create-an-empty-managed-disk"></a><span data-ttu-id="3ee5a-112">Créez un disque géré vide.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-112">Create an empty Managed Disk.</span></span>
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

### <a name="create-a-managed-disk-from-blob-storage"></a><span data-ttu-id="3ee5a-113">Créez un disque géré à partir du Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-113">Create a Managed Disk from Blob Storage.</span></span>
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

### <a name="create-a-managed-disk-from-your-own-image"></a><span data-ttu-id="3ee5a-114">Créer un disque géré à partir de votre propre image</span><span class="sxs-lookup"><span data-stu-id="3ee5a-114">Create a Managed Disk from your own Image</span></span>
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

## <a name="virtual-machine-with-managed-disks"></a><span data-ttu-id="3ee5a-115">Machines virtuelles avec la fonctionnalité Disques managés</span><span class="sxs-lookup"><span data-stu-id="3ee5a-115">Virtual Machine with Managed Disks</span></span>

<span data-ttu-id="3ee5a-116">Vous pouvez créer une machine virtuelle avec disque géré implicite pour une image de disque spécifique.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-116">You can create a Virtual Machine with an implicit Managed Disk for a specific disk image.</span></span> <span data-ttu-id="3ee5a-117">La création est simplifiée avec la création implicite de disques managés, car il n’y a pas besoin de fournir toutes les informations du disque.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-117">Creation is simplified with implicit creation of managed disks without specifying all the disk details.</span></span> <span data-ttu-id="3ee5a-118">Vous n’avez pas à vous soucier de la création et de la gestion des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-118">You do not have to worry about creating and managing Storage Accounts.</span></span>

<span data-ttu-id="3ee5a-119">Un disque géré est créé implicitement lors de la création d’une machine virtuelle à partir d’une image du système d’exploitation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-119">A Managed Disk is created implicitly when creating VM from an OS image in Azure.</span></span> <span data-ttu-id="3ee5a-120">Dans le paramètre ``storage_profile``, ``os_disk`` est maintenant facultatif. Vous n’avez pas besoin de créer un compte de stockage pour créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-120">In the ``storage_profile`` parameter, ``os_disk`` is now optional and you don't have to create a storage account as required precondition to create a Virtual Machine.</span></span>

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
<span data-ttu-id="3ee5a-121">Le paramètre ``storage_profile`` est maintenant valide.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-121">This ``storage_profile`` parameter is now valid.</span></span> <span data-ttu-id="3ee5a-122">Pour avoir un exemple complet de la procédure à suivre pour créer une machine virtuelle dans Python (réseau y compris), consultez l’ensemble du [didacticiel sur les machines virtuelles dans Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span><span class="sxs-lookup"><span data-stu-id="3ee5a-122">To get a complete example on how to create a VM in Python (including network, etc), check the full [VM tutorial in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span></span>

<span data-ttu-id="3ee5a-123">Vous pouvez facilement attacher un disque géré déjà mis en service.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-123">You can easily attach a previously provisioned Managed Disk.</span></span>
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

## <a name="virtual-machine-scale-sets-with-managed-disks"></a><span data-ttu-id="3ee5a-124">Groupes de machines virtuelles identiques avec la fonctionnalité Disques managés</span><span class="sxs-lookup"><span data-stu-id="3ee5a-124">Virtual Machine Scale Sets with Managed Disks</span></span>

<span data-ttu-id="3ee5a-125">Avant la fonctionnalité Disques managés, il fallait créer un compte de stockage manuellement pour chaque machine virtuelle que vous vouliez placer dans votre groupe identique. Il fallait ensuite utiliser le paramètre de liste ``vhd_containers`` afin de fournir tous les noms de comptes de stockage à l’API REST du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-125">Before Managed Disks, you needed to create a storage account manually for all the VMs you wanted inside your Scale Set, and then use the list parameter ``vhd_containers`` to provide all the storage account name to the Scale Set RestAPI.</span></span> <span data-ttu-id="3ee5a-126">Le guide de transition officiel est disponible dans cet article `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-126">The official transition guide is available in this article `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span></span>

<span data-ttu-id="3ee5a-127">Dorénavant, avec Managed Disks, vous n’avez plus à gérer aucun compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-127">Now with Managed Disk, you don't have to manage any storage account at all.</span></span> <span data-ttu-id="3ee5a-128">Si vous êtes habitué au Kit de développement Python VMSS, vous pouvez maintenant utiliser le même ``storage_profile`` que celui utilisé lors de la création d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="3ee5a-128">If you're are used to the VMSS Python SDK, your ``storage_profile`` can now be exactly the same as the one used in VM creation:</span></span>

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

<span data-ttu-id="3ee5a-129">Voici l’exemple complet :</span><span class="sxs-lookup"><span data-stu-id="3ee5a-129">The full sample being:</span></span>

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

## <a name="other-operations-with-managed-disks"></a><span data-ttu-id="3ee5a-130">Autres opérations avec la fonctionnalité Disques managés</span><span class="sxs-lookup"><span data-stu-id="3ee5a-130">Other Operations with Managed Disks</span></span>

### <a name="resizing-a-managed-disk"></a><span data-ttu-id="3ee5a-131">Redimensionnement d’un disque géré.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-131">Resizing a managed disk.</span></span>

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

### <a name="update-the-storage-account-type-of-the-managed-disks"></a><span data-ttu-id="3ee5a-132">Mettez à jour le type de compte de stockage de la fonctionnalité Disques managés.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-132">Update the Storage Account type of the Managed Disks.</span></span>
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

### <a name="create-an-image-from-blob-storage"></a><span data-ttu-id="3ee5a-133">Créez une image à partir d’un Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-133">Create an image from Blob Storage.</span></span>
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

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a><span data-ttu-id="3ee5a-134">Créez un instantané d’un disque géré actuellement attaché à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ee5a-134">Create a snapshot of a Managed Disk that is currently attached to a Virtual Machine.</span></span>
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
