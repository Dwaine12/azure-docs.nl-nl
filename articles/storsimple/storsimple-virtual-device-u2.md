---
title: Update 2 voor virtuele StorSimple-apparaten | Microsoft Docs
description: Informatie over het maken, implementeren en beheren van een virtueel StorSimple-apparaat in een Microsoft Azure Virtual Network. (Van toepassing op StorSimple Update 2.)
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/03/2017
ms.author: alkohli
ms.openlocfilehash: 98892a0919b1ba49308fd3bc51c735977bbff437
ms.sourcegitcommit: 0930aabc3ede63240f60c2c61baa88ac6576c508
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/07/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Een virtueel StorSimple-apparaat implementeren en beheren in Azure
> [!NOTE]
> De klassieke portal voor StorSimple is afgeschaft. De StorSimple-apparaatbeheerfuncties worden automatisch volgens schema verplaatst naar de nieuwe Azure Portal. U ontvangt hierover een e-mailbericht en een portalmelding. Dit document wordt binnenkort ook ingetrokken. Als u de versie van dit artikel voor de nieuwe Azure Portal wilt bekijken, gaat u naar [Deploy and manage a StorSimple virtual device in Azure](storsimple-8000-cloud-appliance-u2.md) (Een virtueel StorSimple-apparaat implementeren en beheren in Azure). Zie [FAQ: Move to Azure portal](storsimple-8000-move-azure-portal-faq.md) (Veelgestelde vragen: verplaatsing naar Azure Portal) voor vragen met betrekking tot de verplaatsing.

## <a name="overview"></a>Overzicht
De virtuele apparaten van de serie StorSimple 8000 dienen ter aanvulling op de Microsoft Azure StorSimple-oplossing. Het virtuele StorSimple-apparaat wordt uitgevoerd op een virtuele machine in een Microsoft Azure Virtual Network. U kunt het gebruiken om back-ups te maken van gegevens en om gegevens van uw hosts te klonen. In deze zelfstudie wordt beschreven hoe u een virtueel apparaat implementeert en beheert in Azure. De informatie in deze zelfstudie geldt voor alle virtuele apparaten met softwareversie Update 2 en ouder.

#### <a name="virtual-device-model-comparison"></a>Vergelijking van de verschillende modellen virtuele apparaten
Het virtuele StorSimple-apparaat is beschikbaar in twee modellen: de Standard 8010 (voorheen bekend als de 1100) en de Premium 8020 (geïntroduceerd bij Update 2). Hieronder vindt u een vergelijking van de twee modellen in een tabel.

