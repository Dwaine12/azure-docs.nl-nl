---
title: Toegangsbeleid toewijzen aan Azure Service Fabric service-eindpunten | Microsoft Docs
description: Informatie over het toewijzen van beveiliging toegangsbeleid met HTTP of HTTPS-eindpunten in uw Service Fabric-service.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/21/2018
ms.author: mfussell
ms.openlocfilehash: dac15f0b96e9e295f92f250fe387e5b6ba9ae000
ms.sourcegitcommit: 6b7c8b44361e87d18dba8af2da306666c41b9396
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/12/2018
ms.locfileid: "51567601"
---
# <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Toewijzen van een beveiligingsbeleid voor toegang voor HTTP en HTTPS-eindpunten
Als u een run as-beleid toepassen en het servicemanifest HTTP-eindpunt resources verklaart, moet u een **SecurityAccessPolicy**.  **SecurityAccessPolicy** zorgt ervoor dat de poorten die zijn toegewezen aan deze eindpunten correct zijn beperkt tot het gebruikersaccount dat de service wordt uitgevoerd als. Anders **http.sys** geen toegang tot de service, en u fouten met aanroepen van de client. Het volgende voorbeeld wordt de Customer1-account naar een eindpunt met de naam **EndpointName**, waardoor het volledige toegangsrechten.

```xml
<Policies>
  <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
  <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Voor een HTTPS-eindpunt, moet u ook de naam van het certificaat om terug te keren naar de client aangeven. U verwijst naar het certificaat met behulp van **EndpointBindingPolicy**.  Het certificaat is gedefinieerd in de **certificaten** gedeelte van het toepassingsmanifest.

```xml
<Policies>
  <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
  <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies>
```

> [!WARNING] 
> Wanneer u HTTPS gebruikt, gebruik niet de dezelfde poort en het certificaat dat voor andere service-exemplaren (onafhankelijk van de toepassing) is geïmplementeerd op hetzelfde knooppunt. Upgraden van twee verschillende services met behulp van dezelfde poort in verschillende toepassingsinstanties resulteert in een upgrade mislukt. Zie voor meer informatie, [bijwerken van meerdere toepassingen met HTTPS-eindpunten ](service-fabric-application-upgrade.md#upgrading-multiple-applications-with-https-endpoints).
> 

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged--> Lees de volgende artikelen voor de volgende stappen:
* [Inzicht krijgen in het toepassingsmodel](service-fabric-application-model.md)
* [Resources specificeren in een servicemanifest](service-fabric-service-manifest-resources.md)
* [Een app implementeren](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
