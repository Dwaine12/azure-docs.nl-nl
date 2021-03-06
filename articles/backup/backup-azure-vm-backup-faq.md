---
title: Veelgestelde vragen over Azure VM Backup
description: Antwoorden op veelgestelde vragen over de werking van Azure VM Backup, over de beperkingen en over wat er gebeurt wanneer het beleid wordt gewijzigd
services: backup
author: trinadhk
manager: shreeshd
keywords: azure vm backup, virtuele azure-machines herstellen, back-upbeleid
ms.service: backup
ms.topic: conceptual
ms.date: 8/16/2018
ms.author: trinadhk
ms.openlocfilehash: ff97d164ee8b2059e1b46377067041d6c381052b
ms.sourcegitcommit: 3dcb1a3993e51963954194ba2a5e42260d0be258
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/01/2018
ms.locfileid: "50753964"
---
# <a name="questions-about-the-azure-vm-backup-service"></a>Vragen over de Azure VM Backup-service
In dit artikel vindt u antwoorden op veelgestelde vragen om u snel een beeld te geven van de verschillende onderdelen van Azure VM Backup. Sommige antwoorden bevatten koppelingen naar artikelen met uitgebreide informatie over het onderwerp. U kunt ook in het [discussieforum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup) vragen over de Azure Backup-service plaatsen.