| Apparaatmodel | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maximale capaciteit** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 kerngeheugens, 7 GB geheugen) |Standard_DS3 (4 kerngeheugens, 14 GB geheugen) |
| **Versiecompatibiliteit** |Versies met Update 2 of oudere of nieuwere software |Versies met Update 2 of nieuwere software |
| **Beschikbaarheid in regio’s** |Alle Azure-regio's |Alle Azure-regio's waar ondersteuning wordt geboden voor Premium Storage en Azure-VM’s met DS3<br></br> Gebruik [deze lijst](https://azure.microsoft.com/en-us/regions/services) om te kijken of zowel *Virtuele Machines > DS-serie* als *Opslag > Schijfruimte* beschikbaar is in uw regio. |
| **Opslagtype** |Maakt gebruik van Azure Standard-opslag voor lokale schijven<br></br> Ontdek hoe u [een Standard-opslagaccount maakt](../storage/common/storage-create-storage-account.md) |Maakt gebruik van Azure Premium Storage voor lokale schijven<sup>2</sup> <br></br>Ontdek hoe u [een Premium Storage-account maakt](../storage/common/storage-premium-storage.md) |
| **Richtlijnen voor de workload** |Bestanden ophalen uit back-ups op itemniveau |Cloudontwikkelings- en testscenario’s, lage latentie en werkbelasting met hogere prestaties <br></br>Secundair apparaat voor herstel na noodgevallen |

<sup>1</sup> *Voorheen bekend als de 1100*.

<sup>2</sup> *Voor zowel de 8010 als de 8020 wordt voor de cloudlaag Azure Standard-opslag gebruikt. Het verschil zit hem alleen in de lokale laag in het apparaat*.

In dit artikel wordt stapsgewijs beschreven hoe u een virtueel StorSimple-apparaat implementeert in Azure. Wanneer u dit artikel hebt gelezen:

* Begrijpt u waarin het virtuele apparaat verschilt van het fysieke apparaat.
* Kunt u het virtuele apparaat maken en configureren.
* Kunt u verbinding maken met het virtuele apparaat.
* Kunt u met het virtuele apparaat werken.

Deze zelfstudie is van toepassing op alle virtuele StorSimple-apparaten met Update 2 en hoger.

## <a name="how-the-virtual-device-differs-from-the-physical-device"></a>Waarin het virtuele apparaat verschilt van het fysieke apparaat
Het virtuele StorSimple-apparaat is een versie van StorSimple die alleen uit software bestaat en wordt uitgevoerd op één knooppunt in een virtuele Microsoft Azure-machine. Het virtuele apparaat biedt ondersteuning voor herstel na noodgevallen waarbij uw fysieke apparaat niet beschikbaar is. Het kan worden gebruikt om op itemniveau bestanden te herstellen van back-ups, voor on-premises herstel na noodgevallen, en voor cloudontwikkelings- en testscenario’s.

#### <a name="differences-from-the-physical-device"></a>Verschillen met het fysieke apparaat
In de volgende tabel ziet u enkele belangrijke verschillen tussen het virtuele StorSimple-apparaat en het fysieke StorSimple-apparaat.

|  | Fysiek apparaat | Virtueel apparaat |
| --- | --- | --- |
| **Locatie** |Bevindt zich in het datacenter. |Wordt uitgevoerd in Azure. |
| **Netwerkinterfaces** |Heeft zes netwerkinterfaces: DATA 0 t/m DATA 5. |Heeft slechts één netwerkinterface: DATA 0 |
| **Registratie** |Geregistreerd tijdens de configuratiestap. |Registratie is een afzonderlijke taak. |
| **Gegevensversleutelingssleutel van service** |Genereer de sleutel opnieuw op het fysieke apparaat en werk het virtuele apparaat daarna bij met de nieuwe sleutel. |Het is niet mogelijk om sleutels opnieuw te genereren op het virtuele apparaat. |

## <a name="prerequisites-for-the-virtual-device"></a>Vereisten voor het virtuele apparaat
In de volgende gedeelten worden de configuratievereisten voor het virtuele StorSimple-apparaat toegelicht. Zie [Beveiligingsoverwegingen voor het gebruik van een virtueel apparaat](storsimple-8000-security.md#storsimple-cloud-appliance-security) voordat u een virtueel apparaat implementeert.

#### <a name="azure-requirements"></a>Azure-vereisten
Voordat u het virtuele apparaat inricht, moet u de volgende voorbereidingen treffen in uw Azure-omgeving:

* Voor het virtuele apparaat [configureert u een virtueel netwerk in Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Als u Premium-opslag gebruikt, moet u een virtueel netwerk maken in een Azure-regio die ondersteuning biedt voor Premium-opslag. De Premium Storage-regio's zijn regio's die overeenkomen met de rij voor *Schijfruimte* in de lijst met [Azure Services per regio](https://azure.microsoft.com/en-us/regions/services).
* Het is raadzaam om de standaard-DNS-server van Azure te gebruiken. Geef liever geen eigen naam op voor de DNS-server. Als uw DNS-servernaam niet geldig is of als de DNS-server IP-adressen niet correct kan omzetten, mislukt het maken van het virtuele apparaat.
* Punt-naar-site en site-naar-site zijn optioneel, maar niet vereist. Als u wilt, kunt u deze opties configureren in meer geavanceerde scenario's.
* U kunt [virtuele Azure-machines](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (hostservers) maken in het virtuele netwerk; deze maken gebruik van de volumes die beschikbaar worden gesteld door het virtuele apparaat. Deze servers moeten aan de volgende vereisten voldoen:                             

  * Het moeten virtuele Windows- of Linux-machines zijn waarop de iSCSI-initiatorsoftware is geïnstalleerd.
  * Ze moeten in hetzelfde virtuele netwerk worden uitgevoerd als het virtuele apparaat.
  * Ze moeten in staat zijn om verbinding te maken met het iSCSI-doel van het virtuele apparaat via het interne IP-adres van het virtuele apparaat.
* Zorg ervoor dat u ondersteuning voor iSCSI en cloudverkeer hebt geconfigureerd in hetzelfde virtuele netwerk.

#### <a name="storsimple-requirements"></a>StorSimple-vereisten
Breng de volgende updates aan in uw Azure StorSimple-service voordat u een virtueel apparaat maakt:

* Voeg [Access Control Records](storsimple-manage-acrs.md) toe voor de virtuele machines die gebruikt gaan worden als hostservers voor uw virtuele apparaat.
* Gebruik een [opslagaccount](storsimple-manage-storage-accounts.md#add-a-storage-account) in dezelfde regio als het virtuele apparaat. Als u opslagaccounts in andere regio's gebruikt, kan dat leiden tot slechte prestaties. U kunt met het virtuele apparaat een Standard- of Premium-opslagaccount gebruiken. Meer informatie over het maken van een [Standard-opslagaccount](../storage/common/storage-create-storage-account.md) of een [Premium Storage-account](../storage/common/storage-premium-storage.md)
* Gebruik een ander opslagaccount voor het maken van het virtuele apparaat dan voor het apparaat dat u gebruikt voor uw gegevens. Als u hetzelfde opslagaccount gebruikt, kan dat leiden tot slechte prestaties.

Zorg ervoor dat u over de volgende informatie beschikt voordat u begint:

* Uw account voor de klassieke Azure Portal met referenties voor toegang.
* Een kopie van de gegevensversleutelingssleutel van de service van uw fysieke apparaat.

## <a name="create-and-configure-the-virtual-device"></a>Het virtuele apparaat maken en configureren
Voordat u deze procedures uitvoert, zorgt u ervoor dat u voldoet aan de [vereisten voor het virtuele apparaat](#prerequisites-for-the-virtual-device).

Wanneer u een virtueel netwerk hebt gemaakt, een StorSimple Manager-service hebt gemaakt en uw fysieke StorSimple-apparaat hebt geregistreerd bij de service, volgt u de volgende stappen om een virtueel StorSimple-apparaat te maken en te configureren.

### <a name="step-1-create-a-virtual-device"></a>Stap 1: een virtueel apparaat maken
Voer de volgende stappen uit om het virtuele StorSimple-apparaat te maken.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Als het maken van het virtuele apparaat in deze stap mislukt, hebt u mogelijk geen verbinding met internet. Ga voor meer informatie naar [Problemen met internetverbinding oplossen](#troubleshoot-internet-connectivity-errors) wanneer u een virtueel apparaat maakt.

### <a name="step-2-configure-and-register-the-virtual-device"></a>Stap 2: het virtuele apparaat configureren en registreren
Voordat u aan deze procedure begint, zorgt u ervoor dat u een kopie van de gegevensversleutelingssleutel van de service hebt. De gegevensversleutelingssleutel van de service is gemaakt toen u uw eerste StorSimple-apparaat configureerde. U hebt toen de instructie gekregen om de sleutel op een veilige locatie op te slaan. Als u geen kopie van de gegevensversleutelingssleutel van de service hebt, moet u contact opnemen met Microsoft Ondersteuning voor hulp.

Voer de volgende stappen uit om het virtuele StorSimple-apparaat te configureren en te registreren.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-the-device-configuration-settings"></a>Stap 3: (optioneel) de configuratie-instellingen van het apparaat wijzigen
In het volgende gedeelte wordt beschreven welke apparaatconfiguratie-instellingen vereist zijn voor het virtuele StorSimple-apparaat als u CHAP of StorSimple Snapshot Manager wilt gebruiken of als u het beheerderswachtwoord van het apparaat wilt wijzigen.

#### <a name="configure-the-chap-initiator"></a>De CHAP-initiator configureren
Deze parameter bevat de referenties die uw virtuele apparaat (doel) verwacht te ontvangen van de initiators (servers) die proberen de volumes te openen. De initiators bieden een CHAP-gebruikersnaam en een CHAP-wachtwoord om zichzelf tijdens de verificatie te identificeren bij uw apparaat. Zie [CHAP configureren voor uw apparaat](storsimple-configure-chap.md#unidirectional-or-one-way-authentication) voor gedetailleerde stappen.

#### <a name="configure-the-chap-target"></a>Het CHAP-doel configureren
Deze parameter bevat de referenties die uw virtuele apparaat gebruikt wanneer een CHAP-initiator wederzijdse verificatie of verificatie in twee richtingen aanvraagt. Uw virtuele apparaat maakt gebruik van een omgekeerde CHAP-gebruikersnaam en een omgekeerd CHAP-wachtwoord om zich tijdens het verificatieproces bij de initiator te identificeren. De CHAP-doelinstellingen zijn algemene instellingen. Wanneer deze worden toegepast, wordt CHAP-verificatie gebruikt voor alle volumes die zijn verbonden met het virtuele opslagapparaat. Zie [CHAP configureren voor uw apparaat](storsimple-configure-chap.md#bidirectional-or-mutual-authentication) voor gedetailleerde stappen.

#### <a name="configure-the-storsimple-snapshot-manager-password"></a>Het wachtwoord voor StorSimple Snapshot Manager configureren
De StorSimple Snapshot Manager-software bevindt zich op uw Windows-host. Met deze software kunnen beheerders de back-ups van uw StorSimple-apparaat beheren. De back-ups zijn in feite momentopnamen die lokaal en in de cloud worden opgeslagen.

> [!NOTE]
> Voor het virtuele apparaat is uw Windows-host een virtuele Azure-machine.
>
>

Wanneer u in StorSimple Snapshot Manager een apparaat configureert, wordt u gevraagd om het IP-adres en het wachtwoord van het StorSimple-apparaat op te geven voor verificatie van uw opslagapparaat. Zie [Het wachtwoord voor StorSimple Snapshot Manager configureren](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password) voor gedetailleerde stappen.

#### <a name="change-the-device-administrator-password"></a>Het beheerderswachtwoord voor het apparaat wijzigen
Als u de Windows PowerShell-interface gebruikt voor toegang tot het virtuele apparaat, moet u een beheerderswachtwoord voor het apparaat invoeren. Voor de beveiliging van uw gegevens moet u dit wachtwoord wijzigen voordat u het virtuele apparaat kunt gebruiken. Zie [Het beheerderswachtwoord voor het apparaat configureren](storsimple-change-passwords.md#change-the-device-administrator-password) voor gedetailleerde stappen.

## <a name="connect-remotely-to-the-virtual-device"></a>Extern verbinding maken met het virtuele apparaat
Externe toegang tot uw virtuele apparaat via de Windows PowerShell-interface is niet standaard ingeschakeld. U moet eerst extern beheer van het virtuele apparaat inschakelen en dit daarna inschakelen op de client die u gaat gebruiken voor toegang tot uw virtuele apparaat.

Het proces om extern verbinding te maken, bestaat uit twee stappen en wordt hieronder beschreven.

### <a name="step-1-configure-remote-management"></a>Stap 1: extern beheer configureren
Voer de volgende stappen uit om extern beheer te configureren voor uw virtuele StorSimple-apparaat.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-the-virtual-device"></a>Stap 2: extern toegang verkrijgen tot het virtuele apparaat
Wanneer u extern beheer hebt ingeschakeld op de configuratiepagina van het StorSimple-apparaat, kunt u met behulp van Windows PowerShell extern verbinding maken met het virtuele apparaat vanaf een andere virtuele machine in hetzelfde virtuele netwerk. U kunt bijvoorbeeld verbinding maken vanaf de host-VM die u hebt geconfigureerd en gebruikt om verbinding te maken met iSCSI. Bij de meeste implementaties hebt u al eerder een openbaar eindpunt geopend voor toegang tot uw host-VM; deze virtuele machine kunt u vervolgens gebruiken voor toegang tot het virtuele apparaat.

> [!WARNING]
> **Voor een betere beveiliging wordt aangeraden HTTPS te gebruiken bij het verbinden met de eindpunten en om de eindpunten te verwijderen nadat u uw externe PowerShell-sessie hebt voltooid.**
>
>

U moet de procedures in [Op afstand verbinding maken met uw StorSimple-apparaat](storsimple-remote-connect.md) volgen voor het instellen van externe toegang tot uw virtuele apparaat.

## <a name="connect-directly-to-the-virtual-device"></a>Rechtstreeks verbinding maken met het virtuele apparaat
U kunt ook rechtstreeks verbinding maken met het virtuele apparaat. Als u rechtstreeks verbinding wilt maken met het virtuele apparaat vanaf een andere computer buiten het virtuele netwerk of buiten de Microsoft Azure-omgeving, moet u extra eindpunten maken, zoals wordt beschreven in de volgende procedure.

Voer de volgende stappen uit om een openbaar eindpunt te maken op het virtuele apparaat.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

U doet er verstandig aan om verbinding te maken via een andere virtuele machine in hetzelfde virtuele netwerk, omdat er dan in uw virtuele netwerk een minimaal aantal openbare eindpunten nodig is. Als u deze methode gebruikt, maakt u verbinding met de virtuele machine via een extern bureaublad. Daarna configureert u de virtuele machine voor gebruik, net zoals u dat bij andere Windows-clients zou doen in een lokaal netwerk. U hoeft het openbare-poortnummer niet toe te voegen omdat de poort al bekend is.

## <a name="work-with-the-storsimple-virtual-device"></a>Werken met het virtuele StorSimple-apparaat
Nu u het virtuele StorSimple-apparaat hebt gemaakt en geconfigureerd, kunt u ermee aan de slag. U kunt werken met volumecontainers, volumes en back-upbeleid op een virtueel apparaat, net zoals u dat met een fysiek StorSimple-apparaat zou doen. Het enige verschil is dat u ervoor moet zorgen dat u het virtuele apparaat hebt geselecteerd in de apparatenlijst. Zie [De StorSimple Manager-service gebruiken voor het beheren van een virtueel apparaat](storsimple-manager-service-administration.md) voor stapsgewijze instructies voor de verschillende beheertaken voor het virtuele apparaat.

In de volgende gedeelten worden enkele van de verschillen besproken die u tegenkomt wanneer u met een virtueel apparaat werkt.

### <a name="maintain-a-storsimple-virtual-device"></a>Een virtueel StorSimple-apparaat onderhouden
In vergelijking met het fysieke apparaat is voor het virtuele apparaat slechts weinig onderhoud vereist, omdat het apparaat alleen uit software bestaat. U hebt de volgende opties:

* **Software-updates**: u kunt de datum bekijken waarop de software voor het laatst is bijgewerkt én u ziet een overzicht van de updatestatusberichten. U kunt **Op updates scannen** onder aan de pagina gebruiken om handmatig te controleren op nieuwe updates. Als er updates beschikbaar zijn, klikt u op **Updates installeren** om ze te installeren. Omdat er op het virtuele apparaat slechts één interface beschikbaar is, vindt er een korte serviceonderbreking plaats tijdens het toepassen van de updates. Het virtuele apparaat wordt afgesloten en opnieuw opgestart (indien nodig) om nieuwe updates toe te passen. Zie [Uw apparaat bijwerken](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal) voor stapsgewijze instructies.
* **Ondersteuningspakket**: u kunt een ondersteuningspakket maken en uploaden om Microsoft Ondersteuning te helpen met het oplossen van problemen met uw virtuele apparaat. Zie [Een ondersteuningspakket maken en beheren](storsimple-create-manage-support-package.md) voor stapsgewijze instructies.

### <a name="storage-accounts-for-a-virtual-device"></a>Opslagaccounts voor een virtueel apparaat
Opslagaccounts worden gemaakt voor gebruik door de StorSimple Manager-service, het virtuele apparaat en het fysieke apparaat. Wanneer u uw opslagaccounts maakt, doet u er verstandig aan om in de beschrijvende naam een regio-id te gebruiken; zo zorgt u ervoor dat de regio consistent wordt gebruikt in alle systeemonderdelen. Voor een virtueel apparaat is het van belang dat alle onderdelen zich in dezelfde regio bevinden. Dit voorkomt prestatieproblemen.

Zie [Een opslagaccount toevoegen](storsimple-manage-storage-accounts.md#add-a-storage-account) voor stapsgewijze instructies.

### <a name="deactivate-a-storsimple-virtual-device"></a>Een virtueel StorSimple-apparaat deactiveren
Als u een virtueel apparaat deactiveert, worden de virtuele machine en de resources verwijderd die zijn gemaakt tijdens het inrichten van het apparaat. Wanneer het virtuele apparaat wordt gedeactiveerd, kan het niet meer worden hersteld naar de oorspronkelijke staat. Voordat u het virtuele apparaat deactiveert, beëindigt of verwijdert u de clients en hosts die er afhankelijk van zijn.

Als u een virtueel apparaat deactiveert, resulteert dat in de volgende acties:

* Het virtuele apparaat wordt verwijderd.
* De besturingssysteemschijf en gegevensschijven die voor het virtuele apparaat zijn gemaakt, worden verwijderd.
* De gehoste service en het virtuele netwerk die zijn gemaakt tijdens het inrichten, blijven behouden. Als u deze niet gebruikt, moet u ze handmatig verwijderen.
* De cloudmomentopnamen die voor het virtuele apparaat zijn gemaakt, blijven behouden.

Zie [Uw StorSimple-apparaat deactiveren en verwijderen](storsimple-deactivate-and-delete-device.md) voor stapsgewijze instructies.

Zodra het virtuele apparaat op de StorSimple Manager-servicepagina wordt weergegeven als gedeactiveerd, kunt u het virtuele apparaat uit de apparatenlijst op de pagina **Apparaten** verwijderen.

### <a name="start-stop-and-restart-a-virtual-device"></a>Een virtueel apparaat starten, stoppen en opnieuw opstarten
Op het fysieke StorSimple-apparaat zit een aan/uit-knop, maar dat is bij een virtueel StorSimple-apparaat niet het geval. Er kunnen zich echter situaties voordoen waarin u het virtuele apparaat wilt stoppen om het opnieuw op te starten. Voor sommige updates moet de virtuele machine bijvoorbeeld opnieuw worden opgestart om het updateproces te voltooien. De eenvoudigste manier om een virtueel apparaat te starten, te stoppen en opnieuw op te starten, is via de beheerconsole voor virtuele machines.

In de beheerconsole is de status van het virtuele apparaat **Actief**, omdat het apparaat standaard wordt gestart nadat het is gemaakt. U kunt virtuele machines te allen tijde starten, stoppen en opnieuw opstarten.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-to-factory-defaults"></a>De fabrieksinstellingen terugzetten
Als u besluit dat u helemaal opnieuw wilt beginnen met uw virtuele apparaat, deactiveert en verwijdert u het oude apparaat en maakt u een nieuw apparaat. Net als bij het opnieuw instellen van uw fysieke apparaat, zijn er voor uw nieuwe virtuele apparaat nog geen updates geïnstalleerd. Controleer daarom op updates voordat u het nieuwe apparaat gebruikt.

## <a name="fail-over-to-the-virtual-device"></a>Failover naar het virtuele apparaat
Het virtuele StorSimple-apparaat is onder meer ontworpen voor herstel na noodgevallen. In noodgevallen is het fysieke StorSimple-apparaat of zelfs het gehele datacenter mogelijk niet beschikbaar. In dergelijke gevallen kunt u een virtueel apparaat gebruiken om de werkzaamheden op een andere locatie voort te zetten. Tijdens het herstel na een noodgeval krijgen de volumecontainers van het bronapparaat een andere eigenaar en worden ze overgedragen naar het virtuele apparaat. De vereisten voor herstel na noodgevallen zijn dat het virtuele apparaat al is gemaakt en geconfigureerd, dat alle volumes in de volumecontainer offline beschikbaar zijn en dat er een cloudmomentopname aan de volumecontainer is gekoppeld.

> [!NOTE]
> * Als u een virtueel apparaat als secundair apparaat gebruikt voor herstel na noodgevallen, moet u er rekening mee houden dat de 8010 30 TB aan Standard-opslag biedt en de 8020 64 TB aan Premium-opslag. De 8020 met een hogere capaciteit is mogelijk beter geschikt voor herstel na noodgevallen.
> * Als u een apparaat hebt met Update 2, kunt u er geen failover voor uitvoeren naar een apparaat met software die ouder is dan Update 1. Ook kunt u er op een dergelijk apparaat geen kloon van opslaan. U kunt echter wel een failover van een apparaat met Update 2 uitvoeren naar een apparaat met Update 1 (1.1 of 1.2)
>
>

Zie [Failover naar een virtueel apparaat](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device) voor een stapsgewijze procedure.

## <a name="shut-down-or-delete-the-virtual-device"></a>Het virtuele apparaat uitschakelen of verwijderen
Als u al eerder een virtueel StorSimple-apparaat hebt geconfigureerd, maar u geen rekenkosten meer wilt betalen voor het gebruik hiervan, kunt u het virtuele apparaat uitschakelen. Als u het virtuele apparaat uitschakelt, worden het besturingssysteem en de gegevensschijven in de opslag niet verwijderd. Er worden dan alleen geen kosten meer doorberekend voor uw abonnement. De opslagkosten voor het besturingssysteem en de gegevensschijven blijven echter van toepassing.

Als u het virtuele apparaat verwijdert of uitschakelt, wordt het als **Offline** weergegeven op de pagina Apparaten van de StorSimple Manager-service. U kunt ervoor kiezen om het apparaat te deactiveren of uit te schakelen als u ook de back-ups wilt verwijderen die door het virtuele apparaat zijn gemaakt. Zie [Een StorSimple-apparaat deactiveren en verwijderen](storsimple-deactivate-and-delete-device.md) voor meer informatie.

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Problemen met internetverbinding oplossen
Als er tijdens het maken van een virtueel apparaat geen verbinding is met internet, mislukt deze stap. Als u wilt vaststellen of de fout wordt veroorzaakt door de internetverbinding, voert u de volgende stappen uit in de klassieke Azure-portal:

1. Maak een virtuele Windows Server 2012-machine in Azure. Deze virtuele machine moet hetzelfde opslagaccount, VNet en subnet gebruiken als die worden gebruikt door uw virtuele apparaat. Als u al een bestaande Windows Server-host in Azure hebt die hetzelfde opslagaccount, Vnet en subnet gebruikt, kunt u deze ook gebruiken om het probleem met de internetverbinding op te lossen.
2. Meld u extern aan bij de virtuele machine die u in de vorige stap hebt gemaakt.
3. Open een opdrachtvenster in de virtuele machine (Win + R en typ vervolgens `cmd`).
4. Voer de volgende opdracht uit bij de prompt.

    `nslookup windows.net`
5. Als `nslookup` mislukt, zorgt het probleem met de internetverbinding ervoor dat het virtuele apparaat zich niet kan registreren bij de StorSimple Manager-service.
6. Breng de benodigde wijzigingen aan in uw virtuele netwerk om ervoor te zorgen dat het virtuele apparaat toegang kan krijgen tot Azure-sites zoals 'windows.net'.

## <a name="next-steps"></a>Volgende stappen
* Ontdek hoe u [de StorSimple Manager-service gebruikt om een virtueel apparaat te beheren](storsimple-manager-service-administration.md).
* Ontdek hoe u [een StorSimple-volume herstelt op basis van een back-upset](storsimple-restore-from-backup-set.md).
