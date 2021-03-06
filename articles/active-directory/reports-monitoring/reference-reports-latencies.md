---
title: Azure Active Directory reporting latenties | Microsoft Docs
description: Meer informatie over de hoeveelheid tijd die nodig is voor rapportage gebeurtenissen worden weergegeven in uw Azure-portal
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: e5ceae2959f79c677f5b89c0c3f0a487f92ad1c6
ms.sourcegitcommit: 1f9e1c563245f2a6dcc40ff398d20510dd88fd92
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/14/2018
ms.locfileid: "51623176"
---
# <a name="azure-active-directory-reporting-latencies"></a>Azure Active Directory reporting latenties

Latentie is de hoeveelheid tijd die nodig is voor Azure Active Directory (Azure AD) rapportagegegevens worden weergegeven in de [Azure-portal](https://portal.azure.com). In dit artikel geeft een lijst van de verwachte latentie voor de verschillende typen rapporten. 

## <a name="activity-reports"></a>Activiteitsrapporten

Er zijn twee soorten activiteitsrapporten:

- [Aanmeldingen](concept-sign-ins.md) : bevat informatie over het gebruik van beheerde toepassingen en de gebruiker aanmeldingsactiviteiten
- [Auditlogboeken](concept-audit-logs.md) -biedt systeeminformatie over systeemactiviteit van gebruikers en groepen, beheerde toepassingen en directory-activiteiten

De volgende tabel bevat de latentie-informatie voor activiteitenrapporten. 

> [!NOTE]
> **Latentie (95e percentiel)** verwijst naar de tijd waarop 95% van de logboeken worden gerapporteerd, en **latentie (99%)** verwijst naar de tijd waarop 99% van de logboeken worden gerapporteerd. 
>

| Rapport | Latentie (95e percentiel) |Latentie (99%)|
| :-- | --- | --- | 
| Controlelogboeken | 2 minuten  | 5 minuten  |
| Aanmeldingen | 2 minuten  | 5 minuten |

## <a name="security-reports"></a>Beveiligingsrapporten

Er zijn twee soorten beveiligingsrapporten:

- [Riskante aanmeldingen](concept-risky-sign-ins.md) - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is. 
- [Gebruikers voor wie wordt aangegeven dat ze risico lopen](concept-user-at-risk.md) - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast. 

De volgende tabel bevat de latentie-informatie voor beveiligingsrapporten.

| Rapport | Minimum | Gemiddeld | Maximum |
| :-- | --- | --- | --- |
| Gebruikers die risico lopen          | 5 minuten   | 15 minuten  | 2 uur  |
| Riskante aanmeldingen         | 5 minuten   | 15 minuten  | 2 uur  |

## <a name="risk-events"></a>Risicogebeurtenissen

Azure AD maakt gebruik van adaptieve machine learning-algoritmes en -methodieken voor het detecteren van verdachte activiteit die is gekoppeld aan uw gebruikersaccounts. Elke gedetecteerde verdachte actie wordt opgeslagen in een record met de naam een **risicogebeurtenis**.

De volgende tabel bevat de latentie-informatie voor risicogebeurtenissen.

| Rapport | Minimum | Gemiddeld | Maximum |
| :-- | --- | --- | --- |
| Aanmeldingen vanaf anonieme IP-adressen |5 minuten |15 minuten |2 uur |
| Aanmeldingen vanaf onbekende locaties |5 minuten |15 minuten |2 uur |
| Gebruikers van wie de referenties zijn gelekt |2 uur |4 uur |8 uur |
| Onmogelijke reis naar ongewone locaties |5 minuten |1 uur |8 uur  |
| Aanmeldingen vanaf geïnfecteerde apparaten |2 uur |4 uur |8 uur  |
| Aanmeldingen van IP-adressen met verdachte activiteit |2 uur |4 uur |8 uur  |


## <a name="next-steps"></a>Volgende stappen

* [Overzicht van Azure AD-rapporten](overview-reports.md)
* [Programmatische toegang tot Azure AD-rapporten](concept-reporting-api.md)
* [Risicogebeurtenissen in Azure Active Directory](concept-risk-events.md)
