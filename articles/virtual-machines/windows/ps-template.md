---
title: Een Windows-VM maken van een sjabloon in Azure | Microsoft Docs
description: Een Resource Manager-sjabloon en PowerShell gebruiken om eenvoudig een nieuwe Windows-VM.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7be724a93eb951a3f9e35048a3c70571e43e79cf
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53184743"
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Een Windows virtuele machine maken van een Resource Manager-sjabloon

Dit artikel laat u over het implementeren van een Azure Resource Manager-sjabloon met behulp van PowerShell. De sjabloon die u maakt implementeert een enkele virtuele machine met Windows Server in een nieuw virtueel netwerk met één subnet.

Zie voor een gedetailleerde beschrijving van de bron van de virtuele machine, [virtuele machines in een Azure Resource Manager-sjabloon](template-description.md). Zie voor meer informatie over alle resources in een sjabloon, [overzicht Azure Resource Manager-sjabloon](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Het duurt ongeveer vijf minuten aan de stappen in dit artikel.

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

Als u PowerShell lokaal wilt installeren en gebruiken, is voor deze zelfstudie moduleversie 5.3 of later van Azure PowerShell vereist. Voer `Get-Module -ListAvailable AzureRM` uit om de versie te bekijken. Als u PowerShell wilt upgraden, raadpleegt u [De Azure PowerShell-module installeren](/powershell/azure/install-azurerm-ps). Als u PowerShell lokaal uitvoert, moet u ook `Connect-AzureRmAccount` uitvoeren om verbinding te kunnen maken met Azure.

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Alle resources moeten worden geïmplementeerd in een [resourcegroep](../../azure-resource-manager/resource-group-overview.md).

1. Haal een lijst op met beschikbare locaties waar resources kunnen worden gemaakt.
   
    ```powershell   
    Get-AzureRmLocation | sort-object DisplayName | Select DisplayName
    ```

2. Maak de resourcegroep op de locatie die u selecteert. In dit voorbeeld toont het maken van een resourcegroep met de naam **myResourceGroup** in de **VS-West** locatie:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a>De bestanden maken

In deze stap maakt u een sjabloon voor bestanden die worden geïmplementeerd en een parameterbestand waarmee de parameterwaarden voor de sjabloon. U maakt ook een bestand met autorisatieregels die wordt gebruikt voor het Azure Resource Manager-bewerkingen uitvoeren. 

1. Maak een bestand met de naam *CreateVMTemplate.json* en voeg uw JSON-code toe. Vervang de waarde van `domainNameLabel` door uw eigen unieke naam.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]" 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. Maak een bestand met de naam *Parameters.json* en voeg deze JSON-code toe:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. Maak een nieuw opslagaccount en container:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. De bestanden uploaden naar het storage-account:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Wijzig de - paden naar de locatie waar u de bestanden hebt opgeslagen.

## <a name="create-the-resources"></a>De resources maken

Implementeer de sjabloon met behulp van de parameters:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> U kunt ook parameters van lokale bestanden en sjablonen implementeren. Zie voor meer informatie, [Azure PowerShell gebruiken met Azure Storage](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Volgende stappen

- Als er problemen met de implementatie zijn, kunt u Kijk eens [veelvoorkomende problemen oplossen Azure-implementatie met Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
- Meer informatie over het maken en beheren van een virtuele machine in [maken en beheren van Windows-VM's met de Azure PowerShell-module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

