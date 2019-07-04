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
ms.openlocfilehash: 9fd11cbc7b987b970ceee85c7b11b22e3d6299ea
ms.sourcegitcommit: 31d7df367b15ec09a5a610eb333295bba0f6b351
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67395450"
---
# <a name="installation"></a>Installation

## <a name="which-python-and-which-version-to-use"></a>Quelle solution Python et quelle version utiliser ?

Il existe différents interpréteurs Python, par exemple :

* CPython : interpréteur Python standard le plus couramment utilisé
* PyPy : implémentation rapide et conforme autre que CPython
* IronPython : interpréteur Python qui s'exécute sur .Net/CLR
* Jython : interpréteur Python qui s’exécute sur la Machine Virtuelle Java

**CPython** version 2.7 ou 3.4+ et PyPy 5.4.0 sont testés et pris en charge par le kit de développement logiciel Microsoft Azure SDK pour Python.

## <a name="where-to-get-python"></a>Où télécharger Python ?

Il existe plusieurs façons de télécharger CPython :

* Directement à partir de [Python](https://www.python.org/)
* À partir d’un distributeur digne de confiance comme [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) ou [ActiveState](https://www.activestate.com/)
* Génération à partir de la source !

Sauf en cas de nécessité particulière, nous vous recommandons d’opter pour l’une des deux premières options.

## <a name="installation-with-pip"></a>Installation avec pip

Vous pouvez installer chaque bibliothèque de service Azure individuellement :

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

L’aperçu des packages peut être installé à l’aide de l’indicateur `--pre` :

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

Vous pouvez également installer un ensemble de bibliothèques Azure d’une seule ligne à l’aide du méta-package `azure` .

```bash
pip install azure
```

Nous publions une version préliminaire de ce package, auquel vous pouvez accéder à l’aide de l’indicateur --pre :

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>Installer à partir de GitHub

Si vous souhaitez installer `azure` à partir de la source :

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a>Installer une version antérieure avec pip
Vous pouvez installer une version antérieure de `azure` en spécifiant les détails de version 'azure==3.0.0'.
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a>Vérifier les détails de l’installation du SDK avec pip
Vous pouvez vérifier l’emplacement d’installation, les détails de version du SDK `azure` et plus encore.
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a>Pour désinstaller avec pip
Vous pouvez désinstaller toutes les bibliothèques Azure en une seule ligne avec le méta-package `azure`.
```bash
pip uninstall azure 
```
> [!NOTE]
> `pip uninstall azure` supprime le méta-package `azure` mais laisse les packages `azure-*` individuels derrière (et d’autres comme `adal` et `msrest`). Avec Python et pip, pour tous les packages qui ont des dépendances, la désinstallation du package initial ne désinstalle pas les dépendances. Pour supprimer `azure-` et ses packages associés, exécutez la commande `pip freeze | grep 'azure-' | xargs pip uninstall -y` (puis effectuez des désinstallations individuelles pour adal, msrest et msrestazure).