## <a name="configure-backup"></a>Back-up configureren
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Ondersteunen Recovery Services-kluizen klassieke virtuele machines of virtuele machines op basis van Resource Manager? <br/>
Recovery Services-kluizen ondersteunen beide modellen.  U kunt back-up van een klassieke virtuele machine of een Resource Manager-VM naar een Recovery Services-kluis.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup"></a>Welke configuraties worden niet ondersteund door Azure VM backup?
Doorloop [ondersteunde besturingssystemen](backup-azure-arm-vms-prepare.md#supported-operating-systems-for-backup) en [beperkingen van Azure VM backup](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Waarom zie ik mijn virtuele machine niet in de wizard Back-up configureren?
In configureren de wizard Back-up, Azure Backup alleen een lijst met virtuele machines die zijn:
  * Nog niet zijn beveiligd kunt u de status van de back-up van een virtuele machine controleren door te gaan naar de blade van de virtuele machine en de status van de back-up van Menu instellingen controleren. Meer informatie over [hoe u de back-upstatus van een virtuele machine controleert](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-operations-menu)
  * Tot dezelfde regio behoren als de virtuele machine

## <a name="backup"></a>Back-up maken
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>Geldt voor back-uptaken op aanvraag hetzelfde bewaarschema als voor geplande back-ups?
Nee. U moet de bewaartermijn voor een back-uptaak op aanvraag. Standaard is dit 30 dagen bewaard bij activering vanuit de portal.

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-to-work"></a>Ik heb onlangs Azure Disk Encryption ingeschakeld op een aantal virtuele machines. Worden mijn back-ups gewoon uitgevoerd?
U moet de Azure Backup-service toegang verlenen tot Key Vault. De hiervoor benodigde machtigingen kunt u in PowerShell opgeven door de stappen te volgen die worden beschreven in het gedeelte *Back-up inschakelen* van de documentatie voor [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-to-managed-disks-will-my-backups-continue-to-work"></a>Ik heb schijven van een virtuele machine gemigreerd naar beheerde schijven. Worden mijn back-ups gewoon uitgevoerd?
Ja, back-ups werken naadloos en niet nodig om back-up opnieuw te configureren.

### <a name="my-vm-is-shut-down-will-an-on-demand-or-a-scheduled-backup-work"></a>Mijn virtuele machine wordt afgesloten. Maakt een on-demand of een geplande back-werk?
Ja. Zelfs wanneer een virtuele machine is afgesloten back-ups werken en het herstelpunt dat is gemarkeerd als Crash consistent. Voor meer informatie, Zie de sectie van de consistentie van gegevens in [in dit artikel](backup-azure-vms-introduction.md#how-does-azure-back-up-virtual-machines)

### <a name="can-i-cancel-an-in-progress-backup-job"></a>Kan ik een back-uptaak in uitvoering annuleren?
Ja. Als het zich in de fase "Om momentopname te maken", kunt u back-uptaak annuleren. **U kunt een taak niet annuleren als de overdracht van gegevens van de momentopname uitgevoerd wordt**.

### <a name="i-enabled-resource-group-lock-on-my-backed-up-managed-disk-vms-will-my-backups-continue-to-work"></a>Ik resourcegroep vergrendeling ingeschakeld op mijn back-up virtuele machines op beheerde schijven. Worden mijn back-ups gewoon uitgevoerd?
Als de gebruiker Hiermee vergrendelt u de resourcegroep, is back-up-service niet kunt verwijderen van de oudere herstelpunten. Vanwege dit nieuwe back-ups mislukken omdat er een limiet van maximaal 18 herstelpunten die zijn opgelegd vanuit de back-end. Als uw back-ups met een interne fout opgetreden na de RG-vergrendeling mislukken, volgt u deze [stappen voor het verwijderen van de herstelbewerking wijst verzameling](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#clean-up-restore-point-collection-from-azure-portal).

### <a name="does-backup-policy-take-daylight-saving-timedst-into-account"></a>Back-upbeleid zomer-en opslaan van Time(DST) rekening gehouden?
Nee. Let erop dat de datum en tijd op uw lokale computer wordt weergegeven in uw lokale tijd en met uw huidige afwijking van de zomer-en wintertijd. Dus kan de geconfigureerde tijd voor geplande back-ups afwijken van de lokale tijd vanwege de Zomertijd.

### <a name="maximum-of-how-many-data-disks-can-i-attach-to-a-vm-to-be-backed-up-by-azure-backup"></a>Maximum van het aantal gegevensschijven kunnen ik toevoegen aan een virtuele machine naar een back-up door Azure Backup?
Azure Backup biedt nu ondersteuning voor back-up van virtuele machines met maximaal 16 schijven. Om op te halen van ondersteuning voor 16 schijven [een upgrade uitvoeren naar Azure VM Backup-stack V2](backup-upgrade-to-vm-backup-stack-v2.md). Alle virtuele machines inschakelen van beveiliging vanaf 24 september 2018 wordt get wordt ondersteund.

### <a name="does-azure-backup-support-standard-ssd-managed-disk"></a>Ondersteuning voor Azure back-Standard-SSD beheerde schijf?
Azure Backup ondersteunt [Standard-SSD Managed Disks](https://azure.microsoft.com/blog/announcing-general-availability-of-standard-ssd-disks-for-azure-virtual-machine-workloads/), een nieuw type duurzame opslag voor Microsoft Azure Virtual machines. Dit wordt ondersteund voor beheerde schijven in [Azure VM Backup-stack V2](backup-upgrade-to-vm-backup-stack-v2.md).

## <a name="restore"></a>Herstellen
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Hoe bepaal ik of ik beter afzonderlijke schijven kan herstellen of de virtuele machine als geheel?
Azure virtuele machine als geheel beschouwen als de optie voor een snelle versie maken. Wijzigingen voor VM-optie de namen van containers die worden gebruikt door deze schijven, het openbare IP-adressen en de netwerkinterfacenamen schijven herstellen. De wijziging is vereist voor het onderhouden van de uniekheid van resources die zijn gemaakt tijdens het maken van virtuele machine. Maar wordt de virtuele machine niet wordt toegevoegd aan de beschikbaarheidsset.

Gebruik de optie voor het herstellen van afzonderlijke schijven voor het volgende:
  * De virtuele machine die wordt gemaakt van point in time-configuratie zoals het wijzigen van de grootte aanpassen
  * Configuraties die niet aanwezig op het moment van back-up toevoegen
  * De naamgevingsconventie beheren voor de resources die worden gemaakt
  * De virtuele machine toevoegen aan de beschikbaarheidsset
  * Voor een andere configuratie die kan worden bereikt alleen met behulp van PowerShell of een declaratieve Sjabloondefinitie

### <a name="can-i-use-backups-of-unmanaged-disk-vm-to-restore-after-i-upgrade-my-disks-to-managed-disks"></a>Kan ik back-ups van niet-beheerde schijf-VM herstellen nadat ik mijn schijven te naar beheerde schijven upgraden gebruiken?
Ja, kunt u de back-ups uitgevoerd voordat de migratie van de schijven van niet-beheerde beheren. Standaard wordt de hersteltaak voor de virtuele machine een virtuele machine maken met niet-beheerde schijven. Herstel schijven functionaliteit kunt u schijven herstellen en te gebruiken voor het maken van een virtuele machine op beheerde schijven.

### <a name="what-is-the-procedure-to-restore-a-vm-to-a-restore-point-taken-before-the-conversion-from-unmanaged-to-managed-disks-was-done-for-a-vm"></a>Wat is de procedure voor het herstellen van een virtuele machine naar een herstelpunt gemaakt voordat de conversie van niet-beheerde naar beheerde schijven voor een virtuele machine is uitgevoerd?
In dit scenario wordt standaard hersteltaak voor de virtuele machine wordt een virtuele machine maken met niet-beheerde schijven. Een virtuele machine maken met beheerde schijven:
1. [Herstellen naar niet-beheerde schijven](tutorial-restore-disk.md#restore-a-vm-disk)
2. [De herstelde schijven converteren naar managed disks](tutorial-restore-disk.md#convert-the-restored-disk-to-a-managed-disk)
3. [Een virtuele machine maken met beheerde schijven](tutorial-restore-disk.md#create-a-vm-from-the-restored-disk) <br>
Voor PowerShell-cmdlets, raadpleegt u [hier](backup-azure-vms-automation.md#restore-an-azure-vm).

### <a name="can-i-restore-the-vm-if-my-vm-is-deleted"></a>Kan ik de virtuele machine herstellen als mijn virtuele machine wordt verwijderd?
Ja. Levenscyclus van de VM en de bijbehorende back-upitem zijn verschillend. Dus, zelfs als u de virtuele machine verwijdert, kunt u Ga naar het bijbehorende item in de Recovery Services-kluis back-up en herstellen met behulp van een van de herstelpunten te activeren.

## <a name="manage-vm-backups"></a>Back-ups van uw virtuele machine beheren
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>Wat gebeurt er wanneer ik het back-upbeleid voor een of meer virtuele machines wijzig?
Wanneer een nieuw beleid wordt toegepast op een of meer virtuele machines, schema en de retentie van het nieuwe beleid gevolgd. Als de retentie is uitgebreid, worden de bestaande herstelpunten gemarkeerd voor bewaring conform het nieuwe beleid. Als de retentie is beperkt, worden de bestaande herstelpunten gemarkeerd voor verwijdering in de eerstvolgende opschoontaak, en worden ze vervolgens verwijderd.

### <a name="how-can-i-move-a-vm-enrolled-in-azure-backup-between-resource-groups"></a>Hoe kan ik een virtuele machine geregistreerd bij Azure backup tussen resourcegroepen verplaatsen?
Volg de onderstaande stappen is in de doelresourcegroep die naar de VM waarvan een back-up is gemaakt
1. Tijdelijk back-up stoppen en back-upgegevens behouden
2. De virtuele machine verplaatsen naar de doelresourcegroep
3. Opnieuw beveiligen met dezelfde/nieuwe kluis

Gebruikers kunnen herstellen met de beschikbare herstelpunten die zijn gemaakt vóór de verplaatsing.
