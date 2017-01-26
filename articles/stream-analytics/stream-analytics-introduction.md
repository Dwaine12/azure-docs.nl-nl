---
title: Inleiding tot Stream Analytics | Microsoft Docs
description: Lees over Stream Analytics, een beheerde service waarmee u streaminggegevens van het Internet of Things (IoT) in realtime kun analyseren.
keywords: analyse als een service, beheerde services, verwerking van streams, analyse van streams, wat is analyse van streams
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 09/26/2016
ms.author: jeffstok
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 2b5d8c4a2bc20bee96f82d6d6394fda983d8a38a


---
# <a name="what-is-stream-analytics"></a>Wat is een Stream Analytics?
Azure Stream Analytics is een volledig beheerde, kosteneffectieve engine voor de verwerking van realtime-gebeurtenissen, waarmee u veel inzicht in gegevens kunt krijgen. Met Stream Analytics kunt u eenvoudig realtime analytische berekeningen configureren voor gegevensstreaming van apparaten, sensoren, websites, sociale media, toepassingen, infrastructuursystemen en meer.

Met slechts enkele klikken in de Azure-portal kunt u een Stream Analytics-taak maken die de invoerbron van de streaminggegevens, de uitvoerlocatie voor de resultaten van de taak en een gegevenstransformatie, uitgedrukt in een SQL-achtige taal bevat. U kunt de schaal/snelheid van de taak in de Azure-portal bewaken en aanpassen, om van enkele kilobytes tot een gigabyte of meer aan verwerkte gebeurtenissen per seconde te schalen.

Stream Analytics maakt gebruik van jarenlange inspanningen van Microsoft Research op het gebied van de ontwikkeling van uiterst afgestemde streamingengines voor tijdgebonden verwerking, evenals taalintegraties voor intuïtieve specificaties daarvan.

## <a name="what-can-i-use-stream-analytics-for"></a>Waarvoor kan ik Stream Analytics gebruiken?
Dagelijks worden enorme hoeveelheden gegevens met hoge snelheid via de kabel getransporteerd. Organisaties die deze streaminggegevens in realtime kunnen verwerken en inzetten, kunnen hun efficiëntie aanzienlijk verbeteren en zich onderscheiden in de markt. Scenario's van de analyse van realtime-gegevens vindt u in alle sectoren: aangepaste analyse van realtime-handel in aandelen en waarschuwingen van financiële diensten, realtime-fraudedetectie, diensten voor gegevens- en identiteitsbescherming, betrouwbare opname en analyse van gegevens die worden gegenereerd door sensoren en aansturingen in fysieke objecten (Internet of Things of IoT), clickstream-analyse voor websites, CRM-toepassingen (Customer Relationship Management) die waarschuwingen genereren wanneer de klantervaring binnen een periode is gedegradeerd. Bedrijven zoeken altijd de meest flexibele, betrouwbare en rendabele manier om dergelijke gegevensanalyse van realtime-gebeurtenisstromen uit te voeren in een uiterst concurrerende moderne zakenwereld.

