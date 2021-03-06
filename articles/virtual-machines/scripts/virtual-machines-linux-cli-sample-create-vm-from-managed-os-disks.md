---
title: Voorbeeld van Azure CLI-script - Een virtuele machine maken door een beheerde schijf te koppelen als besturingssysteemschijf | Microsoft Docs
description: Voorbeeld van Azure CLI-script - Een virtuele machine maken door een beheerde schijf te koppelen als besturingssysteemschijf
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 5d86710fd9173cd0bc3416fedec226f97f12d9d2
ms.sourcegitcommit: 8c3267c34fc46c681ea476fee87f5fb0bf858f9e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/09/2018
ms.locfileid: "29847672"
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>Een virtuele machine maken met behulp van een bestaande beheerde besturingssysteemschijf met CLI

Met dit script maakt u een virtuele machine door een bestaande beheerde schijf als besturingssysteemschijf te koppelen. Gebruik dit script in de volgende scenario's:
* Een virtuele machine maken van een bestaande beheerde besturingssysteemschijf die is gekopieerd van een beheerde schijf in een ander abonnement
* Een virtuele machine maken van een bestaande beheerde schijf die is gemaakt met behulp van een speciaal VHD-bestand 
* Een virtuele machine maken van een bestaande beheerde schijf die is gemaakt aan de hand van een momentopname 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Voorbeeldscript

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie 

Gebruik de volgende opdracht om de resourcegroep, VM, en alle gerelateerde resources te verwijderen.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Uitleg van het script

Dit script gebruikt de volgende opdrachten voor het opvragen van de eigenschappen van de beheerde schijf, het koppelen van een beheerde schijf aan een nieuwe virtuele machine en het maken van een virtuele machine. Elk item in de tabel is een koppeling naar specifieke documentatie over de opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#az_disk_show) | Hiermee haalt u de eigenschappen van de beheerde schijf op door de naam van de schijf en de naam van de resourcegroep op te geven. De eigenschap Id wordt gebruikt om een beheerde schijf te koppelen aan een nieuwe virtuele machine. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#az_vm_create) | Hiermee maakt u een virtuele machine die gebruikmaakt van een beheerde besturingssysteemschijf. |
## <a name="next-steps"></a>Volgende stappen

Raadpleeg de [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure) voor meer informatie over de Azure CLI.

U kunt extra CLI-scriptvoorbeelden voor virtuele machines vinden in de [Azure-documentatie voor Linux-VM's](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
