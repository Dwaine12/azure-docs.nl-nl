---
title: Partitionering en horizontaal schalen in Azure Cosmos DB
description: Meer informatie over hoe partitionering werkt in Azure Cosmos DB, over het configureren van de partitionering en partitioneren van sleutels en hoe de juiste partitiesleutel voor uw toepassing kiest.
author: aliuy
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 10/30/2018
ms.author: andrl
ms.openlocfilehash: 5dd1926496351f5bbfe8e5b3e4d1e0b68e82d272
ms.sourcegitcommit: ba4570d778187a975645a45920d1d631139ac36e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/08/2018
ms.locfileid: "51283390"
---
# <a name="partitioning-and-horizontal-scaling-in-azure-cosmos-db"></a>Partitionering en horizontaal schalen in Azure Cosmos DB

Dit artikel wordt uitgelegd over fysieke en logische partities in Azure Cosmos DB en de aanbevolen procedures voor het schalen en te partitioneren. 

## <a name="logical-partitions"></a>Logische partities

Een logische partitie bestaat uit een reeks items met dezelfde partitiesleutel. Neem bijvoorbeeld een container waarin alle items bevatten een `City` eigenschap, dan hebt u kunt `City` als de partitiesleutel voor de container. Groepen van items met specifieke waarden voor de `City` , zoals "Londen", "Parijs", "NYC" enzovoort een afzonderlijke logische partitie vormen.

In Azure Cosmos DB is een container de fundamentele eenheid van de schaalbaarheid. De gegevens die zijn toegevoegd aan de container en de doorvoer die u in te op de container richten worden automatisch (horizontaal) gepartitioneerde in een set met logische partities. Ze worden gepartitioneerd op basis van de partitiesleutel die u opgeeft voor de Cosmos-container. Zie voor meer informatie, [opgeven van de partitiesleutel voor de container van Cosmos](how-to-create-container.md) artikel.

Een logische partitie definieert het bereik van databasetransacties. U kunt items in een logische partitie bijwerken met behulp van een transactie met snapshot-isolatie.

Wanneer nieuwe items worden toegevoegd aan de container of als de doorvoer die is ingericht voor de container wordt verhoogd, worden nieuwe logische partities worden transparant gemaakt door het systeem.

## <a name="physical-partitions"></a>Fysieke partities

Een Cosmos-container wordt geschaald door de gegevens en de doorvoer te verdelen over een groot aantal logische partities. Intern, een of meer logische partities zijn toegewezen aan een **resourcepartitie** die bestaat uit een verzameling van replica's ook aangeduid als een replica-set. Elke replicaset als host fungeert voor een exemplaar van de Cosmos-database-engine. Een replica-set maakt de gegevens die zijn opgeslagen in de resourcepartitie duurzame, maximaal beschikbare en consistent. Een resourcepartitie biedt ondersteuning voor een vaste en maximale hoeveelheid opslag en ru's. Elke replica die bestaat uit de resourcepartitie neemt over van de opslag van inhoud. En alle replica's van een resourcepartitie gezamenlijk ondersteuning voor de doorvoer die is toegewezen aan de resourcepartitie. De volgende afbeelding ziet u hoe logische partities zijn toegewezen aan de fysieke partities die wereldwijd worden gedistribueerd:

![Partitioneren van Azure Cosmos DB](./media/partition-data/logical-partitions.png)

Ingerichte doorvoer voor een container wordt evenredig verdeeld over de fysieke partities. Daarom kan 'hot' partities maken om een partitie belangrijke ontwerp dat de doorvoer van aanvragen niet gelijkmatig verdelen. Hot-partities kunnen resulteren in gelden enkele beperkingen en inefficiënt gebruik van de ingerichte doorvoer.

In tegenstelling tot logische partities zijn fysieke partities een interne implementatie van het systeem. U kunt niet bepalen van de grootte, positie, het aantal of de toewijzing tussen de logische partities en de fysieke partities. U kunt echter het aantal logische partities en de distributie van gegevens en doorvoer beheren met de juiste partitiesleutel kiezen.

## <a name="next-steps"></a>Volgende stappen

Opgegeven in dit artikel wordt een overzicht van het partitioneren van gegevens en aanbevolen procedures voor het schalen en partitionering in Azure Cosmos DB. 

* Meer informatie over [ingerichte doorvoer in Azure Cosmos DB](request-units.md)
* Meer informatie over [wereldwijde distributie in Azure Cosmos DB](distribute-data-globally.md)
* Meer informatie over [een partitiesleutel kiezen](partitioning-overview.md#choose-partitionkey)
* Informatie over [over het inrichten van doorvoer voor een Cosmos-container](how-to-provision-container-throughput.md)
* Informatie over [hoe u de doorvoer voor een Cosmos-database inrichten](how-to-provision-database-throughput.md)
