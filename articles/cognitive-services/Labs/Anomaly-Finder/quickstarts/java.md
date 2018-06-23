---
title: Het gebruik van de Afwijkingsdetectie zoeken-API met behulp van Java - cognitieve Microsoft-Services | Microsoft Docs
description: Get-informatie en codevoorbeelden kunt u snel aan de slag met Java en de Afwijkingsdetectie in cognitieve Services.
services: cognitive-services
author: chliang
manager: bix
ms.service: cognitive-services
ms.technology: anomaly-detection
ms.topic: article
ms.date: 05/01/2018
ms.author: kefre
ms.openlocfilehash: 8152c23e6c5332d243d851be56bab1e4085dbe5a
ms.sourcegitcommit: 95d9a6acf29405a533db943b1688612980374272
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/23/2018
ms.locfileid: "35345062"
---
# <a name="use-the-anomaly-finder-api-with-java"></a>De zoekfunctie Afwijkingsdetectie API gebruiken met Java

In dit artikel bevat informatie en codevoorbeelden kunt u snel aan de slag met behulp van de Afwijkingsdetectie Detection-API met behulp van Java taak van het ophalen van detectieresultaat afwijkingsdetectie voor reeksgegevens tijd uit te voeren.

## <a name="prerequisites"></a>Vereisten

[!INCLUDE [GetSubscriptionKey](../includes/get-subscription-key.md)]

## <a name="getting-anomaly-points-with-the-anomaly-detection-api-using-java"></a>Afwijkingsdetectie punten ophalen met de Afwijkingsdetectie Detection-API met Java

[!INCLUDE [DataContract](../includes/datacontract.md)]

### <a name="example-of-time-series-data"></a>Voorbeeld van een reeksgegevens

In het voorbeeld van de gegevenspunten van reeksen tijd is als volgt.

[!INCLUDE [Request](../includes/request.md)]

### <a name="analyze-data-and-get-anomaly-points-java-example"></a>Gegevens analyseren en afwijkingsdetectie punten Java-voorbeeld

Als u wilt het voorbeeld uitvoert, moet u de volgende stappen uitvoeren:
1. Maak een nieuwe App voor de opdrachtregel.
2. De klasse Main vervangen door de volgende code (behouden `package` instructies).
3. Vervang de `[YOUR_SUBSCRIPTION_KEY]` waarde met de sleutel geldig abonnement.
4. Vervang de `[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]` met het voorbeeld of uw eigen gegevenspunten.
5. Deze algemene bibliotheken downloaden vanuit de opslagplaats met Maven naar de `lib` map in uw project:
   * `org.apache.httpcomponents:httpclient:4.5.2`
6. Voer 'Main'.

```java

import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

public class Main {
    // **********************************************
    // *** Update or verify the following values. ***
    // **********************************************

    // Replace the subscriptionKey string value with your valid subscription key.
    public static final String subscriptionKey = "[YOUR_SUBSCRIPTION_KEY]";

    public static final String uriBase = "https://api.labs.cognitive.microsoft.com/anomalyfinder/v1.0/anomalydetection";

    public static void main(String[] args) {
        final String content = "[REPLACE_WITH_THE_EXAMPLE_OR_YOUR_OWN_DATA_POINTS]";

        CloseableHttpClient client = HttpClients.createDefault();
        HttpPost request = new HttpPost(uriBase);

        // Request headers.
        request.setHeader("Content-Type", "application/json");
        request.setHeader("Ocp-Apim-Subscription-Key", subscriptionKey);

        try {
            StringEntity params = new StringEntity(content);
            request.setEntity(params);

            CloseableHttpResponse response = client.execute(request);
            try {
                HttpEntity respEntity = response.getEntity();
                if (respEntity != null) {
                    System.out.println("----------");
                    System.out.println(response.getStatusLine());
                    System.out.println("Response content is :\n");
                    System.out.println(EntityUtils.toString(respEntity, "utf-8"));
                    System.out.println("----------");
                }
            } catch (Exception respEx) {
                respEx.printStackTrace();
            } finally {
                response.close();
            }

        } catch (Exception ex) {
            System.err.println("Exception on Anomaly Detection: " + ex.getMessage());
            ex.printStackTrace();
        } finally {
            try {
                client.close();
            } catch (Exception e) {
                System.err.println("Exception on closing HttpClient: " + e.getMessage());
                e.printStackTrace();
            }
        }
    }
}

```

### <a name="example-response"></a>Voorbeeld van een antwoord

Een geslaagde reactie wordt geretourneerd als JSON. Voorbeeld van een antwoord is als volgt.
[!INCLUDE [Response](../includes/response.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Java-app](../tutorials/java-tutorial.md)
