---
title: Aan de slag met Azure IoT Hub voor Java | Microsoft Docs
description: Handleiding voor Azure IoT Hub met Java. Gebruik Azure IoT Hub en Java in combinatie met de Microsoft Azure IoT-SDK's voor het implementeren van een Internet of Things (IoT)-oplossing.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: ''

ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2016
ms.author: dobett

---
# Aan de slag met Azure IoT Hub voor Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Aan het eind van deze zelfstudie beschikt u over drie Java-consoletoepassingen:

* **create-device-identity**: deze toepassing maakt een apparaat-id en de bijbehorende beveiligingssleutel waarmee uw gesimuleerde apparaat verbonden kan worden.
* **read-d2c-messages**: deze toepassing geeft de telemetrie weer die is verzonden door uw gesimuleerde apparaat.
* **simulated-device**: deze toepassing koppelt uw IoT-hub aan de apparaat-id die u eerder hebt gemaakt, en verzendt iedere seconde een telemetriebericht via het AMQPS-protocol.

> [!NOTE]
> Het artikel [IoT-Hub SDK's][lnk-hub-sdks] bevat informatie over de verschillende SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.
> 
> 

Voor het voltooien van deze zelfstudie hebt u het volgende nodig:

* Java SE 8. <br/> In het gedeelte [Uw ontwikkelingsomgeving voorbereiden][lnk-dev-setup] staat beschreven hoe u Java voor deze handleiding kunt installeren op Windows of Linux.
* Maven 3.  <br/> In het gedeelte [Uw ontwikkelingsomgeving voorbereiden][lnk-dev-setup] staat beschreven hoe u Maven voor deze handleiding kunt installeren op Windows of Linux.
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een gratis proefaccount aanmaken. Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Als laatste stap noteert u de waarde van de **primaire sleutel** en klikt u daarna op **Messaging**. Noteer in de blade **Messaging** de **Event Hub-compatibele naam** en het **Event Hub-compatibele eindpunt**. U hebt deze drie waarden nodig wanneer u uw **read-d2c-messages**-toepassing maakt.

![Blade IoT Hub-berichten op de Azure-portal][6]

U hebt nu uw IoT-hub gemaakt en u beschikt over de hostnaam en verbindingsreeks van de IoT-hub, de primaire sleutel van de IoT-hub, de Event Hubs-compatibele naam en het Event Hubs-compatibele eindpunt. Deze gegevens hebt u nodig voor de rest van deze zelfstudie.

## Een apparaat-id maken
In dit gedeelte gaat u een Java-consoletoepassing maken die een nieuwe apparaat-id kan maken in het identiteitenregister van uw IoT-hub. Een apparaat kan geen verbinding maken met de IoT-hub, tenzij het vermeld staat in het registers met apparaat-id’s. Raadpleeg het gedeelte **Register met apparaat-id’s** in de [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identiteit] voor meer informatie. Wanneer u deze consoletoepassing uitvoert, worden er een unieke apparaat-id en sleutel gegenereerd waarmee uw apparaat zichzelf kan identificeren tijdens het verzenden van apparaat-naar-cloud-berichten naar IoT Hub.

1. Maak een nieuwe lege map genaamd iot-java-get-started. Maak een nieuw Maven-project in de map iot-java-get-started en noem dit **create-device-identity**. Gebruik hierbij de volgende opdracht in uw opdrachtvenster. Let op: dit is één enkele, lange opdracht:
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. Navigeer naar de nieuwe map create-device-identity vanuit het opdrachtvenster.
3. Open het bestand pom.xml in de map create-device-identity met een teksteditor en voeg de volgende afhankelijkheden toe aan de node **dependencies**. Hiermee kunt u het iothub-service-sdk-pakket gebruiken in uw toepassing:
   
    ```
    <dependency>
      <groupId>com.microsoft.azure.iothub-java-client</groupId>
      <artifactId>iothub-java-service-client</artifactId>
      <version>1.0.9</version>
    </dependency>
    ```
4. Sla het bestand pom.xml op en sluit het af.
5. Open het bestand create-device-identity\src\main\java\com\mycompany\app\App.java met een teksteditor.
6. Voeg de volgende **import**instructies toe aan het bestand:
   
    ```
    import com.microsoft.azure.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.iot.service.sdk.Device;
    import com.microsoft.azure.iot.service.sdk.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```
7. Voeg de volgende variabelen op klasseniveau toe aan de **App**-klasse. Vervang daarbij **{yourhubconnectionstring}** door de waarde die u eerder hebt genoteerd:
   
    ```
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
   
    ```
8. Wijzig de handtekening van de **main**-methode om de uitzonderingen als volgt op te nemen:
   
    ```
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```
9. Voeg de volgende code toe als hoofdtekst van de **belangrijkste** methode. Deze code maakt een apparaat in het identiteitsregister van de IoT Hub dat *javadevice* heet als dit nog niet bestaat. Vervolgens wordt het apparaat-id en de sleutel weergegeven. Deze hebt u later nodig:
   
    ```
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
   
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }
    System.out.println("Device id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```
10. Sla het bestand App.java op en sluit het af.
11. Als u de toepassing **create-device-identity** wilt creëren met behulp van Maven, geef dan de volgende opdracht in het opdrachtvenster in de map create-device-identity:
    
    ```
    mvn clean package -DskipTests
    ```
12. Als u de toepassing **create-device-identity** wilt uitvoeren met behulp van Maven, geef dan de volgende opdracht in het opdrachtvenster in de map create-device-identity:
    
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```
13. Noteer de **apparaat-id** en de **apparaatsleutel**. Deze hebt u later weer nodig wanneer u een toepassing gaat maken die verbinding maakt met IoT Hub als apparaat.

> [!NOTE]
> In het id-register van IoT Hub worden alleen apparaat-id’s opgeslagen waarmee veilig toegang tot de hub kan worden verkregen. De apparaat-id’s en sleutels worden opgeslagen en gebruikt als beveiligingsreferenties. Met de vlag voor ingeschakeld/uitgeschakeld kunt u toegang tot een afzonderlijk apparaat uitschakelen. Als uw toepassing andere apparaatspecifieke metagegevens moet opslaan, moet deze een toepassingsspecifieke opslagmethode gebruiken. Raadpleeg de [IoT Hub Developer Guide ][lnk-devguide-identiteit] (Ontwikkelaarshandleiding voor IoT Hub) voor meer informatie.
> 
> 

## Apparaat-naar-cloud-berichten ontvangen
In dit gedeelte maakt u een Java-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen. Een IoT-hub toont een [Event Hub][lnk-event-hubs-overview]-compatibel eindpunt waarmee u apparaat-naar-cloud-berichten kunt lezen. Om de zaken niet nodeloos ingewikkeld te maken, maakt u met deze handleiding een basislezer die niet geschikt is voor hoge doorvoersnelheden. In de handleiding [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial] leert u hoe u op grote schaal apparaat-naar-cloud-berichten kunt verwerken. In de zelfstudie [Aan de slag met Event Hubs][lnk-eventhubs-tutorial] leest u meer over het verwerken van berichten van Event Hubs. Deze zelfstudie is van toepassing op de Event Hubs-compatibele eindpunten van IoT Hub.

> [!NOTE]
> Het met Event Hubs compatibele eindpunt voor het lezen van apparaat-naar-cloud-bericht maakt altijd gebruik van het AMQPS-protocol.
> 
> 

1. Maak een nieuw Maven-project in de map iot-java-get-started die u hebt gemaakt in het gedeelte *Een apparaat-id maken* en noem dit **read-d2c-messages**. Gebruik hierbij de volgende opdracht in uw opdrachtvenster. Let op: dit is één enkele, lange opdracht:
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. Navigeer naar de nieuwe map read-d2c-messages vanuit het opdrachtvenster.
3. Open het bestand pom.xml in de map read-d2c-messages met een teksteditor en voeg de volgende afhankelijkheden toe aan de node **dependencies**. Hiermee kunt u het eventhubs-client-pakket in uw toepassing gebruiken om berichten te lezen van het eindpunt dat compatibel is met Event Hubs:
   
    ```
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.8.2</version> 
    </dependency>
    ```
4. Sla het bestand pom.xml op en sluit het af.
5. Open het bestand read-d2c-messages\src\main\java\com\mycompany\app\App.java met een teksteditor.
6. Voeg de volgende **import**instructies toe aan het bestand:
   
    ```
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;
   
    import java.io.IOException;
    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.Collection;
    import java.util.concurrent.ExecutionException;
    import java.util.function.*;
    import java.util.logging.*;
    ```
7. Voeg de volgende variabelen op klasseniveau toe aan de **App**-klasse. Vervang **{youriothubkey}**, **{youreventhubcompatibleendpoint}** en **{youreventhubcompatiblename}** door de waarden die u eerder hebt genoteerd:
   
    ```
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```
8. Voeg de volgende **receiveMessages**-methode toe aan de **App**-klasse. Met deze methode maakt u een **EventHubClient**-exemplaar dat verbinding maakt met het Event Hubs-compatibele eindpunt. Vervolgens maakt u asynchroon een **PartitionReceiver**-exemplaar voor het lezen van een Event Hubs-partitie. Dit wordt continu uitgevoerd en de berichtgegevens worden afgedrukt totdat de toepassing wordt gesloten.
   
    ```
    private static EventHubClient receiveMessages(final String partitionId)
    {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      }
      catch(Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
        System.exit(1);
      }
      try {
        client.createReceiver( 
          EventHubClient.DEFAULT_CONSUMER_GROUP_NAME,  
          partitionId,  
          Instant.now()).thenAccept(new Consumer<PartitionReceiver>()
        {
          public void accept(PartitionReceiver receiver)
          {
            System.out.println("** Created receiver on partition " + partitionId);
            try {
              while (true) {
                Iterable<EventData> receivedEvents = receiver.receive(100).get();
                int batchSize = 0;
                if (receivedEvents != null)
                {
                  for(EventData receivedEvent: receivedEvents)
                  {
                    System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s", 
                      receivedEvent.getSystemProperties().getOffset(), 
                      receivedEvent.getSystemProperties().getSequenceNumber(), 
                      receivedEvent.getSystemProperties().getEnqueuedTime()));
                    System.out.println(String.format("| Device ID: %s", receivedEvent.getProperties().get("iothub-connection-device-id")));
                    System.out.println(String.format("| Message Payload: %s", new String(receivedEvent.getBody(),
                      Charset.defaultCharset())));
                    batchSize++;
                  }
                }
                System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId,batchSize));
              }
            }
            catch (Exception e)
            {
              System.out.println("Failed to receive messages: " + e.getMessage());
            }
          }
        });
      }
      catch (Exception e)
      {
        System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```
   
   > [!NOTE]
   > Deze methode maakt gebruik van een filter bij het maken van de ontvanger, zodat de ontvanger alleen de berichten leest die naar de IoT Hub zijn verzonden nadat de ontvanger actief is geworden. Dit is handig in een testomgeving, omdat u zo de huidige reeks berichten kunt zien. In een productieomgeving moet uw code er echter voor zorgen dat alle berichten worden verwerkt. Zie de zelfstudie [How to process IoT Hub device-to-cloud messages (IoT Hub apparaat-naar-cloud-berichten verwerken)][lnk-process-d2c-tutorial] voor meer informatie.
   > 
   > 
9. Wijzig de handtekening van de **main**-methode om de uitzondering als volgt op te nemen:
   
    ```
    public static void main( String[] args ) throws IOException
    ```
10. Voeg de volgende code aan de **belangrijkste** methode in de **App**-klasse. Deze code wordt gemaakt van de twee **EventHubClient** en **PartitionReceiver** exemplaren. U kunt de toepassing sluiten als u klaar bent met het verwerken van berichten:
    
    ```
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
    System.in.read();
    try
    {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    }
    catch (ServiceBusException sbe)
    {
      System.exit(1);
    }
    ```
    
    > [!NOTE]
    > Voor deze code wordt ervan uitgegaan dat u uw IoT-hub in de (gratis) F1-categorie hebt gemaakt. Een gratis IoT-hub heeft twee partities, genaamd "0" en "1".
    > 
    > 
11. Sla het bestand App.java op en sluit het af.
12. Als u de toepassing **read-d2c-messages** wilt creëren met behulp van Maven, geef dan de volgende opdracht in het opdrachtvenster in de map read-d2c-messages:
    
    ```
    mvn clean package -DskipTests
    ```

## Een gesimuleerde apparaattoepassing maken
In dit gedeelte maakt u een Java-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloud-berichten naar een IoT Hub verzendt.

1. Maak een nieuw Maven-project in de map iot-java-get-started die u hebt gemaakt in het gedeelte *Een apparaat-id maken* en noem dit **simulated-device**. Gebruik hierbij de volgende opdracht in uw opdrachtvenster. Let op: dit is één enkele, lange opdracht:
   
    ```
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```
2. Navigeer naar de nieuwe map simulated-device vanuit het opdrachtvenster.
3. Open het bestand pom.xml in de map simulated-device met een teksteditor en voeg de volgende afhankelijkheden toe aan de node **dependencies**. Hiermee kunt u het iothub-java-clients pakket in uw toepassing gebruiken om te communiceren met uw IoT Hub en om Java-objecten te serialiseren naar JSON:
   
    ```
    <dependency>
      <groupId>com.microsoft.azure.iothub-java-client</groupId>
      <artifactId>iothub-java-device-client</artifactId>
      <version>1.0.14</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```
4. Sla het bestand pom.xml op en sluit het af.
5. Open het bestand simulated-device\src\main\java\com\mycompany\app\App.java met een teksteditor.
6. Voeg de volgende **import**instructies toe aan het bestand:
   
    ```
    import com.microsoft.azure.iothub.DeviceClient;
    import com.microsoft.azure.iothub.IotHubClientProtocol;
    import com.microsoft.azure.iothub.Message;
    import com.microsoft.azure.iothub.IotHubStatusCode;
    import com.microsoft.azure.iothub.IotHubEventCallback;
    import com.microsoft.azure.iothub.IotHubMessageResult;
    import com.google.gson.Gson;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```
7. Voeg de volgende variabelen op klasseniveau toe aan de **App**-klasse. Vervang daarbij **{youriothubname}** door de naam van uw IoT-hub en **{yourdevicekey}** door de waarde van de apparaatsleutel die u hebt gegenereerd tijdens het gedeelte *Een apparaat-id maken*:
   
    ```
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.AMQPS;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Deze voorbeeldtoepassing gebruikt de variabele **protocol** bij het creëren van een **DeviceClient**-object. U kunt het HTTPS- of AMQPS-protocol gebruiken om te communiceren met de IoT-Hub.
8. Voeg de volgende geneste **TelemetryDataPoint**-klasse toe binnen de **App**-klasse om de telemetriegegevens op te geven die uw apparaat verzendt naar uw IoT-hub:
   
    ```
    private static class TelemetryDataPoint {
      public String deviceId;
      public double windSpeed;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Voeg de volgende geneste **EventCallback**-klasse toe binnen de **App**-klasse om de bevestigingsstatus weer te geven die wordt geretourneerd door de IoT-hub wanneer deze een bericht verwerkt van het gesimuleerde apparaat. Met deze methode wordt ook een bericht verstuurd aan de hoofdthread in de toepassing wanneer het bericht is verwerkt:
   
    ```
    private static class EventCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```
10. Voeg de volgende geneste **MessageSender**-klasse toe binnen de **App**-klasse. De **uitvoeren**-methode in deze klasse genereert voorbeeldtelemetrie die u kunt verzenden naar uw IoT-hub en die wacht op een bevestiging voordat het volgende bericht wordt verzonden:
    
    ```
    private static class MessageSender implements Runnable {
      public volatile boolean stopThread = false;
    
      public void run()  {
        try {
          double avgWindSpeed = 10; // m/s
          Random rand = new Random();
    
          while (!stopThread) {
            double currentWindSpeed = avgWindSpeed + rand.nextDouble() * 4 - 2;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.windSpeed = currentWindSpeed;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```
    
    Deze methode verzendt één seconde nadat de IoT-hub het vorige bericht erkent een nieuw apparaat-naar-cloud bericht. Het bericht bevat een JSON-geserialiseerd object met de apparaat-id en een willekeurig gegenereerd nummer om een windsnelheidssensor te simuleren.
11. Vervang de **belangrijkste** methode door de volgende code die een thread maakt om apparaat-naar-cloudberichten te verzenden naar uw IoT-hub:
    
    ```
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.close();
    }
    ```
12. Sla het bestand App.java op en sluit het af.
13. Als u de toepassing **simulated-device** wilt creëren met behulp van Maven, geef dan de volgende opdracht in het opdrachtvenster in de map simulated-device:
    
    ```
    mvn clean package -DskipTests
    ```

> [!NOTE]
> Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd. Bij de productiecode moet u een beleid voor opnieuw proberen implementeren (zoals exponentieel uitstel), zoals aangegeven in het MSDN-artikel [Transient Fault Handling ][lnk-transient-faults] (Afhandeling van tijdelijke fouten).
> 
> 

## De toepassingen uitvoeren
U kunt nu de toepassingen gaan uitvoeren.

1. Voer bij een opdrachtprompt in de map read-d2c de volgende opdracht uit om de eerste partitie in uw IoT-hub te kunnen volgen:
   
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```
   
    ![De Java-clienttoepassing voor IoT Hub-services voor het bewaken van berichten die van het apparaat naar de cloud gaan][7]
2. Voer bij een opdrachtprompt in de map simulated-device de volgende opdracht uit om telemetriegegevens naar uw IoT-hub te verzenden:
   
    ```
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```
   
    ![De Java-clienttoepassing voor IoT Hub-apparaten voor het verzenden van berichten van het apparaat naar de cloud][8]
3. De tegel **Usage** in de [Azure Portal][lnk-portal] toont het aantal berichten dat is verzonden naar de hub:
   
    ![De tegel Usage in de Azure-portal met het aantal berichten dat is verzonden naar IoT Hub][43]

## Volgende stappen
In deze handleiding, hebt u een nieuwe IoT-hub geconfigureerd in de portal en vervolgens hebt u een apparaat-id gemaakt in het id-register van de hub. U hebt deze apparaat-id gebruikt om de gesimuleerde apparaattoepassing in staat te stellen om apparaat-naar-cloud-berichten te verzenden naar de hub. Ook hebt een app gemaakt die de berichten weergeeft die worden ontvangen door de hub. 

Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:

* [Connecting your device (Uw apparaat verbinden)][lnk-connect-device]
* [Getting started with device management (Aan de slag met apparaatbeheer)][lnk-device-management]
* [Getting started with the Gateway SDK (Aan de slag met de Gateway-SDK)][lnk-gateway-SDK]

Raadpleeg de zelfstudie [Process device-to-cloud messages (Apparaat-naar-cloud-berichten verwerken)][lnk-process-d2c-tutorial] voor meer informatie over het uitbreiden van uw IoT-oplossing en het op schaal verwerken van apparaat-naar-cloud-berichten.

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identiteit]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/java-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-device-management-get-started.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/


<!--HONumber=Oct16_HO3-->


