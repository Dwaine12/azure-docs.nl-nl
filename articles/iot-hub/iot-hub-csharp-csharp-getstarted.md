---
title: Aan de slag met Azure IoT Hub voor C# | Microsoft Docs
description: Instructiehandleiding voor Azure IoT Hub met C#. Gebruik Azure IoT Hub en C# in combinatie met de Microsoft Azure IoT SDK's voor het implementeren van een Internet of Things-oplossing.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''

ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/12/2016
ms.author: dobett

---
# Aan de slag met Azure IoT Hub voor .NET
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Nadat u deze handleiding volledig hebt doorlopen, beschikt u over drie Windows-consoletoepassingen:

* **CreateDeviceIdentity**: deze toepassing maakt een apparaat-id en de bijbehorende beveiligingssleutel waarmee uw gesimuleerde apparaat verbonden kan worden.
* **ReadDeviceToCloudMessages**: deze toepassing geeft de telemetrie weer die is verzonden door uw gesimuleerde apparaat.
* **SimulatedDevice**: deze toepassing koppelt uw IoT-hub aan de apparaat-id die u eerder hebt gemaakt, en verzendt iedere seconde een telemetriebericht via het AMQPS-protocol.

> [!NOTE]
> Raadpleeg het artikel [IoT-Hub SDK's][lnk-hub-sdks] voor meer  informatie over de verschillende SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.
> 
> 

Voor het voltooien van deze zelfstudie hebt u het volgende nodig:

* Microsoft Visual Studio 2015.
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een gratis proefaccount aanmaken. Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

U hebt nu uw IoT-hub gemaakt, en u hebt de hostnaam en de verbindingsreeks die u nodig hebt voor de rest van deze handleiding.

## Een apparaat-id maken
In dit gedeelte gaat u een Windows-consoletoepassing maken die een apparaat-id maakt in het identiteitenregister van uw IoT-hub. Een apparaat kan geen verbinding maken met de IoT-hub, tenzij het vermeld staat in het registers met apparaat-id’s. Raadpleeg het gedeelte 'Register met apparaat-id’s' in de [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie. Wanneer u deze consoletoepassing uitvoert, worden er een unieke apparaat-id en sleutel gegenereerd waarmee uw apparaat zichzelf kan identificeren tijdens het verzenden van apparaat-naar-cloud-berichten naar IoT Hub.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**. Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is. Noem het project **CreateDeviceIdentity**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. Klik in Solution Explorer met de rechtermuisknop op het project **CreateDeviceIdentity** en klik op **Manage NuGet Packages**.
3. Klik in het venster **NuGet Package Manager** op **Browse** en zoek naar **microsoft.azure.devices**. Accepteer de gebruiksvoorwaarden en klik op **Install** om het **Microsoft.Azure.Devices**-pakket te installeren. Met deze procedure worden het [Microsoft Azure IoT Service SDK][lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.
   
    ![Venster Nuget Package Manager][11]
4. Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. Voeg de volgende velden toe aan de klasse **Program**: Vervang de tijdelijke aanduidingswaarde met de verbindingsreeks voor de IoT-hub die u hebt gemaakt in de vorige paragraaf.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. Voeg de volgende methode toe aan de klasse **Program**:
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    Met deze methode maakt u de apparaat-id **myFirstDevice**. (Als deze apparaat-ID al in het register staat, haalt de code gewoon de bestaande apparaatgegevens op.) De app geeft vervolgens de primaire sleutel voor die identiteit weer. U gebruikt deze sleutel in het gesimuleerde apparaat om verbinding te maken met uw IoT-hub.
7. Voeg tot slot de volgende regels toe aan de methode **Main**:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. Voer deze toepassing uit en noteer de apparaatsleutel.
   
    ![Apparaatsleutel die is gegenereerd door de toepassing][12]

> [!NOTE]
> In het id-register van IoT Hub worden alleen apparaat-id’s opgeslagen waarmee veilig toegang tot de hub kan worden verkregen. De apparaat-id’s en sleutels worden opgeslagen en gebruikt als beveiligingsreferenties. Met de vlag voor ingeschakeld/uitgeschakeld kunt u toegang tot een afzonderlijk apparaat uitschakelen. Als uw toepassing andere apparaatspecifieke metagegevens moet opslaan, moet deze een toepassingsspecifieke opslagmethode gebruiken. Raadpleeg de [IoT Hub Developer Guide][lnk-devguide-identity] voor meer informatie.
> 
> 

## Apparaat-naar-cloud-berichten ontvangen
In dit gedeelte maakt u een Windows-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen. Een IoT-hub geeft een [Azure Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt weer waarmee u apparaat-naar-cloud-berichten kunt lezen. Om de zaken niet nodeloos ingewikkeld te maken, maakt u met deze handleiding een basislezer die niet geschikt is voor hoge doorvoersnelheden. Raadpleeg de handleiding [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial] om te ontdekken hoe u op grote schaal apparaat-naar-cloud-berichten kunt verwerken. Zie voor meer informatie over het verwerken van Event Hubs-berichten de handleiding [Aan de slag met Event Hubs][lnk-eventhubs-tutorial]. (Deze zelfstudie is van toepassing op eindpunten die compatibel zijn met Event Hubs in IoT Hub.)

> [!NOTE]
> Het met Event Hubs compatibele eindpunt voor het lezen van apparaat-naar-cloud-bericht maakt altijd gebruik van het AMQPS-protocol.
> 
> 

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**. Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is. Noem het project **ReadDeviceToCloudMessages**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. Klik in Solution Explorer met de rechtermuisknop op het project **ReadDeviceToCloudMessages** en kies **Manage NuGet Packages**.
3. In het venster **NuGet Package Manager** zoekt u **WindowsAzure.ServiceBus**. Accepteer de gebruikersvoorwaarden en klik op **Install**. Met deze procedure wordt een verwijzing naar de [Azure Service Bus][lnk-servicebus-nuget], inclusief alle afhankelijkheden ervan, gedownload, geïnstalleerd en toegevoegd. Met dit pakket kan de toepassing verbinding maken met het eindpunt dat compatibel is met Event Hubs op uw IoT-hub.
4. Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:
   
        using Microsoft.ServiceBus.Messaging;
        using System.Threading;
5. Voeg de volgende velden toe aan de klasse **Program**: Vervang de tijdelijke aanduidingswaarde met de verbindingsreeks voor de IoT-hub die u hebt gemaakt in het gedeelte 'Een IoT-hub maken'.
   
        static string connectionString = "{iothub connection string}";
        static string iotHubD2cEndpoint = "messages/events";
        static EventHubClient eventHubClient;
6. Voeg de volgende methode toe aan de klasse **Program**:
   
        private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
        {
            var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
            while (true)
            {
                if (ct.IsCancellationRequested) break;
                EventData eventData = await eventHubReceiver.ReceiveAsync();
                if (eventData == null) continue;
   
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
   
    Deze methode gebruikt een exemplaar van **EventHubReceiver** om berichten te ontvangen van alle apparaat-naar-cloud ontvangstpartities van de IoT-hub. U geeft nu een `DateTime.Now` parameter door bij het maken van het object **EventHubReceiver**, zodat alleen berichten worden ontvangen die zijn verzonden nadat het object is gestart. Dit filter is handig in een testomgeving, omdat u zo de huidige reeks berichten kunt zien. In een productieomgeving moet de code ervoor zorgen dat alle berichten worden verwerkt. Zie voor meer informatie de handleiding [IoT Hub-apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial].
7. Voeg tot slot de volgende regels toe aan de methode **Main**:
   
        Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);
   
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
   
        CancellationTokenSource cts = new CancellationTokenSource();
   
        System.Console.CancelKeyPress += (s, e) =>
        {
          e.Cancel = true;
          cts.Cancel();
          Console.WriteLine("Exiting...");
        };
   
        var tasks = new List<Task>();
        foreach (string partition in d2cPartitions)
        {
           tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }  
        Task.WaitAll(tasks.ToArray());

## Een gesimuleerde apparaattoepassing maken
In dit gedeelte maakt u een Windows-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloud-berichten verzendt naar een IoT-hub.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**. Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is. Noem het project **SimulatedDevice**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. Klik in Solution Explorer met de rechtermuisknop op het project **SimulatedDevice** en kies **Manage NuGet Packages**.
3. Klik in het venster **NuGet Package Manager** op **Browse** en zoek naar **Microsoft.Azure.Devices.Client**. Accepteer de gebruiksvoorwaarden en klik op **Install** om het **Microsoft.Azure.Devices.Client**-pakket te installeren. Met deze procedure worden het [Azure IoT - Device SDK NuGet-pakket][lnk-device-nuget] en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.
4. Voeg aan het begin van het bestand **Program.cs** de volgende `using`-instructie toe:
   
        using Microsoft.Azure.Devices.Client;
        using Newtonsoft.Json;
5. Voeg de volgende velden toe aan de klasse **Program**: Vervang de tijdelijke aanduiding door de hostnaam van de IoT-hub die u in het gedeelte 'Een IoT-hub maken' hebt opgehaald en de apparaatsleutel die u in het gedeelte 'Een apparaat-id maken' hebt opgehaald.
   
        static DeviceClient deviceClient;
        static string iotHubUri = "{iot hub hostname}";
        static string deviceKey = "{device key}";
6. Voeg de volgende methode toe aan de klasse **Program**:
   
        private static async void SendDeviceToCloudMessagesAsync()
        {
            double avgWindSpeed = 10; // m/s
            Random rand = new Random();
   
            while (true)
            {
                double currentWindSpeed = avgWindSpeed + rand.NextDouble() * 4 - 2;
   
                var telemetryDataPoint = new
                {
                    deviceId = "myFirstDevice",
                    windSpeed = currentWindSpeed
                };
                var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
                var message = new Message(Encoding.ASCII.GetBytes(messageString));
   
                await deviceClient.SendEventAsync(message);
                Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);
   
                Task.Delay(1000).Wait();
            }
        }
   
    Met deze methode wordt elke seconde een nieuw apparaat-naar-cloud bericht verzonden. Het bericht bevat een JSON-geserialiseerd object met het apparaat-ID en een willekeurig gegenereerd nummer om een windsnelheidssensor te simuleren.
7. Voeg tot slot de volgende regels toe aan de methode **Main**:
   
        Console.WriteLine("Simulated device\n");
        deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));
   
        SendDeviceToCloudMessagesAsync();
        Console.ReadLine();
   
   Met de **Create**-methode maakt u standaard een **DeviceClient**-exemplaar dat het AMQP-protocol gebruikt om te communiceren met IoT-Hub. Als u het HTTPS-protocol wilt gebruiken, dient u de **Create**-methode te overschrijven. Zo kunt u zelf het protocol bepalen. Als u het HTTPS-protocol gebruikt, moet u ook het NuGet-pakket **Microsoft.AspNet.WebApi.Client** toevoegen om uw project op te nemen in de naamruimte **System.Net.Http.Formatting**.

In deze handleiding doorloopt u de stappen voor het maken van een IoT Hub-apparaatclient. U kunt ook de Visual Studio-extensie [Connected Service for Azure IoT Hub][lnk-connected-service] gebruiken om de benodigde code toe te voegen aan de clienttoepassing van uw apparaat.

> [!NOTE]
> Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd. Bij de productiecode moet u een beleid voor opnieuw proberen implementeren (zoals exponentieel uitstel), zoals aangegeven in het MSDN-artikel [Transient Fault Handling ][lnk-transient-faults] (Afhandeling van tijdelijke fouten).
> 
> 

## De toepassingen uitvoeren
U kunt nu de toepassingen gaan uitvoeren.

1. Klik in Solution Explorer, in Visual Studio, met de rechtermuisknop op uw oplossing en klik vervolgens op **Set StartUp projects**. Klik op **Multiple startup projects** (Meerdere opstartprojecten) en klik vervolgens op **Start** als de actie voor beide projecten **ProcessDeviceToCloudMessages** en **SimulatedDevice**.
   
   ![Eigenschappen van opstartprojecten][41]
2. Druk op **F5** om beide apps uit te voeren. De console-uitvoer van de **SimulatedDevice**-app toont de berichten die uw gesimuleerde apparaat verzendt naar uw IoT-hub. De console-uitvoer van de **ReadDeviceToCloudMessages**-app toont de berichten die uw IoT-hub ontvangt.
   
   ![Console-uitvoer van apps][42]
3. De tegel **Usage** in de [Azure Portal][lnk-portal] toont het aantal berichten dat is verzonden naar de hub:
   
    ![Tegel Usage in de Azure Portal][43]

## Volgende stappen
In deze handleiding, hebt u een IoT-hub geconfigureerd in de portal en vervolgens hebt u een apparaat-id gemaakt in het id-register van de hub. U hebt deze apparaat-id gebruikt om de gesimuleerde apparaattoepassing in staat te stellen om apparaat-naar-cloud-berichten te verzenden naar de hub. Ook hebt een app gemaakt die de berichten weergeeft die worden ontvangen door de hub. 

Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:

* [Connecting your device (Uw apparaat verbinden)][lnk-connect-device]
* [Getting started with device management (Aan de slag met apparaatbeheer)][lnk-device-management]
* [Getting started with the Gateway SDK (Aan de slag met de Gateway-SDK)][lnk-gateway-SDK]

Raadpleeg de zelfstudie [Process device-to-cloud messages (Apparaat-naar-cloud-berichten verwerken)][lnk-process-d2c-tutorial] voor meer informatie over het uitbreiden van uw IoT-oplossing en het op schaal verwerken van apparaat-naar-cloud-berichten.

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10]: ./media/iot-hub-csharp-csharp-getstarted/create-identity-csharp1.png
[11]: ./media/iot-hub-csharp-csharp-getstarted/create-identity-csharp2.png
[12]: ./media/iot-hub-csharp-csharp-getstarted/create-identity-csharp3.png

<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-device-management-get-started.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/



<!--HONumber=Oct16_HO1-->


