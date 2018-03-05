---
title: Verbindingsbibliotheken voor Azure-Database voor MySQL
description: Dit artikel vindt elke tapewisselaar of het stuurprogramma die clientprogramma's gebruiken kunnen bij het verbinden met Azure-Database voor MySQL.
services: mysql
author: mswutao
ms.author: wutao
manager: kfile
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: c22bb9b31e7623daa635f82256e28ed466070481
ms.sourcegitcommit: c765cbd9c379ed00f1e2394374efa8e1915321b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/28/2018
---
# <a name="connection-libraries-for-azure-database-for-mysql"></a>Verbindingsbibliotheken voor Azure-Database voor MySQL
Dit artikel vindt elke tapewisselaar of het stuurprogramma die clientprogramma's gebruiken kunnen bij het verbinden met Azure-Database voor MySQL.

## <a name="client-interfaces"></a>Clientinterfaces
MySQL biedt standaard databaseconnectiviteit stuurprogramma voor het gebruik van MySQL met toepassingen en hulpprogramma's die compatibel zijn met de industriestandaarden ODBC en JDBC. Elk systeem met ODBC of JDBC werkt kunt MySQL gebruiken.

| **Taal** | **Platform** | **Aanvullende bronnen** | **Downloaden** |
| :----------- | :------------| :-----------------------| :------------|
| PHP | Windows, Linux | [Systeemeigen MySQL-stuurprogramma voor PHP - mysqlnd](https://dev.mysql.com/downloads/connector/php-mysqlnd/) | [Downloaden](http://php.net/downloads.php) |
| ODBC | Windows, Linux, Mac OS X en Unix-platforms | [MySQL-Connector/ODBC-handleiding voor ontwikkelaars](https://dev.mysql.com/doc/connector-odbc/en/) | [Downloaden](https://dev.mysql.com/downloads/connector/odbc/) |
| ADO.NET | Windows | [MySQL Connector/Net Developer Guide](https://dev.mysql.com/doc/connector-net/en/) | [Downloaden](https://dev.mysql.com/downloads/connector/net/) |
| JDBC | Platformonafhankelijk | [MySQL Connector/J 5.1 Developer Guide](https://dev.mysql.com/doc/connector-j/5.1/en/) | [Downloaden](https://dev.mysql.com/downloads/connector/j/) |
| Node.js | Windows, Linux, Mac OS X | [sidorares/node-mysql2](https://github.com/sidorares/node-mysql2/tree/master/documentation) | [Downloaden](https://github.com/sidorares/node-mysql2) |
| Python | Windows, Linux, Mac OS X | [MySQL Connector/Python Developer Guide](https://dev.mysql.com/doc/connector-python/en/) | [Downloaden](https://dev.mysql.com/downloads/connector/python/) |
| C++ | Windows, Linux, Mac OS X | [MySQL Connector/C++ Developer Guide](https://dev.mysql.com/doc/connector-cpp/en/) | [Downloaden](https://dev.mysql.com/downloads/connector/python/) |
| C | Windows, Linux, Mac OS X | [MySQL Connector/C Developer Guide](https://dev.mysql.com/doc/connector-c/en/) | [Downloaden](https://dev.mysql.com/downloads/connector/c/)
| Perl | Windows, Linux, Mac OS X en Unix-platforms | [DBD::MySQL](https://metacpan.org/pod/DBD::mysql) | [Downloaden](https://metacpan.org/pod/DBD::mysql) |


## <a name="next-steps"></a>Volgende stappen
Lees deze snelstartgidsen voor het verbinding maken met en doorzoeken op Azure Database MySQL met behulp van de taal van uw keuze:

[PHP](./connect-php.md) | [Java](./connect-java.md) |  [.NET (C#)](./connect-csharp.md) | [Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [Ruby](./connect-ruby.md) | [C++](connect-cpp.md) | [Go](./connect-go.md)

