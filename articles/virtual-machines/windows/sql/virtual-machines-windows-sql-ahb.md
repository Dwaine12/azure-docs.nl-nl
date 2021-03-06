---
title: Het wijzigen van de licentiemodel voor een SQL-VM in Azure | Microsoft Docs
description: Informatie over het wijzigen van de licentieverlening voor een SQL-VM in Azure.
services: virtual-machines-windows
documentationcenter: na
author: MashaMSFT
manager: craigg
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/14/2018
ms.author: mathoma
ms.reviewer: jroth
ms.openlocfilehash: cd784163047f4fe15fde719ce56aba64eed60dd2
ms.sourcegitcommit: edacc2024b78d9c7450aaf7c50095807acf25fb6
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/13/2018
ms.locfileid: "53336982"
---
# <a name="how-to-change-the-licensing-model-for-a-sql-server-virtual-machine-in-azure"></a>Het wijzigen van de licentiemodel voor een virtuele machine van SQL Server in Azure
In dit artikel wordt beschreven hoe u de licentiemodel voor een virtuele machine van SQL Server in Azure met behulp van de nieuwe SQL-resourceprovider - **Microsoft.SqlVirtualMachine**. Er zijn twee modellen voor een virtuele machine (VM) die als host fungeert voor SQL Server - betalen per gebruik, licenties en uw eigen licentie (BYOL). En nu met behulp van PowerShell of Azure CLI, u kunt wijzigen welke licentiemodel maakt gebruik van uw SQL-VM. 

De **betalen per gebruik** model betekent dat de kosten per seconde van het uitvoeren van de virtuele machine van Azure de kosten van de SQL Server-licentie bevat.

