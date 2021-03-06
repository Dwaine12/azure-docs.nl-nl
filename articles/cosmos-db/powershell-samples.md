---
title: Voorbeelden van Azure PowerShell voor Azure Cosmos DB
description: 'Azure PowerShell-voorbeelden: scripts voor het maken en beheren van Azure Cosmos DB-accounts.'
services: cosmos-db
author: SnehaGunda
tags: azure-service-management
ms.service: cosmos-db
ms.custom: mvc
ms.topic: sample
ms.date: 10/16/2017
ms.author: sngun
ms.openlocfilehash: c2bd1ac165e6b17d1bd9604fb1203ae47214278f
ms.sourcegitcommit: b0f39746412c93a48317f985a8365743e5fe1596
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52871027"
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a>Voorbeelden van Azure PowerShell voor Azure Cosmos DB

De volgende tabel bevat links naar Azure PowerShell-voorbeeldscripts voor Azure Cosmos DB. Op dit moment kunt u alleen het Azure Cosmos DB-account beheren via PowerShell. Andere resources, zoals databases en containers, kunnen niet via PowerShell worden beheerd.

| |  |
|---|---|
|**Azure Cosmos DB-account maken**||
|[SQL API-account maken](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Hiermee wordt één Azure Cosmos DB-account gemaakt voor gebruik met de SQL-API. |
|[MongoDB-API-account maken](scripts/create-mongodb-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Hiermee wordt één Azure Cosmos DB-account gemaakt voor gebruik met de MongoDB-API. |
|[Een Gremlin API-account maken](scripts/create-graph-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Hiermee wordt één Azure Cosmos DB-account gemaakt voor gebruik met de Gremlin-API. |
|[Een Cassandra-API-account maken](scripts/create-and-configure-cassandra-database.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Hiermee wordt één Azure Cosmos DB-account gemaakt voor gebruik met de Cassandra-API. |
|[Een tabel-API-account maken](scripts/create-table-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Hiermee wordt één Azure Cosmos DB-account gemaakt voor gebruik met de tabel-API. |
|**Azure Cosmos DB schalen**||
|[Azure Cosmos DB-account in meerdere regio's repliceren en failover-prioriteiten configureren](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|Hiermee worden accountgegevens in meerdere regio's met een bepaalde failover-prioriteit globaal gerepliceerd.|
|**Azure Cosmos DB beveiligen**||
| [Accountsleutels ophalen](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Hiermee worden de primaire en secundaire hoofdsleutels voor schrijven en de primaire en secundaire sleutels voor alleen-lezen voor het account opgehaald.|
| [MongoDB-verbindingsreeks ophalen](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Hiermee wordt de verbindingsreeks opgehaald om uw MongoDB-app te verbinden met uw Azure Cosmos DB-account.|
|[Accountsleutels opnieuw genereren](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|Hiermee wordt de hoofdsleutel of alleen-lezensleutel voor het account opnieuw gegenereerd.|
|[Firewall maken](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Hiermee wordt toegangsbeheerbeleid voor inkomende IP's gemaakt om de toegang tot het account vanaf een goedgekeurde set computers en/of cloudservices te beperken.|
|**Hoge beschikbaarheid, herstel na noodgevallen, back-up maken en herstellen**||
|[Failoverbeleid configureren](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|Hiermee wordt de prioriteit van failover ingesteld voor elke regio waarin het account wordt gerepliceerd.|
|||
