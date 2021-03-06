---
title: De Azure Cosmos DB Emulator-certificaten exporteren
description: Wanneer u ontwikkelt in talen en runtimes waarvoor het Windows-certificaatarchief niet wordt gebruikt, moet u de SSL-certificaten exporteren en beheren. Dit bericht bevat stapsgewijze instructies.
services: cosmos-db
keywords: Azure Cosmos DB Emulator
author: David-Noble-at-work
ms.service: cosmos-db
ms.topic: tutorial
ms.date: 06/06/2017
ms.author: danoble
ms.openlocfilehash: b7a6649fab8b0203c20b93bee9e941614828a99b
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53091795"
---
# <a name="export-the-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>De Azure Cosmos DB Emulator-certificaten exporteren voor gebruik met Java, Python en Node.js

[**De emulator downloaden**](https://aka.ms/cosmosdb-emulator)

De Azure Cosmos DB Emulator is een lokale omgeving waarin de Azure Cosmos DB-service wordt geëmuleerd voor ontwikkelingsdoeleinden, waaronder het gebruik van SSL-verbindingen. In dit bericht kunt u zien hoe u de SSL-certificaten kunt exporteren voor gebruik in talen en runtimes die niet kunnen integreren met het Windows-certificaatarchief, zoals Java, dat een eigen [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) gebruikt, Python dat [socketwrappers](https://docs.python.org/2/library/ssl.html) gebruikt en Node.js dat [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback) gebruikt. Meer informatie over de emulator vindt u in [Azure Cosmos DB Emulator gebruiken voor ontwikkeling en tests](./local-emulator.md).

Deze zelfstudie bestaat uit de volgende taken:

> [!div class="checklist"]
> * Certificaten rouleren
> * SSL-certificaat exporteren
> * Meer informatie over het gebruik van het certificaat in Java, Python en Node.js

## <a name="certification-rotation"></a>Certificering rouleren

Certificaten in Azure Cosmos DB Local Emulator worden gegenereerd wanneer de emulator de eerste keer wordt uitgevoerd. Er zijn twee certificaten. Eén wordt gebruikt voor het maken van verbinding met de lokale emulator en één voor het beheren van geheimen in de emulator. Het certificaat dat u wilt exporteren, is het verbindingscertificaat met de beschrijvende naam DocumentDBEmulatorCertificate.

Beide certificaten kunnen opnieuw worden gegenereerd door te klikken op **Gegevens herstellen**, zoals hieronder wordt weergegeven, vanuit Azure Cosmos DB Emulator dat actief is in het Windows-systeemvak. Als u de certificaten opnieuw genereert en deze hebt geïnstalleerd in het Java-certificaatarchief of ze ergens anders gebruikt, moet u deze bijwerken. Anders maakt de toepassing geen verbinding meer met de lokale emulator.

![Gegevens herstellen met de lokale emulator van Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-to-export-the-azure-cosmos-db-ssl-certificate"></a>Het SSL-certificaat van Azure Cosmos DB exporteren

1. Start het Windows-certificaatbeheer door certlm.msc uit te voeren en ga naar de map Persoonlijk->Certificaten om het certificaat met de beschrijvende naam **DocumentDbEmulatorCertificate** te openen.

    ![Stap 1 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Klik op **Details** en klik op **OK**.

    ![Stap 2 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Klik op **Kopiëren naar bestand...** .

    ![Stap 3 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Klik op **Volgende**.

    ![Stap 4 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Klik op **Nee, persoonlijke sleutel niet exporteren** en klik op **Volgende**.

    ![Stap 5 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Klik op **Base-64 encoded X.509 (.CER)** en klik op **Volgende**.

    ![Stap 6 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Geef het certificaat een naam, in dit geval **documentdbemulatorcert**, en klik op **Volgende**.

    ![Stap 7 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Klik op **Voltooien**.

    ![Stap 8 van exporteren met lokale Azure DB Cosmos-emulator](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-to-use-the-certificate-in-java"></a>Het certificaat gebruiken in Java

Wanneer u Java- of MongoDB-toepassingen uitvoert waarvoor de Java-client wordt gebruikt, is het makkelijker om het certificaat te installeren in het standaardcertificaatarchief van Java dan om de vlaggen "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" door te geven. De opgenomen [Java-voorbeeldtoepassing](https://localhost:8081/_explorer/index.html) is bijvoorbeeld afhankelijk van het standaardcertificaatarchief.

Volg de instructies in [Een certificaat toevoegen aan het Java CA certificaatarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store) om het X.509-certificaat te importeren in het standaardcertificaatarchief van Java. Vergeet niet dat u in de map %JAVA_HOME% werkt wanneer u keytool uitvoert.

Wanneer het certificaat CosmosDBEmulatorCertificate is geïnstalleerd, kan de toepassing verbinding maken met de lokale Azure Cosmos DB-emulator en deze gebruiken. Als u problemen blijft ondervinden, leest u het artikel [Fouten in SSL/TLS-verbindingen opsporen](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html). Het certificaat is waarschijnlijk niet geïnstalleerd in het archief %JAVA_HOME%/jre/lib/security/cacerts store. Als u bijvoorbeeld meerdere versies van Java hebt geïnstalleerd, kan de toepassing een ander cacerts-archief gebruiken dan het archief dat u hebt bijgewerkt.

## <a name="how-to-use-the-certificate-in-python"></a>Het certificaat gebruiken in Python

Standaard wordt door de [Python SDK (versie 2.0.0 of hoger)](sql-api-sdk-python.md) voor de SQL-API niet het SSL-certificaat gebruikt bij het maken van verbinding met de lokale emulator. Als u echter wel SSL-validatie wilt gebruiken, volgt u de voorbeelden in de documentatie voor [Python-socketwrappers](https://docs.python.org/2/library/ssl.html).

## <a name="how-to-use-the-certificate-in-nodejs"></a>Het certificaat gebruiken in Node.js

Standaard wordt door de [Node.js SDK (versie 1.10.1 of hoger)](sql-api-sdk-node.md) voor de SQL-API niet het SSL-certificaat gebruikt bij het maken van verbinding met de lokale emulator. Als u echter wel SSL-validatie wilt gebruiken, volgt u de voorbeelden in de [Node.js-documentatie](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende gedaan:

> [!div class="checklist"]
> * Certificaten gerouleerd
> * Het SSL-certificaat geëxporteerd
> * Geleerd over het gebruik van het certificaat in Java, Python en Node.js

U kunt nu doorgaan naar de sectie Concepten voor meer informatie over Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Instelbare gegevensconsistentieniveaus in Azure Cosmos DB](../cosmos-db/consistency-levels.md)
