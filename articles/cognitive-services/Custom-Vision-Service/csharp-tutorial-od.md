---
title: Bouw een object-detectie-project in C# - Custom Vision Service - Azure Cognitive Services | Microsoft Docs
description: Verken een eenvoudige Windows-app die gebruikmaakt van de aangepaste Vision-API in Microsoft Cognitive Services. Maak een project, tags toevoegen, afbeeldingen uploaden, trainen van uw project en een voorspelling te maken met behulp van het eindpunt.
services: cognitive-services
author: areddish
manager: chbuehle
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: article
ms.date: 05/07/2018
ms.author: areddish
ms.openlocfilehash: e3def864267a590c86a2dd6663561d8488081ad6
ms.sourcegitcommit: 9819e9782be4a943534829d5b77cf60dea4290a2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/06/2018
ms.locfileid: "36301077"
---
# <a name="use-custom-vision-api-to-build-an-object-detection-project-in-c35"></a>Custom Vision-API gebruiken om te maken van een object-detectie-project in C&#35; 
Informatie over het gebruik van een eenvoudige Windows-toepassing die gebruikmaakt van de Computer Vision-API om een object-detectie-project te maken. Nadat deze gemaakt, kunt u gecodeerde regio's toevoegen, afbeeldingen uploaden, trainen van het project, verkrijgen van het project standaard voorspelling eindpunt-URL en het eindpunt voor het testen van een installatiekopie van een via een programma gebruiken. In dit voorbeeld open-source als sjabloon gebruiken voor het bouwen van uw eigen app voor Windows met behulp van de aangepaste Vision-API.

## <a name="prerequisites"></a>Vereisten

### <a name="get-the-custom-vision-sdk-and-samples"></a>Ophalen van de aangepaste Vision SDK en voorbeelden
Als u wilt maken in dit voorbeeld, moet u de aangepaste Vision SDK NuGet-pakketten:

* [Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training/)
* [Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction/)

