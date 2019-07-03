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
# <a name="azure-cognitive-services-modules-for-python"></a><span data-ttu-id="8bfcd-104">Modules Azure Cognitive Services pour Python</span><span class="sxs-lookup"><span data-stu-id="8bfcd-104">Azure Cognitive Services modules for Python</span></span>

<span data-ttu-id="8bfcd-105">Ajoutez la reconnaissance faciale et d’image, l’analyse linguistique et la recherche à vos applications Python, sites Web et outils à l’aide des modules Azure Cognitive Services pour Python.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-105">Add image and face recognition, language analysis, and search to your Python apps, websites, and tools using the Azure Cognitive Services modules for Python.</span></span>

## <a name="vision-modules"></a><span data-ttu-id="8bfcd-106">Modules de vision</span><span class="sxs-lookup"><span data-stu-id="8bfcd-106">Vision modules</span></span>

### <a name="computer-vision"></a><span data-ttu-id="8bfcd-107">Vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="8bfcd-107">Computer Vision</span></span> 

<span data-ttu-id="8bfcd-108">Retourne des informations sur le contenu visuel d’une image :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-108">Returns information about visual content found in an image:</span></span>

- <span data-ttu-id="8bfcd-109">Utilisez le marquage, les descriptions et les modèles propres au domaine pour identifier le contenu et le marquer en toute confiance.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-109">Use tagging, descriptions, and domain-specific models to identify content and label it with confidence.</span></span>
- <span data-ttu-id="8bfcd-110">Appliquez des paramètres relatifs au contenu osé/pour adulte pour activer la restriction automatique du contenu réservé aux adultes.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-110">Apply adult/racy settings to enable automated restriction of adult content.</span></span>
- <span data-ttu-id="8bfcd-111">Identifiez les types d’image et de jeu de couleurs dans les images.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-111">Identify image types and color schemes in pictures.</span></span>

<span data-ttu-id="8bfcd-112">[Essayez Vision par ordinateur](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) gratuitement dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-112">[Try Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) for free in your browser.</span></span>

<span data-ttu-id="8bfcd-113">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-113">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="8bfcd-114">[Obtenez plus d’informations](/azure/cognitive-services/computer-vision/home) sur l’API Vision par ordinateur et la prise en main avec le [démarrage rapide Python API Vision par ordinateur](/azure/cognitive-services/computer-vision/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-114">[Learn more](/azure/cognitive-services/computer-vision/home) about the Computer Vision API and get started with the [Computer Vision API Python quickstart](/azure/cognitive-services/computer-vision/quickstarts/python).</span></span>

### <a name="content-moderator"></a><span data-ttu-id="8bfcd-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="8bfcd-115">Content Moderator</span></span>

<span data-ttu-id="8bfcd-116">Modération assistée par ordinateur de texte, de vidéo et d’images, à laquelle s’ajoutent des outils de vérification par un opérateur humain.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-116">Machine-assisted moderation of text, video and images, augmented with human review tools.</span></span>

