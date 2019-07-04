---
title: Bibliothèques Azure Key Vault pour Python
description: Consulter la documentation sur les bibliothèques de client Python pour Azure Key Vault
author: sptramer
manager: carmonm
ms.author: sttramer
ms.date: 06/10/2019
ms.topic: conceptual
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: f4661ee389c13ce8546e7b5cc8866ab7b216d3b0
ms.sourcegitcommit: 92fa5dbcfd9a20f4a49da5f4bdc03045783d3495
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149336"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="65b8c-103">Bibliothèques Azure Key Vault pour Python</span><span class="sxs-lookup"><span data-stu-id="65b8c-103">Azure Key Vault libraries for Python</span></span>

<span data-ttu-id="65b8c-104">[Azure Key Vault](/azure/key-vault/) est le système de stockage et de gestion d’Azure pour les clés de chiffrement, les secrets et la gestion des certificats.</span><span class="sxs-lookup"><span data-stu-id="65b8c-104">[Azure Key Vault](/azure/key-vault/) is Azure's storage and management system for cryptographic keys, secrets, and certificate management.</span></span> <span data-ttu-id="65b8c-105">L’API du SDK Python pour Key Vault est partagée entre les bibliothèques clientes et les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="65b8c-105">The Python SDK API for Key Vault is split between client libraries and management libraries.</span></span>

<span data-ttu-id="65b8c-106">Utilisez la bibliothèque cliente pour :</span><span class="sxs-lookup"><span data-stu-id="65b8c-106">Use the client library to:</span></span>
- <span data-ttu-id="65b8c-107">Accéder, mettre à jour ou supprimer des éléments stockés dans un coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="65b8c-107">Access, update, or delete items stored in an Azure Key Vault</span></span>
- <span data-ttu-id="65b8c-108">Obtenir des métadonnées pour les certificats stockés</span><span class="sxs-lookup"><span data-stu-id="65b8c-108">Get metadata for stored certificates</span></span>
- <span data-ttu-id="65b8c-109">Vérifier les signatures sur les clés symétriques dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="65b8c-109">Verify signatures against symmetric keys in Key Vault</span></span>

<span data-ttu-id="65b8c-110">Utilisez la bibliothèque de gestion pour :</span><span class="sxs-lookup"><span data-stu-id="65b8c-110">Use the management library to:</span></span>
- <span data-ttu-id="65b8c-111">Créer, mettre à jour ou supprimer des magasins Key Vault</span><span class="sxs-lookup"><span data-stu-id="65b8c-111">Create, update, or delete new Key Vault stores</span></span>
- <span data-ttu-id="65b8c-112">Contrôler les stratégies d’accès au coffre</span><span class="sxs-lookup"><span data-stu-id="65b8c-112">Control vault access policies</span></span>
- <span data-ttu-id="65b8c-113">Lister les coffres par abonnement ou groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="65b8c-113">List vaults by subscription or resource group</span></span>
- <span data-ttu-id="65b8c-114">Vérifier la disponibilité des noms de coffre</span><span class="sxs-lookup"><span data-stu-id="65b8c-114">Check for vault name availability</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="65b8c-115">Installer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="65b8c-115">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="65b8c-116">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="65b8c-116">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="65b8c-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="65b8c-117">Examples</span></span>

<span data-ttu-id="65b8c-118">Les exemples suivants utilisent l’authentification de principal de service, méthode de connexion recommandée pour les applications qui se connectent à Azure.</span><span class="sxs-lookup"><span data-stu-id="65b8c-118">The following examples use service principal authentication, which is the recommended sign in method for applications that connect to Azure.</span></span> <span data-ttu-id="65b8c-119">Pour en savoir plus sur l’authentification de principal de service, consultez [S’authentifier avec le SDK Azure pour Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span><span class="sxs-lookup"><span data-stu-id="65b8c-119">To learn about service principal authentication, see [Authenticate with the Azure SDK for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span></span>

<span data-ttu-id="65b8c-120">Récupérez la partie publique d’une clé asymétrique dans un coffre :</span><span class="sxs-lookup"><span data-stu-id="65b8c-120">Retrieve the public portion of an asymmetric key from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# KEY_VERSION is required, and can be obtained with the KeyVaultClient.get_key_versions(self, vault_url, key_name) API
key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
key = key_bundle.key
```

<span data-ttu-id="65b8c-121">Récupérez un secret dans un coffre :</span><span class="sxs-lookup"><span data-stu-id="65b8c-121">Retrieve a secret from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# SECRET_VERSION is required, and can be obtained with the KeyVaultClient.get_secret_versions(self, vault_url, secret_id) API
secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)
secret = secret_bundle.value
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="65b8c-122">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="65b8c-122">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a><span data-ttu-id="65b8c-123">Bibliothèque de gestion</span><span class="sxs-lookup"><span data-stu-id="65b8c-123">Management library</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="65b8c-124">Exemples</span><span class="sxs-lookup"><span data-stu-id="65b8c-124">Example</span></span>

<span data-ttu-id="65b8c-125">L’exemple suivant montre comment créer un coffre Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65b8c-125">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient
from azure.common.credentials import ServicePrincipalCredentials


credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

# Even when using service principal credentials, a subscription ID is required. For service principals,
# this should be the subscription used to create the service principal. Storing a token like a valid
# subscription ID in code is not recommended and only shown here for example purposes.
SUBSCRIPTION_ID = '...'
client = KeyVaultManagementClient(credentials, SUBSCRIPTION_ID)

# The object ID and organization ID (tenant) of the user, application, or service principal for access policies.
# These values can be found through the Azure CLI or the Portal.
ALLOW_OBJECT_ID = '...'
ALLOW_TENANT_ID = '...'

RESOURCE_GROUP = '...'
VAULT_NAME = '...'

# Vault properties may also be created by using the azure.mgmt.keyvault.models.VaultCreateOrUpdateParameters
# class, rather than a map. 
operation = client.vaults.create_or_update(
    RESOURCE_GROUP,
    VAULT_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'object_id': OBJECT_ID,
                'tenant_id': ALLOW_TENANT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()
print(f'New vault URI: {vault.properties.vault_uri}')
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="65b8c-126">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="65b8c-126">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="65b8c-127">Exemples</span><span class="sxs-lookup"><span data-stu-id="65b8c-127">Samples</span></span>
* <span data-ttu-id="65b8c-128">[Gérer les coffres de clés Azure][1]</span><span class="sxs-lookup"><span data-stu-id="65b8c-128">[Manage Azure Key Vaults][1]</span></span> 
* <span data-ttu-id="65b8c-129">[Récupération d’un coffre de clés Azure][2]</span><span class="sxs-lookup"><span data-stu-id="65b8c-129">[Azure Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="65b8c-130">Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) des exemples de coffres Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65b8c-130">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
