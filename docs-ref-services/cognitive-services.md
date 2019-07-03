---
title: Modules Azure Cognitive Services pour Python
description: Références pour les modules Azure Cognitive Services pour Python
keywords: Azure, Python, Kit de développement logiciel (SDK), API, Cognitive Services
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/04/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5a23a52414e70facd6feae3af3956a5131f6b5c4
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534342"
---
# <a name="azure-cognitive-services-modules-for-python"></a>Modules Azure Cognitive Services pour Python

Ajoutez la reconnaissance faciale et d’image, l’analyse linguistique et la recherche à vos applications Python, sites Web et outils à l’aide des modules Azure Cognitive Services pour Python.

## <a name="vision-modules"></a>Modules de vision

### <a name="computer-vision"></a>Vision par ordinateur 

Retourne des informations sur le contenu visuel d’une image :

- Utilisez le marquage, les descriptions et les modèles propres au domaine pour identifier le contenu et le marquer en toute confiance.
- Appliquez des paramètres relatifs au contenu osé/pour adulte pour activer la restriction automatique du contenu réservé aux adultes.
- Identifiez les types d’image et de jeu de couleurs dans les images.

[Essayez Vision par ordinateur](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) gratuitement dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-vision-computervision
```

[Obtenez plus d’informations](/azure/cognitive-services/computer-vision/home) sur l’API Vision par ordinateur et la prise en main avec le [démarrage rapide Python API Vision par ordinateur](/azure/cognitive-services/computer-vision/quickstarts/python).

### <a name="content-moderator"></a>Content Moderator

Modération assistée par ordinateur de texte, de vidéo et d’images, à laquelle s’ajoutent des outils de vérification par un opérateur humain.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-vision-contentmoderator
```

[En savoir plus](/azure/cognitive-services/content-moderator/overview) sur le service Content Moderator.

### <a name="custom-vision-service"></a>Service Vision personnalisée

Téléchargez des images pour effectuer l’apprentissage et personnaliser un modèle de vision par ordinateur pour votre cas d’usage spécifique. Une fois que l’apprentissage du modèle est effectué, vous pouvez utiliser l’API pour marquer des images à l’aide du modèle et évaluer les résultats pour améliorer votre classifieur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-vision-customvision
```

[En savoir plus](/azure/cognitive-services/Custom-Vision-Service/home) sur le service Vision personnalisée et la prise en main du [tutoriel Python Vision personnalisée](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)

### <a name="face-api"></a>API Visage

Détectez, identifiez, analysez, organisez et balisez des visages sur des photos. 

[Essayez l’API Visage](https://azure.microsoft.com/en-us/services/cognitive-services/face/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install cognitive-face
```

[En savoir plus](/azure/cognitive-services/face/overview) sur l’API Visage et la prise en main avec le [démarrage rapide Python API Visage](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).

## <a name="search-modules"></a>Modules de recherche

### <a name="web-search"></a>Recherche Web

Récupérez des documents web indexés par l’API Recherche Web Bing et affinez les résultats par type, date et bien plus encore. 

[Essayez l’API Recherche Web](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-search-websearch
```

[En savoir plus](/azure/cognitive-services/bing-web-search/overview) sur l’API Recherche Web Bing et la prise en main avec le [démarrage rapide Python API Recherche Web Bing](/azure/cognitive-services/bing-web-search/quickstarts/python).

### <a name="image-search"></a>Recherche d’images

Recherchez des images et obtenez des miniatures, des URL d’images complètes, des métadonnées d’images et bien plus encore dans vos résultats.

[Essayez l’API Recherche d’images Bing](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-search-imagesearch
```

[En savoir plus](/azure/cognitive-services/bing-image-search/overview) sur l’API Recherche d’images Bing et la prise en main avec le [démarrage rapide Python API Recherche d’images Bing](/azure/cognitive-services/bing-image-search/quickstarts/python).


### <a name="entity-search"></a>Recherche d’entité

Recherchez l’entité la plus pertinente (lieu, personne ou chose) pour un emplacement ou un terme de recherche donné.

[Essayez l’API Recherche d’entités Bing](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-search-entitysearch
```

[En savoir plus](/azure/cognitive-services/bing-entities-search/search-the-web) sur l’API Recherche d’entités Bing et la prise en main avec le [démarrage rapide Python API Recherche d’entités Bing](/azure/cognitive-services/bing-entities-search/quickstarts/python).

### <a name="custom-search"></a>Recherche personnalisée

Générez une recherche personnalisée sur le web qui répond à votre domaine de recherche spécifique.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-search-customsearch
```

[En savoir plus](/azure/cognitive-services/bing-custom-search/) sur le service Recherche personnalisée Bing et commencer à interroger votre recherche personnalisée à partir de Python avec le [démarrage rapide Python API Recherche personnalisée Bing](/azure/cognitive-services/bing-custom-search/call-endpoint-python).

### <a name="video-search"></a>Recherche de vidéos

Recherchez des vidéos sur le web et obtenez des résultats comprenant les métadonnées d’auteur, d’encodage, de longueur et de nombre d’affichages.

[Essayez l’API Recherche de vidéos Bing](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-search-videosearch
```

[En savoir plus](/azure/cognitive-services/bing-video-search/search-the-web) sur le service Recherche de vidéos et la prise en main avec le [démarrage rapide Python API Recherche de vidéos Bing](/azure/cognitive-services/bing-video-search/python).


### <a name="news-search"></a>Recherche Actualités

Recherchez sur le web des articles d’actualité et travaillez avec des métadonnées d’articles, d’informations liées, d’images et d’informations de fournisseur.

[Essayez l’API Recherche d’actualités Bing](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-search-newssearch
```

[En savoir plus](/azure/cognitive-services/bing-news-search/search-the-web) sur le service Recherche d’actualités Bing et la prise en main avec le [démarrage rapide Python API Recherche d’actualités Bing](/azure/cognitive-services/bing-news-search/python).


## <a name="language-modules"></a>Modules linguistiques

### <a name="text-analytics"></a>Analyse de texte 

L’API Analyse de texte est un service informatique qui fournit un traitement en langage naturel sur le texte brut. L’API comprend trois fonctions principales :

- analyse de sentiments
- Extraction d’expressions clés
- Détection de la langue

[Essayez l’API Analyse de texte](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-language-textanalytics
```

[En savoir plus](/azure/cognitive-services/text-analytics/overview) sur l’API Analyse de texte et la prise en main avec le [démarrage rapide Python API Analyse de texte](/azure/cognitive-services/text-analytics/quickstarts/python).


### <a name="spell-check"></a>API Vérification orthographique

Utilisez la vérification orthographique et de grammaire contextuelle avec l’API Vérification orthographique Bing.

[Essayez l’API Vérification orthographique](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) dans votre navigateur.

Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :

```python
pip install azure-cognitiveservices-language-spellcheck
```

[En savoir plus](/azure/cognitive-services/bing-spell-check/proof-text) sur l’API Vérification orthographique et la prise en main avec le [démarrage rapide Python API Vérification orthographique](/azure/cognitive-services/bing-spell-check/quickstarts/python).
