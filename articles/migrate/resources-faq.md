---
title: Azure Migrate - Frequently Asked Questions (FAQ) | Microsoft Docs
description: Veelgestelde vragen over Azure Migrate adressen
author: snehaamicrosoft
ms.service: azure-migrate
ms.topic: conceptual
ms.date: 12/05/2018
ms.author: snehaa
ms.openlocfilehash: ebc4393341341b3b73165a166a650ae1a6f431ff
ms.sourcegitcommit: 1c1f258c6f32d6280677f899c4bb90b73eac3f2e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/11/2018
ms.locfileid: "53257791"
---
# <a name="azure-migrate---frequently-asked-questions-faq"></a>Azure Migrate - Asked Frequently Questions (FAQ)

Dit artikel bevat veelgestelde vragen over Azure Migrate. Hebt u geen verdere query's na het lezen van dit artikel, plaatst u deze op de [Azure Migrate forum](https://aka.ms/AzureMigrateForum).

## <a name="general"></a>Algemeen

### <a name="does-azure-migrate-support-assessment-of-only-vmware-workloads"></a>Biedt Azure Migrate ondersteuning voor beoordeling van de VMware-workloads?

Ja, Azure Migrate ondersteunt momenteel alleen beoordeling van de VMware-workloads. Ondersteuning voor Hyper-V en fysieke servers wordt in de toekomst worden ingeschakeld.

### <a name="does-azure-migrate-need-vcenter-server-to-discover-a-vmware-environment"></a>Heeft Azure Migrate vCenter-Server voor het detecteren van een VMware-omgeving nodig?

Ja, vereist Azure Migrate vCenter-Server voor het detecteren van een VMware-omgeving. Het biedt geen ondersteuning voor detectie van ESXi-hosts die niet worden beheerd door een vCenter-Server.

### <a name="how-is-azure-migrate-different-from-azure-site-recovery"></a>Wat is Azure Migrate verschil met Azure Site Recovery?

Azure Migrate is een service voor beveiligingsbeoordeling die helpt u bij het detecteren van uw on-premises workloads en plan uw migratie naar Azure. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure), samen met enkel een oplossing voor noodherstel, helpt u bij het migreren van on-premises werkbelastingen naar IaaS-VM's in Azure.

### <a name="whats-the-difference-between-using-azure-migrate-for-assessments-and-the-map-toolkit"></a>Wat is het verschil tussen het gebruik van Azure Migrate voor beoordelingen en de Map Toolkit?

[Azure Migrate](migrate-overview.md) biedt migratie-analyse met name om te helpen bij de voorbereiding op de migratie en evaluatie van de on-premises werkbelastingen in Azure. [Microsoft Assessment and Planning (MAP) Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=7826) heeft andere functies. Voorbeeld: de migratie plannen voor nieuwere versies van Windows-client en server-besturingssystemen, software gebruik bijhouden enzovoort. Voor deze scenario's, echter ook doorgaan met de MAP Toolkit.


### <a name="how-is-azure-migrate-different-from-azure-site-recovery-deployment-planner"></a>Wat is Azure Migrate verschil met Azure Site Recovery Deployment Planner?

Azure Migrate is een hulpprogramma voor migratieplanning en Azure Site Recovery Deployment Planner is een hulpprogramma voor het plannen noodherstel (DR).

**Migratie van VMware naar Azure**: Als u van plan bent uw on-premises workloads migreren naar Azure, Azure Migrate gebruiken voor het plannen van de migratie. Azure Migrate beoordeelt on-premises werkbelastingen en biedt richtlijnen, inzichten en mechanismen om u te helpen bij het migreren naar Azure. Wanneer u klaar met uw migratieplan bent, kunt u services zoals Azure Site Recovery en Azure Database Migration Service de machines migreren naar Azure.

**Migratie van Hyper-V naar Azure**: Azure Migrate ondersteunt momenteel alleen evaluatie van virtuele VMware-machines voor migratie naar Azure. Ondersteuning voor Hyper-V is op de roadmap voor Azure Migrate. In de tussentijd kunt u Site Recovery Deployment Planner. Zodra de Hyper-V-ondersteuning is ingeschakeld in Azure Migrate, kunt u Azure Migrate kunt gebruiken voor het plannen van de migratie van Hyper-V-werkbelastingen.

