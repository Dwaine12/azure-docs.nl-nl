---
title: Azure voor firewallregels voor PostgreSQL Server-Database
description: Dit artikel worden de firewallregels voor uw Azure-Database voor PostgreSQL-server.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 8a3f5d9fa8f1c36d8468c38f7dda803d3ca1d832
ms.sourcegitcommit: c765cbd9c379ed00f1e2394374efa8e1915321b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/28/2018
ms.locfileid: "29689884"
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Azure voor firewallregels voor PostgreSQL Server-Database
Azure-Database voor de firewall PostgreSQL-Server voorkomt alle toegang tot uw database-server, totdat u opgeven welke computers over machtigingen beschikken. De firewall verleent toegang tot de server op basis van het oorspronkelijke IP-adres van elke aanvraag.
U configureert de firewall door firewallregels te maken die bereiken opgeven van acceptabele IP-adressen. U kunt firewallregels op serverniveau maken.

**Firewall-regels:** deze regels kunnen clients toegang tot uw volledige Azure-Database voor PostgreSQL-Server, dat wil zeggen, alle databases binnen dezelfde logische server. Firewallregels op serverniveau kunnen worden geconfigureerd met behulp van de Azure-portal of met Azure CLI-opdrachten. U moet eigenaar van het abonnement of een bijdrager abonnement zijn voor het maken van de firewallregels op serverniveau.

## <a name="firewall-overview"></a>Firewalloverzicht
Alle databasetoegang tot uw Azure-Database voor PostgreSQL-server is standaard geblokkeerd door de firewall. Om te beginnen met behulp van uw server uit een andere computer, moet u een of meer serverniveau firewallregels voor toegang tot uw server opgeven. Gebruik de firewallregels om op te geven welke IP-adresbereiken van het Internet om toe te staan. Toegang tot de Azure portal-website zelf wordt niet beïnvloed door de firewall-regels.
Verbindingspogingen van Internet en Azure moeten eerst doorgeven via de firewall voordat ze uw PostgreSQL-Database kunnen bereiken zoals weergegeven in het volgende diagram:

![Voorbeeld van de stroom van de werking van de firewall](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a>Verbinding maken vanuit internet
Firewallregels op serverniveau gelden voor alle databases op dezelfde Azure-Database voor PostgreSQL-server. Als het IP-adres van de aanvraag binnen een van de bereiken ligt die zijn opgegeven in de firewallregels op serverniveau, wordt de verbinding toegestaan.
Als het IP-adres van de aanvraag niet binnen de bereiken die in de firewallregels op serverniveau zijn opgegeven is, wordt de verbindingsaanvraag mislukt.
Bijvoorbeeld, als uw toepassing verbinding met JDBC-stuurprogramma voor PostgreSQL maakt, u deze fout kan optreden wanneer de verbinding wordt geblokkeerd door de firewall verbinding proberen te maken.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATALE: Er is geen pg\_hba.conf-vermelding voor de host ": 123.45.67.890", gebruiker 'adminuser', database 'postgresql', SSL

## <a name="connecting-from-azure"></a>Verbinding maken vanuit Azure
Zodat toepassingen van Azure te verbinden met uw Azure-Database voor PostgreSQL-server moeten de Azure-verbindingen zijn ingeschakeld. Bijvoorbeeld als host voor een Web-Apps van Azure-toepassing of een toepassing die wordt uitgevoerd in een Azure VM of verbinding te maken uit een Azure Data Factory data management gateway. De resources hoeft niet te worden in het hetzelfde virtuele netwerk (VNet) of de resourcegroep voor de firewallregel inschakelen van deze verbindingen. Wanneer een toepassing vanuit Azure probeert verbinding te maken met uw databaseserver, verifieert de firewall of Azure-verbindingen zijn toegestaan. Er zijn een aantal methoden aan de hand van deze typen verbindingen. Een firewallinstelling waarvan het begin- en eindadres gelijk zijn aan 0.0.0.0 geeft aan dat deze verbindingen zijn toegestaan. U kunt ook instellen de **toegang tot Azure-services toestaan** optie naar **ON** in de portal van de **verbindingsbeveiliging** deelvenster en drukt **Opslaan**. Als de verbindingspoging is niet toegestaan, wordt in de aanvraag de Azure-Database voor PostgreSQL-server niet bereiken.

> [!IMPORTANT]
> Met deze optie configureert u de firewall zo dat alle verbindingen vanuit Azure zijn toegestaan, inclusief verbindingen vanuit de abonnementen van andere klanten. Wanneer u deze optie selecteert, zorg dan dat uw aanmeldings- en gebruikersmachtigingen de toegang beperken tot alleen geautoriseerde gebruikers.
> 

![Toegang tot Azure-services in de portal configureren](media/concepts-firewall-rules/allow-azure-services.png)

## <a name="programmatically-managing-firewall-rules"></a>Firewallregels programmatisch beheren
Naast de Azure portal firewallregels, worden beheerd via een programma met Azure CLI.
Zie ook [maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-the-database-server-firewall"></a>Het oplossen van de firewall van de database-server
Houd rekening met de volgende punten wanneer toegang tot de Microsoft Azure-Database voor PostgreSQL Server-service niet meer werkt zoals verwacht:

* **Wijzigingen aan de lijst zijn niet van kracht:** mogelijk zijn er zoveel een vertraging vijf minuten voor in de Azure-Database voor de firewallconfiguratie PostgreSQL-Server wijzigingen te activeren.

* **De aanmelding is niet gemachtigd of een onjuist wachtwoord is gebruikt:** als een aanmelding heeft geen machtigingen voor de Azure-Database voor PostgreSQL-server of het wachtwoord onjuist is, de verbinding met de Azure-Database voor PostgreSQL-server is geweigerd. Maken van een firewallinstelling biedt alleen clients met een kans om het proberen verbinding te maken met uw server. elke client moet nog steeds de benodigde beveiligingsreferenties opgeven.

Bijvoorbeeld met behulp van een JDBC-client de volgende fout kan worden weergegeven.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATALE: wachtwoordverificatie is mislukt voor gebruiker 'uwgebruikersnaam'

* **Dynamisch IP-adres:** als u een internetverbinding hebt met dynamische IP-adressering en problemen ondervindt bij het passeren van de firewall, kunt u een van de volgende oplossingen proberen:

* Vraag uw serviceprovider (ISP) om het IP-adresbereik is toegewezen aan de clientcomputers die toegang hebben tot de Azure-Database voor PostgreSQL-Server en vervolgens het IP-adresbereik toevoegen als een firewallregel.

* Statische IP-adressen in plaats daarvan voor uw clientcomputers ophalen en voeg vervolgens het statische IP-adres als een firewallregel.

## <a name="next-steps"></a>Volgende stappen
Zie voor artikelen over het maken van server- en databaseniveau firewall-regels:
* [Maken en beheren van Azure-Database voor firewallregels PostgreSQL met de Azure portal](howto-manage-firewall-using-portal.md)
* [Maken en beheren van Azure-Database voor firewallregels PostgreSQL met Azure CLI](howto-manage-firewall-using-cli.md)
