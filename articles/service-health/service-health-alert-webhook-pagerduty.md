---
title: Azure service health waarschuwingen configureren met PagerDuty | Microsoft Docs
description: Ophalen persoonlijke meldingen over service health-gebeurtenissen naar uw PagerDuty-exemplaar.
author: shawntabrizi
manager: scotthit
editor: ''
services: service-health
documentationcenter: service-health
ms.assetid: ''
ms.service: service-health
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/14/2017
ms.author: shtabriz
ms.openlocfilehash: 5f6f3f61b5f7a06ac4056499edfb811780838cdc
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39441874"
---
# <a name="configure-service-health-alerts-with-pagerduty"></a>Service health waarschuwingen configureren met PagerDuty

In dit artikel leest u hoe u Azure service health meldingen via PagerDuty instelt met behulp van een webhook. Met behulp van [PagerDuty](https://www.pagerduty.com/)van aangepaste type voor Microsoft Azure-integratie, kunt u moeiteloos servicestatus waarschuwingen toevoegen aan uw nieuwe of bestaande PagerDuty-services.

## <a name="creating-a-service-health-integration-url-in-pagerduty"></a>Het maken van een service-URL voor de integratie van health in PagerDuty
1.  Zorg ervoor dat u hebt zich heeft aangemeld en bent aangemeld bij uw [PagerDuty](https://www.pagerduty.com/) account.

1.  Navigeer naar de **Services** sectie in PagerDuty.

    ![De sectie 'Services' in PagerDuty](./media/webhook-alerts/pagerduty-services-section.png)

1.  Selecteer **nieuwe Service toevoegen** of open een bestaande service die u hebt ingesteld.

1.  In de **instellingen voor Adreslijstintegratie**, selecteert u het volgende:

    a. **Van Integratietype**: Microsoft Azure

    b. **De naam van de integratie van**: \<naam\>

    ![De 'integratie-instellingen' in PagerDuty](./media/webhook-alerts/pagerduty-integration-settings.png)

1.  Vul alle vereiste velden en selecteer **toevoegen**.

1.  Deze nieuwe integratie en exemplaar te openen en sla de **URL voor de integratie**.

    ![De 'integratie-URL' in PagerDuty](./media/webhook-alerts/pagerduty-integration-url.png)

## <a name="create-an-alert-using-pagerduty-in-the-azure-portal"></a>Een waarschuwing met behulp van PagerDuty in Azure portal maken
### <a name="for-a-new-action-group"></a>Voor een nieuwe actiegroep:
1. Volg de stappen 1 tot en met 8 in [een waarschuwing op een melding van de health service voor een nieuwe actiegroep maken met behulp van de Azure-portal](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).

1. In de lijst van definiëren **acties**:

    a. **Actietype:** *Webhook*

    b. **Details:** de PagerDuty **URL voor de integratie** u eerder hebt opgeslagen.

    c. **Naam:** van de Webhook-naam, alias of id.

1. Selecteer **opslaan** wanneer u klaar bent om de waarschuwing te genereren.

### <a name="for-an-existing-action-group"></a>Voor een bestaande actiegroep:
1. In de [Azure-portal](https://portal.azure.com/), selecteer **Monitor**.

1. In de **instellingen** sectie, selecteer **actiegroepen**.

1. Zoek en selecteer de actiegroep die u wilt bewerken.

1. Toevoegen aan de lijst met **acties**:

    a. **Actietype:** *Webhook*

    b. **Details:** de PagerDuty **URL voor de integratie** u eerder hebt opgeslagen.

    c. **Naam:** van de Webhook-naam, alias of id.

1. Selecteer **opslaan** wanneer u klaar bent voor het bijwerken van de actiegroep.

## <a name="testing-your-webhook-integration-via-an-http-post-request"></a>Testen van de integratie van webhooks via een HTTP POST-aanvraag
1. Maak de nettolading van de service health die u wilt verzenden. U vindt een voorbeeld van de service health webhookpayload op [Webhooks voor Azure-activiteit waarschuwingen voor activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook.md).

1. Maak een HTTP POST-aanvraag als volgt:

    ```
    POST        https://events.pagerduty.com/integration/<IntegrationKey>/enqueue

    HEADERS     Content-Type: application/json

    BODY        <service health payload>
    ```
1. U ontvangt een `202 Accepted` met een bericht met uw 'gebeurtenis-ID."

1. Ga naar [PagerDuty](https://www.pagerduty.com/) om te bevestigen dat uw integratie met succes is ingesteld.

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over het [configureren van de webhook-meldingen voor bestaande beheersystemen voor probleem](service-health-alert-webhook-guide.md).
- Controleer de [activiteit log waarschuwing webhook-schema](../monitoring-and-diagnostics/monitoring-activity-log-alerts-webhook.md). 
- Meer informatie over [health servicemeldingen](../monitoring-and-diagnostics/monitoring-service-notifications.md).
- Meer informatie over [actiegroepen](../monitoring-and-diagnostics/monitoring-action-groups.md).