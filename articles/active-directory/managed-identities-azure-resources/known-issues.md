---
title: Veelgestelde vragen en bekende problemen met beheerde identiteiten voor Azure-resources
description: Bekende problemen met beheerde identiteiten voor Azure-resources.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.assetid: 2097381a-a7ec-4e3b-b4ff-5d2fb17403b6
ms.service: active-directory
ms.component: msi
ms.devlang: ''
ms.topic: conceptual
ms.tgt_pltfrm: ''
ms.workload: identity
ms.date: 12/12/2017
ms.author: daveba
ms.openlocfilehash: b535939e200b533c06c97686897e283fb6cf57bc
ms.sourcegitcommit: 333d4246f62b858e376dcdcda789ecbc0c93cd92
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/01/2018
ms.locfileid: "52720181"
---
# <a name="faqs-and-known-issues-with-managed-identities-for-azure-resources"></a>Veelgestelde vragen en bekende problemen met beheerde identiteiten voor Azure-resources

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

## <a name="frequently-asked-questions-faqs"></a>Veelgestelde vragen

> [!NOTE]
> Beheerde identiteiten voor Azure-resources is de nieuwe naam voor de service die eerder de naam Managed Service Identity (MSI) had.

### <a name="does-managed-identities-for-azure-resources-work-with-azure-cloud-services"></a>Werkt beheerde identiteiten voor Azure-resources met Azure Cloud Services?

Nee, er zijn geen plannen voor de ondersteuning van beheerde identiteiten voor Azure-resources in Azure Cloud Services.

### <a name="does-managed-identities-for-azure-resources-work-with-the-active-directory-authentication-library-adal-or-the-microsoft-authentication-library-msal"></a>Werkt beheerde identiteiten voor Azure-resources met de Active Directory Authentication Library (ADAL) of de Microsoft Authentication Library (MSAL)?

Nee, beheerde identiteiten voor Azure-resources nog niet is geïntegreerd met ADAL of MSAL. Zie voor meer informatie over het ophalen van een token voor beheerde identiteiten voor Azure-resources met behulp van de REST-eindpunt, [over het gebruik van beheerde identiteiten voor Azure-resources op een Azure-VM aan een toegangstoken verkrijgen ](how-to-use-vm-token.md).

### <a name="what-is-the-security-boundary-of-managed-identities-for-azure-resources"></a>Wat is de beveiligingsgrens van beheerde identiteiten voor Azure-resources?

De beveiligingsgrens van de identiteit is de resource waaraan deze is gekoppeld. Bijvoorbeeld, de beveiligingsgrens voor een virtuele Machine met beheerde identiteiten voor Azure-resources ingeschakeld, wordt de virtuele Machine. Een code die wordt uitgevoerd op deze VM is kan aanroepen van de beheerde identiteiten voor Azure-resources eindpunt en de aanvraag-tokens. Het is de vergelijkbare ervaring met andere resources die ondersteuning bieden voor beheerde identiteiten voor Azure-resources.

### <a name="what-identity-will-imds-default-to-if-dont-specify-the-identity-in-the-request"></a>Welke identiteit wordt IMDS standaard als de identiteit niet opgeeft in de aanvraag?

- Als systeem toegewezen beheerde identiteit is ingeschakeld en er is geen identiteit in de aanvraag is opgegeven, wordt het systeem toegewezen identiteit beheerde IMDS standaard.
- Als het systeem toegewezen beheerde identiteit niet is ingeschakeld, en slechts één gebruiker toegewezen beheerde identiteit bestaat, standaard IMDS die door één gebruiker toegewezen beheerde identiteit. 
- Als systeem toegewezen beheerde identiteit is niet ingeschakeld en meerdere gebruiker beheerde identiteiten toegewezen bestaat, is het vereist dat u vervolgens een beheerde identiteit op te geven in de aanvraag.

### <a name="should-i-use-the-managed-identities-for-azure-resources-vm-imds-endpoint-or-the-vm-extension-endpoint"></a>Moet ik de beheerde identiteiten voor Azure-resources VM IMDS eindpunt of het eindpunt van de VM-extensie gebruiken?

