---
title: Upgrade van een Azure Container Service (AKS)-cluster | Microsoft Docs
description: Upgrade van een Azure Container Service (AKS)-cluster
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: aks, azure-container-service
keywords: Kubernetes, Docker, containers, microservices, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/15/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: 15e3e96587962ef9cc531e1825f37b92d26928fd
ms.sourcegitcommit: c25cf136aab5f082caaf93d598df78dc23e327b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/15/2017
---
# <a name="upgrade-an-azure-container-service-aks-cluster"></a>Upgrade van een Azure Container Service (AKS)-cluster

Azure Container Service (AKS) kunt gemakkelijk algemene beheertaken uitvoeren, waaronder Kubernetes clusters upgraden.

## <a name="upgrade-an-aks-cluster"></a>Een AKS-cluster upgraden

Vóór de upgrade van een cluster, gebruikt u de `az aks get-versions` opdracht om te controleren die Kubernetes versies zijn beschikbaar voor de upgrade.

```azurecli-interactive
az aks get-versions --name myK8sCluster --resource-group myResourceGroup --output table
```

Uitvoer:

```console
Name     ResourceGroup    MasterVersion    MasterUpgrades       NodePoolVersion     NodePoolUpgrades
-------  ---------------  ---------------  -------------------  ------------------  -------------------
default  myResourceGroup  1.7.7            1.8.2, 1.7.9, 1.8.1  1.7.7               1.8.2, 1.7.9, 1.8.1
```

Er zijn drie versies beschikbaar voor de upgrade: 1.7.9, 1.8.1 en 1.8.2. Kunnen we gebruiken de `az aks upgrade` opdracht bijwerken naar de meest recente versie.  Tijdens het upgradeproces knooppunten zijn zorgvuldig [cordoned en geleegd](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/) onderbreking van actieve toepassingen minimaliseren.

```azurecli-interactive
az aks upgrade --name myK8sCluster --resource-group myResourceGroup --kubernetes-version 1.8.2
```

Uitvoer:

```json
{
  "id": "/subscriptions/4f48eeae-9347-40c5-897b-46af1b8811ec/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myK8sCluster",
  "location": "eastus",
  "name": "myK8sCluster",
  "properties": {
    "accessProfiles": {
      "clusterAdmin": {
        "kubeConfig": "..."
      },
      "clusterUser": {
        "kubeConfig": "..."
      }
    },
    "agentPoolProfiles": [
      {
        "count": 1,
        "dnsPrefix": null,
        "fqdn": null,
        "name": "myK8sCluster",
        "osDiskSizeGb": null,
        "osType": "Linux",
        "ports": null,
        "storageProfile": "ManagedDisks",
        "vmSize": "Standard_D2_v2",
        "vnetSubnetId": null
      }
    ],
    "dnsPrefix": "myK8sClust-myResourceGroup-4f48ee",
    "fqdn": "myk8sclust-myresourcegroup-4f48ee-406cc140.hcp.eastus.azmk8s.io",
    "kubernetesVersion": "1.8.2",
    "linuxProfile": {
      "adminUsername": "azureuser",
      "ssh": {
        "publicKeys": [
          {
            "keyData": "..."
          }
        ]
      }
    },
    "provisioningState": "Succeeded",
    "servicePrincipalProfile": {
      "clientId": "e70c1c1c-0ca4-4e0a-be5e-aea5225af017",
      "keyVaultSecretRef": null,
      "secret": null
    }
  },
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "type": "Microsoft.ContainerService/ManagedClusters"
}
```

U kunt nu Bevestig de upgrade is geslaagd met de `az aks show` opdracht.

```azurecli-interactive
az aks show --name myK8sCluster --resource-group myResourceGroup --output table
```

Uitvoer:

```json
Name          Location    ResourceGroup    KubernetesVersion    ProvisioningState    Fqdn
------------  ----------  ---------------  -------------------  -------------------  ----------------------------------------------------------------
myK8sCluster  eastus     myResourceGroup  1.8.2                Succeeded            myk8sclust-myresourcegroup-3762d8-2f6ca801.hcp.eastus.azmk8s.io
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het implementeren en beheren van AKS met de zelfstudies AKS.

> [!div class="nextstepaction"]
> [AKS-zelfstudie](./tutorial-kubernetes-prepare-app.md)