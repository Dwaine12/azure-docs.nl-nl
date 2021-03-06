---
title: 'Zelfstudie: Een interne Basic-load balancer maken met behulp van de Azure-portal | Microsoft Docs'
description: In deze zelfstudie ziet u hoe u een interne Basic-load balancer kunt maken met behulp van de Azure-portal.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: As an IT administrator, I want to create a load balancer that load balances incoming internal traffic to virtual machines within a specific zone in a region.
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/28/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 9ccbbb107dfd8fde237cdfdd4b0c3fcc080fd70e
ms.sourcegitcommit: 11d8ce8cd720a1ec6ca130e118489c6459e04114
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52839242"
---
# <a name="tutorial-balance-internal-traffic-load-with-a-basic-load-balancer-in-the-azure-portal"></a>Zelfstudie: Interne-verkeersbelasting verdelen met een Basic-load balancer in de Azure-portal

Taakverdeling zorgt voor een hogere beschikbaarheid en betere schaalbaarheid door binnenkomende aanvragen te spreiden over meerdere virtuele machines (VM's). U kunt de Azure-portal gebruiken om een Basic-load balancer te maken en intern verkeer over virtuele machines te verdelen. In deze zelfstudie wordt beschreven hoe u een interne load balancer, back-endservers en netwerkresources kunt maken in de prijscategorie Basic.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint. 

Indien gewenst, kunt u deze stappen uitvoeren met behulp van de [Azure CLI](load-balancer-get-started-ilb-arm-cli.md) of [Azure PowerShell](load-balancer-get-started-ilb-arm-ps.md) in plaats van met de portal.

Als u de stappen met behulp van deze zelfstudie wilt uitvoeren. moet u zich aanmelden bij de Azure-portal op [https://portal.azure.com](https://portal.azure.com).

## <a name="create-a-vnet-back-end-servers-and-a-test-vm"></a>Een VNet, back-endservers en een test-VM maken

Eerst moet u een virtueel netwerk (VNet) maken. In het VNet maakt u twee virtuele machines die u gaat gebruiken voor de back-endpool van de Basic-load balancer, vervolgens maakt u een derde VM die u gaat gebruiken voor het testen van de load balancer. 

### <a name="create-a-virtual-network"></a>Een virtueel netwerk maken

1. Selecteer **Een resource maken** > **Netwerken** > **Virtueel netwerk** linksboven in de portal.
   
1. In het deelvenster **Virtueel netwerk maken** typt of selecteert u de volgende waarden:
   
   - **Naam**: typ *MyVNet*.
   - **ResourceGroup**: selecteer **Nieuwe maken**, voer vervolgens *MyResourceGroupLB* in en selecteer **OK**. 
   - **Subnet** > **Naam**: typ *MyBackendSubnet*.
   
1. Selecteer **Maken**.

   ![Een virtueel netwerk maken](./media/tutorial-load-balancer-basic-internal-portal/2-load-balancer-virtual-network.png)

### <a name="create-virtual-machines"></a>Virtuele machines maken

1. Selecteer **Een resource maken** > **Compute** > **Windows Server 2016 Datacenter** linksboven in de portal. 
   
1. In **Een virtuele machine maken** typt of selecteert u de volgende waarden op het tabblad **Basisinformatie**:
   - **Abonnement** > **Resourcegroep**: selecteer **MyResourceGroupLB** in de vervolgkeuzelijst.
   - **Instantiedetails** > **Naam van virtuele machine**: typ *MyVM1*.
   - **Instantiedetails** > **Beschikbaarheidsopties**: 
     1. Selecteer in de vervolgkeuzelijst **Beschikbaarheidsset**. 
     2. Selecteer **Nieuwe maken**, typ *MyAvailabilitySet* en selecteer **OK**.
   - **Administrator-account** > **Gebruikersnaam**: typ *azureuser*.
   - **Administrator-account** > **Wachtwoord**: typ *Azure1234567*. 
     Typ nogmaals het wachtwoord in het veld **Wachtwoord bevestigen**.
   
1. Selecteer het tabblad **Netwerken** of selecteer **Volgende: Schijven** en vervolgens **Volgende: Netwerken**. 
   
   Zorg ervoor dat de volgende opties zijn geselecteerd:
   - **Virtueel netwerk**: **MyVNet**
   - **Subnet**: **MyBackendSubnet**
   
   Bij **Netwerkbeveiligingsgroep**:
   1. selecteert u **Geavanceerd**. 
   1. In de vervolgkeuzelijst **Netwerkbeveiligingsgroep configureren** selecteert u **Geen**. 
   
1. Selecteer het tabblad **Beheer** of selecteer **Volgende** > **Beheer**. Stel bij **Bewaking** **Diagnostische gegevens over opstarten** in op **Uit**.
   
1. Selecteer **Controleren + maken**.
   
1. Controleer de instellingen en selecteer vervolgens **Maken**. 

1. Volg de stappen voor het maken van een tweede virtuele machine met de naam *MyVM2*, en stel daarvoor alle andere instellingen in zoals bij MyVM1. 

1. Volg dezelfde stappen nogmaals om een derde VM met de naam *MyTestVM* te maken. 

## <a name="create-a-basic-load-balancer"></a>Een Basic-load Balancer maken

Maak met behulp van de portal een interne Basic-load balancer. De naam en het IP-adres die u maakt, worden automatisch geconfigureerd als de front-end van de load balancer.

1. Selecteer **Een resource maken** > **Netwerken** > **Load Balancer** linksboven in het scherm.
   
1. Typ of selecteer de volgende waarden in het deelvenster **Load balancer maken**:
   
   - **Naam**: typ *MyLoadBalancer*.
   - **Type**: selecteer **Interne**. 
   - **SKU**: selecteer **Basic**.
   - **Virtueel netwerk**: selecteer **Een virtueel netwerk kiezen** en selecteer vervolgens **MyVNet**.
   - **Subnet**: selecteer **Een subnet kiezen** en selecteer vervolgens **MyBackendSubnet**.
   - **IP-adrestoewijzing**: selecteer **Statisch** als dit niet is geselecteerd.
   - **Privé IP-adres**: typ een adres dat zich in de adresruimte van uw virtuele netwerk en subnet bevindt, bijvoorbeeld *10.3.0.7*.
   - **ResourceGroup**: in de vervolgkeuzelijst **Selecteer een bestaande** en selecteer **MyResourceGroupLB**. 
   
1. Selecteer **Maken**.
   
![Een load balancer maken](./media/tutorial-load-balancer-basic-internal-portal/1-load-balancer.png)

## <a name="create-basic-load-balancer-resources"></a>Resources voor een Basic-load balancer maken

In deze sectie configureert u de instellingen van de load balancer voor een back-endadresgroep en een statustest en geeft u regels voor de load balancer op.

### <a name="create-a-back-end-address-pool"></a>Een back-endadresgroep maken

De load balancer gebruikt een backend-adresgroep om verkeer te distribueren over de virtuele machines. De back-endadresgroep bevat de IP-adressen van de virtuele netwerkinterfacekaarten (NIC's) die zijn verbonden met de load balancer. 

**Voor het maken van een back-endadresgroep bevat die VM1 en VM2:**

1. Selecteer **Alle resources** in het linkermenu en selecteer vervolgens **myLoadBalancer** in de lijst met resources.
   
1. Selecteer onder **Instellingen** de optie **Back-endpools** en selecteer vervolgens **Toevoegen**.
   
1. Op de pagina **Een back-endpool toevoegen** typt of selecteert u de volgende waarden:
   
   - **Naam**: typ *MyBackendPool*.
   - **Gekoppeld aan**: selecteer in de vervolgkeuzelijst **Beschikbaarheidsset**.
   - **Beschikbaarheidsset**: selecteer **myAvailabilitySet**.
   
1. Selecteer **Een doel-netwerk-IP-configuratie toevoegen**. 
   1. Voeg **MyVM1** en **MyVM2** aan de back-endpool toe.
   2. Nadat u alle machines hebt toegevoegd, selecteert u in de vervolgkeuzelijst de bijbehorende **netwerk-IP-configuratie**. 
   
   >[!NOTE]
   >Voeg geen **MyTestVM** aan de groep toe. 
   
1. Selecteer **OK**.
   
   ![De back-endadresgroep toevoegen](./media/tutorial-load-balancer-basic-internal-portal/3-load-balancer-backend-02.png)
   
1. Vouw op de pagina **Back-endpools** **MyBackendPool** uit en controleer of zowel **VM1** als **VM2** worden vermeld.

### <a name="create-a-health-probe"></a>Een statustest maken

U gebruikt een statustest om de load balancer toe te staan de status van uw virtuele machine te bewaken. De statustest voegt dynamisch VM's toe aan de load balancer-rotatie of verwijdert ze, op basis van hun reactie op statuscontroles. 

**Een statustest maken om de status van de VM's te maken, doet u als volgt:**

1. Selecteer **Alle resources** in het linkermenu en selecteer vervolgens **myLoadBalancer** in de lijst met resources.
   
1. Selecteer onder **Instellingen** de optie **Statustests** en selecteer vervolgens **Toevoegen**.
   
1. Op de pagina **Een statustest toevoegen** typt of selecteert u de volgende waarden:
   
   - **Naam**: typ *MyHealthProbe*.
   - **Protocol**: selecteer in de vervolgkeuzelijst **HTTP**. 
   - **Poort**: typ *80*. 
   - **Pad**: accepteer */* als de standaard-URI. U kunt deze waarde vervangen door een andere URI. 
   - **Interval**: typ *15*. Een interval is het aantal seconden tussen tests.
   - **Drempelwaarde voor onjuiste status**: typ *2*. Deze waarde duidt het aantal opeenvolgende mislukte tests aan dat moet optreden voordat wordt besloten dat een VM een onjuiste status heeft.
   
1. Selecteer **OK**.
   
   ![Een test toevoegen](./media/tutorial-load-balancer-basic-internal-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a>Een load balancer-regel maken

Een load balancer-regel bepaalt hoe het verkeer over de VM's wordt verdeeld. De regel definieert de front-end-IP-configuratie voor het inkomende verkeer en de back-end-IP-groep om het verkeer te ontvangen, samen met de gewenste bron- en doelpoorten. 

De load balancer-regel met de naam **myLoadBalancerRuleWeb** luistert op poort 80 van de front-end **LoadBalancerFrontEnd**. Met de regel wordt netwerkverkeer naar de back-endadresgroep **myBackEndPool** verzonden, ook op poort 80. 

**Een load balancer-regel maken, gaat als volgt:**

1. Selecteer **Alle resources** in het linkermenu en selecteer vervolgens **myLoadBalancer** in de lijst met resources.
   
1. Selecteer onder **Instellingen** **Taakverdelingsregels** en selecteer vervolgens **Toevoegen**.
   
1. Op de pagina **Load balancer-regel toevoegen** typt of selecteert u de volgende waarden, als die er nog niet op voorkomen:
   
   - **Naam**: typ *MyLoadBalancerRule*.
   - **Frontend-IP-adres:** typ *LoadBalancerFrontEnd* als deze niet aanwezig is.
   - **Protocol**: selecteer **TCP**.
   - **Poort**: typ *80*.
   - **Back-endpoort**: typ *80*.
   - **Back-endpool**: selecteer **MyBackendPool**.
   - **Statustest**: selecteer **MyHealthProbe**. 
   
1. Selecteer **OK**.
   
  ![Een load balancer-regel toevoegen](./media/tutorial-load-balancer-basic-internal-portal/5-load-balancing-rules.png)

## <a name="test-the-load-balancer"></a>Load balancer testen

Installeer Internet Information Services (IIS) op de back-endservers en gebruik vervolgens MyTestVM om de load balancer met behulp van het privé IP-adres ervan te testen. Elke back-end-VM bedient een andere versie van de standaard IIS-webpagina, zodat u kunt zien dat de load balancer aanvragen over de twee virtuele machines verdeelt.

Zoek in de portal op de **overzichtspagina** voor **MyLoadBalancer** naar het IP-adres onder **Privé IP-adres**. Beweeg de muisaanwijzer over het adres en selecteer het pictogram **Kopiëren** om het te kopiëren. In dit voorbeeld is dat **10.3.0.7**. 

### <a name="connect-to-the-vms-with-rdp"></a>Verbinding maken met de virtuele machines via Extern bureaublad (RDP)

Maak eerst verbinding met alle drie de virtuele machines via Extern bureaublad. 

>[!NOTE]
>Standaard hebben de virtuele machines al de **Extern bureaublad**-poort geopend om toegang via Extern bureaublad toe te staan. 

**Met Extern bureaublad naar de VM's gaat als volgt:**

1. Selecteer in de portal **Alle resources** in het menu aan de linkerkant. Selecteer in de lijst met resources elke afzonderlijke VM in de resourcegroep **MyResourceGroupLB**.
   
1. Op de **overzichtspagina** selecteert u **Verbinding maken** en vervolgens **RDP-bestand downloaden**. 
   
1. Open het gedownloade RDP-bestand en selecteer **Verbinding maken**.
   
1. Selecteer in het scherm Windows-beveiliging **Meer opties** en vervolgens **Een ander account gebruiken**. 
   
   Voer de gebruikersnaam *azureuser* en het wachtwoord *Azure1234567!* in en selecteer **OK**.
   
1. Antwoord met **Ja** als u om een certificaat wordt gevraagd. 
   
   Het bureaublad van de virtuele machine wordt in een nieuw venster geopend. 

### <a name="install-iis-and-replace-the-default-iis-page-on-the-back-end-vms"></a>IIS op de back-end-VM's installeren en de standaard-IIS-pagina vervangen

Gebruik op elke back-endserver PowerShell om IIS te installeren en de standaard IIS-webpagina door een aangepaste pagina te vervangen.

>[!NOTE]
>U kunt ook de **wizard Rollen en functies toevoegen** in **Serverbeheer** gebruiken om IIS te installeren. 

**Als u IIS wilt installeren en de standaardwebpagina wilt bijwerken met behulp van PowerShell, gaat u als volgt te werk:**

1. Start vanuit het **startmenu** op MyVM1 en MyVM2 **Windows PowerShell**. 

2. Voer de volgende opdrachten uit om IIS te installeren en de standaard webpagina van IIS te vervangen:
   
   ```powershell-interactive
    # Install IIS
      Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # Remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    #Add custom htm file
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
    ```
1. Sluit de RDP-verbindingen met MyVM1 en MyVM2 door **Verbinding verbreken** te selecteren. Sluit de virtuele machines niet af.

### <a name="test-the-load-balancer"></a>Load balancer testen

1. Open **Internet Explorer** op MyTestVM en antwoord met **OK** op configuratieprompts. 
   
1. Plak of typ het privé IP-adres van de load balancer (*10.3.0.7*) in de adresbalk van de browser. 
   
   De aangepaste standaardpagina van de IIS-webserver wordt weergegeven in de browser. Het bericht bestaat uit te tekst **Hallo wereld van MyVM1** of uit **Hallo wereld van MyVM2**.
   
1. Vernieuw de browser zodat u kunt zien dat de load balancer verkeer verdeelt tussen de virtuele machines. U moet tussen pogingen mogelijk ook de cache van uw browser leegmaken.

   Soms wordt de pagina **MyVM1** weergegeven en op andere momenten wordt de pagina **MyVM2** weergegeven, omdat de load balancer de aanvragen naar elke back-end-VM distribueert. 

   ![Nieuwe IIS-standaardpagina](./media/tutorial-load-balancer-basic-internal-portal/9-load-balancer-test.png) 
   
## <a name="clean-up-resources"></a>Resources opschonen

Als u de load balancer en alle bijbehorende resources wilt verwijderen omdat u deze niet meer nodig hebt, opent u de resourcegroep **MyResourceGroupLB** en selecteert u **Resourcegroep verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt een u een interne load balancer op Basic-niveau gemaakt. U hebt netwerresources, back-endservers, een statustest en regels voor de load balancer gemaakt en geconfigureerd. U hebt IIS geïnstalleerd op de back-end-VM's en een test-VM gebruikt om de load balancer in de browser te testen. 

Hierna leert u hoe u taken verdeelt over VM's in meerdere beschikbaarheidszones.

> [!div class="nextstepaction"]
> [Taken over VM's in meerdere beschikbaarheidszones verdelen](tutorial-load-balancer-standard-public-zone-redundant-portal.md)
