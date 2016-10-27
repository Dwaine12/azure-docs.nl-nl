<properties
    pageTitle="Aan de slag met Event Hubs in C# | Microsoft Azure"
    description="Volg deze zelfstudie om aan de slag te gaan met Azure Event Hubs met C# en de EventProcessorHost."
    services="event-hubs"
    documentationCenter=""
    authors="jtaubensee"
    manager="timlt"
    editor=""/>

<tags
    ms.service="event-hubs"
    ms.workload="na"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="hero-article"
    ms.date="09/02/2016"
    ms.author="jotaub;sethm"/>


# <a name="get-started-with-event-hubs"></a>Aan de slag met Event Hubs

[AZURE.INCLUDE [service-bus-selector-get-started](../../includes/service-bus-selector-get-started.md)]

## <a name="introduction"></a>Inleiding

Event Hubs is een service die grote hoeveelheden gebeurtenisgegevens (telemetrie) van verbonden apparaten en toepassingen verwerkt. Nadat u gegevens in Event Hubs hebt verzameld, kunt u de gegevens opslaan met behulp van een opslagcluster of transformeren met een provider van realtime-analyses. Deze functie voor grootschalige gebeurtenisverzameling en -verwerking is een belangrijk onderdeel van de architectuur van moderne toepassingen, met inbegrip van het Internet der dingen (IoT).

In deze zelfstudie kunt u zien hoe u de klassieke Azure-portal gebruikt om een Event Hub te maken. U ziet ook hoe u berichten in een Event Hub verzamelt met een consoletoepassing die is geschreven in C# en hoe u deze bericht parallel ophaalt met de C# [Event Processor Host][]-bibliotheek.

Om deze handleiding volledig door te kunnen nemen, hebt u het volgende nodig:

+ [Microsoft Visual Studio](http://visualstudio.com)

+ Een actief Azure-account. Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.

[AZURE.INCLUDE [event-hubs-create-event-hub](../../includes/event-hubs-create-event-hub.md)]

[AZURE.INCLUDE [service-bus-event-hubs-get-started-send-csharp](../../includes/service-bus-event-hubs-get-started-send-csharp.md)]

[AZURE.INCLUDE [service-bus-event-hubs-get-started-receive-ephcs](../../includes/service-bus-event-hubs-get-started-receive-ephcs.md)]

## <a name="run-the-applications"></a>De toepassingen uitvoeren

U kunt nu de toepassingen gaan uitvoeren.

1. Open in Visual Studio het **Ontvanger**-project dat u eerder hebt gemaakt.

2. Klik met de rechtermuisknop op de **Ontvanger**-oplossing, klik op **Toevoegen** en klik vervolgens op **Bestaand project**.
 
3. Zoek het bestaande Sender.csproj-bestand op en dubbelklik erop om het toe te voegen aan de oplossing.
 
4. Klik nogmaals met de rechtermuisknop op de **Ontvanger**-oplossing en klik vervolgens op **Eigenschappen**. De eigenschappenpagina van **Ontvanger** wordt weergegeven.

5. Klik op **Opstartproject** en vervolgens op de knop **Meerdere opstartprojecten**. Stel in het vak **Actie** het **Ontvanger**- en het **Afzender**-project in op **Starten**.

    ![][19]

6. Klik op **Projectafhankelijkheden**. Klik in het vak **Projecten** op **Afzender**. Zorg dat in het vak **Is afhankelijk van** **Ontvanger** is geselecteerd.

    ![][20]

7. Klik op **OK** om het dialoogvenster **Eigenschappen** te sluiten.

1.  Druk op F5 het **Ontvanger**-project uit te voeren vanuit Visual Studio en wacht tot de ontvangers voor alle partities worden gestart.

    ![][21]

2.  Het **Afzender**-project wordt automatisch uitgevoerd. Druk op **Enter** in het consolevenster. U ziet dat er gebeurtenissen worden weergegeven in het venster van de ontvanger.

    ![][22]

Druk op **Ctrl+C** in het venster **Afzender** om de Afzender-toepassing te beëindigen en druk op **Enter** in het venster Ontvanger om die toepassing af te sluiten.

## <a name="next-steps"></a>Volgende stappen

Nu u een werkende toepassing hebt gebouwd die een Event Hub maakt en gegevens verzendt en ontvangt, kunt u naar de volgende scenario's gaan:

- Een complete [voorbeeldtoepassing die gebruikmaakt van Event Hubs][].
- Het voorbeeld [Verwerking van de gebeurtenis Uitschalen met Event Hubs][].
- [Event Hubs-overzicht][]

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[Klassieke Azure Portal]: https://manage.windowsazure.com/
[Gebeurtenisprocessorhost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs-overzicht]: event-hubs-overview.md
[voorbeeldtoepassing die gebruikmaakt van Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Verwerking van de gebeurtenis Uitschalen met Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[oplossing voor berichten in de wachtrij]: ../service-bus-messaging/service-bus-dotnet-multi-tier-app-using-service-bus-queues.md
 



<!--HONumber=Oct16_HO3-->


