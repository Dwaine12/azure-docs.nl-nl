---
title: Veelvoorkomende problemen oplossen
description: Informatie over het oplossen van problemen met het maken en toewijzen van blauwdrukken
services: blueprints
author: DCtheGeek
ms.author: dacoulte
ms.date: 10/25/2018
ms.topic: troubleshooting
ms.service: blueprints
manager: carmonm
ms.custom: seodec18
ms.openlocfilehash: 40668fed2fcc2a04e39fa3a4d7e8e8923c75ae05
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53315519"
---
# <a name="troubleshoot-errors-using-azure-blueprints"></a>Problemen oplossen met behulp van Azure blauwdrukken

U kunt uitvoeren in fouten bij het maken of toewijzen van blauwdrukken. Dit artikel wordt beschreven voor verschillende fouten die zich kunnen voordoen en hoe u ze op te lossen.

## <a name="finding-error-details"></a>Foutdetails zoeken

Veel fouten is het resultaat van een blauwdruk toewijzen aan een bereik. Wanneer een toewijzing is mislukt, bevat de blauwdruk informatie over de mislukte implementatie. Deze informatie geeft aan dat het probleem zodat deze kan worden opgelost en de volgende implementatie is geslaagd.

1. Klik op **Alle services** en selecteer **Beleid** in het linkerdeelvenster. Klik op de pagina **Beleid** op **Blueprints**.

1. Selecteer **toegewezen blauwdrukken** op de pagina aan de linkerkant en gebruik het zoekvak om te filteren van het blueprint-toewijzingen voor de mislukte-toewijzing niet vinden. U kunt ook de lijst met toewijzingen door sorteren de **Inrichtingsstatus** kolom om te zien van alle mislukte toewijzingen gegroepeerd.

1. Klik op de blauwdruk met de _mislukt_ status of met de rechtermuisknop en selecteer **Toewijzingsdetails weergeven**.

1. Er is een rode banner waarschuwing dat de toewijzing is mislukt aan de bovenkant van de pagina van de toewijzing van blauwdruk. Klik ergens op de koptekst voor meer informatie.

Het is gebruikelijk voor de fout wordt veroorzaakt door een artefact en niet de blauwdruk als geheel. Als een artefact een Key Vault maakt en Azure Policy wordt voorkomen het maken van Key Vault dat, mislukt de hele toewijzing.

## <a name="general-errors"></a>Algemene fouten

### <a name="policy-violation"></a>Scenario: Schending van het beleid

#### <a name="issue"></a>Probleem

De sjabloonimplementatie is mislukt vanwege schending van het beleid.

#### <a name="cause"></a>Oorzaak

Een beleid voor kan strijdig zijn met de implementatie voor een aantal oorzaken hebben:

- De resource wordt gemaakt, is beperkt door het beleid (meestal SKU of locatie beperkingen)
- De implementatie is bezig met velden die zijn geconfigureerd door het beleid (algemene met tags)

#### <a name="resolution"></a>Oplossing

De blauwdruk wijzigen zodat deze niet met de beleidsregels in de foutdetails conflicteert. Als deze wijziging niet mogelijk is, wordt een alternatief is dat het bereik van de beleidstoewijzing gewijzigd, zodat de blauwdruk is niet langer een conflict met het beleid.

## <a name="next-steps"></a>Volgende stappen

Als u uw probleem niet zien of u niet kunt oplossen van uw probleem, gaat u naar een van de volgende kanalen voor ondersteuning van meer:

- Krijg antwoorden van Azure-experts op [Azure-Forums](https://azure.microsoft.com/support/forums/)
- Maak verbinding met [@AzureSupport](https://twitter.com/azuresupport), het officiële Microsoft Azure-account voor het verbeteren van de gebruikerservaring door de Azure-community in contact te brengen met de juiste resources: antwoorden, ondersteuning en experts.
- Als u meer hulp nodig hebt, kunt u een Azure-ondersteuning-incident indienen. Ga naar de [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.