<span data-ttu-id="8bfcd-117">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-117">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-contentmoderator
```

<span data-ttu-id="8bfcd-118">[En savoir plus](/azure/cognitive-services/content-moderator/overview) sur le service Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-118">[Learn more](/azure/cognitive-services/content-moderator/overview) about the Content Moderator service.</span></span>

### <a name="custom-vision-service"></a><span data-ttu-id="8bfcd-119">Service Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="8bfcd-119">Custom Vision Service</span></span>

<span data-ttu-id="8bfcd-120">Téléchargez des images pour effectuer l’apprentissage et personnaliser un modèle de vision par ordinateur pour votre cas d’usage spécifique.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-120">Upload images to train and customize a computer vision model for your specific use case.</span></span> <span data-ttu-id="8bfcd-121">Une fois que l’apprentissage du modèle est effectué, vous pouvez utiliser l’API pour marquer des images à l’aide du modèle et évaluer les résultats pour améliorer votre classifieur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-121">Once the model is trained, you can use the API to tag images using the model and evaluate the results to improve your classifier.</span></span>

<span data-ttu-id="8bfcd-122">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-122">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="8bfcd-123">[En savoir plus](/azure/cognitive-services/Custom-Vision-Service/home) sur le service Vision personnalisée et la prise en main du [tutoriel Python Vision personnalisée](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span><span class="sxs-lookup"><span data-stu-id="8bfcd-123">[Learn more](/azure/cognitive-services/Custom-Vision-Service/home) about the Custom Vision service and get started with the [Custom Vision Python tutorial](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span></span>

### <a name="face-api"></a><span data-ttu-id="8bfcd-124">API Visage</span><span class="sxs-lookup"><span data-stu-id="8bfcd-124">Face API</span></span>

<span data-ttu-id="8bfcd-125">Détectez, identifiez, analysez, organisez et balisez des visages sur des photos.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-125">Detect, identify, analyze, organize, and tag faces in photos.</span></span> 

<span data-ttu-id="8bfcd-126">[Essayez l’API Visage](https://azure.microsoft.com/en-us/services/cognitive-services/face/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-126">[Try the Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in your browser.</span></span>

<span data-ttu-id="8bfcd-127">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-127">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install cognitive-face
```

