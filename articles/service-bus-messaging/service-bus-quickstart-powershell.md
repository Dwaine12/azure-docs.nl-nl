---
title: Snelstart - Berichten verzenden naar en ontvangen van Azure Service Bus | Microsoft Docs
description: In deze snelstart leert u hoe u met behulp van PowerShell en de .NET Standard-client Service Bus-berichten verzendt en ontvangt
services: service-bus-messaging
author: spelluru
manager: timlt
ms.service: service-bus-messaging
ms.devlang: dotnet
ms.topic: quickstart
ms.custom: mvc
ms.date: 09/22/2018
ms.author: spelluru
ms.openlocfilehash: 2669b3ad9abc2370b4ecb66596d6edde17c82ddd
ms.sourcegitcommit: da3459aca32dcdbf6a63ae9186d2ad2ca2295893
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/07/2018
ms.locfileid: "51242429"
---
# <a name="quickstart-send-and-receive-messages-using-azure-powershell-and-net"></a>Snelstart: Berichten verzenden en ontvangen met Azure PowerShell en .NET

Microsoft Azure Service Bus is een geïntegreerde berichtenbroker voor bedrijven die voor een beveiligde en absoluut betrouwbare berichtenuitwisseling zorgt. In een typisch Service Bus-scenario hebt u gewoonlijk te maken met het van elkaar loskoppelen van twee of meer toepassingen, services of processen en het overbrengen van status- of gegevenswijzigingen. Dergelijke scenario's kunnen betrekking hebben op het plannen van meerdere batchtaken in andere toepassingen of services, of het activeren van de orderafhandeling. Een detailhandelsbedrijf kan bijvoorbeeld gegevens van het verkooppunt naar een back-office of regionaal distributiecentrum verzenden voor het aanvullen en bijwerken van de voorraad. In dit scenario verzendt en ontvangt de client-app berichten naar en van een Service Bus-wachtrij.

![wachtrij](./media/service-bus-quickstart-powershell/quick-start-queue.png)

In deze quickstart wordt beschreven hoe u berichten naar een Service Bus-wachtrij verzendt en van de wachtrij ontvangt. U gebruikt daarbij PowerShell om een berichtennaamruimte te maken en binnen deze naamruimte een wachtrij te maken. Ook wordt beschreven hoe u de autorisatiereferenties binnen die naamruimte kunt verkrijgen. De procedure laat vervolgens zien hoe u berichten naar deze wachtrij verzendt en van de wachtrij ontvangt met behulp van de [.NET Standard-bibliotheek](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus).

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account][] aan voordat u begint.

## <a name="prerequisites"></a>Vereisten

Het volgende moet zijn geïnstalleerd om deze zelfstudie te voltooien:

