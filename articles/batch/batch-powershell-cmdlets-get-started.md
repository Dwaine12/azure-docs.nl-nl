---
title: Aan de slag met Azure Batch PowerShell | Microsoft Docs
description: Een korte inleiding in de Azure PowerShell-cmdlets die u kunt gebruiken voor het beheren van de Azure Batch-service
services: batch
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''

ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 07/28/2016
ms.author: danlep

---
# Aan de slag met PowerShell-cmdlets voor Azure Batch
Met de PowerShell-cmdlets voor Azure Batch kunt u veel dezelfde taken die u uitvoert met de Batch-API's, Azure Portal en de Azure-opdrachtregelinterface (CLI), uitvoeren en er scripts voor uitvoeren. Dit is een korte inleiding in de cmdlets die u kunt gebruiken om uw Batch-accounts te beheren en te werken met uw Batch-resources, zoals pools en taken. Dit artikel is gebaseerd op cmdlets in Azure PowerShell versie 1.6.0.

Zie [Naslaginformatie over Azure Batch-cmdlets](https://msdn.microsoft.com/library/azure/mt125957.aspx) voor een volledige lijst met Batch-cmdlets en gedetailleerde cmdlet-syntaxis. 

## Vereisten
* **Azure PowerShell** - Zie [How to install and configure Azure PowerShell](../powershell-install-configure.md) (Azure PowerShell installeren en configureren) voor instructies voor het downloaden en installeren van Azure PowerShell. 
  
  * Omdat de Azure Batch-cmdlets in de module Azure Resource Manager worden geleverd, moet u de cmdlet **Login-AzureRmAccount** uitvoeren om verbinding te maken met uw abonnement. 
  * Het wordt aangeraden Azure PowerShell regelmatig bij te werken om te profiteren van service-updates en verbeteringen. 
* **Registreren bij de naamruimte van de Batch-provider (eenmalige bewerking)** - Voordat u met uw Batch-accounts kunt werken, moet u zich eerst registreren bij de naamruimte van de Batch-provider. Deze bewerking hoeft slechts één keer per abonnement te worden uitgevoerd. Voer de volgende cmdlet uit:
  
        Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch

## Batch-accounts en -sleutels beheren
### Batch-account maken
Met **New-AzureRmBatchAccount** wordt een nieuw Batch-account in een opgegeven resourcegroep gemaakt. Als u nog geen resourcegroep hebt, maakt u er een door de cmdlet [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/azure/mt603739.aspx) uit te voeren, waarbij u een van de Azure-regio's opgeeft in de parameter **Locatie**, zoals 'VS - midden'. Bijvoorbeeld:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"


Maak een nieuw account van de Batch-account in de resourcegroep, waarbij u een naam voor het account in <*accountnaam*> opgeeft, evenals voor de locatie en de naam van uw resourcegroep. Het kan even duren voordat het Batch-account is gemaakt. Bijvoorbeeld:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName MyBatchResourceGroup

> [!NOTE]
> De Batch-accountnaam moet uniek zijn voor de Azure-regio voor de resourcegroep, minimaal 3 en maximaal 24 tekens bevatten en alleen bestaan uit kleine letters en cijfers.
> 
> 

### Toegangssleutels van account ophalen
Met **Get-AzureRmBatchAccountKeys** worden de toegangssleutels weergegeven die aan een Azure Batch-account zijn gekoppeld. Voer bijvoorbeeld de volgende opdracht uit om de primaire en secundaire sleutels op te halen van het account dat u hebt gemaakt.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <accountname>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey


### Een nieuwe toegangssleutel genereren
Met **New-AzureRmBatchAccountKey** wordt een nieuwe primaire of secundaire accountsleutel voor een Azure Batch-account gegenereerd. Typ bijvoorbeeld de volgende opdracht voor het genereren van een nieuwe primaire sleutel voor het Batch-account:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary


> [!NOTE]
> Als u een nieuwe secundaire sleutel wilt genereren, geeft u 'Secundair' op voor de parameter **KeyType**. U moet de primaire en secundaire sleutels afzonderlijk opnieuw genereren.
> 
> 

### Batch-account verwijderen
Met **Remove-AzureRmBatchAccount** wordt een Batch-account verwijderd. Bijvoorbeeld:

    Remove-AzureRmBatchAccount -AccountName <account_name>

Als hierom wordt gevraagd, bevestigt u dat u het account wilt verwijderen. Het kan even duren voordat het account is verwijderd.

## Een BatchAccountContext-object maken
Als u wilt verifiëren met de Batch PowerShell-cmdlets wanneer u Batch-pools, -jobs, -taken en andere -resources maakt en beheert, maakt u eerst een BatchAccountContext-object om uw accountnaam en sleutels op te slaan.

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

U geeft het BatchAccountContext-object door aan cmdlets waarvoor de parameter **BatchContext** wordt gebruikt.

> [!NOTE]
> Standaard wordt de primaire sleutel van het account gebruikt voor verificatie, maar u kunt expliciet de te gebruiken sleutel selecteren door de eigenschap **KeyInUse** van het object BatchAccountContext te wijzigen: `$context.KeyInUse = "Secondary"`.
> 
> 

## Batch-resources maken en wijzigen
Gebruik cmdlets zoals **New-AzureBatchPool**, **New-AzureBatchJob** en **New-AzureBatchTask** om resources onder een Batch-account te maken. Er zijn overeenkomende **Get-**- en **Set-**-cmdlets voor het bijwerken van de eigenschappen van bestaande resources en **Remove-**-cmdlets om resources onder een Batch-account te verwijderen. 

Wanneer u veel van deze cmdlets gebruikt, moet u niet alleen een BatchContext-object doorgeven, maar ook objecten maken of doorgeven die gedetailleerde resource-instellingen bevatten, zoals weergegeven in het volgende voorbeeld. Raadpleeg de gedetailleerde Help-informatie voor elke cmdlet voor meer voorbeelden.

### Batch-pool maken
Wanneer u een Batch-pool maakt of bijwerkt, selecteert u een cloud-serviceconfiguratie of een virtuele-machineconfiguratie voor het besturingssysteem op de rekenknooppunten (zie [Batch feature overview](batch-api-basics.md#pool) (Overzicht van Batch-functies)). Uw keuze bepaalt of van de rekenknooppunten een installatiekopie wordt gemaakt met een van de [Azure-gastbesturingssysteemreleases](../cloud-services/cloud-services-guestos-update-matrix.md#releases) of met een van de ondersteunde VM-images voor Linux of Windows in de Azure Marketplace. 

Bij het uitvoeren van **New-AzureBatchPool** geeft u de instellingen van het besturingssysteem door in een PSCloudServiceConfiguration- of PSVirtualMachineConfiguration-object. Met de volgende cmdlet wordt bijvoorbeeld een nieuwe Batch-pool gemaakt met rekenknooppunten met de grootte Klein in de cloudserviceconfiguratie, met een installatiekopie van de meest recente versie van het besturingssysteem van type 3 (Windows Server 2012). Hier geeft de parameter **CloudServiceConfiguration** de variabele *$configuration* op als het PSCloudServiceConfiguration-object. Met de parameter **BatchContext** wordt een eerder gedefinieerde variabele *$context* opgegeven als het BatchAccountContext-object.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(3,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

Het doelaantal rekenknooppunten in de nieuwe pool wordt bepaald met een formule voor automatisch schalen. In dit geval is de formule gewoon **$TargetDedicated=4**, waarmee wordt aangegeven dat het aantal rekenknooppunten in de pool maximaal 4 is. 

## Query voor pools, jobs, taken en andere details
Gebruik cmdlets zoals **Get-AzureBatchPool**, **Get-AzureBatchJob** en **Get-AzureBatchTask** om een query uit te voeren voor entiteiten die zijn gemaakt onder een Batch-account.

### Query voor gegevens
Gebruik bijvoorbeeld **Get-AzureBatchPools** om uw pools te vinden. Standaard wordt deze query voor alle pools onder uw account uitgevoerd, in de veronderstelling dat u het object BatchAccountContext al hebt opgeslagen in *$context*:

    Get-AzureBatchPool -BatchContext $context

### Een OData-filter gebruiken
U kunt een OData-filter opgeven met behulp van de parameter **Filter** om alleen de objecten te zoeken waarin u bent geïnteresseerd. U kunt bijvoorbeeld alle pools zoeken met id's die beginnen met 'myPool':

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context


Deze methode is niet zo flexibel als het gebruik van een 'Where-Object' in een lokale pijplijn. De query wordt rechtstreeks naar de Batch-service verzonden zodat al het filteren aan de serverzijde plaatsvindt, waardoor er internetbandbreedte wordt bespaard.

### De parameter Id gebruiken
Een alternatief voor een OData-filter is het gebruik van de parameter **Id**. Als u een query uit wilt voeren voor een specifieke pool met id 'myPool':

    Get-AzureBatchPool -Id "myPool" -BatchContext $context


Met de parameter **Id** wordt alleen een zoekopdracht voor een volledige id ondersteund, geen jokertekens of filters van het OData-type.

### De parameter MaxCount gebruiken
Standaard worden met elke cmdlet maximaal 1000 objecten geretourneerd. Als deze limiet is bereikt, moet u uw filter verfijnen zodat er minder objecten worden opgehaald, of moet u expliciet een maximum instellen met de parameter **MaxCount**. Bijvoorbeeld:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

Als u de bovengrens wilt verwijderen, stelt u **MaxCount** in op 0 of minder.

### De pijplijn gebruiken
Met Batch-cmdlets kunt u gebruikmaken van de PowerShell-pijplijn om gegevens tussen cmdlets te verzenden. Dit heeft hetzelfde effect als het opgeven van een parameter, maar het weergeven van meerdere entiteiten is hiermee eenvoudiger. Met de volgende opdracht worden bijvoorbeeld alle taken onder uw account gevonden:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context


## Volgende stappen
* Zie [Naslaginformatie over Azure Batch-cmdlets](https://msdn.microsoft.com/library/azure/mt125957.aspx) voor gedetailleerde cmdlet-syntaxis en voorbeelden.
* Zie [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) (Efficiënt query's uitvoeren op de Azure Batch-service) voor meer informatie over het verminderen van het aantal items en het type informatie dat wordt geretourneerd voor query's naar Batch. 

<!--HONumber=Sep16_HO3-->


