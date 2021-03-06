---
title: Overzicht Azure Containers bewaken | Microsoft Docs
description: Dit artikel bevat een overzicht van de verschillende methoden die beschikbaar zijn in Azure om Containers in Azure om te zien een clusters status en beschikbaarheid te bewaken.
services: log-analytics
documentationcenter: ''
author: MGoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2018
ms.author: magoedte
ms.openlocfilehash: 574b2ad048ca9572447b55885deb98415c3e3753
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53183196"
---
# <a name="overview-of-monitoring-containers-in-azure"></a>Overzicht van de bewaking van Containers in Azure
Met Azure, kunt u effectief bewaken en beheren van uw workloads op Azure met Kubernetes of Docker-containers geïmplementeerd. Het is belangrijk om te begrijpen hoe containers met meerdere microservice-toepassingen worden uitgevoerd om te kunnen leveren van een betrouwbare service op schaal en de controle-ondersteuningsabonnement. In dit artikel geeft een kort overzicht van het beheer en de bewakingsmogelijkheden in Azure om te begrijpen en die geschikt zijn gebaseerd op uw vereisten.

Met behulp van [Azure Monitor voor containers](container-insights-overview.md), kunt u de prestaties en status van de infrastructuur voor uw Linux-container in een oogopslag bekijken en snel problemen onderzoeken. De telemetrie wordt opgeslagen in een Log Analytics-werkruimte en geïntegreerd in Azure portal, waar u bekijken kunt, filteren en segment cumulatieve gegevens met dashboards te laden, prestaties en status in de gaten houden.  

Voor containers die worden uitgevoerd buiten de gehoste service voor Azure Kubernetes, de Log Analytics [oplossing voor Windows- en Docker-Container](../../azure-monitor/insights/containers.md) kunt u weergeven en beheren van uw Windows- en Docker-container-hosts. Van uw Log Analytics-werkruimte, kunt u inventarisgegevens, prestaties en gebeurtenissen van knooppunten en de containers weergeven in de omgeving. Vindt u gedetailleerde controle-informatie met opdrachten die worden gebruikt met containers en u kunt containers oplossen weer te geven en gecentraliseerde logboeken zoeken zonder dat u hoeft voor externe toegang tot Docker of Windows-hosts.

Als u wilt bereiken holistische of end-to-end bewaking van de toepassing, moet een afhankelijkheid of er een Azure is of on-premises resource, worden gecontroleerd met Azure Monitor of Log Analytics.  Niveau van de toepassing moet worden opgenomen om toe te voegen een extra laag van health-status, zowel op het niveau van het platform en de toepassing met behulp van Application Insights. Op het niveau van het platform, zijn er Application Insights-SDK's voor [Kubernetes]( https://github.com/Microsoft/ApplicationInsights-Kubernetes), [Docker](https://hub.docker.com/r/microsoft/applicationinsights/), en [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights). Voor microservice-toepassingen, er is ondersteuning voor [Java](../../application-insights/app-insights-java-get-started.md), [Node.js](../../application-insights/app-insights-nodejs-quick-start.md), [.Net](../../application-insights/app-insights-asp-net.md), [.Net Core](../../application-insights/app-insights-asp-net-core.md), evenals een aantal andere [talen/frameworks](../../application-insights/app-insights-platforms.md). 

Anders problemen gaat niet-geïdentificeerde die mogelijk invloed op de beschikbaarheid van de toepassing en serviceniveaudoelen niet voldaan aan.  
