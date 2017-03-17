---
title: Uw eerste Azure-microservices-app maken | Microsoft Docs
description: Een Service Fabric-toepassing met Visual Studio maken, implementeren en foutopsporing uitvoeren
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/07/2017
ms.author: ryanwi
translationtype: Human Translation
ms.sourcegitcommit: 72b2d9142479f9ba0380c5bd2dd82734e370dee7
ms.openlocfilehash: 296f02dd7deb22fd4ca15478b7f90a7688b4304a
ms.lasthandoff: 03/08/2017


---
# <a name="create-your-first-azure-service-fabric-application"></a>Uw eerste Azure Service Fabric-toepassing maken
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
> 
> 

De Service Fabric SDK bevat een invoegtoepassing voor Visual Studio voor sjablonen en hulpprogramma's om Service Fabric-toepassingen te maken, te implementeren en foutopsporing uit te voeren. In dit onderwerp vindt u meer informatie over het maken van uw eerste toepassing in Visual Studio 2017 of Visual Studio 2015.

## <a name="prerequisites"></a>Vereisten
Voordat u begint, zorgt u ervoor dat u [uw ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started.md).

## <a name="video-walkthrough"></a>Video-overzicht
De volgende video leidt u door de stappen in deze zelfstudie:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Creating-your-first-Service-Fabric-application-in-Visual-Studio/player]
> 
> 

## <a name="create-the-application"></a>De toepassing maken
Een Service Fabric-toepassing kan een of meer services bevatten, elk met een specifieke functie met betrekking tot het leveren van de functionaliteit van de toepassing. Met de wizard Nieuw project kunt u een toepassingsproject maken, samen met uw eerste serviceproject. U kunt desgewenst later meer services toevoegen.

1. Visual Studio starten als beheerder.
2. Klik op **Bestand > Nieuw Project > Cloud > Service Fabric-toepassing**.
3. Geef een naam op voor de toepassing en klik op **OK**.
   
    ![Dialoogvenster voor nieuw project in Visual Studio][1]
4. Kies op de volgende pagina **Stateful** als het eerste servicetype om in uw toepassing op te nemen. Geef het servicetype een naam en klik op **OK**.
   
    ![Dialoogvenster voor nieuwe service in Visual Studio][2]
   
   > [!NOTE]
   > Zie [Service Fabric programming model overview](service-fabric-choose-framework.md) (Overzicht van het Service Fabric-programmeermodel) voor meer informatie over de opties.
   > 
   > 
   
    Visual Studio maakt het toepassingsproject en het stateful service-project en geeft deze weer in Solution Explorer.
   
    ![Solution Explorer na het maken van de stateful service-toepassing][3]
   
    Het toepassingsproject bevat geen directe code. Het verwijst naar een reeks serviceprojecten. Daarnaast bevat het project drie andere typen inhoud:
   
   * **Profielen publiceren**: deze optie wordt gebruikt voor het beheren van voorkeuren voor tools voor verschillende omgevingen.
   * **Scripts**: bevat een PowerShell-script voor het implementeren van/bijwerken van uw toepassing. Visual Studio gebruikt het script-achter-de-schermen. Het script kan ook rechtstreeks op de opdrachtregel worden aangeroepen.
   * **Toepassingsdefinitie**: bevat het toepassingsmanifest onder *ApplicationPackageRoot*. Gekoppelde bestanden met toepassingsparameters vindt u onder *ApplicationParameters*, die de toepassing definiëren en waarmee u deze specifiek voor een bepaalde omgeving kunt configureren.
     
     Zie [Aan de slag met Reliable Services](service-fabric-reliable-services-quick-start.md) voor een overzicht van de inhoud van het serviceproject.

## <a name="deploy-and-debug-the-application"></a>De toepassing implementeren en fouten opsporen in de toepassing
Nu u een toepassing hebt, kunt u proberen deze uit te voeren.

1. Druk op F5 in Visual Studio om de toepassing voor foutopsporing te implementeren.
   
   > [!NOTE]
   > De implementatie duurt de eerste keer enige tijd omdat Visual Studio een lokaal ontwikkelingscluster maakt. Een lokaal cluster voert dezelfde platformcode uit als op een cluster met meerdere machines, alleen op één computer. U ziet de status van het maken van het cluster in het Visual Studio-uitvoervenster.
   > 
   > 
   
    Als het cluster gereed is, ontvangt u een melding van de lokale toepassing die het systeemvak voor het cluster beheert en die in de SDK is opgenomen.
   
    ![Melding van het systeemvak van het lokale cluster][4]
2. Als de toepassing wordt gestart, geeft Visual Studio automatisch de diagnostische logboeken met gebeurtenissen weer, waarin u de traceringsuitvoer van de service kunt bekijken.
   
    ![Diagnostische logboeken][5]
   
    Als het gaat om een stateful servicesjabloon, geven de berichten de itemwaarde weer die wordt verhoogd in de methode `RunAsync` van MyStatefulService.cs.
3. Vouw een van de gebeurtenissen uit voor meer informatie, zoals het knooppunt waarop de code wordt uitgevoerd. In dit geval is het _Node_2. Dit kan anders zijn op uw machine.
   
    ![Details van de gebeurtenissenviewer][6]
   
    Het lokale cluster bevat vijf knooppunten die worden gehost op een enkele computer. Het lijkt op een cluster met vijf knooppunten, waarbij de knooppunten zich op afzonderlijke computers bevinden. We bekijken een van de knooppunten op het lokale cluster om het verlies van gegevens van een machine te simuleren en tegelijkertijd te oefenen met de foutopsporingsfunctie.
   
   > [!NOTE]
   > De diagnostische gebeurtenissen van de toepassingen die worden gegenereerd door de projectsjabloon, maken gebruik van de klasse `ServiceEventSource`. Zie [Services lokaal bewaken en onderzoeken](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md) voor meer informatie.
   > 
   > 
