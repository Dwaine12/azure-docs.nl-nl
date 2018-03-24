---
title: Actoren op Azure Service Fabric opsommen | Microsoft Docs
description: Informatie over het opsommen van Reliable Actors en de metagegevens.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/19/2018
ms.author: vturecek
ms.openlocfilehash: 037138f68e5c18822e4d7b3fa47591411e8a2407
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/23/2018
---
# <a name="enumerate-service-fabric-reliable-actors"></a>Service Fabric Reliable Actors opsommen
De service Reliable Actors kan een client opsommen metagegevens over de actoren waarmee de service wordt gehost. Omdat de actor-service een gepartitioneerde stateful service is, wordt de opsomming per partitie uitgevoerd. Omdat elke partitie veel actoren bevat mogelijk, wordt de opsomming geretourneerd als een set pagina's met zoekresultaten. De pagina's worden via herhaald totdat alle pagina's worden gelezen. Het volgende voorbeeld ziet u het maken van een lijst met alle actieve actoren in een partitie van een actor-service:

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```



## <a name="next-steps"></a>Volgende stappen
* [Statusbeheer actor](service-fabric-reliable-actors-state-management.md)
* [Acteur lifecycle en garbage collection](service-fabric-reliable-actors-lifecycle.md)
* [API-naslagdocumentatie actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Voorbeeldcode voor .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Voorbeeldcode voor Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