- [Visual Studio 2017 update 3 (versie 15.3, 26730.01)](https://www.visualstudio.com/vs) of hoger.
- [NET Core SDK](https://www.microsoft.com/net/download/windows), versie 2.0 of later.

Voor deze snelstart moet u de nieuwste versie van Azure PowerShell uitvoeren. Als u Azure PowerShell wilt installeren of upgraden, raadpleegt u [Azure PowerShell installeren en configureren][].

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.

1. Installeer eerst de PowerShell-module van Service Bus, als u dat nog niet hebt gedaan:

   ```azurepowershell-interactive
   Install-Module AzureRM.ServiceBus
   ```

2. Voer de volgende opdracht uit om u aan te melden bij Azure:

   ```azurepowershell-interactive
   Login-AzureRmAccount
   ```

3. Geef de volgende opdrachten om de context van het huidige abonnement in te stellen of het actieve abonnement te bekijken:

   ```azurepowershell-interactive
   Select-AzureRmSubscription -SubscriptionName "MyAzureSubName" 
   Get-AzureRmContext
   ```

## <a name="provision-resources"></a>Resources inrichten

Geef bij de PowerShell-prompt de volgende opdrachten om Service Bus-resources in te richten. Zorg dat u alle tijdelijke aanduidingen vervangt door de juiste waarden:

```azurepowershell-interactive
# Create a resource group 
New-AzureRmResourceGroup –Name my-resourcegroup –Location eastus

# Create a Messaging namespace
New-AzureRmServiceBusNamespace -ResourceGroupName my-resourcegroup -NamespaceName namespace-name -Location eastus

# Create a queue 
New-AzureRmServiceBusQueue -ResourceGroupName my-resourcegroup -NamespaceName namespace-name -Name queue-name -EnablePartitioning $False

# Get primary connection string (required in next step)
Get-AzureRmServiceBusKey -ResourceGroupName my-resourcegroup -Namespace namespace-name -Name RootManageSharedAccessKey
```

Wanneer de cmdlet `Get-AzureRmServiceBusKey` is uitgevoerd, kopieert en plakt u de verbindingstekenreeks en de naam van de wachtrij die u hebt geselecteerd, naar een tijdelijke locatie, zoals Kladblok. U hebt deze gegevens nodig in de volgende stap.

## <a name="send-and-receive-messages"></a>Berichten verzenden en ontvangen

Wanneer de naamruimte en wachtrij zijn gemaakt en u over de benodigde referenties beschikt, kunt u berichten gaan verzenden en ontvangen. U kunt de code in [deze GitHub-voorbeeldmap](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/GettingStarted/BasicSendReceiveQuickStart) bestuderen.

Ga als volgt te werk om de code uit te voeren:

1. Kloon de [Service Bus GitHub-opslagplaats](https://github.com/Azure/azure-service-bus/) met behulp van de volgende opdracht:

   ```shell
   git clone https://github.com/Azure/azure-service-bus.git
   ```

3. Navigeer naar de voorbeeldmap `azure-service-bus\samples\DotNet\GettingStarted\BasicSendReceiveQuickStart\BasicSendReceiveQuickStart`.

4. Als u dit nog niet hebt gedaan, haalt u de verbindingsreeks op met behulp van de volgende PowerShell-cmdlet. Zorg dat u `my-resourcegroup`  en  `namespace-name` vervangt door uw specifieke waarden: 

   ```azurepowershell-interactive
   Get-AzureRmServiceBusKey -ResourceGroupName my-resourcegroup -Namespace namespace-name -Name RootManageSharedAccessKey
   ```

5.  Typ de volgende opdracht bij de PowerShell-prompt:

   ```shell
   dotnet build
   ```

6.  Navigeer naar de map `bin\Debug\netcoreapp2.0`.

7.  Typ de volgende opdracht om het programma uit te voeren. Zorg ervoor dat u `myConnectionString` vervangt door de waarde die u eerder hebt verkregen, en vervang `myQueueName` door de naam van de wachtrij die u hebt gemaakt:

   ```shell
   dotnet BasicSendReceiveQuickStart.dll -ConnectionString "myConnectionString" -QueueName "myQueueName"
   ``` 

8. Bekijk tien berichten die naar de wachtrij zijn verzonden en vervolgens van de wachtrij zijn ontvangen:

   ![programma-uitvoer](./media/service-bus-quickstart-powershell/dotnet.png)

## <a name="clean-up-resources"></a>Resources opschonen

Voer de volgende opdracht uit om de resourcegroep, de naamruimte en alle gerelateerde resources te verwijderen:

```powershell-interactive
Remove-AzureRmResourceGroup -Name my-resourcegroup
```

## <a name="understand-the-sample-code"></a>De voorbeeldcode begrijpen

Deze sectie bevat meer informatie over de werking van de voorbeeldcode. 

### <a name="get-connection-string-and-queue"></a>Verbindingsreeks en wachtrij ophalen

De verbindingsreeks en de naam van de wachtrij worden als opdrachtregelargumenten doorgegeven aan de methode `Main()`. `Main()` declareert twee tekenreeksvariabelen die deze waarden kunnen omvatten:

```csharp
static void Main(string[] args)
{
    string ServiceBusConnectionString = "";
    string QueueName = "";

    for (int i = 0; i < args.Length; i++)
    {
        var p = new Program();
        if (args[i] == "-ConnectionString")
        {
            Console.WriteLine($"ConnectionString: {args[i+1]}");
            ServiceBusConnectionString = args[i + 1]; 
        }
        else if(args[i] == "-QueueName")
        {
            Console.WriteLine($"QueueName: {args[i+1]}");
            QueueName = args[i + 1];
        }                
    }

    if (ServiceBusConnectionString != "" && QueueName != "")
        MainAsync(ServiceBusConnectionString, QueueName).GetAwaiter().GetResult();
    else
    {
        Console.WriteLine("Specify -Connectionstring and -QueueName to execute the example.");
        Console.ReadKey();
    }                            
}
```
 
De methode `Main()` start vervolgens de asynchrone berichtenlus `MainAsync()`.

### <a name="message-loop"></a>Berichtenlus

De methode MainAsync() maakt een wachtrijclient met de opdrachtregelargumenten, roept een ontvangende berichtenhandler met de naam `RegisterOnMessageHandlerAndReceiveMessages()` aan, en verzendt de berichtenreeks:

```csharp
static async Task MainAsync(string ServiceBusConnectionString, string QueueName)
{
    const int numberOfMessages = 10;
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

    Console.WriteLine("======================================================");
    Console.WriteLine("Press any key to exit after receiving all the messages.");
    Console.WriteLine("======================================================");

    // Register QueueClient's MessageHandler and receive messages in a loop
    RegisterOnMessageHandlerAndReceiveMessages();

    // Send Messages
    await SendMessagesAsync(numberOfMessages);

    Console.ReadKey();

    await queueClient.CloseAsync();
}
```

De methode `RegisterOnMessageHandlerAndReceiveMessages()` stelt gewoon enkele opties voor de berichtenhandler in en roept vervolgens de methode `RegisterMessageHandler()` van de wachtrijclient aan, waardoor het ontvangen begint:

```csharp
static void RegisterOnMessageHandlerAndReceiveMessages()
{
    // Configure the MessageHandler Options in terms of exception handling, number of concurrent messages to deliver etc.
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        // Maximum number of Concurrent calls to the callback `ProcessMessagesAsync`, set to 1 for simplicity.
        // Set it according to how many messages the application wants to process in parallel.
        MaxConcurrentCalls = 1,

        // Indicates whether MessagePump should automatically complete the messages after returning from User Callback.
        // False below indicates the Complete will be handled by the User Callback as in `ProcessMessagesAsync` below.
        AutoComplete = false
    };

    // Register the function that will process messages
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
} 
```

### <a name="send-messages"></a>Berichten verzenden

De bewerkingen voor het maken en verzenden van berichten vinden in de methode `SendMessagesAsync()` plaats:

```csharp
static async Task SendMessagesAsync(int numberOfMessagesToSend)
{
    try
    {
        for (var i = 0; i < numberOfMessagesToSend; i++)
        {
            // Create a new message to send to the queue
            string messageBody = $"Message {i}";
            var message = new Message(Encoding.UTF8.GetBytes(messageBody));

            // Write the body of the message to the console
            Console.WriteLine($"Sending message: {messageBody}");

            // Send the message to the queue
            await queueClient.SendAsync(message);
        }
    }
    catch (Exception exception)
    {
        Console.WriteLine($"{DateTime.Now} :: Exception: {exception.Message}");
    }
}
```

### <a name="process-messages"></a>Berichten verwerken

De methode `ProcessMessagesAsync()` bevestigt, verwerkt en voltooit de ontvangst van de berichten:

```csharp
static async Task ProcessMessagesAsync(Message message, CancellationToken token)
{
    // Process the message
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");

    // Complete the message so that it is not received again.
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
}
```

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt u een Service Bus-naamruimte en andere resources gemaakt die zijn vereist voor het verzenden en ontvangen van berichten in een wachtrij. Voor meer informatie over het schrijven van code voor het verzenden en ontvangen van berichten, gaat u naar de volgende zelfstudie over Service Bus:

> [!div class="nextstepaction"]
> [Inventaris bijwerken met behulp van Azure PowerShell](./service-bus-tutorial-topics-subscriptions-powershell.md)

[gratis account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
[Azure PowerShell installeren en configureren]: /powershell/azure/install-azurerm-ps