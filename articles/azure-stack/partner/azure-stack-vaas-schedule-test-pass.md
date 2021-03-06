---
title: De validatie als een Service voor Azure Stack-portal gebruiken om te plannen van uw eerste test | Microsoft Docs
description: De validatie gebruiken als een Service voor Azure Stack-portal voor het plannen van uw eerste test.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: How to
ms.date: 11/26/2018
ms.author: mabrigg
ms.reviewer: johnhas
ms.openlocfilehash: 3021fafe7d74f71450eec9b3720c974b04ada224
ms.sourcegitcommit: c61c98a7a79d7bb9d301c654d0f01ac6f9bb9ce5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/27/2018
ms.locfileid: "52426924"
---
# <a name="schedule-your-first-test"></a>Uw eerste test plannen

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

Plan een test in de validatie uit als een (VaaS)-serviceportal voor uw Azure Stack-oplossing. Een oplossing VaaS vertegenwoordigt een Azure Stack-oplossing met een bepaalde hardware stuklijst (BoM). U kunt een test om te controleren dat Azure Stack kan worden uitgevoerd door uw hardware kunt plannen.

Om te controleren of uw oplossing, de werkstroom voor een test te maken. Een werkstroom VaaS werkt binnen de context van een VaaS-oplossing. Hiermee geeft u een verzameling testsuites die de functionaliteit van een Azure Stack-implementatie op uw hardware. Uitwerking parameters van uw oplossing toevoegen en selecteer een of meer tests uit te voeren op uw oplossing.

Terwijl de werkstroom testronde kan worden gebruikt om uit te voeren van elke test geleverd door VaaS, met inbegrip van tests vanaf de validatie-werkstromen, resultaten van de werkstroom testronde worden niet beschouwd als *officiële*. Zie voor meer informatie over werkstromen officiële validatie [werkstromen](azure-stack-vaas-key-concepts.md#workflows).

## <a name="prerequisites"></a>Vereisten

Voordat u deze Quick Start volgen, moet u klaar bent met de volgende items:

- [De validatie als een serviceresources instellen](azure-stack-vaas-set-up-resources.md)
- [Implementeren van de lokale agent](azure-stack-vaas-local-agent.md) (aanbevolen)
- [Validatie uit als een Service-belangrijkste concepten](azure-stack-vaas-key-concepts.md) (aanbevolen)

## <a name="start-a-workflow"></a>Een werkstroom starten

![Meld u aan bij de portal VaaS](media/vaas_portalsignin.png)

Meld u aan bij de portal, selecteert of het maken van een oplossing en selecteer vervolgens de oplossing.

1. Aanmelden bij de [VaaS portal](https://azurestackvalidation.com).
2. Typ de naam van een bestaande oplossing of selecteer **nieuwe oplossing** om een nieuwe oplossing te maken. Zie voor instructies [een oplossing maken in de portal VaaS](azure-stack-vaas-key-concepts.md#create-a-solution-in-the-vaas-portal).
3. Selecteer **Start** op de **Test passen** tegel.

## <a name="specify-parameters"></a>Parameters opgeven

![Alternatieve tekst](media/vaas_test_pass_parameters.png)

De werkstroom voor uw oplossing definieert. De werkstroom bevat de stappen die gebruikt voor het testen van uw oplossing.

1. [!INCLUDE [azure-stack-vaas-workflow-step_naming](includes/azure-stack-vaas-workflow-step_naming.md)]
2. [!INCLUDE [azure-stack-vaas-workflow-step_upload-stampinfo](includes/azure-stack-vaas-workflow-step_upload-stampinfo.md)]
3. [!INCLUDE [azure-stack-vaas-workflow-step_test-params](includes/azure-stack-vaas-workflow-step_test-params.md)]
4. [!INCLUDE [azure-stack-vaas-workflow-step_tags](includes/azure-stack-vaas-workflow-step_tags.md)]
5. Selecteer **volgende** om te selecteren van tests om te plannen.

## <a name="select-tests-to-run"></a>Selecteer tests om uit te voeren

Kies de tests die u wilt uitvoeren in uw werkstroom.

1. Selecteer de (s) die u wilt uitvoeren in uw werkstroom.

    Als u overschrijven van de algemene parameters (dat wil zeggen, de parameters die is opgegeven in de vorige sectie) voor elke test wilt, selecteert u op de **bewerken** koppeling volgende om door te geven van de nieuwe waarden.

1. [!INCLUDE [azure-stack-vaas-workflow-step_select-agent](includes/azure-stack-vaas-workflow-step_select-agent.md)]
1. Selecteer **volgende** om te controleren van de werkstroom.

## <a name="review-and-submit"></a>Controleren en verzenden

Bekijk, maken en plannen u werkstroom.

1. Controleer de gegevens weergegeven.

    De services maakt u uw werkstroom met de opgegeven informatie en de geselecteerde tests wordt gepland.

    Als wordt onjuist weergegeven, gebruikt u de **vorige** knoppen om naar een eerdere sectie te gaan.

1. [!INCLUDE [azure-stack-vaas-workflow-step_submit](includes/azure-stack-vaas-workflow-step_submit.md)]

## <a name="next-steps"></a>Volgende stappen

- [Controleren en beheren van tests in de portal VaaS](azure-stack-vaas-monitor-test.md)
