---
title: Installation
description: Installation du kit de développement logiciel (SDK) Azure pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 478118642122d7c0c80b1ddf37b13f71d8ca3adc
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534456"
---
# <a name="installation"></a><span data-ttu-id="d8e79-104">Installation</span><span class="sxs-lookup"><span data-stu-id="d8e79-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="d8e79-105">Quelle solution Python et quelle version utiliser ?</span><span class="sxs-lookup"><span data-stu-id="d8e79-105">Which Python and which version to use</span></span>

<span data-ttu-id="d8e79-106">Il existe différents interpréteurs Python, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d8e79-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="d8e79-107">CPython : interpréteur Python standard le plus couramment utilisé</span><span class="sxs-lookup"><span data-stu-id="d8e79-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="d8e79-108">PyPy : implémentation rapide et conforme autre que CPython</span><span class="sxs-lookup"><span data-stu-id="d8e79-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="d8e79-109">IronPython : interpréteur Python qui s'exécute sur .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="d8e79-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="d8e79-110">Jython : interpréteur Python qui s’exécute sur la Machine Virtuelle Java</span><span class="sxs-lookup"><span data-stu-id="d8e79-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="d8e79-111">**CPython** version 2.7 ou 3.4+ et PyPy 5.4.0 sont testés et pris en charge par le kit de développement logiciel Microsoft Azure SDK pour Python.</span><span class="sxs-lookup"><span data-stu-id="d8e79-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="d8e79-112">Où télécharger Python ?</span><span class="sxs-lookup"><span data-stu-id="d8e79-112">Where to get Python?</span></span>

<span data-ttu-id="d8e79-113">Il existe plusieurs façons de télécharger CPython :</span><span class="sxs-lookup"><span data-stu-id="d8e79-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="d8e79-114">Directement à partir de [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="d8e79-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="d8e79-115">À partir d’un distributeur digne de confiance comme [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) ou [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="d8e79-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="d8e79-116">Génération à partir de la source !</span><span class="sxs-lookup"><span data-stu-id="d8e79-116">Build from source!</span></span>

<span data-ttu-id="d8e79-117">Sauf en cas de nécessité particulière, nous vous recommandons d’opter pour l’une des deux premières options.</span><span class="sxs-lookup"><span data-stu-id="d8e79-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="d8e79-118">Installation avec pip</span><span class="sxs-lookup"><span data-stu-id="d8e79-118">Installation with pip</span></span>

<span data-ttu-id="d8e79-119">Vous pouvez installer chaque bibliothèque de service Azure individuellement :</span><span class="sxs-lookup"><span data-stu-id="d8e79-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="d8e79-120">L’aperçu des packages peut être installé à l’aide de l’indicateur `--pre` :</span><span class="sxs-lookup"><span data-stu-id="d8e79-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="d8e79-121">Vous pouvez également installer un ensemble de bibliothèques Azure d’une seule ligne à l’aide du méta-package `azure` .</span><span class="sxs-lookup"><span data-stu-id="d8e79-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="d8e79-122">Nous publions une version préliminaire de ce package, auquel vous pouvez accéder à l’aide de l’indicateur --pre :</span><span class="sxs-lookup"><span data-stu-id="d8e79-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="d8e79-123">Installer à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="d8e79-123">Install from GitHub</span></span>

<span data-ttu-id="d8e79-124">Si vous souhaitez installer `azure` à partir de la source :</span><span class="sxs-lookup"><span data-stu-id="d8e79-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a><span data-ttu-id="d8e79-125">Installer une version antérieure avec pip</span><span class="sxs-lookup"><span data-stu-id="d8e79-125">Install an older version with pip</span></span>
<span data-ttu-id="d8e79-126">Vous pouvez installer une version antérieure de `azure` en spécifiant les détails de version 'azure==3.0.0'.</span><span class="sxs-lookup"><span data-stu-id="d8e79-126">You can install an older version of `azure` by specifying 'azure==3.0.0' version details.</span></span>
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a><span data-ttu-id="d8e79-127">Vérifier les détails de l’installation du SDK avec pip</span><span class="sxs-lookup"><span data-stu-id="d8e79-127">Check SDK installation details with pip</span></span>
<span data-ttu-id="d8e79-128">Vous pouvez vérifier l’emplacement d’installation, les détails de version du SDK `azure` et plus encore.</span><span class="sxs-lookup"><span data-stu-id="d8e79-128">You can check `azure` SDK installation location, version details etc.</span></span>
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a><span data-ttu-id="d8e79-129">Pour désinstaller avec pip</span><span class="sxs-lookup"><span data-stu-id="d8e79-129">To uninstall with pip</span></span>
<span data-ttu-id="d8e79-130">Vous pouvez désinstaller toutes les bibliothèques Azure en une seule ligne avec le méta-package `azure`.</span><span class="sxs-lookup"><span data-stu-id="d8e79-130">You can uninstall all Azure libraries in a single line using the `azure` meta-package.</span></span>
```bash
pip uninstall azure 
```
> [!NOTE]
> <span data-ttu-id="d8e79-131">`pip uninstall azure` supprime le méta-package `azure` mais laisse les packages `azure-*` individuels derrière (et d’autres comme `adal` et `msrest`).</span><span class="sxs-lookup"><span data-stu-id="d8e79-131">`pip uninstall azure`removes the `azure` meta-package but leaves the individual `azure-*` packages behind (and others, like `adal` and `msrest` ).</span></span> <span data-ttu-id="d8e79-132">Avec Python et pip, pour tous les packages qui ont des dépendances, la désinstallation du package initial ne désinstalle pas les dépendances.</span><span class="sxs-lookup"><span data-stu-id="d8e79-132">An aspect of Python and pip is that for all packages that have dependencies, uninstalling the initial package does not uninstall the dependencies.</span></span> <span data-ttu-id="d8e79-133">Pour supprimer `azure-` et ses packages associés, exécutez la commande `pip freeze | grep 'azure-' | xargs pip uninstall -y` (puis effectuez des désinstallations individuelles pour adal, msrest et msrestazure).</span><span class="sxs-lookup"><span data-stu-id="d8e79-133">To remove `azure-` and its supporting packages, run the command `pip freeze | grep 'azure-' | xargs pip uninstall -y` (and then perform individual uninstalls for adal, msrest, and msrestazure).</span></span>