**Herstel na noodgevallen van VMware/Hyper-V naar Azure**: Als u van plan bent om te doen, herstel na noodgeval (DR) op Azure met behulp van Azure Site Recovery (Site Recovery), gebruikt u Site Recovery Deployment Planner voor herstel na Noodgevallen plannen. Site Recovery Deployment Planner biedt een diepgaande, ASR-specifieke beoordeling van uw on-premises omgeving. Het biedt aanbevelingen die door Site Recovery voor geslaagde DR-bewerkingen, zoals replicatie, failover van uw virtuele machines vereist zijn.  

### <a name="which-azure-geographies-are-supported-by-azure-migrate"></a>Welke Azure-regio's worden ondersteund door Azure Migrate?

Azure Migrate ondersteunt momenteel Verenigde Staten en Azure Government als de project-locaties. Hoewel u alleen migration-projecten in deze regio's maken kunt, kunt u nog steeds uw machines voor beoordelen [doellocaties voor meerdere](https://docs.microsoft.com/azure/migrate/how-to-modify-assessment#edit-assessment-properties). De geografische locatie van project wordt alleen gebruikt voor het opslaan van de gedetecteerde metagegevens.

**Geografie** | **De metagegevens van opslaglocatie**
--- | ---
Koppelt statussen zijn netwerk | West-Centraal VS of VS-Oost
Azure Government | VS (overheid) - Virginia

### <a name="how-does-the-on-premises-site-connect-to-azure-migrate"></a>Hoe worden de on-premises site, maakt verbinding met Azure Migrate?

De verbinding kan worden via internet of het gebruik van ExpressRoute met openbare peering.

### <a name="can-i-harden-the-vm-set-up-with-the-ova-template"></a>Kan ik beveiliging van de virtuele machine met behulp van het OVA-sjabloon instellen?

