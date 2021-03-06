---
title: '(AFGESCHAFT) Snelstartgids: Azure Docker CE-cluster voor Linux'
description: Leer snel hoe u een Docker CE-cluster voor Linux-containers in Azure Container Service maakt met de Azure CLI.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/16/2018
ms.author: iainfou
ms.custom: ''
ms.openlocfilehash: a7a7455ce9167a9c480d317d50fdce49e2ef06a9
ms.sourcegitcommit: 2469b30e00cbb25efd98e696b7dbf51253767a05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/06/2018
ms.locfileid: "52994300"
---
# <a name="deprecated-deploy-docker-ce-cluster"></a>(AFGESCHAFT) Docker CE-cluster implementeren

[!INCLUDE [ACS deprecation](../../../includes/container-service-deprecation.md)]

In deze snelstartgids wordt een Docker CE-cluster geïmplementeerd met behulp van de Azure CLI. Vervolgens wordt er een toepassing met meerdere containers die bestaat uit een web-front-end en een Redis-exemplaar geïmplementeerd en uitgevoerd op het cluster. Zodra de toepassing is voltooid, is deze toegankelijk via internet.

Docker CE in Azure Container Service is in de preview-fase. **Gebruik dit daarom niet voor productieworkloads**.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor deze snelstartgids de versie Azure CLI 2.0.4 of hoger uitvoeren. Voer `az --version` uit om de versie te bekijken. Als u uw CLI wilt installeren of upgraden, raadpleegt u [De Azure CLI installeren]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#az-group-create). Een Azure-resourcegroep is een logische groep waarin Azure-resources worden geïmplementeerd en beheerd.

Het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *westus2* locatie.

```azurecli-interactive
az group create --name myResourceGroup --location westus2
```

Uitvoer:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westus2",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Docker Swarm-cluster maken

Maak een Dock CE-cluster in Azure Container Service met de opdracht [az acs create](/cli/azure/acs#az-acs-create). Zie voor meer informatie over regio availaiblity van Docker CE [ACS-regio's voor Docker CE](https://github.com/Azure/ACS/blob/master/announcements/2017-08-04_additional_regions.md)

In het volgende voorbeeld wordt een cluster gemaakt met de naam *mySwarmCluster* met een Linux-hoofdknooppunt en drie knooppunten van de Linux-agent.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

In sommige gevallen, zoals met een beperkte proefversie, heeft een Azure-abonnement beperkte toegang tot Azure-resources. Als de implementatie mislukt vanwege beperkte beschikbare kernen, verminder dan het aantal standaardagenten door `--agent-count 1` toe te voegen aan de opdracht [az acs create](/cli/azure/acs#az-acs-create). 

Na enkele minuten is de opdracht voltooid en retourneert deze informatie over het cluster in JSON-indeling.

## <a name="connect-to-the-cluster"></a>Verbinding maken met het cluster

In deze snelstartgids hebt u de FQDN nodig van zowel de Docker Swarm-master als de Docker-agentpool. Voer de volgende opdracht uit om FQDN van de master en van de agent te retourneren.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Uitvoer:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Maak een SSH-tunnel naar de Swarm-master. Vervang `MasterFQDN` door het FQDN-adres van de Swarm-master.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Stel de omgevingsvariabele `DOCKER_HOST` in. Hierdoor kunt u Docker-opdrachten voor de Docker-swarm uitvoeren zonder dat u de hostnaam hoeft op te geven.

```bash
export DOCKER_HOST=localhost:2374
```

U bent nu klaar om Docker-services uit te voeren op de Docker-swarm.


## <a name="run-the-application"></a>De toepassing uitvoeren

Maak een bestand met de naam `azure-vote.yaml` en kopieer de volgende inhoud in het bestand.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Voer de opdracht [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) uit om de Azure Vote-service te maken.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Uitvoer:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Gebruik de opdracht [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) om de implementatiestatus van de toepassing te retourneren.

```bash
docker stack ps azure-vote
```

De toepassing is gereed, zodra de `CURRENT STATE` van elke service is: `Running`.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-the-application"></a>De toepassing testen

Browse naar de FQDN van de Swarm-agentpool om de Azure Vote-toepassing te testen.

![Afbeelding van browsen naar Azure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Cluster verwijderen
U kunt de opdracht [az group delete](/cli/azure/group#az-group-delete) gebruiken om de resourcegroep, de containerservice en alle gerelateerde resources te verwijderen wanneer u het cluster niet meer nodig hebt.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a>Code ophalen

In deze snelstartgids zijn vooraf gemaakte containerinstallatiekopieën gebruikt om een Docker-service te maken. De gerelateerde toepassingscode, Dockerfile en het Opstellen-bestand zijn beschikbaar op GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u een Docker Swarm-cluster geïmplementeerd. Vervolgens hebt u een toepassing met meerdere containers op dit cluster geïmplementeerd.

Voor meer informatie over het integreren van Docker swarm met Azure DevOps, blijven de CI/CD met Docker Swarm en Azure DevOps.

> [!div class="nextstepaction"]
> [CI/CD met Docker Swarm en Azure DevOps](./container-service-docker-swarm-setup-ci-cd.md)
