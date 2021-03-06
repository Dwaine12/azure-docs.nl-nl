---
title: De configuratieserver voor VMware-noodherstel met Azure Site Recovery implementeren | Microsoft Docs
description: In dit artikel wordt beschreven hoe u een configuratieserver voor VMware-noodherstel met Azure Site Recovery implementeren
services: site-recovery
author: Rajeswari-Mamilla
manager: rochakm
ms.service: site-recovery
ms.topic: article
ms.date: 12/11/2018
ms.author: mayg
ms.openlocfilehash: 58d45036cac6ad985b7b1ffb2736a500fdcb5ce2
ms.sourcegitcommit: 1c1f258c6f32d6280677f899c4bb90b73eac3f2e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/11/2018
ms.locfileid: "53251025"
---
# <a name="deploy-a-configuration-server"></a>Een configuratieserver implementeren

U implementeert een on-premises configuratieserver wanneer u [Azure Site Recovery](site-recovery-overview.md) voor herstel na noodgevallen van virtuele VMware-machines en fysieke servers naar Azure. De configuratie van server coördinaten communicatie tussen on-premises VMware en Azure. Deze beheert de gegevensreplicatie. In dit artikel begeleidt u bij de stappen die nodig zijn voor de configuratieserver implementeren wanneer u virtuele VMware-machines naar Azure repliceert. [In dit artikel volgen](physical-azure-set-up-source.md) als u nodig hebt voor het instellen van een configuratieserver voor replicatie van fysieke server.

>[!TIP]
U kunt meer informatie over de rol van de configuratieserver als onderdeel van Azure Site Recovery-architectuur [hier](vmware-azure-architecture.md).

## <a name="deployment-of-configuration-server-through-ova-template"></a>Implementatie van de configuratieserver via OVA-sjabloon

Configuratieserver moet worden ingesteld als een maximaal beschikbare VMware-VM met bepaalde minimale hardware- en vereisten voor volumegrootte. Site Recovery biedt handige en eenvoudige implementatie wilt uitvoeren, een downloadbare OVA (Open Virtualization-toepassing)-sjabloon voor het instellen van de configuratieserver die aan de verplichte vereisten die voldoet hieronder worden vermeld.

## <a name="prerequisites"></a>Vereisten

Minimale hardwarevereisten voor een configuratieserver worden samengevat in de volgende tabel.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="capacity-planning"></a>Capaciteitsplanning

Vereisten voor de configuratieserver de grootte is afhankelijk van de mogelijke veranderingssnelheid van gegevens. Gebruik deze tabel als richtlijn.

| **CPU** | **Geheugen** | **Cachegrootte van de schijf** | **Veranderingssnelheid van gegevens** | **Beveiligde machines** |
| --- | --- | --- | --- | --- |
| 8 vcpu's (2-sockets * 4 kernen \@ 2,5 GHz) |16 GB |300 GB |500 GB of minder |Minder dan 100 machines repliceren. |
| 12 vcpu's (2-sockets * 6 kernen \@ 2,5 GHz) |18 GB |600 GB |500 GB tot 1 TB |100-150-machines repliceren. |
| 16 vcpu's (2-sockets * 8 kernen \@ 2,5 GHz) |32 GB |1 TB |1 TB tot 2 TB |150 tot 200-machines repliceren. |

Als u meer dan een VMware-VM repliceert, leest u [overwegingen voor capaciteitsplanning](site-recovery-plan-capacity-vmware.md). Voer de [tool voor implementatieplanning](site-recovery-deployment-planner.md) voor VMWare-replicatie.

## <a name="download-the-template"></a>De sjabloon downloaden

1. Ga in de kluis naar **Infrastructuur voorbereiden** > **Bron**.
2. Selecteer **+Configuratieserver** in **Bron voorbereiden**.
3. Controleer in **Server toevoegen** of **Configuratieserver voor VMware** wordt weergegeven in **Servertype**.
4. Download de Open Virtualization-toepassing (OVA)-sjabloon voor de configuratieserver.

  > [!TIP]
