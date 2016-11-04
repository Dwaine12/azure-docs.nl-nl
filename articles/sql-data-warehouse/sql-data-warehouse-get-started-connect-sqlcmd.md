---
title: Query’s uitvoeren bij Azure SQL Data Warehouse (sqlcmd)| Microsoft Docs
description: Query’s uitvoeren bij Azure SQL Data Warehouse met het opdrachtregelhulpprogramma sqlcmd.
services: sql-data-warehouse
documentationcenter: NA
author: sonyam
manager: barbkess
editor: ''

ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 09/06/2016
ms.author: barbkess;sonyama

---
# Query’s uitvoeren bij Azure SQL Data Warehouse (sqlcmd)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> 
> 

In dit scenario maakt u gebruik van het opdrachtregelhulpprogramma [sqlcmd][sqlcmd] om een query uit te voeren bij een Azure SQL Data Warehouse.  

## 1. Verbinding maken
U gaat als volgt aan de slag met [sqlcmd][sqlcmd]: open de opdrachtprompt en voer **sqlcmd** in, gevolgd door de verbindingstekenreeks voor uw SQL Data Warehouse-database. De verbindingstekenreeks moet de volgende parameters bevatten:

* **Server (-S):** server in de notatie `<`servernaam`>`.database.windows.net
* **Database (-d):** databasenaam.
* **Id's tussen aanhalingstekens inschakelen (-I):** id's tussen aanhalingstekens moeten zijn ingeschakeld om verbinding te kunnen maken met een exemplaar van SQL Data Warehouse.

Als u gebruik wilt maken van SQL Server-verificatie, moet u de gebruikersnaam- en wachtwoordparameters toevoegen:

* **Gebruiker (-U):** servergebruiker in de notatie `<`gebruiker`>`
* **Wachtwoord (-P):** wachtwoord dat is gekoppeld aan de gebruiker.

Een voorbeeld: uw verbindingstekenreeks kan er als volgt uitzien:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Als u geïntegreerde verificatie van Azure Active Directory wilt gebruiken, moet u de Azure Active Directory-parameters toevoegen:

* **Azure Active Directory Authentication (-G):** Azure Active Directory gebruiken voor verificatie

Een voorbeeld: uw verbindingstekenreeks kan er als volgt uitzien:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> U moet [Azure Active Directory Authentication inschakelen](sql-data-warehouse-authentication.md) om te verifiëren met Active Directory.
> 
> 

## 2. Query’s uitvoeren
Wanneer verbinding is gemaakt, kunt u elke ondersteunde Transact-SQL-instructie voor het exemplaar uitvoeren.  In dit voorbeeld worden query's in de interactieve modus verzonden.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

In de volgende voorbeelden ziet u hoe u uw query's in de batchmodus uitvoert met behulp van de optie -Q of door uw SQL naar sqlcmd te sluizen.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## Volgende stappen
Zie [sqlcmd-documentatie][sqlcmd] voor meer informatie over de opties die beschikbaar zijn in sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure Portal]: https://portal.azure.com

<!--Other Web references-->



<!--HONumber=Sep16_HO3-->


