---
title: Bibliothèques RBAC Graph pour Python
description: Référence sur les bibliothèques RBAC Graph pour Python
keywords: Azure, Python, SDK, API, RBAC Graph
author: rloutlaw
ms.author: routlaw
manager: jfriend
ms.date: 05/10/2019
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: e9b0aba7998565284ae18e0036da96d033b2b05f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534276"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a>Bibliothèques Azure Active Directory Graph pour Python

> [!IMPORTANT]
>
> Depuis février 2019, nous avons lancé le processus ayant pour but de déprécier certaines versions antérieures de l’API Azure Active Directory Graph au profit de l’API Microsoft Graph. 
>
> Pour plus de détails, de mises à jour et de délais, consultez la page [Microsoft Graph ou Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) dans le centre de développement Office.
>
> Pour l’avenir, les applications doivent utiliser l’API Microsoft Graph. 

## <a name="overview"></a>Vue d'ensemble 

Authentifiez des utilisateurs et contrôlez l’accès aux applications et aux API avec [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api).    

## <a name="client-library"></a>Bibliothèque cliente   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a>Exemples 
> [!NOTE]   
> Vous devez remplacer le paramètre de ressource par https://graph.windows.net lors de la création de l’instance d’informations d’identification    
 ```python  
from azure.graphrbac import GraphRbacManagementClient   
from azure.common.credentials import UserPassCredentials    
 credentials = UserPassCredentials( 
            'user@domain.com',      # Your user 
            'my_password',          # Your password 
            resource="https://graph.windows.net"    
    )   
 tenant_id = "myad.onmicrosoft.com" 
 graphrbac_client = GraphRbacManagementClient(  
    credentials,    
    tenant_id   
)   
``` 
Le code suivant crée un utilisateur. Récupérez-le en filtrant la liste et supprimez-le.   
```python   
from azure.graphrbac.models import UserCreateParameters, PasswordProfile    
 user = graphrbac_client.users.create(  
    UserCreateParameters(   
        user_principal_name="testbuddy@{}".format(MY_AD_DOMAIN),    
        account_enabled=False,  
        display_name='Test Buddy',  
        mail_nickname='testbuddy',  
        password_profile=PasswordProfile(   
            password='MyStr0ngP4ssword',    
            force_change_password_next_login=True   
        )   
    )   
)   
# user is a User instance   
self.assertEqual(user.display_name, 'Test Buddy')   
 user = graphrbac_client.users.get(user.object_id)  
self.assertEqual(user.display_name, 'Test Buddy')   
 for user in graphrbac_client.users.list(filter="displayName eq 'Test Buddy'"): 
    self.assertEqual(user.display_name, 'Test Buddy')   
 graphrbac_client.users.delete(user.object_id)  
```