U kunt downloaden van de installatiekopieën van samen met de [C#-voorbeelden](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/CustomVision).

## <a name="get-the-training-and-prediction-keys"></a>Ophalen van de sleutels trainen en voorspellen

Als u de sleutels in dit voorbeeld gebruikt, gaat u naar de [Custom Vision webpagina](https://customvision.ai) en selecteer de __tandwielpictogram__ in de rechterbovenhoek. In de __Accounts__ sectie, Kopieer de waarden van de __Training sleutel__ en __voorspelling sleutel__ velden.

![Afbeelding van de gebruikersinterface van de sleutels](./media/csharp-tutorial/training-prediction-keys.png)

## <a name="step-1-create-a-console-application"></a>Stap 1: Maak een consoletoepassing

In deze stap maakt u een consoletoepassing maken en voorbereiden van de training-sleutel en de afbeeldingen die nodig zijn voor het voorbeeld:

1. Start Visual Studio 2015 Community-editie. 
2. Maak een nieuwe consoletoepassing.
3. Verwijzingen naar de twee nuget-pakketten toevoegen:
    * Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training
    * Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction

4. Vervang de inhoud van **Program.cs** met de code die volgt.

```csharp
using Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction;
using Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training;
using Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training.Models;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading;

namespace SampleObjectDetection
{
    class Program
    {
        static void Main(string[] args)
        {
            // Add your training key from the settings page of the portal
            string trainingKey = "<your key here>";

            // Create the Api, passing in the training key
            TrainingApi trainingApi = new TrainingApi() { ApiKey = trainingKey };
        }        
    }
}
```

## <a name="step-2-create-a-custom-vision-service-project"></a>Stap 2: Maak een project Custom Vision Service

Voor het maken van een nieuw project voor Custom Vision Service, voeg de volgende code toe aan het einde van uw **Main()** methode.

```csharp
    // Find the object detection domain
    var domains = trainingApi.GetDomains();
    var objDetectionDomain = domains.FirstOrDefault(d => d.Type == "ObjectDetection");

    // Create a new project
    Console.WriteLine("Creating new project:");
    var project = trainingApi.CreateProject("My New Project", null, objDetectionDomain.Id);
```

## <a name="step-3-add-tags-to-your-project"></a>Stap 3: Labels toevoegen aan uw project

Voeg labels toevoegen aan uw project, de volgende code na het aanroepen van **CreateProject()**:

```csharp
    // Make two tags in the new project
    var forkTag = trainingApi.CreateTag(project.Id, "fork");
    var scissorsTag = trainingApi.CreateTag(project.Id, "scissors");
```

## <a name="step-4-upload-images-to-the-project"></a>Stap 4: Afbeeldingen uploaden naar het project

Voor object detectie projecten moeten we de regio van het object met behulp van genormaliseerde coördinaten en een tag bepalen. Voeg de installatiekopieën en gelabelde regio's wilt toevoegen, de volgende code aan het einde van de **Main()** methode:

```csharp
    Dictionary<string, double[]> fileToRegionMap = new Dictionary<string, double[]>()
    {
        // The bounding box is specified in normalized coordinates.
        //  Normalized Left = Left / Width (in Pixels)
        //  Normalized Top = Top / Height (in Pixels)
        //  Normalized Bounding Box Width = (Right - Left) / Width (in Pixels)
        //  Normalized Bounding Box Height = (Bottom - Top) / Height (in Pixels)
        // FileName, Left, Top, Width, Height of the bounding box.
        {"scissors_1", new double[] { 0.4007353, 0.194068655, 0.259803921, 0.6617647 } },
        {"scissors_2", new double[] { 0.426470578, 0.185898721, 0.172794119, 0.5539216 } },
        {"scissors_3", new double[] { 0.289215684, 0.259428144, 0.403186262, 0.421568632 } },
        {"scissors_4", new double[] { 0.343137264, 0.105833367, 0.332107842, 0.8055556 } },
        {"scissors_5", new double[] { 0.3125, 0.09766343, 0.435049027, 0.71405226 } },
        {"scissors_6", new double[] { 0.379901975, 0.24308826, 0.32107842, 0.5718954 } },
        {"scissors_7", new double[] { 0.341911763, 0.20714055, 0.3137255, 0.6356209 } },
        {"scissors_8", new double[] { 0.231617644, 0.08459154, 0.504901946, 0.8480392 } },
        {"scissors_9", new double[] { 0.170343131, 0.332957536, 0.767156839, 0.403594762 } },
        {"scissors_10", new double[] { 0.204656869, 0.120539248, 0.5245098, 0.743464053 } },
        {"scissors_11", new double[] { 0.05514706, 0.159754932, 0.799019635, 0.730392158 } },
        {"scissors_12", new double[] { 0.265931368, 0.169558853, 0.5061275, 0.606209159 } },
        {"scissors_13", new double[] { 0.241421565, 0.184264734, 0.448529422, 0.6830065 } },
        {"scissors_14", new double[] { 0.05759804, 0.05027781, 0.75, 0.882352948 } },
        {"scissors_15", new double[] { 0.191176474, 0.169558853, 0.6936275, 0.6748366 } },
        {"scissors_16", new double[] { 0.1004902, 0.279036, 0.6911765, 0.477124184 } },
        {"scissors_17", new double[] { 0.2720588, 0.131977156, 0.4987745, 0.6911765 } },
        {"scissors_18", new double[] { 0.180147052, 0.112369314, 0.6262255, 0.6666667 } },
        {"scissors_19", new double[] { 0.333333343, 0.0274019931, 0.443627447, 0.852941155 } },
        {"scissors_20", new double[] { 0.158088237, 0.04047389, 0.6691176, 0.843137264 } },
        {"fork_1", new double[] { 0.145833328, 0.3509314, 0.5894608, 0.238562092 } },
        {"fork_2", new double[] { 0.294117659, 0.216944471, 0.534313738, 0.5980392 } },
        {"fork_3", new double[] { 0.09191177, 0.0682516545, 0.757352948, 0.6143791 } },
        {"fork_4", new double[] { 0.254901975, 0.185898721, 0.5232843, 0.594771266 } },
        {"fork_5", new double[] { 0.2365196, 0.128709182, 0.5845588, 0.71405226 } },
        {"fork_6", new double[] { 0.115196079, 0.133611143, 0.676470637, 0.6993464 } },
        {"fork_7", new double[] { 0.164215669, 0.31008172, 0.767156839, 0.410130739 } },
        {"fork_8", new double[] { 0.118872553, 0.318251669, 0.817401946, 0.225490168 } },
        {"fork_9", new double[] { 0.18259804, 0.2136765, 0.6335784, 0.643790841 } },
        {"fork_10", new double[] { 0.05269608, 0.282303959, 0.8088235, 0.452614367 } },
        {"fork_11", new double[] { 0.05759804, 0.0894935, 0.9007353, 0.3251634 } },
        {"fork_12", new double[] { 0.3345588, 0.07315363, 0.375, 0.9150327 } },
        {"fork_13", new double[] { 0.269607842, 0.194068655, 0.4093137, 0.6732026 } },
        {"fork_14", new double[] { 0.143382356, 0.218578458, 0.7977941, 0.295751631 } },
        {"fork_15", new double[] { 0.19240196, 0.0633497, 0.5710784, 0.8398692 } },
        {"fork_16", new double[] { 0.140931368, 0.480016381, 0.6838235, 0.240196079 } },
        {"fork_17", new double[] { 0.305147052, 0.2512582, 0.4791667, 0.5408496 } },
        {"fork_18", new double[] { 0.234068632, 0.445702642, 0.6127451, 0.344771236 } },
        {"fork_19", new double[] { 0.219362751, 0.141781077, 0.5919118, 0.6683006 } },
        {"fork_20", new double[] { 0.180147052, 0.239820287, 0.6887255, 0.235294119 } }
    };

    // Add all images for fork
    var imagePath = Path.Combine("Images", "fork");
    var imageFileEntries = new List<ImageFileCreateEntry>();
    foreach (var fileName in Directory.EnumerateFiles(imagePath))
    {
        var region = fileToRegionMap[Path.GetFileNameWithoutExtension(fileName)];
        imageFileEntries.Add(new ImageFileCreateEntry(fileName, File.ReadAllBytes(fileName), null, new List<Region>(new Region[] { new Region(forkTag.Id, region[0], region[1], region[2], region[3]) })));
    }
    trainingApi.CreateImagesFromFiles(project.Id, new ImageFileCreateBatch(imageFileEntries));

    // Add all images for scissors
    imagePath = Path.Combine("Images", "scissors");
    imageFileEntries = new List<ImageFileCreateEntry>();
    foreach (var fileName in Directory.EnumerateFiles(imagePath))
    {
        var region = fileToRegionMap[Path.GetFileNameWithoutExtension(fileName)];
        imageFileEntries.Add(new ImageFileCreateEntry(fileName, File.ReadAllBytes(fileName), null, new List<Region>(new Region[] { new Region(scissorsTag.Id, region[0], region[1], region[2], region[3]) })));
    }
    trainingApi.CreateImagesFromFiles(project.Id, new ImageFileCreateBatch(imageFileEntries));
```

## <a name="step-5-train-the-project"></a>Stap 5: Het project trainen

Nu dat u kunt labels en afbeeldingen hebt toegevoegd aan het project, kunt u deze training: 

1. Voeg de volgende code aan het einde van **Main()**. Hiermee maakt u de eerste versie in het project.
2. Markeer deze herhaling als de standaard-iteratie.

```csharp
    // Now there are images with tags start training the project
    Console.WriteLine("\tTraining");
    var iteration = trainingApi.TrainProject(project.Id);

    // The returned iteration will be in progress, and can be queried periodically to see when it has completed
    while (iteration.Status != "Completed")
    {
        Thread.Sleep(1000);

        // Re-query the iteration to get its updated status
        iteration = trainingApi.GetIteration(project.Id, iteration.Id);
    }

    // The iteration is now trained. Make it the default project endpoint
    iteration.IsDefault = true;
    trainingApi.UpdateIteration(project.Id, iteration.Id, iteration);
    Console.WriteLine("Done!\n");
```

## <a name="step-6-get-and-use-the-default-prediction-endpoint"></a>Stap 6: Halen en gebruik het standaardeindpunt voor de voorspelling

U bent nu klaar voor gebruik van het model voor voorspelling: 

1. Ophalen van het eindpunt die zijn gekoppeld aan de standaard-iteratie door het invoegen van de volgende code aan het einde van **Main()**. 
2. Een testinstallatiekopie aan het project verzenden met behulp van dit eindpunt.

```csharp
    // Now there is a trained endpoint, it can be used to make a prediction

    // Add your prediction key from the settings page of the portal
    // The prediction key is used in place of the training key when making predictions
    string predictionKey = "<your key here>";

    // Create a prediction endpoint, passing in the obtained prediction key
    PredictionEndpoint endpoint = new PredictionEndpoint() { ApiKey = predictionKey };

    // Make a prediction against the new project
    Console.WriteLine("Making a prediction:");
    var imageFile = Path.Combine("Images", "test", "test_image.jpg");
    using (var stream = File.OpenRead(imageFile))
    {
        var result = endpoint.PredictImage(project.Id, File.OpenRead(imageFile));

        // Loop over each prediction and write out the results
        foreach (var c in result.Predictions)
        {
            Console.WriteLine($"\t{c.TagName}: {c.Probability:P1} [ {c.BoundingBox.Left}, {c.BoundingBox.Top}, {c.BoundingBox.Width}, {c.BoundingBox.Height} ]");
        }
    }
```

## <a name="step-7-run-the-example"></a>Stap 7: Het voorbeeld uitvoeren

Ontwikkel en voer de oplossing. De voorspellingsresultaten op die worden weergegeven in de console.
