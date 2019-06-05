---
title: Installation
description: Installation du kit de développement logiciel (SDK) Azure pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 6014937fb41d6074e94578ccc47c30eb7b3f63d2
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376879"
---
# <a name="installation"></a><span data-ttu-id="b8cb9-104">Installation</span><span class="sxs-lookup"><span data-stu-id="b8cb9-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="b8cb9-105">Quelle solution Python et quelle version utiliser ?</span><span class="sxs-lookup"><span data-stu-id="b8cb9-105">Which Python and which version to use</span></span>

<span data-ttu-id="b8cb9-106">Il existe différents interpréteurs Python, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b8cb9-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="b8cb9-107">CPython : interpréteur Python standard le plus couramment utilisé</span><span class="sxs-lookup"><span data-stu-id="b8cb9-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="b8cb9-108">PyPy : implémentation rapide et conforme autre que CPython</span><span class="sxs-lookup"><span data-stu-id="b8cb9-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="b8cb9-109">IronPython : interpréteur Python qui s'exécute sur .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="b8cb9-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="b8cb9-110">Jython : interpréteur Python qui s’exécute sur la Machine Virtuelle Java</span><span class="sxs-lookup"><span data-stu-id="b8cb9-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="b8cb9-111">**CPython** version 2.7 ou 3.4+ et PyPy 5.4.0 sont testés et pris en charge par le kit de développement logiciel Microsoft Azure SDK pour Python.</span><span class="sxs-lookup"><span data-stu-id="b8cb9-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="b8cb9-112">Où télécharger Python ?</span><span class="sxs-lookup"><span data-stu-id="b8cb9-112">Where to get Python?</span></span>

<span data-ttu-id="b8cb9-113">Il existe plusieurs façons de télécharger CPython :</span><span class="sxs-lookup"><span data-stu-id="b8cb9-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="b8cb9-114">Directement à partir de [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="b8cb9-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="b8cb9-115">À partir d’un distributeur digne de confiance comme [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) ou [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="b8cb9-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="b8cb9-116">Génération à partir de la source !</span><span class="sxs-lookup"><span data-stu-id="b8cb9-116">Build from source!</span></span>

<span data-ttu-id="b8cb9-117">Sauf en cas de nécessité particulière, nous vous recommandons d’opter pour l’une des deux premières options.</span><span class="sxs-lookup"><span data-stu-id="b8cb9-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="b8cb9-118">Installation avec pip</span><span class="sxs-lookup"><span data-stu-id="b8cb9-118">Installation with pip</span></span>

<span data-ttu-id="b8cb9-119">Vous pouvez installer chaque bibliothèque de service Azure individuellement :</span><span class="sxs-lookup"><span data-stu-id="b8cb9-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="b8cb9-120">L’aperçu des packages peut être installé à l’aide de l’indicateur `--pre` :</span><span class="sxs-lookup"><span data-stu-id="b8cb9-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="b8cb9-121">Vous pouvez également installer un ensemble de bibliothèques Azure d’une seule ligne à l’aide du méta-package `azure` .</span><span class="sxs-lookup"><span data-stu-id="b8cb9-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="b8cb9-122">Nous publions une version préliminaire de ce package, auquel vous pouvez accéder à l’aide de l’indicateur --pre :</span><span class="sxs-lookup"><span data-stu-id="b8cb9-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="b8cb9-123">Installer à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="b8cb9-123">Install from GitHub</span></span>

<span data-ttu-id="b8cb9-124">Si vous souhaitez installer `azure` à partir de la source :</span><span class="sxs-lookup"><span data-stu-id="b8cb9-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```