Extra onderdelen (zoals antivirusprogramma's) kunnen worden toegevoegd in het OVA-sjabloon, zolang de communicatie en firewall-regels die zijn vereist voor het apparaat Azure Migrate om te werken zijn ongewijzigd worden gelaten.   

## <a name="discovery"></a>Detectie

### <a name="what-data-is-collected-by-azure-migrate"></a>Welke gegevens worden verzameld door Azure Migrate?

Azure Migrate biedt ondersteuning voor twee detectiemethoden: op apparaten gebaseerde detectie en op agents gebaseerde detectie.
De detectie op basis van een apparaat verzamelt metagegevens over de on-premises VM's, de volledige lijst met metagegevens die zijn verzameld door het apparaat vindt u hieronder:

**Configuratiegegevens van de virtuele machine**
- Naam van de virtuele machine weergegeven (op vCenter)
- VM-inventarisatie-pad (host/cluster/map in vCenter)
- IP-adres
- MAC-adres
- Besturingssysteem
- Aantal kernen, schijven, NIC 's
- Grootte van geheugen, schijf-grootten

**Prestatiegegevens van de virtuele machine**
- CPU-gebruik
- Geheugengebruik
- Voor elke schijf die is gekoppeld aan de virtuele machine:
  - Schijf lezen doorvoer
  - Doorvoer van schrijfbewerkingen per schijf
  - Schijf lezen-bewerkingen per seconde
  - Schijf schrijft-bewerkingen per seconde
- Voor elke netwerkadapter die is gekoppeld aan de virtuele machine:
  - Het netwerk
  - Netwerk-uitgaand

De op agents gebaseerde detectie is een optie die beschikbaar is naast de op apparaten gebaseerde detectie, en helpt klanten om [afhankelijkheden van de on-premises VM's te visualiseren](how-to-create-group-machine-dependencies.md). Met de afhankelijkheidsagents worden details verzameld zoals FQDN, besturingssysteem, IP-adres, MAC-adres, processen die worden uitgevoerd op de VM, en de binnenkomende/uitgaande TCP-verbindingen van de VM. De detectie op basis van een agent is optioneel en u kunt de agents niet te installeren als u niet wilt visualiseren van de afhankelijkheden van de virtuele machines.

### <a name="would-there-be-any-performance-impact-on-the-analyzed-esxi-host-environment"></a>Zou er prestatie-invloed op de geanalyseerde ESXi-host-omgeving?

In het geval van de [benadering van de detectie één keer](https://docs.microsoft.com/azure/migrate/concepts-collector#discovery-methods), de prestatiegegevens worden verzameld het statistiekniveau van de voor de vCenter-server zelf zou moeten zijn ingesteld op 3. Instellen op dit niveau verzamelen over een grote hoeveelheid gegevens die in de vCenter-Server-database zouden worden opgeslagen voor probleemoplossing verzameld. Het kan dus leiden tot prestatieproblemen op de vCenter-Server. Er is minimaal effect heeft op de ESXi-host.

Geïntroduceerd continue profileren van prestatiegegevens (dat zich in preview). Met continue-profilering, is er niet langer een hoeft te wijzigen van de vCenter Server statistiekniveau een analyse op basis van prestaties uit te voeren. Het collector-apparaat wordt nu de on-premises computers om te meten van de prestatiegegevens van de virtuele machines profileren. Dit zou bijna nul prestatie-invloed hebben op de ESXi-hosts, maar ook op de vCenter-Server.

### <a name="where-is-the-collected-data-stored-and-for-how-long"></a>Waar worden de verzamelde gegevens opgeslagen en hoe lang?

De gegevens die zijn verzameld door de collector-apparaat is opgeslagen in de Azure-locatie die u opgeeft tijdens het maken van het migratieproject. De gegevens worden veilig opgeslagen in een Microsoft-abonnement en wordt verwijderd wanneer de gebruiker wordt verwijderd van de Azure Migrate-project.

Als u agents op de virtuele machines installeren, wordt de gegevens die zijn verzameld door de agents van de afhankelijkheid voor visualisatie van afhankelijkheden opgeslagen in de Verenigde Staten in een Log Analytics-werkruimte hebt gemaakt in het abonnement van de gebruiker. Deze gegevens worden verwijderd wanneer u de Log Analytics-werkruimte in uw abonnement verwijdert. [Meer informatie](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization).

### <a name="is-the-data-encrypted-at-rest-and-while-in-transit"></a>De gegevens worden versleuteld in rust en onderweg zijn?

Ja, de verzamelde gegevens worden versleuteld in rust en onderweg zijn. De metagegevens die zijn verzameld door het apparaat veilig verzonden naar de Azure Migrate-service via internet via https. De verzamelde metagegevens worden opgeslagen in [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/database-encryption-at-rest) en [Azure blob-opslag](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) in een Microsoft-abonnement en in rust worden versleuteld.

De gegevens die zijn verzameld door de agents afhankelijkheid is ook versleuteld in doorvoer (beveiligde https-kanaal) en wordt opgeslagen in een Log Analytics-werkruimte in het abonnement van de gebruiker. Het is ook versleuteld in rust.

### <a name="how-does-the-collector-communicate-with-the-vcenter-server-and-the-azure-migrate-service"></a>Hoe de collector communiceren met de vCenter-Server en de service Azure Migrate?

Het collector-apparaat verbinding maakt met de vCenter-Server (poort 443) met behulp van de referenties die zijn opgegeven door de gebruiker in het apparaat. Deze query uitgevoerd voor de vCenter-Server met behulp van VMware PowerCLI voor het verzamelen van metagegevens over de VM's beheerd door vCenter Server. Deze verzamelt beide configuratiegegevens over VM's (kernen, geheugen, schijven, NIC enzovoort) en de prestatiegeschiedenis van elke virtuele machine voor de laatste maand van vCenter-Server. De verzamelde metagegevens wordt verzonden naar de service Azure Migrate (via internet via https) voor de beoordeling. [Meer informatie](concepts-collector.md)

### <a name="can-i-connect-the-same-collector-appliance-to-multiple-vcenter-servers"></a>Kan ik het dezelfde collector-apparaat verbinden met meerdere vCenter-servers?

Ja, een enkel collector-apparaat kan worden gebruikt voor het detecteren van meerdere vCenter-Servers, maar niet gelijktijdig. U moet de detecties na elkaar uitgevoerd.

### <a name="is-the-ova-template-used-by-site-recovery-integrated-with-the-ova-used-by-azure-migrate"></a>Is het OVA-sjabloon die wordt gebruikt door Site Recovery geïntegreerd met het ova-bestand gebruikt door Azure Migrate?

Er is momenteel geen-integratie. De. OVA-sjabloon in Site Recovery wordt gebruikt voor het instellen van een Site Recovery-configuratieserver voor replicatie van virtuele VMware-machine/fysieke server. De. OVA die worden gebruikt door Azure Migrate wordt gebruikt voor het detecteren van VMware-VM's beheerd door een vCenter-server voor de doeleinden van migratie-analyse.

### <a name="i-changed-my-machine-size-can-i-rerun-the-assessment"></a>Ik heb mijn machinegrootte gewijzigd. Kan ik de evaluatie opnieuw uitvoeren?

Als u wijzigt de instellingen op een virtuele machine die u wilt beoordelen, Ontdek trigger opnieuw met behulp van het collector-apparaat. Gebruik in het toestel, de **verzamelen opnieuw starten** optie om dit te doen. Nadat de verzameling gereed is, selecteert u in de portal de optie **Opnieuw berekenen** voor de evaluatie om de evaluatieresultaten op te halen.

### <a name="how-can-i-discover-a-multi-tenant-environment-in-azure-migrate"></a>Hoe kan ik een multitenant-omgeving in Azure Migrate detecteren?

Als u een omgeving die wordt gedeeld door tenants hebt en u niet wilt detecteren van de virtuele machines van één tenant in een andere tenant-abonnement, kunt u het veld bereik in het collector-apparaat als bereik voor de detectie. Als de tenants hosts delen, een referentie met alleen-lezen toegang tot alleen de virtuele machines die horen bij de specifieke tenant maken en deze referentie gebruiken in het collector-apparaat en het bereik opgeven als de host te doen de detectie. U kunt ook u kunt ook mappen maken in vCenter Server (Stel Map1 voor tenant1 en folder2 voor tenant2), onder de gedeelde host, de virtuele machines voor tenant1 in Map1 en tenant2 verplaatsen naar folder2 en vervolgens het bereik van de detecties in de collector dienovereenkomstig door op te geven op de juiste map.

### <a name="how-many-virtual-machines-can-be-discovered-in-a-single-migration-project"></a>Het aantal virtuele machines kunnen worden gevonden in een enkele migration-project?

U kunt 1500 virtuele machines in een enkele migratieproject detecteren. Als u meer computers in uw on-premises-omgeving hebt [meer](how-to-scale-assessment.md) over hoe u een grote omgeving in Azure Migrate kunt detecteren.

## <a name="assessment"></a>Beoordeling

### <a name="does-azure-migrate-support-enterprise-agreement-ea-based-cost-estimation"></a>Ondersteuning voor Azure Migrate Enterprise Agreement (EA) op basis van kostenraming?

Azure Migrate ondersteunt momenteel geen schatting van de kosten voor [Enterprise overeenkomst-aanbieding](https://azure.microsoft.com/offers/enterprise-agreement-support/). De oplossing is om te betalen per gebruik als de aanbieding en handmatig opgeven van het kortingspercentage (van toepassing op het abonnement) in het veld 'Korting' van de evaluatie-eigenschappen opgeven.

  ![Korting](./media/resources-faq/discount.png)


## <a name="dependency-visualization"></a>Visualisatie van afhankelijkheden

> [!NOTE]
> De functie voor visualisatie van afhankelijkheden is niet beschikbaar in Azure Government.

### <a name="what-is-dependency-visualization"></a>Wat is visualisatie van afhankelijkheden?

Visualisatie van afhankelijkheden, kunt u groepen met VM's voor migratie met meer vertrouwen beoordelen door machineafhankelijkheden cross controleren voordat u een evaluatie uitvoert. Visualisatie van afhankelijkheden helpt u om ervoor te zorgen dat er niets is overgebleven, voorkomen van onverwachte storingen wanneer u naar Azure migreert. Azure Migrate maakt gebruik van de oplossing Serviceoverzicht in Log Analytics om in te schakelen visualisatie van afhankelijkheden.

### <a name="do-i-need-to-pay-to-use-the-dependency-visualization-feature"></a>Moet ik betalen voor het gebruik van de functie voor visualisatie van afhankelijkheden?

Nee. Meer informatie over prijzen voor Azure Migrate vindt u [hier](https://azure.microsoft.com/pricing/details/azure-migrate/).

### <a name="do-i-need-to-install-anything-for-dependency-visualization"></a>Moet ik niets voor visualisatie van afhankelijkheden te installeren?

Voor het gebruik van visualisatie van afhankelijkheden, die u wilt downloaden en installeren van agents op elke on-premises computer die u wilt evalueren.

- [Microsoft Monitoring agent(MMA)](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) moet worden geïnstalleerd op elke computer.
- De [agent voor afhankelijkheden](https://docs.microsoft.com/azure/monitoring/monitoring-service-map-configure) moet worden geïnstalleerd op elke computer.
- Bovendien, als u computers geen verbinding met internet hebt, moet u om te downloaden en Log Analytics-gateway installeren op deze.

U hoeft niet deze agents op computers die u beoordelen wilt, tenzij u visualisatie van afhankelijkheden.

### <a name="can-i-use-an-existing-workspace-for-dependency-visualization"></a>Kan ik een bestaande werkruimte gebruiken voor visualisatie van afhankelijkheden?

Ja, Azure Migrate nu kunt u een bestaande werkruimte koppelen aan het migratieproject en gebruikmaken van deze voor visualisatie van afhankelijkheden. [Meer informatie](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization#how-does-it-work).

### <a name="can-i-export-the-dependency-visualization-report"></a>Kan ik de visualisatie Afhankelijkheidsrapport exporteren?

Nee, de visualisatie van afhankelijkheden kan niet worden geëxporteerd. Echter, omdat Azure Migrate maakt gebruik van servicetoewijzing voor visualisatie van afhankelijkheden, kunt u de [Service kaart REST-API's](https://docs.microsoft.com/rest/api/servicemap/machines/listconnections) om de afhankelijkheden in een json-indeling.

### <a name="how-can-i-automate-the-installation-of-microsoft-monitoring-agent-mma-and-dependency-agent"></a>Hoe kan ik de installatie van Microsoft Monitoring Agent (MMA) en de agent voor afhankelijkheden automatiseren?

[Hier](https://docs.microsoft.com/azure/monitoring/monitoring-service-map-configure#installation-script-examples) is een script dat u voor de installatie van agent voor afhankelijkheden gebruiken kunt. Voor de MMA, [hier](https://gallery.technet.microsoft.com/scriptcenter/Install-OMS-Agent-with-2c9c99ab) is een script dat beschikbaar is op TechNet waarvan u gebruik kunt maken.

Naast scripts, kunt u ook gebruikmaken van hulpprogramma's voor implementatie, zoals System Center Configuration Manager (SCCM), [Intigua](https://www.intigua.com/getting-started-intigua-for-azure-migration) enzovoort naar de agents te implementeren.

### <a name="what-are-the-operating-systems-supported-by-mma"></a>Wat zijn de besturingssystemen die door MMA?

De lijst van Windows-besturingssystemen wordt ondersteund door de MMA is [hier](https://docs.microsoft.com/azure/log-analytics/log-analytics-concept-hybrid#supported-windows-operating-systems).
De lijst met Linux-besturingssystemen wordt ondersteund door de MMA is [hier](https://docs.microsoft.com/azure/log-analytics/log-analytics-concept-hybrid#supported-linux-operating-systems).

### <a name="what-are-the-operating-systems-supported-by-dependency-agent"></a>Wat zijn de besturingssystemen die ondersteund door de agent voor afhankelijkheden?

De lijst van Windows-besturingssystemen wordt ondersteund door de agent voor afhankelijkheden is [hier](https://docs.microsoft.com/azure/monitoring/monitoring-service-map-configure#supported-windows-operating-systems).
De lijst met Linux-besturingssystemen wordt ondersteund door de agent voor afhankelijkheden is [hier](https://docs.microsoft.com/azure/monitoring/monitoring-service-map-configure#supported-linux-operating-systems).

### <a name="can-i-visualize-dependencies-in-azure-migrate-for-more-than-one-hour-duration"></a>Kan ik meer dan één uur duurt afhankelijkheden in Azure Migrate visualiseren?
Nee, kunt u visualiseren afhankelijkheden voor de duur van maximaal één uur voor Azure Migrate. Azure Migrate kunt u terugkeren naar een bepaalde datum in de geschiedenis voor maximaal laatste maand, maar de maximale duur waarvoor u de afhankelijkheden visualiseren is tot 1 uur. Bijvoorbeeld, u kunt de functionaliteit van de duur van de tijd in de kaart van afhankelijkheden, gebruiken om afhankelijkheden voor gisteren, maar kan alleen weergeven voor een venster van één uur.

### <a name="is-dependency-visualization-supported-for-groups-with-more-than-10-vms"></a>Visualisatie van afhankelijkheden is wordt ondersteund voor groepen met meer dan 10 virtuele machines?
U kunt [visualiseren afhankelijkheden voor groepen](https://docs.microsoft.com/azure/migrate/how-to-create-group-dependencies) dat hebben van 10 virtuele machines, hebt u een groep met meer dan 10 virtuele machines, we raden u aan de groep in kleinere groepen splitsen en de afhankelijkheden visualiseren.


## <a name="next-steps"></a>Volgende stappen

- Lees de [Azure Migrate-overzicht](migrate-overview.md)
- Leer hoe u kunt [detecteren en evalueren](tutorial-assessment-vmware.md) een VMware-omgeving