Bij gebruik van beheerde identiteiten voor Azure-resources met virtuele machines, wordt u aangeraden met behulp van de beheerde identiteiten voor Azure-resources IMDS eindpunt. De Azure Instance Metadata Service is een toegankelijk is voor alle IaaS-VM's die zijn gemaakt via de Azure Resource Manager REST-eindpunt. Enkele van de voordelen van het gebruik van beheerde identiteiten voor Azure-resources via IMDS zijn:
    - Alle besturingssystemen van Azure IaaS ondersteund kunt beheerde identiteiten gebruiken voor Azure-resources via IMDS.
    - Niet meer hoeft te installeren van een uitbreiding op de virtuele machine om in te schakelen van beheerde identiteiten voor Azure-resources. 
    - De certificaten die op beheerde identiteiten voor Azure-resources zijn niet meer aanwezig zijn in de virtuele machine.
    - Het eindpunt IMDS is een bekende niet-routeerbare IP-adres, alleen beschikbaar vanuit de virtuele machine.

De beheerde identiteiten voor VM-extensie nog steeds beschikbaar is voor gebruik vandaag nog; Azure-resources echter vooruit we standaard het IMDS-eindpunt. De beheerde identiteiten voor VM-extensie voor Azure-resources worden afgeschaft in januari 2019. 

