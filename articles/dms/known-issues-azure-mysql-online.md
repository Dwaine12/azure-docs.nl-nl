---
title: Artikel over bekende problemen/migratiebeperkingen met online migratie naar Azure Database for MySQL | Microsoft Docs
description: Meer informatie over bekende problemen/migratiebeperkingen met online migratie naar Azure Database voor MySQL.
services: database-migration
author: HJToland3
ms.author: scphang
manager: ''
ms.reviewer: ''
ms.service: database-migration
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 10/09/2018
ms.openlocfilehash: 6e82c10d8e9109279045095c1b856520245a5a6f
ms.sourcegitcommit: 55952b90dc3935a8ea8baeaae9692dbb9bedb47f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/09/2018
ms.locfileid: "48884507"
---
# <a name="known-issuesmigration-limitations-with-online-migrations-to-azure-db-for-mysql"></a>Bekende problemen/migratiebeperkingen met online migratie naar Azure DB voor MySQL

Bekende problemen en beperkingen die zijn gekoppeld aan online migratie van MySQL naar Azure Database voor MySQL worden in de volgende secties beschreven. 

## <a name="online-migration-configuration"></a>Configuratie voor de online migratie
- De bronversie van MySQL Server moet versie 5.6.35, 5.7.18 of hoger zijn
- Azure Database for MySQL ondersteunt:
    - Bewerking door MySQL-community
    - InnoDB-engine
- Versiemigratie van dezelfde. Migreren van MySQL 5.6 met Azure Database voor MySQL 5.7 wordt niet ondersteund.
- Binaire logboekregistratie inschakelen in my.ini (Windows) of my.cnf (Unix)
    - Server_id op een willekeurig getal groter of gelijk is aan instellen op 1, bijvoorbeeld Server_id = 1 (alleen voor MySQL 5.6)
    - Instellen van log-bin = <path> (alleen voor MySQL 5.6)
    - Stel binlog_format = rij
    - Expire_logs_days = 5 (aanbevolen - alleen voor MySQL 5.6)
- Gebruiker moet de rol ReplicationAdmin hebben.
- Sorteringen gedefinieerd voor de bron-MySQL-database zijn hetzelfde als de die zijn gedefinieerd in de doel-Azure Database voor MySQL.
- Schema moet overeenkomen met tussen source MySQL-database en de doeldatabase in Azure Database voor MySQL.
- Schema in de doel-Azure Database for MySQL mag geen refererende sleutels. Gebruik de volgende query refererende sleutels verwijderen:
    ```
    SET group_concat_max_len = 8192;
    SELECT SchemaName, GROUP_CONCAT(DropQuery SEPARATOR ';\n') as DropQuery, GROUP_CONCAT(AddQuery SEPARATOR ';\n') as AddQuery
    FROM
    (SELECT 
    KCU.REFERENCED_TABLE_SCHEMA as SchemaName, KCU.TABLE_NAME, KCU.COLUMN_NAME,
        CONCAT('ALTER TABLE ', KCU.TABLE_NAME, ' DROP FOREIGN KEY ', KCU.CONSTRAINT_NAME) AS DropQuery,
        CONCAT('ALTER TABLE ', KCU.TABLE_NAME, ' ADD CONSTRAINT ', KCU.CONSTRAINT_NAME, ' FOREIGN KEY (`', KCU.COLUMN_NAME, '`) REFERENCES `', KCU.REFERENCED_TABLE_NAME, '` (`', KCU.REFERENCED_COLUMN_NAME, '`) ON UPDATE ',RC.UPDATE_RULE, ' ON DELETE ',RC.DELETE_RULE) AS AddQuery
        FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE KCU, information_schema.REFERENTIAL_CONSTRAINTS RC
        WHERE
          KCU.CONSTRAINT_NAME = RC.CONSTRAINT_NAME
          AND KCU.REFERENCED_TABLE_SCHEMA = RC.UNIQUE_CONSTRAINT_SCHEMA
      AND KCU.REFERENCED_TABLE_SCHEMA = ['schema_name']) Queries
      GROUP BY SchemaName;
    ```

    Voer de drop refererende sleutel (dit is de tweede kolom) in het queryresultaat.
- Schema in de doel-Azure Database for MySQL mag geen geen triggers. Laten vallen van triggers in de doeldatabase:
    ```
    SELECT Concat('DROP TRIGGER ', Trigger_Name, ';') FROM  information_schema.TRIGGERS WHERE TRIGGER_SCHEMA = 'your_schema';
    ```

## <a name="datatype-limitations"></a>Beperkingen van gegevenstype
- **Beperking**: als er een JSON-gegevenstype in de bron-database voor MySQL is, migratie mislukt tijdens de continue synchronisatie.

    **Tijdelijke oplossing**: JSON wijzigen datatype gemiddeld tekst of longtext in source MySQL-database.

- **Beperking**: als er geen primaire sleutel voor tabellen, doorlopende synchronisatie mislukken.
 
    **Tijdelijke oplossing**: een primaire sleutel voor de tabel voor de migratie om door te gaan tijdelijk in te stellen. Nadat de migratie van gegevens is voltooid, kunt u de primaire sleutel verwijderen.

## <a name="lob-limitations"></a>LOB-beperkingen
Grote Object (LOB)-kolommen zijn kolommen die kunnen worden vergroot groot. Voor MySQL, middelgrote tekst, zijn sommige van de gegevenstypen van LOB Longtext, Blob, Mediumblob, Longblob, enzovoort.

- **Beperking**: als LOB-gegevenstypen worden gebruikt als primaire sleutels, dan mislukt de migratie.

    **Tijdelijke oplossing**: primaire sleutel met andere gegevenstypen of kolommen die LOB niet vervangen.

- **Beperking**: als de lengte van het grote Object (LOB)-kolom groter dan 32 KB is, gegevens op het doel kan worden afgekapt. U kunt de lengte van LOB-kolom met behulp van deze query controleren:
    ```
    SELECT max(length(description)) as LEN from catalog;
    ```

    **Tijdelijke oplossing**: hebt u LOB-object dat groter is dan 32 KB, neem dan contact op met de engineering-team op [ dmsfeedback@microsoft.com ](mailto:dmsfeedback@microsoft.com). 

## <a name="other-limitations"></a>Andere beperkingen
- Een wachtwoord met openen en sluiten accolades {} aan het begin en einde van de tekenreeks van het wachtwoord wordt niet ondersteund. Deze beperking geldt voor zowel verbinden met MySQL bron en doel-Azure Database voor MySQL.
- De volgende DDLs worden niet ondersteund:
    - Alle partitie DDLs
    - Tabel verwijderen
    - Tabelnaam wijzigen
- Met behulp van de *alter table < table_name > kolom < kolomnaam > toevoegen* kolommen toevoegen aan het begin of het midden van een tabel-instructie wordt niet ondersteund. De *alter table < table_name > kolom < kolomnaam > toevoegen* voegt de kolom toe aan het einde van de tabel.
- Gemaakt op slechts een deel van de kolomgegevens indexen worden niet ondersteund. De volgende instructie is een voorbeeld van een index met behulp van slechts een deel van de kolomgegevens gemaakt:
    ``` 
    CREATE INDEX partial_name ON customer (name(10));
    ```

- In DMS is de limiet van databases voor het migreren van de van een enkele migratieactiviteit vier.
