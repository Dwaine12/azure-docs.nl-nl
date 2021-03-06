---
title: bestand opnemen
description: bestand opnemen
services: digital-twins
author: dsk-2015
ms.service: digital-twins
ms.topic: include
ms.date: 09/17/2018
ms.author: dkshir
ms.custom: include file
ms.openlocfilehash: e5e015c1e12e68f54ae7fd32082faed1abfebe74
ms.sourcegitcommit: b62f138cc477d2bd7e658488aff8e9a5dd24d577
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51626388"
---
1. Meld u aan bij de [Azure-portal](http://portal.azure.com).

1. Selecteer **Een resource maken** in het linkerdeelvenster. Zoek naar **digital twins** en selecteer **Digital Twins (preview)**. Selecteer **Maken** om het implementatieproces te starten.

   ![Selecties voor het maken van een nieuw Digital Twins-exemplaar](./media/create-digital-twins-portal/create-digital-twins.png)

1. In het deelvenster **Digital Twins** voert u de volgende informatie in:
   * **Resourcenaam**: geef uw instantie van Digital Twins een unieke naam.
   * **Abonnement**: kies het abonnement dat u wilt gebruiken om deze instantie van Digital Twins te maken. 
   * **Resourcegroep**: selecteer of maak een [resourcegroep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) voor de instantie van Digital Twins.
   * **Locatie**: selecteer de locatie die het dichtst bij uw apparaten in de buurt is.

    ![Digital Twins-deelvenster met ingevoerde gegevens](./media/create-digital-twins-portal/create-digital-twins-param.png)

1. Controleer uw Digital Twins-gegevens en selecteer **Maken**. Het kan een paar minuten duren voordat uw instantie van Digital Twins is gemaakt. U kunt de voortgang bewaken via het deelvenster **Meldingen**.

1. Open het deelvenster **Overzicht** van de instantie van Digital Twins. Zoals u ziet, wordt er een koppeling weergegeven onder **Beheer API**.

   De indeling van de URL van de **Beheer API** is: _https://yourDigitalTwinsName.yourLocation.azuresmartspaces.net/management/swagger_. Deze URL leidt u naar de documentatie van de REST API van Azure Digital Twins, die van toepassing is op uw instantie. Zie [Het gebruik van Azure Digital Twins Swagger](../articles/digital-twins/how-to-use-swagger.md) voor informatie over hoe u deze API-documentatie dient te lezen en gebruiken.

    Wijzig de URL van de **Beheer API** als volgt: _https://yourDigitalTwinsName.yourLocation.azuresmartspaces.net/management/api/v1.0/_. Uw toepassing gebruikt de aangepaste URL als de basis-URL voor toegang tot uw instantie. Kopieer deze gewijzigde URL naar een tijdelijk bestand. U hebt deze URL nodig in de volgende sectie.

    ![Beheer-API](./media/create-digital-twins-portal/digital-twins-management-api.png)