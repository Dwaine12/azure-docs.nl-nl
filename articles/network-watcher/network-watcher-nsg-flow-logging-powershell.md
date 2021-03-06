---
title: Logboeken met Azure Network Watcher - PowerShell Network Security Group stromen beheren | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u voor het beheren van Network Security Group Flow Logboeken in Azure Network Watcher met PowerShell
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 752370564c52513d59e99b18d5343b0575900463
ms.sourcegitcommit: 8899e76afb51f0d507c4f786f28eb46ada060b8d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/16/2018
ms.locfileid: "51819352"
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a>Network Security Group Flow logboeken configureren met PowerShell

> [!div class="op_single_selector"]
> - [Azure Portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Azure-CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Stroomlogboeken van Netwerkbeveiligingsgroep zijn een functie van Network Watcher waarmee u informatie wilt weergeven over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep. Deze logboeken van de stroom zijn geschreven in json-indeling en weergeven van binnenkomende en uitgaande stromen op basis van per regel, de NIC die de stroom is van toepassing op, 5-tuple-informatie over de stroom (bron-/ doel-IP-adres, poort van de bron-/ doel, Protocol), en als het verkeer is toegestaan of geweigerd.

> [!NOTE] 
> Stroom logboeken versie 2 zijn alleen beschikbaar in de centrale regio VS-West. Configuratie is beschikbaar via de Azure Portal en de REST-API. Inschakelen van versie 2 resulteert-Logboeken in een niet-ondersteunde regio in versie 1-logboeken output naar uw opslagaccount.

## <a name="register-insights-provider"></a>Insights-provider registreren

Stroom logboekregistratie om te werken, zodat de **Microsoft.Insights** provider moet worden geregistreerd. Als u niet zeker weet als de **Microsoft.Insights** provider is geregistreerd, voer het volgende script.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Stroomlogboeken van Netwerkbeveiligingsgroep inschakelen

De opdracht uit om Logboeken van de stroom wordt weergegeven in het volgende voorbeeld:

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG -Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

Het opslagaccount dat u opgeeft kan niet zijn geconfigureerd voor het netwerkregels waarmee toegang tot het netwerk wordt beperkt tot alleen Microsoft-services of specifieke virtuele netwerken. Het opslagaccount kan zich in dezelfde of een ander Azure-abonnement, dan de NSG waarmee het stroomlogboek voor. Als u verschillende abonnementen vallen, moeten ze beide zijn gekoppeld aan dezelfde Azure Active Directory-tenant. Het account dat u voor elk abonnement gebruikt moet hebben de [benodigde machtigingen](required-rbac-permissions.md).

## <a name="disable-network-security-group-flow-logs"></a>Stroomlogboeken van Netwerkbeveiligingsgroep uitschakelen

Gebruik het volgende voorbeeld om uit te schakelen van Logboeken van de stroom:

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a>Een Flow-log Download

De opslaglocatie van het stroomlogboek van een wordt gedefinieerd bij het maken ervan. Een handig hulpmiddel voor toegang tot deze stroomlogboeken die zijn opgeslagen op een storage-account is Microsoft Azure Storage Explorer, die u kunt hier downloaden:  http://storageexplorer.com/

Als een storage-account is opgegeven, worden pakketten vastleggen van bestanden worden opgeslagen in een storage-account op de volgende locatie:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json
```

Ga voor informatie over de structuur van het logboek naar [Network Security Group Flow-log overzicht](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het [visualiseren met Power BI uw NSG-stroomlogboeken](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Meer informatie over het [visualiseren van uw NSG-stroomlogboeken met open-sourcehulpprogramma's](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