Zie voor meer informatie over Azure Instance Metadata Service [IMDS-documentatie](https://docs.microsoft.com/azure/virtual-machines/windows/instance-metadata-service)

### <a name="will-managed-identities-be-recreated-automatically-if-i-move-a-subscription-to-another-directory"></a>Beheerde identiteiten worden opnieuw gemaakt automatisch als ik een abonnement naar een andere directory verplaatst?

Nee. Als u een abonnement naar een andere map verplaatst, moet u handmatig opnieuw te maken en Azure RBAC-roltoewijzingen opnieuw verlenen.
    - Voor het systeem beheerde identiteiten toegewezen: uitschakelen en weer inschakelen.
    - Voor de gebruiker toegewezen beheerde identiteiten: verwijderen, opnieuw te maken en ze opnieuw koppelen aan de benodigde resources (bijvoorbeeld virtuele machines)

### <a name="can-i-use-a-managed-identity-to-access-a-resource-in-a-different-directorytenant"></a>Kan ik een beheerde identiteit gebruiken voor toegang tot een bron in een andere directory/tenant?

Nee. Beheerde identiteiten bieden momenteel geen ondersteuning voor scenario's voor cross-directory. 

### <a name="what-are-the-supported-linux-distributions"></a>Wat zijn de ondersteunde Linux-distributies?

Alle Linux-distributies ondersteund door Azure IaaS kunnen worden gebruikt met beheerde identiteiten voor Azure-resources via de IMDS-eindpunt. 

De beheerde identiteit voor Azure-resources VM-extensie (gepland voor de afschaffing in januari 2019) biedt alleen ondersteuning voor de volgende Linux-distributies:
- Stable van CoreOS
- CentOS 7.1
- Red Hat 7.2
- Ubuntu 15.04
- Ubuntu 16.04

Andere Linux-distributies worden momenteel niet ondersteund en extensie mislukken op niet-ondersteunde distributies.

De extensie werkt op CentOS 6,9. Echter, vanwege de afwezigheid van systeemondersteuning in 6,9, de uitbreiding wordt niet automatisch opnieuw starten als is vastgelopen of gestopt. Er wordt opnieuw opgestart wanneer de virtuele machine opnieuw wordt opgestart. Als u wilt de extensie handmatig opnieuw opstart, Zie [hoe doet u het beheerde identiteiten voor uitbreiding van de Azure-resources?](#how-do-you-restart-the-managed-identities-for-Azure-resources-extension)

### <a name="how-do-you-restart-the-managed-identities-for-azure-resources-extension"></a>Hoe start u de beheerde identiteit voor Azure-resources-uitbreiding opnieuw?
Op Windows en bepaalde versies van Linux, als de extensie wordt gestopt, kan de volgende cmdlet worden gebruikt om handmatig opnieuw starten:

```powershell
Set-AzureRmVMExtension -Name <extension name>  -Type <extension Type>  -Location <location> -Publisher Microsoft.ManagedIdentity -VMName <vm name> -ResourceGroupName <resource group name> -ForceRerun <Any string different from any last value used>
```

Waar: 
- Naam van de uitbreiding en het type voor Windows is: ManagedIdentityExtensionForWindows
- Naam van de uitbreiding en het type voor Linux is: ManagedIdentityExtensionForLinux

## <a name="known-issues"></a>Bekende problemen

### <a name="automation-script-fails-when-attempting-schema-export-for-managed-identities-for-azure-resources-extension"></a>"Automatiseringsscript" is mislukt bij het schema exporteren voor beheerde identiteiten voor uitbreiding van de Azure-resources

Als beheerde identiteiten voor Azure-resources op een virtuele machine is ingeschakeld, wordt de volgende fout weergegeven bij het gebruik van de functie 'Automatiseringsscript' voor de virtuele machine of de resourcegroep:

![Beheerde identiteiten voor een Azure-resources automatiseringsscript exportfout](./media/msi-known-issues/automation-script-export-error.png)

De beheerde identiteiten voor VM-extensie (gepland voor de afschaffing in januari 2019) momenteel geen biedt Azure-resources bieden ondersteuning voor het bijbehorende schema exporteren naar een resourcegroepsjabloon. Als gevolg hiervan weergegeven de gegenereerde sjabloon niet. configuratieparameters voor het inschakelen van beheerde identiteiten voor Azure-resources op de resource. Deze secties kunnen handmatig worden toegevoegd aan de hand van de voorbeelden in [configureren beheerde identiteiten voor een Azure-resources op een Azure-VM met behulp van een sjablonen](qs-configure-template-windows-vm.md).

Wanneer de schema-export-functionaliteit beschikbaar is voor de beheerde identiteiten voor VM-extensie van een Azure-resources (gepland voor de afschaffing in januari 2019), wordt deze weergegeven in [exporteren van resourcegroepen met VM-extensies](../../virtual-machines/extensions/export-templates.md#supported-virtual-machine-extensions).

### <a name="configuration-blade-does-not-appear-in-the-azure-portal"></a>Configuratieblade wordt niet weergegeven in de Azure-portal

Als de VM-configuratie-blade op de virtuele machine niet wordt weergegeven, klikt u vervolgens beheerde identiteiten voor Azure-resources niet is ingeschakeld in de portal in uw regio nog.  Probeer het later opnieuw.  U kunt ook beheerde identiteiten voor Azure-resources inschakelen voor uw virtuele machine met [PowerShell](qs-configure-powershell-windows-vm.md) of de [Azure CLI](qs-configure-cli-windows-vm.md).

### <a name="cannot-assign-access-to-virtual-machines-in-the-access-control-iam-blade"></a>Kan geen toegang toewijzen aan virtuele machines in de blade toegangsbeheer (IAM)

Als **virtuele Machine** wordt niet weergegeven in de Azure-portal als een keuze voor **toegang toewijzen aan** in **toegangsbeheer (IAM)** > **functie toevoegen toewijzing**, en vervolgens de beheerde identiteiten voor Azure-resources is nog niet ingeschakeld in de portal in uw regio. Probeer het later opnieuw.  U kunt nog steeds de identiteit voor de virtuele machine voor de roltoewijzing selecteren door te zoeken naar de beheerde identiteit voor Azure-resources Service-Principal.  Voer de naam van de virtuele machine in de **Selecteer** veld en de Service-Principal wordt weergegeven in de zoekresultaten.

### <a name="vm-fails-to-start-after-being-moved-from-resource-group-or-subscription"></a>Virtuele machine niet kan worden gestart na worden verplaatst van resourcegroep of abonnement

Als u een virtuele machine in de status running doorbrengt verplaatst, blijft tijdens het verplaatsen uitgevoerd. Echter na de verplaatsing mislukt als de virtuele machine wordt gestopt en opnieuw opgestart, dit om te starten. Dit probleem treedt op omdat de virtuele machine niet voor de verwijzing naar de beheerde identiteit voor de id van de Azure-resources bijwerken is en wijst u deze in de oude resourcegroep wordt voortgezet.

**Tijdelijke oplossing** 
 
Trigger voor een update voor de virtuele machine, zodat de juiste waarden voor de beheerde identiteit voor Azure-resources kunnen worden opgehaald. U kunt de wijziging van een VM-eigenschap voor het bijwerken van de verwijzing naar de beheerde identiteit voor de id van de Azure-resources kunt doen. U kunt bijvoorbeeld een nieuwe tagwaarde instellen op de virtuele machine met de volgende opdracht:

```azurecli-interactive
 az  vm update -n <VM Name> -g <Resource Group> --set tags.fixVM=1
```
 
Met deze opdracht wordt een nieuwe tag 'fixVM' met een waarde van 1 ingesteld op de virtuele machine. 
 
Deze eigenschap instelt, de virtuele machine wordt bijgewerkt met de juiste beheerde identiteit voor Azure-resources resource-URI en vervolgens moet u de virtuele machine gestart. 
 
Nadat de virtuele machine is gestart, kan de tag worden verwijderd met behulp van de volgende opdracht:

```azurecli-interactive
az vm update -n <VM Name> -g <Resource Group> --remove tags.fixVM
```

### <a name="vm-extension-provisioning-fails"></a>VM-extensie mislukt inrichten

Inrichting van de VM-extensie kan mislukken vanwege DNS-lookup-fouten. Start de VM opnieuw op en probeer het opnieuw.
 
> [!NOTE]
> De VM-extensie is gepland voor de afschaffing van januari 2019. Het is raadzaam om dat u aan met behulp van het eindpunt IMDS verplaatsen.

### <a name="transferring-a-subscription-between-azure-ad-directories"></a>Een abonnement wordt overgedragen tussen Azure AD-mappen

Beheerde identiteiten doen niet bijgewerkt wanneer u een abonnement is verplaatst/overgedragen naar een andere map. Als gevolg hiervan is een bestaand systeem toegewezen of de gebruiker toegewezen identiteiten op beheerde verbroken. 

Als tijdelijke oplossing nadat het abonnement is verplaatst, kunt u uitschakelen door het systeem toegewezen beheerde identiteiten en deze opnieuw inschakelen. U kunt op deze manier verwijderen en opnieuw maken van een beheerde gebruiker toegewezen identiteiten. 

## <a name="known-issues-with-user-assigned-managed-identities"></a>Bekende problemen met beheerde identiteiten gebruiker toegewezen

- Het maken van een gebruiker toegewezen beheerde identiteit met speciale tekens (dat wil zeggen onderstrepingstekens) in de naam, wordt niet ondersteund.
- Identiteitsnamen van de gebruiker toegewezen zijn beperkt tot 24 tekens bestaan. Als de naam langer dan 24 tekens is, de identiteit niet worden toegewezen aan een resource (dat wil zeggen virtuele Machine.)
- Als u de extensie van de beheerde identiteit-virtuele machine (gepland voor de afschaffing in januari 2019) gebruikt, is de ondersteunde limiet van 32 gebruiker toegewezen beheerde identiteiten. De ondersteunde limiet is zonder de extensie van de virtuele machine beheerde identiteit 512.  
- Een gebruiker toegewezen beheerde identiteit verplaatsen naar een andere resourcegroep zorgt ervoor dat de identiteit te kraken. Als gevolg hiervan niet mogelijk op aanvragen van tokens voor die identiteit. 
- Een abonnement overbrengen naar een andere map, wordt geen bestaande gebruiker toegewezen beheerde identiteiten verbroken. 