<span data-ttu-id="8bfcd-128">[En savoir plus](/azure/cognitive-services/face/overview) sur l’API Visage et la prise en main avec le [démarrage rapide Python API Visage](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-128">[Learn more](/azure/cognitive-services/face/overview) about the Face API and get started with the [Face API Python quickstart](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span></span>

## <a name="search-modules"></a><span data-ttu-id="8bfcd-129">Modules de recherche</span><span class="sxs-lookup"><span data-stu-id="8bfcd-129">Search modules</span></span>

### <a name="web-search"></a><span data-ttu-id="8bfcd-130">Recherche Web</span><span class="sxs-lookup"><span data-stu-id="8bfcd-130">Web search</span></span>

<span data-ttu-id="8bfcd-131">Récupérez des documents web indexés par l’API Recherche Web Bing et affinez les résultats par type, date et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-131">Retrieve web documents indexed by the Bing Web Search API and narrow down the results by result type, freshness and more.</span></span> 

<span data-ttu-id="8bfcd-132">[Essayez l’API Recherche Web](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-132">[Try the Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in your browser.</span></span>

<span data-ttu-id="8bfcd-133">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-133">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-websearch
```

<span data-ttu-id="8bfcd-134">[En savoir plus](/azure/cognitive-services/bing-web-search/overview) sur l’API Recherche Web Bing et la prise en main avec le [démarrage rapide Python API Recherche Web Bing](/azure/cognitive-services/bing-web-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-134">[Learn more](/azure/cognitive-services/bing-web-search/overview) about the Bing Web Search API and get started with the [Web Search API Python quickstart](/azure/cognitive-services/bing-web-search/quickstarts/python).</span></span>

### <a name="image-search"></a><span data-ttu-id="8bfcd-135">Recherche d’images</span><span class="sxs-lookup"><span data-stu-id="8bfcd-135">Image search</span></span>

<span data-ttu-id="8bfcd-136">Recherchez des images et obtenez des miniatures, des URL d’images complètes, des métadonnées d’images et bien plus encore dans vos résultats.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-136">Search for images and get thumbnails, full image URLs, image metadata and more in your results.</span></span>

<span data-ttu-id="8bfcd-137">[Essayez l’API Recherche d’images Bing](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-137">[Try the Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in your browser.</span></span>

<span data-ttu-id="8bfcd-138">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-138">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-imagesearch
```

<span data-ttu-id="8bfcd-139">[En savoir plus](/azure/cognitive-services/bing-image-search/overview) sur l’API Recherche d’images Bing et la prise en main avec le [démarrage rapide Python API Recherche d’images Bing](/azure/cognitive-services/bing-image-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-139">[Learn more](/azure/cognitive-services/bing-image-search/overview) about the Bing Image Search API and get started with the [Image Search API Python quickstart](/azure/cognitive-services/bing-image-search/quickstarts/python).</span></span>


### <a name="entity-search"></a><span data-ttu-id="8bfcd-140">Recherche d’entité</span><span class="sxs-lookup"><span data-stu-id="8bfcd-140">Entity search</span></span>

<span data-ttu-id="8bfcd-141">Recherchez l’entité la plus pertinente (lieu, personne ou chose) pour un emplacement ou un terme de recherche donné.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-141">Search for the most relevant entity (place, person, or thing) for a given search term or location.</span></span>

<span data-ttu-id="8bfcd-142">[Essayez l’API Recherche d’entités Bing](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-142">[Try the Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in your browser.</span></span>

<span data-ttu-id="8bfcd-143">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-143">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-entitysearch
```

<span data-ttu-id="8bfcd-144">[En savoir plus](/azure/cognitive-services/bing-entities-search/search-the-web) sur l’API Recherche d’entités Bing et la prise en main avec le [démarrage rapide Python API Recherche d’entités Bing](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-144">[Learn more](/azure/cognitive-services/bing-entities-search/search-the-web) about the Bing Entity Search API and get started with the [Entity Search API Python quickstart](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span></span>

### <a name="custom-search"></a><span data-ttu-id="8bfcd-145">Recherche personnalisée</span><span class="sxs-lookup"><span data-stu-id="8bfcd-145">Custom search</span></span>

<span data-ttu-id="8bfcd-146">Générez une recherche personnalisée sur le web qui répond à votre domaine de recherche spécifique.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-146">Build and a custom web search that meets your specific search domain.</span></span>

<span data-ttu-id="8bfcd-147">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-147">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-customsearch
```

<span data-ttu-id="8bfcd-148">[En savoir plus](/azure/cognitive-services/bing-custom-search/) sur le service Recherche personnalisée Bing et commencer à interroger votre recherche personnalisée à partir de Python avec le [démarrage rapide Python API Recherche personnalisée Bing](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-148">[Learn more](/azure/cognitive-services/bing-custom-search/) about the Bing Custom Search service and get started with querying your custom search from Python with the [Custom Search API Python quickstart](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span></span>

### <a name="video-search"></a><span data-ttu-id="8bfcd-149">Recherche de vidéos</span><span class="sxs-lookup"><span data-stu-id="8bfcd-149">Video search</span></span>

<span data-ttu-id="8bfcd-150">Recherchez des vidéos sur le web et obtenez des résultats comprenant les métadonnées d’auteur, d’encodage, de longueur et de nombre d’affichages.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-150">Find videos across the web and get results with creator, encoding, length, and view count metadata.</span></span>

<span data-ttu-id="8bfcd-151">[Essayez l’API Recherche de vidéos Bing](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-151">[Try the Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in your browser.</span></span>

<span data-ttu-id="8bfcd-152">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-152">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-videosearch
```

<span data-ttu-id="8bfcd-153">[En savoir plus](/azure/cognitive-services/bing-video-search/search-the-web) sur le service Recherche de vidéos et la prise en main avec le [démarrage rapide Python API Recherche de vidéos Bing](/azure/cognitive-services/bing-video-search/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-153">[Learn more](/azure/cognitive-services/bing-video-search/search-the-web) about the Bing Video Search service and get started with the [Video Search API Python quickstart](/azure/cognitive-services/bing-video-search/python).</span></span>


### <a name="news-search"></a><span data-ttu-id="8bfcd-154">Recherche Actualités</span><span class="sxs-lookup"><span data-stu-id="8bfcd-154">News search</span></span>

<span data-ttu-id="8bfcd-155">Recherchez sur le web des articles d’actualité et travaillez avec des métadonnées d’articles, d’informations liées, d’images et d’informations de fournisseur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-155">Search the web for news articles and work with article, related news, images, and provider info metadata.</span></span>

<span data-ttu-id="8bfcd-156">[Essayez l’API Recherche d’actualités Bing](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-156">[Try the News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in your browser.</span></span>

<span data-ttu-id="8bfcd-157">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-157">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-newssearch
```

<span data-ttu-id="8bfcd-158">[En savoir plus](/azure/cognitive-services/bing-news-search/search-the-web) sur le service Recherche d’actualités Bing et la prise en main avec le [démarrage rapide Python API Recherche d’actualités Bing](/azure/cognitive-services/bing-news-search/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-158">[Learn more](/azure/cognitive-services/bing-news-search/search-the-web) about the Bing News Search service and get started with the [News Search API Python quickstart](/azure/cognitive-services/bing-news-search/python).</span></span>


## <a name="language-modules"></a><span data-ttu-id="8bfcd-159">Modules linguistiques</span><span class="sxs-lookup"><span data-stu-id="8bfcd-159">Language modules</span></span>

### <a name="text-analytics"></a><span data-ttu-id="8bfcd-160">Analyse de texte</span><span class="sxs-lookup"><span data-stu-id="8bfcd-160">Text Analytics</span></span> 

<span data-ttu-id="8bfcd-161">L’API Analyse de texte est un service informatique qui fournit un traitement en langage naturel sur le texte brut.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-161">The Text Analytics API is a cloud-based service that provides  natural language processing over raw text.</span></span> <span data-ttu-id="8bfcd-162">L’API comprend trois fonctions principales :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-162">The API includes three main functions:</span></span>

- <span data-ttu-id="8bfcd-163">analyse de sentiments</span><span class="sxs-lookup"><span data-stu-id="8bfcd-163">Sentiment analysis</span></span>
- <span data-ttu-id="8bfcd-164">Extraction d’expressions clés</span><span class="sxs-lookup"><span data-stu-id="8bfcd-164">Key phrase extraction</span></span>
- <span data-ttu-id="8bfcd-165">Détection de la langue</span><span class="sxs-lookup"><span data-stu-id="8bfcd-165">Language detection</span></span>

<span data-ttu-id="8bfcd-166">[Essayez l’API Analyse de texte](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-166">[Try the Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in your browser.</span></span>

<span data-ttu-id="8bfcd-167">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-167">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-language-textanalytics
```

<span data-ttu-id="8bfcd-168">[En savoir plus](/azure/cognitive-services/text-analytics/overview) sur l’API Analyse de texte et la prise en main avec le [démarrage rapide Python API Analyse de texte](/azure/cognitive-services/text-analytics/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-168">[Learn more](/azure/cognitive-services/text-analytics/overview) about the Text Analytics API and get started with the [Text Analytics API Python quickstart](/azure/cognitive-services/text-analytics/quickstarts/python).</span></span>


### <a name="spell-check"></a><span data-ttu-id="8bfcd-169">API Vérification orthographique</span><span class="sxs-lookup"><span data-stu-id="8bfcd-169">Spell Check</span></span>

<span data-ttu-id="8bfcd-170">Utilisez la vérification orthographique et de grammaire contextuelle avec l’API Vérification orthographique Bing.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-170">Perform contextual grammar and spell checking with the Bing Spell Check API.</span></span>

<span data-ttu-id="8bfcd-171">[Essayez l’API Vérification orthographique](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8bfcd-171">[Try the Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in your browser.</span></span>

<span data-ttu-id="8bfcd-172">Obtenez le module Python avec [pip](https://pip.pypa.io/en/stable/quickstart/) :</span><span class="sxs-lookup"><span data-stu-id="8bfcd-172">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-language-spellcheck
```

<span data-ttu-id="8bfcd-173">[En savoir plus](/azure/cognitive-services/bing-spell-check/proof-text) sur l’API Vérification orthographique et la prise en main avec le [démarrage rapide Python API Vérification orthographique](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="8bfcd-173">[Learn more](/azure/cognitive-services/bing-spell-check/proof-text) about the Spell Check API and get started with the [Spell Check API Python quickstart](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span></span>
