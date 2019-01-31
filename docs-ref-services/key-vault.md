---
title: Bibliothèques Azure Key Vault pour Python
description: Consulter la documentation sur les bibliothèques de client Python pour Azure Key Vault
author: lisawong19
keywords: Azure, Python, Kit de développement logiciel (SDK), API, clés, Key Vault, authentification, secret, clé, sécurité
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: e9ad2630a9004edfb3521f818307c134aa885315
ms.sourcegitcommit: fc9f0188879abc4afab8cc7d8aae8b2899133529
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55065068"
---
# <a name="azure-key-vault-libraries-for-python"></a>Bibliothèques Azure Key Vault pour Python

## <a name="overview"></a>Vue d’ensemble

Créez, mettez à jour et supprimez des clés et des secrets dans Azure Key Vault avec les bibliothèques clientes.

Utilisez les bibliothèques de gestion Azure Key Vault pour créer des coffres de clé, autoriser des applications et gérer les autorisations. 

En savoir plus sur [Azure Key Vault](/azure/key-vault/key-vault-whatis).

## <a name="install-the-libraries"></a>Installer les bibliothèques

### <a name="client-library"></a>Bibliothèque cliente

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Exemples

Récupérez une [clé web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) à partir de Key Vault.

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
json_key = key_bundle.key
```

De même, vous pouvez utiliser l’extrait de code suivant pour récupérer un secret à partir du coffre :

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)

print(secret_bundle.value)
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a>API de gestion

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Exemples
L’exemple suivant montre comment créer un coffre Azure Key Vault. 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'
TENANT_ID = os.environ['AZURE_TENANT_ID']

kv_client = KeyVaultManagementClient(credentials, subscription_id)

operation = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'tenant_id': TENANT_ID,
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()

VAULT_URI = vault.properties.vault_uri
```
> [!div class="nextstepaction"]
> [Explorer les API clientes](/python/api/overview/azure/keyvault/client)

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Exemples
* [Gérer les coffres de clés][1] 
* [Récupération d’un coffre Key Vault][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) des exemples de coffres Azure Key Vault. 