## <a name="key-capabilities-and-benefits"></a>Belangrijkste mogelijkheden en voordelen
* **Gebruiksgemak:** Stream Analytics ondersteunt een eenvoudig, declaratief querymodel voor het beschrijven van transformaties. Voor een optimaal gebruiksgemak gebruikt Stream Analytics een T-SQL-variant, en klanten hoeven zich niet te bekommeren om de technische complexiteit van stroomverwerkingssystemen. Met de [querytaal van Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) in de queryeditor van de browser beschikt u over een intelligente functie voor automatisch aanvullen, waarmee u snel en eenvoudig tijdreeksquery’s, waaronder tijdelijke joins, statistische functies in vensters, tijdelijke filters, en andere veelvoorkomende bewerkingen zoals joins, statistische functies, projecties en filters, kunt implementeren. Daarnaast kunt u de query’s in de browser testen met een voorbeeldgegevensbestand, voor een snelle, herhaaldelijke ontwikkeling.  
* **Schaalbaarheid:** met Stream Analytics kan een hoge doorvoer van gebeurtenissen tot wel 1 GB per seconde worden afgehandeld. Dankzij integratie met [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) en [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/) kan de oplossing miljoenen gebeurtenissen per seconde opnemen, afkomstig van verbonden apparaten, clickstreams, logboekbestanden, enzovoort. Daarvoor wordt in Stream Analytics gebruikgemaakt van de partitioneringswerking van Event Hubs, die 1 MB/s per partitie kan opleveren. Gebruikers kunnen de berekening partitioneren in een aantal logische stappen binnen de querydefinitie, en elke stap kan verder worden gepartitioneerd om schaalbaarheid te vergroten.  
* **Betrouwbaarheid, herhaalbaarheid en snel herstel:** een beheerde service in de cloud, Stream Analytics, helpt gegevensverlies voorkomen en biedt via ingebouwde herstelfuncties zakelijke continuïteit in geval van problemen. Dankzij het vermogen om de interne toestand te handhaven, biedt de service herhaalbare resultaten zodat gebeurtenissen kunnen worden gearchiveerd en verwerking later opnieuw kan worden toegepast, en altijd dezelfde resultaten worden verkregen. Hierdoor kunnen klanten teruggaan in de tijd en berekeningen onderzoeken terwijl de hoofdoorzaak wordt onderzocht, wat-als-analyse wordt uitgevoerd enzovoort.  
* **Lage kosten:** Als een cloudservice is Stream Analytics geoptimaliseerd om gebruikers een realtime-analyseoplossing te bieden die zowel qua implementatie als qua onderhoud niet duur is. De service is zo gemaakt dat u betaalt voor gebruik op basis van het aantal gebruikte streamingeenheden en de hoeveelheid gegevens die door het systeem wordt verwerkt. Gebruik wordt berekend op basis van het aantal gebeurtenissen dat wordt verwerkt en de hoeveelheid computercapaciteit binnen het cluster die nodig is om de respectieve Stream Analytics-taken af te handelen.  
* **Referentiegegevens:** Stream Analytics biedt gebruikers de mogelijkheid om referentiegegevens op te geven en te gebruiken. Dit kunnen historische gegevens zijn of gewone niet-streaminggegevens die minder vaak worden gewijzigd. Het systeem vereenvoudigt het gebruik van referentiegegevens zodat ze kunnen worden behandeld als elke andere gebeurtenisstroom, om te worden samengevoegd met andere gebeurtenisstromen die in realtime worden opgenomen om transformaties uit te voeren.  
* **Door de gebruiker gedefinieerde functies:** Stream Analytics kan worden geïntegreerd in Azure Machine Learning om functieaanroepen te definiëren in de Machine Learning-service als onderdeel van een Stream Analytics-query. Hiermee worden de mogelijkheden van Stream Analytics uitgebreid om gebruik te maken van bestaande Azure Machine Learning-oplossingen. Raadpleeg de [zelfstudie over Machine Learning-integratie](stream-analytics-machine-learning-integration-tutorial.md) voor meer informatie hierover.
* **Connectiviteit:** Stream Analytics maakt rechtstreeks verbinding met Azure Event Hubs en Azure IoT Hubs voor opname van streams, en met de Azure Blob-service voor opname van historische gegevens. Resultaten kunnen vanuit Stream Analytics worden geschreven naar Azure Storage Blobs of Tables, Azure SQL DB, Azure Data Lake Stores, DocumentDB, Event Hubs, Azure Service Bus Topics, of Queues. Ze kunnen ook worden geschreven naar Power BI, waar ze verder kunnen worden verwerkt door werkstromen die via [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) in batchanalyses worden gebruikt of opnieuw als een reeks gebeurtenissen worden verwerkt. Wanneer Event Hubs wordt gebruikt, kunnen meerdere Stream Analytics met andere gegevensbronnen en verwerkingsengines worden gecombineerd zonder het streaming-karakter van de berekeningen te verliezen.  

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
U hebt kennisgemaakt met Stream Analytics, een beheerde service voor streaminganalyse van gegevens afkomstig van het Internet of Things. Raadpleeg de volgende onderwerpen voor meer informatie over deze service:

* [Aan de slag met Azure Stream Analytics](stream-analytics-get-started.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)




<!--HONumber=Nov16_HO2-->


