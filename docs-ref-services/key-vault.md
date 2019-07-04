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
# <a name="azure-key-vault-libraries-for-python"></a>Bibliothèques Azure Key Vault pour Python

[Azure Key Vault](/azure/key-vault/) est le système de stockage et de gestion d’Azure pour les clés de chiffrement, les secrets et la gestion des certificats. L’API du SDK Python pour Key Vault est partagée entre les bibliothèques clientes et les bibliothèques de gestion.

Utilisez la bibliothèque cliente pour :
- Accéder, mettre à jour ou supprimer des éléments stockés dans un coffre de clés Azure
- Obtenir des métadonnées pour les certificats stockés
- Vérifier les signatures sur les clés symétriques dans Key Vault

Utilisez la bibliothèque de gestion pour :
- Créer, mettre à jour ou supprimer des magasins Key Vault
- Contrôler les stratégies d’accès au coffre
- Lister les coffres par abonnement ou groupe de ressources
- Vérifier la disponibilité des noms de coffre

## <a name="install-the-libraries"></a>Installer les bibliothèques

### <a name="client-library"></a>Bibliothèque cliente

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Exemples

Les exemples suivants utilisent l’authentification de principal de service, méthode de connexion recommandée pour les applications qui se connectent à Azure. Pour en savoir plus sur l’authentification de principal de service, consultez [S’authentifier avec le SDK Azure pour Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)

Récupérez la partie publique d’une clé asymétrique dans un coffre :

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

Récupérez un secret dans un coffre :

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
> [Explorer les API clientes](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a>Bibliothèque de gestion

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Exemples

L’exemple suivant montre comment créer un coffre Azure Key Vault. 

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
> [Explorer les API de gestion](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Exemples
* [Gérer les coffres de clés Azure][1] 
* [Récupération d’un coffre de clés Azure][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) des exemples de coffres Azure Key Vault. 
