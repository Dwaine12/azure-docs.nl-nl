---
title: Media Services activa downloaden naar uw computer - Azure | Microsoft Docs
description: Meer informatie over activa downloaden naar uw computer. Codevoorbeelden zijn geschreven in C# en gebruiken van de Media Services SDK voor .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: ed53fe191dcf740f949b2d9cdcc3c97e30d85544
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2018
ms.locfileid: "33788226"
---
# <a name="how-to-deliver-an-asset-by-download"></a>Procedure: een Asset door Download leveren
Dit artikel worden de opties voor het leveren van media-elementen met Media Services wordt geüpload. U kunt inhoud in Media Services leveren in talloze scenario's van toepassing. Nadat de codering, downloaden van de gegenereerde media-elementen of toegang tot deze met behulp van een streaming-locator. U kunt ook inhoud met behulp van een inhoud Delivery Network (CDN) voor betere prestaties en schaalbaarheid leveren.

In dit voorbeeld laat zien hoe media activa downloaden van Media Services op uw lokale computer. De code vraagt de taken die zijn gekoppeld aan het Media Services-account door de taak-ID en toegang tot de **OutputMediaAssets** verzameling (dit is de set van een of meer uitvoer media-elementen die het resultaat is van een taak wordt uitgevoerd). Dit voorbeeld wordt het downloaden van media-elementen voor uitvoer van een taak, maar u kunt dezelfde aanpak voor het downloaden van andere assets toepassen.

>[!NOTE]
>Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Gebruik dezelfde beleids-ID als u altijd dezelfde dagen werkt / toegangsmachtigingen, bijvoorbeeld: beleid voor locators die zijn bedoeld om te blijven aanwezig gedurende een lange periode (niet-upload policies). Raadpleeg [dit artikel](media-services-dotnet-manage-entities.md#limit-access-policies) voor meer informatie.

```csharp
    // Download the output asset of the specified job to a local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how to download a single asset. 
        // However, you can iterate through the OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference to the job. 
        IJob job = GetJob(jobId);

        // Get a reference to the first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator to download the asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use the following event handler to check download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }
```


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zie ook
[Streaming inhoud leveren](media-services-deliver-streaming-content.md)