De **Bring-your-own-license** model wordt ook wel bekend als de [Azure Hybrid Benefit](https://azure.microsoft.com/pricing/hybrid-benefit/), en kunt u uw eigen SQL Server-licentie gebruiken met een virtuele machine met SQL Server. Zie voor meer informatie over prijzen [SQL VM prijzen handleiding](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

Schakelen tussen de twee licentiemodellen worden in rekening gebracht **zonder uitvaltijd**, de virtuele machine niet opnieuw wordt opgestart, wordt toegevoegd **zonder extra kosten** (in feite AHB activering vermindert de kosten) en **met onmiddellijke ingang effectief**. 


## <a name="register-existing-sql-vm-with-new-resource-provider"></a>Bestaande SQL-VM met nieuwe resourceprovider registreren
De mogelijkheid om over te schakelen tussen licentiemodellen is een functie die wordt geleverd door de nieuwe SQL-VM resourceprovider (Microsoft.SqlVirtualMachine). Op dit moment als u wilt overschakelen van uw licentiemodel moet u eerst het registreren van de nieuwe provider voor uw abonnement en vervolgens uw bestaande virtuele machine met de nieuwe SQL-VM-resourceprovider te registreren. Als u wilt gebruikmaken van de resourceprovider van SQL-VM, moet u ook de SQL IaaS-extensie installeren. In dat geval kunt u voor het registreren van een virtuele machine die is geïmplementeerd met een VHD. Zie voor meer informatie, [SQL IaaS-extensie](virtual-machines-windows-sql-server-agent-extension.md). 

  >[!IMPORTANT]
  > Als u uw SQL-VM-resource, gaat u terug naar de vastgelegde licentie-instelling van de installatiekopie. 

### <a name="powershell"></a>PowerShell


Het volgende codefragment wordt u verbinding maken met Azure en controleer of welke abonnements-ID die u gebruikt. 
```PowerShell
# Connect to Azure
Connect-AzureRmAccount
Account: <account_name>

# Verify your subscription ID
Get-AzureRmContext

# Set the correct Azure Subscription ID
Set-AzureRmContext -SubscriptionId <Subscription_ID>
```

Het volgende codefragment eerst registreert de nieuwe SQL-resourceprovider voor uw abonnement en vervolgens uw bestaande SQL-VM voor de nieuwe resourceprovider geregistreerd. 

```powershell
# Register the new SQL resource provider for your subscription
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SqlVirtualMachine

# Register your existing SQL VM with the new resource provider
# example: $vm=Get-AzureRmVm -ResourceGroupName AHBTest -Name AHBTest
$vm=Get-AzureRmVm -ResourceGroupName <ResourceGroupName> -Name <VMName>
New-AzureRmResource -ResourceName $vm.Name -ResourceGroupName $vm.ResourceGroupName -Location $vm.Location -ResourceType Microsoft.SqlVirtualMachine/sqlVirtualMachines -Properties @{virtualMachineResourceId=$vm.Id}
```

### <a name="portal"></a>Portal
U kunt ook de nieuwe SQL-VM-resourceprovider met behulp van de portal registreren. Op dit als volgt te werk:
1. Open de Azure-portal en Ga naar **alle Services**. 
1. Navigeer naar **abonnementen** en selecteer het abonnement van belang zijn.  
1. In de **abonnementen** blade, gaat u naar **Resourceprovider**. 
1. Type `sql` in het filter om de SQL-gerelateerde resourceproviders. 
1. Selecteer een *registreren*, *opnieuw registreren*, of *registratie* voor de **Microsoft.SqlVirtualMachine** provider afhankelijk van uw gewenste actie. 

  ![De provider wijzigen](media/virtual-machines-windows-sql-ahb/select-resource-provider-sql.png)


## <a name="use-powershell"></a>PowerShell gebruiken 
U kunt PowerShell gebruiken om te wijzigen van uw licentiemodel.  Zorg ervoor dat uw SQL-VM is al geregistreerd met de nieuwe SQL-resourceprovider voordat u overschakelt van de licentiemodel. 

Uw licentiemodel voor betalen per gebruik verandert het volgende codefragment in een BYOL (of met behulp van Azure Hybrid Benefit): 
```PowerShell
#example: $SqlVm = Get-AzureRmResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName AHBTest -ResourceName AHBTest
$SqlVm = Get-AzureRmResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName <resource_group_name> -ResourceName <VM_name>
$SqlVm.Properties.sqlServerLicenseType="AHUB"
$SqlVm | Set-AzureRmResource -Force 
``` 

Het volgende codefragment verandert de BYOL-model voor betalen per gebruik:
```PowerShell
#example: $SqlVm = Get-AzureRmResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName AHBTest -ResourceName AHBTest
$SqlVm = Get-AzureRmResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName <resource_group_name> -ResourceName <VM_name>
$SqlVm.Properties.sqlServerLicenseType="PAYG"
$SqlVm | Set-AzureRmResource -Force 
```

  >[!NOTE]
  > Als u wilt overschakelen tussen licenties, moet u de nieuwe SQL-VM-resourceprovider. Als u probeert deze opdrachten uitvoeren voordat u uw SQL-VM met de nieuwe provider registreert, kunt u deze fout kan optreden: `Get-AzureRmResource : The Resource 'Microsoft.SqlVirtualMachine/SqlVirtualMachines/AHBTest' under resource group 'AHBTest' was not found. The property 'sqlServerLicenseType' cannot be found on this object. Verify that the property exists and can be set. ` Als u deze fout ziet, neemt u [registreren van uw SQL-VM met de nieuwe resourceprovider](#register-existing-SQL-vm-with-new-resource-provider). 
 

## <a name="use-azure-cli"></a>Azure CLI gebruiken
Azure CLI kunt u uw licentiemodel wijzigen.  Zorg ervoor dat uw SQL-VM is al geregistreerd met de nieuwe SQL-resourceprovider voordat u overschakelt van de licentiemodel. 

Uw licentiemodel voor betalen per gebruik verandert het volgende codefragment in een BYOL (of met behulp van Azure Hybrid Benefit):
```azurecli
az resource update -g <resource_group_name> -n <sql_virtual_machine_name> --resource-type "Microsoft.SqlVirtualMachine/SqlVirtualMachines" --set properties.sqlServerLicenseType=AHUB
# example: az resource update -g AHBTest -n AHBTest --resource-type "Microsoft.SqlVirtualMachine/SqlVirtualMachines" --set properties.sqlServerLicenseType=AHUB
```

Het volgende codefragment verandert de BYOL-model voor betalen per gebruik: 
```azurecli
az resource update -g <resource_group_name> -n <sql_virtual_machine_name> --resource-type "Microsoft.SqlVirtualMachine/SqlVirtualMachines" --set properties.sqlServerLicenseType=PAYG
# example: az resource update -g AHBTest -n AHBTest --resource-type "Microsoft.SqlVirtualMachine/SqlVirtualMachines" --set properties.sqlServerLicenseType=PAYG
```

  >[!NOTE]
  >Als u wilt overschakelen tussen licenties, moet u de nieuwe SQL-VM-resourceprovider. Als u probeert deze opdrachten uitvoeren voordat u uw SQL-VM met de nieuwe provider registreert, kunt u deze fout kan optreden: `The Resource 'Microsoft.SqlVirtualMachine/SqlVirtualMachines/AHBTest' under resource group 'AHBTest' was not found. ` Als u deze fout ziet, neemt u [registreren van uw SQL-VM met de nieuwe resourceprovider](#register-existing-SQL-vm-with-new-resource-provider). 

## <a name="view-current-licensing"></a>Huidige licentie weergeven 

Het volgende codefragment kunt u uw huidige licentiemodel weergeven voor uw SQL-VM. 

```PowerShell
# View current licensing model for your SQL VM
#example: $SqlVm = Get-AzureRmResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName <resource_group_name> -ResourceName <VM_name>
$SqlVm = Get-AzureRmResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName <resource_group_name> -ResourceName <VM_name>
$SqlVm.Properties.sqlServerLicenseType
```

## <a name="next-steps"></a>Volgende stappen

Raadpleeg voor meer informatie de volgende artikelen: 

* [Overzicht van SQL Server op een Windows VM](virtual-machines-windows-sql-server-iaas-overview.md)
* [SQL Server op een Windows VM-Veelgestelde vragen](virtual-machines-windows-sql-server-iaas-faq.md)
* [SQL Server op een Windows-VM prijsinformatie](virtual-machines-windows-sql-server-pricing-guidance.md)
* [SQL Server op een Windows VM release-opmerkingen](virtual-machines-windows-sql-server-iaas-release-notes.md)


