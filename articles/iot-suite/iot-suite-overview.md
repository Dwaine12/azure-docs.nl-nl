---
title: Overzicht van Microsoft Azure IoT Suite | Microsoft Docs
description: Overzicht van hoe Azure IoT Suite vooraf geconfigureerde oplossingen voor het Internet of Things biedt voor het verzamelen, analyseren en opslaan van gegevens, voor het bieden van visualisaties en voor integratie met andere systemen.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: dobett
translationtype: Human Translation
ms.sourcegitcommit: 1a6dd35278f0a4a4f972642c40a0976986dd79ae
ms.openlocfilehash: 16930bbdc08bdccfdc150d8f25eaa6cec10595e4


---
# <a name="what-is-azure-iot-suite"></a>Wat is Azure IoT Suite?
De Azure Internet of Things-services (IoT) bieden een breed scala aan mogelijkheden. Met deze hoogwaardige services kunt u het volgende doen:

* Gegevens van apparaten verzamelen
* Gegevensstromen in beweging analyseren
* Grote gegevenssets opslaan en er query’s op uitvoeren
* Gegevens in realtime en historische gegevens visualiseren
* Integraties met back-officesystemen uitvoeren

Om deze mogelijkheden te kunnen bieden, bevatten Azure IoT Suite-pakketten meerdere Azure-services met aangepaste extensies als *vooraf geconfigureerde oplossingen*. Deze vooraf geconfigureerde oplossingen zijn basisimplementaties van algemene patronen van IoT-oplossingen die u helpen de tijd voor het leveren van uw IoT-oplossingen te verkorten. Met behulp van de [IoT-SDK’s][lnk-SDK's] kunt u deze oplossingen aanpassen en uitbreiden om aan uw eigen behoeften tegemoet te komen. U kunt deze oplossingen gebruiken als voorbeelden of sjablonen als u nieuwe IoT-oplossingen ontwikkelt.

De volgende video toont een inleiding tot Azure IoT Suite:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Azure IoT-services in Azure IoT Suite
De vooraf geconfigureerde oplossingen gebruiken doorgaans de volgende services:

* Het hart van Azure IoT Suite wordt gevormd door de service [Azure IoT Hub][lnk-iot-hub]. Deze service verzorgt de berichtgeving van het apparaat naar de cloud en van de cloud naar het apparaat, en fungeert als toegangspoort tot de cloud en de andere belangrijke IoT Suite-services. Door deze service kunt u op grote schaal berichten ontvangen van uw apparaten en opdrachten naar uw apparaten verzenden.
* [Azure Stream Analytics][Ink-asa] biedt de mogelijkheid om gegevens in beweging te analyseren. IoT Suite maakt gebruik van deze service voor het verwerken van binnenkomende telemetriegegevens, het uitvoeren van aggregatiebewerkingen en het detecteren van gebeurtenissen. De vooraf geconfigureerde maken ook gebruik van Stream Analytics voor het verwerken van informatieve berichten met gegevens, zoals metagegevens of reacties van apparaten op opdrachten. De oplossingen maken gebruik van Stream Analytics om de berichten van uw apparaten te verwerken en deze berichten bij andere services af te leveren.
* [Azure Storage][lnk-azure-storage] en [Azure DocumentDB][lnk-document-db] bieden de mogelijkheid om gegevens op te slaan. De vooraf geconfigureerde oplossingen gebruiken Blob Storage voor het opslaan van telemetriegegevens en om deze beschikbaar te maken voor analyse. De oplossingen gebruiken DocumentDB om metagegevens van apparaten op te slaan en DocumentDB zorgt er tevens voor dat de oplossingen gebruik kunnen maken van mogelijkheden voor apparaatbeheer.
* [Azure Web Apps][lnk-web-apps] en [Microsoft Power BI][lnk-power-bi] bieden de mogelijkheden om gegevens te visualiseren. Door de flexibiliteit van Power BI kunt u snel uw eigen interactieve dashboards bouwen die gebruikmaken van de gegevens van IoT Suite.

Zie voor een overzicht van de architectuur van een typische IoT-oplossing [Microsoft Azure en het Internet of Things (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>Vooraf geconfigureerde oplossingen
IoT Suite bevat vooraf geconfigureerde oplossingen zodat u snel aan de slag kunt met algemene IoT-scenario's die met Azure IoT Suite mogelijk zijn, zoals *externe controle* en *voorspeld onderhoud*. U kunt deze oplossingen implementeren in uw Azure-abonnement en vervolgens een volledig end-to-end-IoT-scenario uitvoeren.

## <a name="next-steps"></a>Volgende stappen
Nu u een overzicht hebt van wat IoT Suite kan doen en wat de belangrijkste onderdelen zijn, raadpleegt u [What are the Azure IoT preconfigured solutions? (Wat zijn de vooraf geconfigureerde oplossingen in Azure IoT)][lnk-what-are-preconfig] voor meer informatie over de vooraf geconfigureerde oplossingen in IoT Suite.

[lnk-SDK's]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Ink-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md



<!--HONumber=Nov16_HO3-->


