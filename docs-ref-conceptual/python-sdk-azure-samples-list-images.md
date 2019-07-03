---
title: Répertorier des images
description: Imprimez toutes les images disponibles à utiliser pour la création d’ordinateurs virtuels.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: routlaw
ms.openlocfilehash: 5473c2f58af997695b8d1a6b1d2cfb6c504b50a5
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534435"
---
# <a name="list-images"></a><span data-ttu-id="8ebc5-103">Répertorier des images</span><span class="sxs-lookup"><span data-stu-id="8ebc5-103">List images</span></span>

<span data-ttu-id="8ebc5-104">Le code suivant permet d’imprimer toutes les images à utiliser pour créer des machines, toutes références (SKU) et versions disponibles comprises.</span><span class="sxs-lookup"><span data-stu-id="8ebc5-104">Use the following code to print all of the available images to use for creating virtual machines, including all skus and versions.</span></span>

```python
region = 'eastus'

result_list_pub = compute_client.virtual_machine_images.list_publishers(
    region,
)

for publisher in result_list_pub:
    result_list_offers = compute_client.virtual_machine_images.list_offers(
        region,
        publisher.name,
    )

    for offer in result_list_offers:
        result_list_skus = compute_client.virtual_machine_images.list_skus(
            region,
            publisher.name,
            offer.name,
        )

        for sku in result_list_skus:
            result_list = compute_client.virtual_machine_images.list(
                region,
                publisher.name,
                offer.name,
                sku.name,
            )

            for version in result_list:
                result_get = compute_client.virtual_machine_images.get(
                    region,
                    publisher.name,
                    offer.name,
                    sku.name,
                    version.name,
                )

                print('PUBLISHER: {0}, OFFER: {1}, SKU: {2}, VERSION: {3}'.format(
                    publisher.name,
                    offer.name,
                    sku.name,
                    version.name,
                ))
```
