---
title: 'Snelstartgids: Zoeken naar afbeeldingen met de Bing Image Search SDK voor Node.js'
description: Gebruik deze snelstartgids om voor de eerste keer afbeeldingen te zoeken met behulp van de Bing Image Search SDK, wat een wrapper is voor de API en die dus dezelfde functies bevat. Deze eenvoudige Node.js-toepassing verzendt een zoekquery voor afbeeldingen, parseert het JSON-antwoord en geeft de URL weer van de eerst geretourneerde afbeelding.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: aahill
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: aahi
ms.openlocfilehash: a1fda703c74549c351d8eb609819198d7e2856cf
ms.sourcegitcommit: a08d1236f737915817815da299984461cc2ab07e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/26/2018
ms.locfileid: "52311273"
---
# <a name="quickstart-search-for-images-with-the-bing-image-search-sdk-and-nodejs"></a>Snelstartgids: Zoeken naar afbeeldingen met de Bing Image Search SDK en Node.js

Gebruik deze snelstartgids om voor de eerste keer afbeeldingen te zoeken met behulp van de Bing Image Search SDK, wat een wrapper is voor de API en die dus dezelfde functies bevat. Deze eenvoudige JavaScript-toepassing verzendt een zoekquery voor afbeeldingen, parseert het JSON-antwoord en geeft de URL weer van de eerst geretourneerde afbeelding.

De broncode voor dit voorbeeld is beschikbaar op [GitHub](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/imageSearch.js) met extra foutafhandeling en aantekeningen.

## <a name="prerequisites"></a>Vereisten
Haal een [Cognitive Services-toegangssleutel](https://azure.microsoft.com/try/cognitive-services/) op onder **Zoeken**.  Zie ook [Prijsinformatie Cognitive Services - Bing Zoeken-API](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/).  Zie ook [Prijsinformatie Cognitive Services - Bing Zoeken-API](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/).

* De [Cognitive Services Image Search SDK voor Node.js](https://www.npmjs.com/package/azure-cognitiveservices-imagesearch)
    * Installeren met behulp van `npm install azure-cognitiveservices-imagesearch`
* De [Node.js Azure Rest](https://www.npmjs.com/package/ms-rest-azure)-module
    * Installeren met behulp van `npm install ms-rest-azure`

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="create-and-initialize-the-application"></a>De toepassing maken en initialiseren

1. Maak een nieuw JavaScript-bestand in uw favoriete IDE of editor, en stel de striktheid, https en andere vereisten in.

    ```javascript
    'use strict';
    const Search = require('azure-cognitiveservices-imagesearch');
    const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
    ```

2. Maak in de Main-methode van uw project variabelen voor uw geldige abonnementssleutel, de afbeeldingsresultaten die moeten worden geretourneerd door Bing en een zoekterm. Maak vervolgens met behulp van de sleutel een instantie van de client voor het zoeken van afbeeldingen.

    ```javascript
    //replace this value with your valid subscription key.
    let serviceKey = "ENTER YOUR KEY HERE";

    //the search term for the request
    let searchTerm = "canadian rockies";

    //instantiate the image search client 
    let credentials = new CognitiveServicesCredentials(serviceKey);
    let imageSearchApiClient = new Search.ImageSearchAPIClient(credentials);

    ```

## <a name="create-an-asynchronous-helper-function"></a>Een asynchrone helperfunctie maken

1. Maak een functie om de client asynchroon aan te roepen en het antwoord van de service Bing Afbeeldingen zoeken te retourneren.  
    ```javascript
    //a helper function to perform an async call to the Bing Image Search API
    const sendQuery = async () => {
        return await imageSearchApiClient.imagesOperations.search(searchTerm);
    };
    ```
## <a name="send-a-query-and-handle-the-response"></a>Een query verzenden en het antwoord verwerken

1. Roep de helperfunctie aan en verwerk de `promise` om de afbeeldingsresultaten te parseren die in het antwoord zijn geretourneerd.

    Als het antwoord zoekresultaten bevat, wordt het eerste resultaat opgeslagen en worden de bijbehorende gegevens weergegeven, zoals een miniatuur-URL en de oorspronkelijke URL, samen met het totale aantal geretourneerde afbeeldingen.  
    ```javascript
    sendQuery().then(imageResults => {
        if (imageResults == null) {
        console.log("No image results were found.");
        }
        else {
            console.log(`Total number of images returned: ${imageResults.value.length}`);
            let firstImageResult = imageResults.value[0];
            //display the details for the first image result. After running the application,
            //you can copy the resulting URLs from the console into your browser to view the image.
            console.log(`Total number of images found: ${imageResults.value.length}`);
            console.log(`Copy these URLs to view the first image returned:`);
            console.log(`First image thumbnail url: ${firstImageResult.thumbnailUrl}`);
            console.log(`First image content url: ${firstImageResult.contentUrl}`);
        }
      })
      .catch(err => console.error(err))
    ```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Zelfstudie voor app met één pagina voor Bing Image Search](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/tutorial-bing-image-search-single-page-app)

## <a name="see-also"></a>Zie ook

* [Wat is Bing Image Search?](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/overview)  
* [Online interactieve demo proberen](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
* [Gratis Cognitive Services-toegangssleutel ophalen](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)
* [Node.js-voorbeelden voor de Azure Cognitive Services SDK](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)
* [Documentatie van Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services)
* [Naslag voor Bing Afbeeldingen zoeken-API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
