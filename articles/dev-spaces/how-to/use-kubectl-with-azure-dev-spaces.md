---
title: Kubectl gebruiken met Azure Dev spaties | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: zr-msft
ms.author: zarhoads
ms.date: 05/11/2018
ms.topic: article
description: Snelle Kubernetes-ontwikkeling met containers en microservices in Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
ms.openlocfilehash: b522ab9177d963f65ac6ea75538ddc46331875da
ms.sourcegitcommit: 275eb46107b16bfb9cf34c36cd1cfb000331fbff
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/15/2018
ms.locfileid: "51706776"
---
# <a name="use-kubectl-with-an-azure-dev-space"></a>Kubectl gebruiken met een Azure Dev-ruimte

U kunt toegang tot het Kubernetes-cluster in een Azure Dev-ruimte, en gebruik bestaande Kubernetes-hulpprogramma's zoals `kubectl`.

Met `az aks use-dev-spaces` opdracht automatisch wordt toegevoegd een `kubectl` configuratiecontext voor u, zodat u kubectl al moet zijn verbonden met uw Azure Dev spaties Kubernetes-cluster. Voorbeelden:
- Controleer of de huidige context: `kubectl config current-context`
- Lijst met alle beschikbare contexten: `kubectl config get-contexts`. 
- De context wijzigen: `kubectl config use-context <context-name>`
- Het Kubernetes dashboard bekijken: uitvoeren `kubectl proxy`, open uw browser naar het adres dat met deze opdracht verzendt (append `/ui` naar de URL om te navigeren naar het Kubernetes-dashboard).
- Lijst met de actieve services in de standaard Azure Dev spaties ruimte met de naam *standaard*: `kubectl get services --namespace=default`

