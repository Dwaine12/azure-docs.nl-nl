---
author: cynthn
ms.service: virtual-machines-linux
ms.topic: include
ms.date: 10/26/2018
ms.author: cynthn
ms.openlocfilehash: b922b5ea225c61948240e40903ac43f56fde3fb5
ms.sourcegitcommit: 6e09760197a91be564ad60ffd3d6f48a241e083b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/29/2018
ms.locfileid: "50227355"
---
## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#az_group_create). Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *VS - oost*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Een virtuele machine maken

Maak een VM met de opdracht [az vm create](/cli/azure/vm#az_vm_create). 

In het volgende voorbeeld wordt een VM gemaakt met de naam *myVM* en worden er SSH-sleutels gemaakt, als deze nog niet bestaan op een standaardsleutellocatie. Als u een specifieke set sleutels wilt gebruiken, gebruikt u de optie `--ssh-key-value`. Met de opdracht wordt *azureuser* ook ingesteld als gebruikersnaam voor de beheerder. Later gebruikt u deze naam om verbinding te maken met de VM. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Wanneer de virtuele machine is gemaakt, toont de Azure CLI informatie die lijkt op de informatie in het volgende voorbeeld. Noteer het `publicIpAddress`. Dit adres wordt in latere stappen gebruikt voor toegang tot de VM.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>Poort 80 openen voor webverkeer 

Standaard worden alleen SSH-verbindingen toegestaan naar Linux-VM’s die zijn geïmplementeerd in Azure. Omdat deze VM wordt gebruikt als een webserver, moet u poort 80 openen voor verkeer vanaf internet. Gebruik de opdracht [az vm open-port](/cli/azure/vm#az_vm_open_port) om de gewenste poort te openen.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>SSH in uw virtuele machine


Als u het openbare IP-adres van de VM niet weet, voert u de opdracht [az network public-ip list](/cli/azure/network/public-ip#list) uit. U hebt dit IP-adres nodig voor verschillende latere stappen.


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Gebruik de volgende opdracht om een SSH-sessie te starten voor de virtuele machine. Gebruik hierbij het juiste openbare IP-adres van uw virtuele machine. In dit voorbeeld is het IP-adres *40.68.254.142*. *azureuser* is de gebruikersnaam voor de beheerder die u hebt ingesteld bij het maken van de VM.

```bash
ssh azureuser@40.68.254.142
```