>U kunt ook de meest recente versie van de configuratieserversjabloon rechtstreeks vanuit downloaden [Microsoft Download Center](https://aka.ms/asrconfigurationserver).

>[!NOTE]
Het certificaat dat is opgegeven met OVA-sjabloon is een geldig gedurende 180 dagen evaluatie-certificaat. Na deze periode klant nodig heeft om de windows met een geleverde certificaat te activeren.

## <a name="import-the-template-in-vmware"></a>De sjabloon in VMware importeren

1. Meld u bij de VMware vCenter-server of vSphere ESXi-host met behulp van de VMWare vSphere-client.
2. Selecteer in het menu **Bestand** de optie **OVF-sjabloon implementeren** om de wizard voor het implementeren van OVF-sjablonen te starten.

     ![OVF-sjabloon](./media/vmware-azure-deploy-configuration-server/vcenter-wizard.png)

3. In **bron selecteren**, geef de locatie van de gedownloade OVF.
4. In **Beoordelingsdetails**, selecteer **volgende**.
5. In **naam en map selecteren** en **configuratie selecteren**, accepteer de standaardinstellingen.
6. Selecteer in **Opslag selecteren** **Thick Provision Eager Zeroed** in **Indeling virtuele schijf selecteren**.
7. Accepteer de standaardinstellingen in de rest van de wizardpagina’s.
8. In **Klaar om te voltooien**:

    * Selecteer **Inschakelen na de implementatie** > **Voltooien** om de VM in te stellen met de standaardinstellingen.

    * Als u wilt toevoegen een extra netwerkinterface, schakelt u **inschakelen na de implementatie**, en selecteer vervolgens **voltooien**. Standaard wordt de configuratieserversjabloon met één NIC geïmplementeerd. Na de implementatie kunt u meer NIC’s toevoegen.

## <a name="add-an-additional-adapter"></a>Een extra adapter toevoegen

Als u toevoegen van een extra NIC aan de configuratieserver wilt, moet u het toevoegen voordat u de server in de kluis registreert. Het toevoegen van extra adapters wordt niet ondersteund na registratie.

1. Klik in de vSphere Client-inventaris met de rechtermuisknop op de VM en selecteer **Instellingen bewerken**.
2. Selecteer **Toevoegen** > **Ethernet-adapter** bij **Hardware**. Selecteer vervolgens **Volgende**.
3. Selecteer een adaptertype en een netwerk.
4. Selecteer voor de virtuele NIC verbinding wanneer de virtuele machine is ingeschakeld, **verbinding maken met power-on**. Selecteer vervolgens **volgende** > **voltooien** > **OK**.

## <a name="register-the-configuration-server-with-azure-site-recovery-services"></a>De configuratieserver registreren bij Azure Site Recovery-services

1. Schakel de VM in vanuit de VMWare vSphere Client-console.
2. De VM wordt opgestart in een Windows Server 2016-installatie-ervaring. Accepteer de gebruiksrechtovereenkomst en voer een Administrator-wachtwoord in.
3. Meld u nadat de installatie is voltooid bij de virtuele machine aan als de administrator.
4. De eerste keer dat u zich aanmeldt, binnen een paar seconden de Azure Site Recovery Configuration Tool wordt gestart.
5. Voer een naam in die wordt gebruikt voor het registreren van de configuratieserver bij Site Recovery. Selecteer vervolgens **Volgende**.
6. Het hulpprogramma controleert of de VM verbinding kan maken met Azure. Nadat de verbinding tot stand is gebracht, selecteert u **Aanmelden** om u aan te melden bij uw Azure-abonnement. De referenties moeten toegang hebben tot de kluis waarin u de configuratieserver wilt registreren.
7. Het hulpprogramma voert enkele configuratietaken uit en start opnieuw op.
8. Meld u opnieuw aan bij de machine. Start de wizard voor het beheer configuratie **automatisch** in enkele seconden.

### <a name="configure-settings"></a>Instellingen configureren

1. Selecteer in de wizard voor het beheer van de configuratieserver **Connectiviteit instellen** en selecteer vervolgens de NIC die door de processerver wordt gebruikt voor het ontvangen van replicatieverkeer van VM's. Selecteer vervolgens **Opslaan**. U kunt deze instelling niet wijzigen nadat deze is geconfigureerd.
2. In **Selecteer Recovery Services-kluis**, zich aanmelden bij Microsoft Azure, selecteer uw Azure-abonnement en de relevante resourcegroep en kluis.

    > [!NOTE]
    > Zodra geregistreerd, is er geen flexibiliteit om te wijzigen van de recovery services-kluis.

3. In **software van derden installeren**,

    |Scenario   |Stappen om te volgen  |
    |---------|---------|
    |Kan ik downloaden en handmatig installeren van MySQL?     |  Ja. MySQL-toepassing downloaden en plaats deze in de map **C:\Temp\ASRSetup**, installeert u vervolgens handmatig. Nu, wanneer u de voorwaarden accepteert > Klik op **downloaden en installeren**, de portal zegt *al geïnstalleerd*. U kunt doorgaan met de volgende stap.       |
    |Kan ik voorkomen downloaden van MySQL online?     |   Ja. Plaats uw MySQL-installer-toepassing in de map **C:\Temp\ASRSetup**. Accepteer de voorwaarden > Klik op **Download en installeer**, de portal wordt gebruikt het installatieprogramma die u hebt toegevoegd en de toepassing wordt geïnstalleerd. U kunt doorgaan met de volgende stap na de installatie.    |
    |Ik wil downloaden en installeren van MySQL via Azure Site Recovery     |  Accepteer de gebruiksrechtovereenkomst en klik op **Download en installeer**. U kunt vervolgens doorgaan met de volgende stap na de installatie.       |
4. In **De configuratie van het apparaat valideren** worden de vereisten gecontroleerd voordat u doorgaat.
5. In **vCenter Server vSphere/ESXi-server configureren** voert u de FQDN of het IP-adres van de vCenter-server, of vSphere-host, in waar de VM's die u wilt repliceren zich bevinden. Voer de poort in waarop de server luistert. Voer een beschrijvende naam in voor de VMware-server in de kluis.
6. Voer referenties in die door de configuratieserver moeten worden gebruikt voor verbinding met de VMware-server. Site Recovery gebruikt deze referenties voor het automatisch detecteren van VMware-VM’s die beschikbaar zijn voor replicatie. Selecteer **toevoegen**, en vervolgens **blijven**. De referenties die u hier opgeeft, worden lokaal opgeslagen.
7. In **referenties voor virtuele machine configureren**, voer de gebruikersnaam en het wachtwoord van de Mobility-Service automatisch te installeren tijdens de replicatie voor virtuele machines. Voor **Windows** machines, het account moet lokale beheerrechten heeft op de machines die u wilt repliceren. Voor **Linux**, Geef details op voor het root-account.
8. Selecteer **Configuratie voltooien** om de registratie te voltooien.
9. Nadat de registratie is voltooid, opent u Azure portal, controleert u of de configuratieserver en de VMware-server worden weergegeven op **Recovery Services-kluis** > **beheren**  >  **Infrastructuur voor site Recovery** > **configuratieservers**.

## <a name="upgrade-the-configuration-server"></a>De configuratieserver upgraden

Als u de configuratieserver bijwerken naar de nieuwste versie, volgt u deze [stappen](vmware-azure-manage-configuration-server.md#upgrade-the-configuration-server).

## <a name="manage-the-configuration-server"></a>De configuratieserver beheren

Om te voorkomen onderbrekingen in de lopende replicatie, zorg ervoor dat IP-adres van de configuratieserver niet wordt gewijzigd nadat de configuratieserver bij een kluis is geregistreerd. U kunt meer informatie over algemene beheertaken voor configuration server [hier](vmware-azure-manage-configuration-server.md).

## <a name="faq"></a>Veelgestelde vragen

1. Kan ik de virtuele machine, waarop de configuratieserver is geïnstalleerd, voor verschillende doeleinden gebruiken?

    **Geen**, raden we u met de virtuele machine voor enig doel van de configuratieserver. Zorg ervoor dat u de specificaties die zijn vermeld in volgen [vereisten](#prerequisites) voor efficiënt beheer van herstel na noodgevallen.
2. Kan ik wisselen van de kluis die al zijn geregistreerd in de configuratieserver met een nieuwe kluis?

    **Geen**, zodra een kluis is geregistreerd met de configuratieserver, kan niet worden gewijzigd.
3. Kan ik de dezelfde configuratieserver gebruiken voor het beveiligen van zowel fysieke en virtuele machines?

    **Ja**, dezelfde configuratieserver kan worden gebruikt voor het repliceren van fysieke en virtuele machines. Echter kan fysieke machine kan worden niet terug alleen bij een VMware-VM.
4. Wat is het doel van een configuratieserver en waar wordt deze gebruikt?

    Raadpleeg [VMware naar Azure-replicatie-architectuur](vmware-azure-architecture.md) voor meer informatie over de configuratieserver en de functionaliteiten.
5. Waar vind ik de meest recente versie van de configuratieserver

    Zie voor stappen voor het bijwerken van de configuratieserver via de portal, [Upgrade van de configuratieserver](vmware-azure-manage-configuration-server.md#upgrade-the-configuration-server). U kunt ook rechtstreeks downloaden vanaf [Microsoft Download Center](https://aka.ms/asrconfigurationserver).
6. Waar kan ik de wachtwoordzin voor de configuratieserver downloaden?

    Raadpleeg [in dit artikel](vmware-azure-manage-configuration-server.md#generate-configuration-server-passphrase) voor het downloaden van de wachtwoordzin.
7. Waar kan ik registratiesleutels kluis downloaden?

    In de **Recovery Services-kluis**, **beheren** > **infrastructuur voor Site Recovery** > **configuratieservers**. Selecteer in de Servers, **registratiesleutel downloaden** voor het downloaden van het bestand met kluisreferenties.
8. Kan ik klonen van een bestaande configuratieserver en gebruiken voor het indelen van replicatie?

    **Geen**, gebruik van een gekloonde onderdeel van de configuratieserver wordt niet ondersteund. 

## <a name="troubleshoot-deployment-issues"></a>Oplossen van implementatieproblemen

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]



## <a name="next-steps"></a>Volgende stappen

Instellen van herstel na noodgevallen van [virtuele VMware-machines](vmware-azure-tutorial.md) naar Azure.