4. Zoek de klasse in uw serviceproject die is afgeleid van StatefulService (bijvoorbeeld MyStatefulService) en stel een onderbrekingspunt in op de eerste regel van de methode `RunAsync`.
   
    ![Onderbrekingspunt in de stateful service RunAsync-methode][7]
5. Klik met de rechtermuisknop op het systeemvak Lokaal clusterbeheer en kies **Lokaal cluster beheren** om Service Fabric Explorer te starten.
   
    ![Start Service Fabric Explorer vanuit Lokaal clusterbeheer][systray-launch-sfx]
   
    Service Fabric Explorer biedt een visuele representatie van een cluster, waaronder de set toepassingen die is geïmplementeerd en de set fysieke knooppunten waaruit het cluster bestaat. Zie [Uw cluster visualiseren](service-fabric-visualizing-your-cluster.md) voor meer informatie over Service Fabric Explorer.
6. Vouw in het linkerdeelvenster **Cluster > Knooppunten** uit en zoek het knooppunt waarop uw code wordt uitgevoerd.
7. Klik op **Acties > uitschakelen (opnieuw opstarten)** simuleren een machine opnieuw te starten. Of deactiveer het knooppunt vanuit de lijst met knooppunten in het linkerdeelvenster.
   
    ![Een knooppunt in Service Fabric Explorer stoppen][sfx-stop-node]
   
    U ziet uw onderbrekingspunt in Visual Studio, terwijl de berekening die u uitvoerde op één knooppunt naadloos wordt overgenomen door een ander.
8. Terugkeren naar de details van de gebeurtenisviewer en de berichten bekijken. De teller blijft oplopen in stappen, zelfs als de gebeurtenissen daadwerkelijk afkomstig zijn uit een ander knooppunt.
   
    ![Details van de gebeurtenissenviewer na een failover][diagnostic-events-viewer-detail-post-failover]

## <a name="switch-cluster-mode"></a>De clustermodus wijzigen
Het lokale ontwikkelingscluster is standaard geconfigureerd om te worden uitgevoerd als een cluster met vijf knooppunten, wat nuttig is voor het opsporen van fouten in services die worden geïmplementeerd op meerdere knooppunten. Het implementeren van een toepassing op het ontwikkelingscluster met vijf knooppunten kan echter enige tijd in beslag nemen. Als u codewijzigingen snel wilt herhalen zonder uw app op vijf knooppunten uit te voeren, wijzigt u de modus van het ontwikkelingscluster in de modus met één knooppunt. Als u uw code op een cluster met één knooppunt wilt uitvoeren, klikt u met de rechtermuisknop op de Local Cluster Manager op de taakbalk en selecteert u **Clustermodus wijzigen -> één knooppunt**.  

![De clustermodus wijzigen][switch-cluster-mode]

Als u van clustermodus wisselt, wordt het ontwikkelingscluster gereset en worden alle toepassingen verwijderd die op het cluster zijn ingericht of worden uitgevoerd.

U kunt de clustermodus ook wijzigen met behulp van PowerShell:

1. Start een nieuw PowerShell-venster als beheerder.
2. Voer het installatiescript van het  cluster uit wat in de SDK-map staat:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    Het installeren van een cluster duurt even. Nadat Setup is voltooid, ziet u soortgelijke uitvoer als deze:
   
    ![Cluster-installatieuitvoer][cluster-setup-success-1-node]

## <a name="cleaning-up"></a>Opschonen
Voordat u afsluit, is het belangrijk om te onthouden dat het lokale cluster echt is. Als u het foutopsporingsprogramma stopt, worden uw toepassingsexemplaar en de registratie van het toepassingstype verwijderd. Het op de achtergrond uitvoeren van het cluster gaat echter gewoon door. U hebt verschillende mogelijkheden om het cluster te beheren:

1. Als u het cluster wilt verwijderen, maar de toepassingsgegevens en -traceringen wilt behouden, klikt u op **Lokaal cluster stoppen** in het systeemvak.
2. Als u het cluster volledig wilt verwijderen, klikt u op **Lokaal cluster verwijderen** in het systeemvak van de app. Als u dit doet, verloopt de implementatie mogelijk langzamer wanneer u in Visual Studio op F5 drukt. Verwijder het cluster alleen als u het lokale cluster een tijd niet gaat gebruiken of als u resources wilt vrijmaken.

## <a name="next-steps"></a>Volgende stappen
* Leer hoe u een [cluster maakt in Azure](service-fabric-cluster-creation-via-portal.md) of hoe u een [zelfstandig cluster maakt in Windows](service-fabric-cluster-creation-for-windows-server.md).
* Maak een service met het programmeermodel [Reliable Services](service-fabric-reliable-services-quick-start.md) of [Reliable Actors](service-fabric-reliable-actors-get-started.md).
* Probeer een [Windows-container](service-fabric-deploy-container.md) of een bestaande app te implementeren als een [uitvoerbaar gastbestand](service-fabric-deploy-existing-app.md).
* Leer hoe u uw services met de [front-end van een webservice](service-fabric-add-a-web-frontend.md) verbindt met internet.
* Voer een [praktijkoefening](https://msdnshared.blob.core.windows.net/media/2016/07/SF-Lab-Part-I.docx) uit en maak een staatloze service, configureer de controle en statusrapporten en voer een toepassingsupgrade uit.
* Meer informatie over [ondersteuningsopties voor Service Fabric](service-fabric-support.md)

<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png

