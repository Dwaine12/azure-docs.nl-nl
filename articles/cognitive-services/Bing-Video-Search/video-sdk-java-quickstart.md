---
title: Quick Start Bing Video zoeken SDK Java | Microsoft Docs
description: Informatie over het instellen van de consoletoepassing Bing Video Search SDK.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 02/18/2018
ms.author: v-gedod
ms.openlocfilehash: 1d9ccd88de4b91060861c39ab20f6a203c820384
ms.sourcegitcommit: 95d9a6acf29405a533db943b1688612980374272
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/23/2018
ms.locfileid: "35345706"
---
# <a name="bing-video-search-sdk-java-quickstart"></a>Bing Video zoeken SDK Java Quick Start

De Bing Video Search SDK biedt de functionaliteit van de REST-API voor video's en parseren resultaten.

De [broncode voor voorbeelden van Java Bing Video Search SDK](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingVideoSearch) beschikbaar is op de Git-Hub.

## <a name="application-dependencies"></a>Afhankelijkheden voor toepassingen
Ophalen van een [cognitieve toegangssleutel](https://azure.microsoft.com/try/cognitive-services/) onder **Search**. De Bing Video Search SDK-afhankelijkheden installeren met behulp van Maven, Gradle of een ander beheersysteem van afhankelijkheid. Het bestand Maven POM is vereist voor de declaratie:
```
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.cognitiveservices</groupId>
      <artifactId>azure-cognitiveservices-videosearch</artifactId>
      <version>0.0.1-beta-SNAPSHOT</version>
    </dependency>
  </dependencies> 
```
## <a name="video-search-client"></a>Video zoeken client
Invoer toevoegen aan de implementatie van de klasse.
```
import com.microsoft.azure.cognitiveservices.videosearch.*;
import com.microsoft.azure.cognitiveservices.videosearch.Freshness;
import com.microsoft.azure.cognitiveservices.videosearch.VideoObject;
import com.microsoft.azure.cognitiveservices.videosearch.implementation.TrendingVideosInner;
import com.microsoft.azure.cognitiveservices.videosearch.implementation.VideoDetailsInner;
import com.microsoft.azure.cognitiveservices.videosearch.implementation.VideoSearchAPIImpl;
import com.microsoft.azure.cognitiveservices.videosearch.implementation.VideosInner;
import com.microsoft.rest.credentials.ServiceClientCredentials;
import okhttp3.Interceptor;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

```
Implementeer de **VideoSearchAPIImpl** -client, die een exemplaar van vereist de **ServiceClientCredentials** klasse.
```
public static VideoSearchAPIImpl getClient(final String subscriptionKey) {
    return new VideoSearchAPIImpl("https://api.cognitive.microsoft.com/bing/v7.0/",
            new ServiceClientCredentials() {
                @Override
                public void applyCredentialsFilter(OkHttpClient.Builder builder) {
                    builder.addNetworkInterceptor(
                            new Interceptor() {
                                @Override
                                public Response intercept(Chain chain) throws IOException {
                                    Request request = null;
                                    Request original = chain.request();
                                    // Request customization: add request headers
                                    Request.Builder requestBuilder = original.newBuilder()
                                            .addHeader("Ocp-Apim-Subscription-Key", subscriptionKey);
                                    request = requestBuilder.build();
                                    return chain.proceed(request);
                                }
                            });
                }
            });
}
```
Zoeken naar video's over 'SwiftKey'. Controleer of het aantal resultaten. De ID, de naam en de URL voor de eerste video resultaat afdrukken.
```
public static void VideoSearch(String subscriptionKey)
{
    VideoSearchAPIImpl client = VideoSDK.getClient(subscriptionKey);

    try
    {
        VideosInner videoResults = client.searchs().list("SwiftKey");
        System.out.println("\r\nSearch videos for query \"SwiftKey\"");

        if (videoResults == null)
        {
            System.out.println("Didn't see any video result data..");
        }
        else
        {
            if (videoResults.value().size() > 0)
            {
                VideoObject firstVideoResult = videoResults.value().get(0);

                System.out.println(String.format("Video result count: %d", videoResults.value().size()));
                System.out.println(String.format("First video id: %s", firstVideoResult.videoId()));
                System.out.println(String.format("First video name: %s", firstVideoResult.name()));
                System.out.println(String.format("First video url: %s", firstVideoResult.contentUrl()));
            }
            else
            {
                System.out.println("Couldn't find video results!");
            }
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }

}


```
Zoeken naar video's over "Bellevue aanhangwagen." Filteren van de zoekopdracht met de *gratis*, *korte*, en *1080p resolutie* parameters. Controleer of het aantal resultaten. De ID, de naam en de URL voor de eerste video resultaat afdrukken.
```
public static void VideoSearchWithFilters(String subscriptionKey)
{
    VideoSearchAPIImpl client = VideoSDK.getClient(subscriptionKey);

    try
    {
        VideosInner videoResults = client.searchs().list("Bellevue Trailer", "en-us", null, null, null, null, null,
                Freshness.MONTH, null, VideoLength.SHORT, "en-us", null, VideoPricing.FREE, VideoResolution.HD1080P, null, null, null, null);
        System.out.println("\r\nSearch videos for query \"Bellevue Trailer\" free, short and 1080p resolution");

        if (videoResults == null)
        {
            System.out.println("Didn't see any video result data..");
        }
        else
        {
            if (videoResults.value().size() > 0)
            {
                VideoObject firstVideoResult = videoResults.value().get(0);
                System.out.println(String.format("Video result count: %d", videoResults.value().size()));
                System.out.println(String.format("First video id: %s", firstVideoResult.videoId()));
                System.out.println(String.format("First video name: %s", firstVideoResult.name()));
                System.out.println(String.format("First video url: %s", firstVideoResult.contentUrl()));
            }
            else
            {
                System.out.println("Couldn't find video results!");
            }
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }
}

```
Zoeken naar trends video's. Controleer of de **bannerTiles** en **categorieën** parameters.
```
public static void VideoTrending(String subscriptionKey)
{
    VideoSearchAPIImpl client = VideoSDK.getClient(subscriptionKey);

    try
    {
        TrendingVideosInner trendingResults = client.trendings().list();
        System.out.println("\r\nSearch trending videos");

        if (trendingResults == null)
        {
            System.out.println("Didn't see any trending video data..");
        }
        else
        {
            // Verify the banner tiles
            if (trendingResults.bannerTiles().size() > 0)
            {
                TrendingVideosTile firstBannerTile = trendingResults.bannerTiles().get(0);
                System.out.println(
                        String.format("Banner tile count: {trendingResults.BannerTiles.Count}"));
                System.out.println(
                        String.format("First banner tile text: {firstBannerTile.Query.Text}"));
                System.out.println(
                        String.format("First banner tile url: {firstBannerTile.Query.WebSearchUrl}"));
            }
            else
            {
                System.out.println("Couldn't find banner tiles!");
            }

            // Verify the categories
            if (trendingResults.categories().size() > 0)
            {
                TrendingVideosCategory firstCategory = trendingResults.categories().get(0);
                System.out.println(
                        String.format("Category count: %d", trendingResults.categories().size()));
                System.out.println(
                        String.format("First category title: %s", firstCategory.title()));

                if (firstCategory.subcategories().size() > 0)
                {
                    TrendingVideosSubcategory firstSubCategory = firstCategory.subcategories().get(0);
                    System.out.println(
                            String.format("SubCategory count: %d", firstCategory.subcategories().size()));
                    System.out.println(
                            String.format("First sub category title: %s", firstSubCategory.title()));

                    if (firstSubCategory.tiles().size() > 0)
                    {
                        TrendingVideosTile firstTile = firstSubCategory.tiles().get(0);
                        System.out.println(
                                String.format("Tile count: %d", firstSubCategory.tiles().size()));
                        System.out.println(
                                String.format("First tile text: %s", firstTile.query().text()));
                        System.out.println(
                                String.format("First tile url: %s", firstTile.query().webSearchUrl()));
                    }
                    else
                    {
                        System.out.println("Couldn't find tiles!");
                    }
                }
                else
                {
                    System.out.println("Couldn't find subcategories!");
                }
            }
            else
            {
                System.out.println("Couldn't find categories!");
            }
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }

}

```
Zoeken naar video's over 'Bellevue aanhangwagen' en zoek vervolgens naar meer informatie over het eerste video resultaat.
```
public static void VideoDetail(String subscriptionKey)
{
    VideoSearchAPIImpl client = VideoSDK.getClient(subscriptionKey);

    try
    {
        VideosInner videoResults = client.searchs().list("Bellevue Trailer");
        if (videoResults.value().size() > 0)
        {
            VideoObject firstVideo = videoResults.value().get(0);
            List<VideoInsightModule> modules = new ArrayList<VideoInsightModule>();
            modules.add(VideoInsightModule.ALL);
            VideoDetailsInner videoDetail = client.details().list("Bellevue Trailer", null, null, null, null, null,
                    firstVideo.videoId(), modules, "en-us", null, null, null, null, null);
                    //nc(query: "Bellevue Trailer", id: firstVideo.VideoId, modules: modules).Result;
            System.out.println(
                    String.format("\r\nSearch detail for video id={firstVideo.VideoId}, name=%s", firstVideo.name()));

            if (videoDetail != null)
            {
                if (videoDetail.videoResult() != null)
                {
                    System.out.println(
                            String.format("Expected video id: %s", videoDetail.videoResult().videoId()));
                    System.out.println(
                            String.format("Expected video name: %s", videoDetail.videoResult().name()));
                    System.out.println(
                            String.format("Expected video url: %s", videoDetail.videoResult().contentUrl()));
                }
                else
                {
                    System.out.println("Couldn't find expected video!");
                }

                if (videoDetail.relatedVideos().value().size() > 0)
                {
                    VideoObject firstRelatedVideo = videoDetail.relatedVideos().value().get(0);
                    System.out.println(
                            String.format("Related video count: %d", videoDetail.relatedVideos().value().size() ));
                    System.out.println(
                            String.format("First related video id: %s", firstRelatedVideo.videoId()));
                    System.out.println(
                            String.format("First related video name: %s", firstRelatedVideo.name()));
                    System.out.println(
                            String.format("First related video url: %s", firstRelatedVideo.contentUrl()));
                }
                else
                {
                    System.out.println("Couldn't find any related video!");
                }
            }
            else
            {
                System.out.println("Couldn't find detail about the video!");
            }
        }
        else
        {
            System.out.println("Couldn't find video results!");
        }
    }

    catch (ErrorResponseException ex)
    {
        System.out.println("Encountered exception. " + ex.getLocalizedMessage());
    }
}
```
Voeg de methoden die worden beschreven in dit artikel voor een klasse met een belangrijke functie voor het uitvoeren van de code.
```
package videoSDK;
import com.microsoft.azure.cognitiveservices.videosearch.*;

public class VideoSDK {

    public static void main(String[] args) {
        
        
        VideoSDK.VideoSearch("YOUR-SUBSCRIPTION-KEY");
        VideoSDK.VideoSearchWithFilters("YOUR-SUBSCRIPTION-KEY");
        VideoSDK.VideoTrending("YOUR-SUBSCRIPTION-KEY");
        VideoSDK.VideoDetail("YOUR-SUBSCRIPTION-KEY");

    }

    // Include the methods described in this article.
}
```
## <a name="next-steps"></a>Volgende stappen

[Cognitieve Services Java SDK-voorbeelden](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)
