---
title: Uw ontwikkelomgeving instellen | Microsoft Docs
description: Installeer de runtime, SDK en hulpprogramma&quot;s en maak een lokaal ontwikkelcluster. Zodra u dit hebt gedaan, kunt u toepassingen bouwen.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/26/2016
ms.author: ryanwi
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 7ae0fcc689d51479a92c506ea48ab8af2003acfe


---
# <a name="prepare-your-development-environment"></a>Uw ontwikkelomgeving voorbereiden
> [!div class="op_single_selector"]
> -[ Windows](service-fabric-get-started.md)
> 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 Als u [Azure Service Fabric-toepassingen][1] op uw ontwikkelmachine wilt bouwen en uitvoeren, moet u de runtime, de SDK en de hulpprogramma's installeren. U moet er ook voor zorgen dat de Windows PowerShell-scripts die in de SDK zijn opgenomen, kunnen worden uitgevoerd.

## <a name="prerequisites"></a>Vereisten
### <a name="supported-operating-system-versions"></a>Ondersteunde versies van besturingssystemen
De volgende versies van besturingssystemen worden ondersteund voor de ontwikkeling:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows 10

> [!NOTE]
> Windows 7 bevat standaard alleen Windows PowerShell 2.0. Voor Service Fabric PowerShell-cmdlets is PowerShell 3.0 of hoger vereist. U kunt [Windows PowerShell 5.0 downloaden][powershell5-download] via het Microsoft Downloadcentrum.
> 
> 

## <a name="install-the-runtime-sdk-and-tools"></a>De runtime, SDK en hulpprogramma's installeren
Het webplatforminstallatieprogramma biedt twee configuraties voor Service Fabric-ontwikkeling:

* [Installeer de Service Fabric-runtime, -SDK en hulpprogramma's voor Visual Studio 2015 (Visual Studio 2015 Update 2 of later vereist)][full-bundle-vs2015]
* [Installeer alle de Service Fabric-runtime en -SDK (geen hulpprogramma's voor Visual Studio tools)][core-sdk]

## <a name="enable-powershell-script-execution"></a>Uitvoering van PowerShell-script inschakelen
Service Fabric gebruikt Windows PowerShell-scripts om een lokaal ontwikkelcluster te maken en om toepassingen vanuit Visual Studio te implementeren. Standaard worden deze scripts door Windows geblokkeerd zodat ze niet worden uitgevoerd. Als u ze wilt inschakelen, moet u het PowerShell-uitvoeringsbeleid wijzigen. Open PowerShell als een beheerder en voer de volgende opdracht in:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a>Volgende stappen
Nu u uw ontwikkelingsomgeving hebt ingesteld, kunt u apps ontwikkelen en uitvoeren.

* [Uw eerste Service Fabric-toepassing in Visual Studio maken](service-fabric-create-your-first-application-in-visual-studio.md)
* [Meer informatie over het implementeren en beheren van toepassingen op uw lokale cluster](service-fabric-get-started-with-a-local-cluster.md)
* [Meer informatie over de programmeermodellen: Reliable Services en Reliable Actors](service-fabric-choose-framework.md)
* [Voorbeelden van Service Fabric-code op GitHub bekijken](https://aka.ms/servicefabricsamples)
* [Uw cluster visualiseren door gebruik te maken van Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)
* [Het leertraject voor Service Fabric volgen voor een brede inleiding tot het platform](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric-campagnepagina"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI-koppeling"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI-koppeling"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI-koppeling"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395



<!--HONumber=Nov16_HO2-->


