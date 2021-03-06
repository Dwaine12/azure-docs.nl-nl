---
title: Migratie met minimale downtime met Azure Database for PostgreSQL
description: In dit artikel wordt beschreven hoe u een migratie met minimale downtime van een PostgreSQL-database met Azure Database for PostgreSQL uitvoeren met behulp van de Azure Database Migration Service.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 12/07/2018
ms.openlocfilehash: 0c8c3443a19c26dade9699560e883969d3c074df
ms.sourcegitcommit: 698ba3e88adc357b8bd6178a7b2b1121cb8da797
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/07/2018
ms.locfileid: "53010838"
---
# <a name="minimal-downtime-migration-to-azure-database-for-postgresql"></a>Migratie met minimale downtime met Azure Database for PostgreSQL
U kunt migratie naar Azure Database for PostgreSQL voor PostgreSQL met minimale downtime uitvoeren met behulp van de onlangs geïntroduceerde **doorlopende synchronisatie mogelijkheid** voor de [Azure Database Migration Service](https://aka.ms/get-dms) (DMS) . Deze functionaliteit beperkt de hoeveelheid uitvaltijd beperkt die worden gemaakt door de toepassing.

## <a name="overview"></a>Overzicht
Azure DMS wordt uitgevoerd van een aanvankelijke belasting van uw on-premises naar Azure Database voor PostgreSQL, en vervolgens continu worden gesynchroniseerd met een nieuwe transacties naar Azure terwijl de toepassing actief blijft. Nadat de gegevens de resultaten op de doel-Azure aan clientzijde, u stop de toepassing voor een korte moment (minimale downtime) en wacht tot de laatste batch van gegevens (vanaf het moment dat u de toepassing stoppen voordat de toepassing effectief niet beschikbaar is voor alle nieuwe verkeer) om af te vangen omhoog in de doel- en werk vervolgens de verbindingsreeks om te verwijzen naar Azure. Wanneer u klaar bent, wordt uw toepassing worden live in Azure!

![Doorlopende synchronisatie met de Azure Database Migration Service](./media/howto-migrate-online/ContinuousSync.png)

## <a name="next-steps"></a>Volgende stappen
- Bekijk de video [App-modernisering met Microsoft Azure](https://medius.studios.ms/Embed/Video/BRK2102?sid=BRK2102), die een demo van het PostgreSQL apps migreren naar Azure Database for PostgreSQL bevat.
- Zie de zelfstudie [PostgreSQL migreren met Azure Database for PostgreSQL online met behulp van DMS](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online).
