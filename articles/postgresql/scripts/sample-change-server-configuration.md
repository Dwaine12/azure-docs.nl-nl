---
title: 'Azure CLI-script: serverconfiguraties wijzigen'
description: Dit CLI-voorbeeldscript maakt een lijst met alle beschikbare serverconfiguratieopties en werkt de waarde van een van de opties bij.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 02/28/2018
ms.openlocfilehash: 1a2ce1b8f8bdd5c06a4bbd42568166bf0ac73a71
ms.sourcegitcommit: 56d20d444e814800407a955d318a58917e87fe94
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/29/2018
ms.locfileid: "52580402"
---
# <a name="list-and-update-configurations-of-an-azure-database-for-postgresql-server-using-azure-cli"></a>Configuraties van een Azure Database for PostgreSQL-server opsommen en bijwerken met behulp van Azure CLI
Met dit CLI-voorbeeldscript wordt een lijst gemaakt van alle beschikbare configuratieparameters en de toegestane waarden ervan voor Azure-Database for PostgreSQL-server, en wordt *log_retention_days* ingesteld op een andere waarde dan de standaardwaarde.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal uit te voeren, moet u voor dit artikel gebruikmaken van Azure CLI-versie 2.0 of hoger. Controleer de versie door `az --version` uit te voeren. Zie [Azure CLI installeren]( /cli/azure/install-azure-cli) voor het installeren of upgraden van uw versie van Azure CLI. 

## <a name="sample-script"></a>Voorbeeldscript
Bewerk in dit voorbeeldscript de gemarkeerde regels om de gebruikersnaam en het wachtwoord van de beheerder naar uw eigen bij te werken.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/change-server-configurations/change-server-configurations.sh?highlight=15-16 "List and update configurations of Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie
Gebruik de volgende opdracht om de resourcegroep en alle resources die er aan zijn gekoppeld te verwijderen nadat het script is uitgevoerd. 
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/change-server-configurations/delete-postgresql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a>Uitleg van het script
Dit script maakt gebruik van de opdrachten die in de volgende tabel worden weergegeven:

| **Opdracht** | **Opmerkingen** |
|---|---|
| [az group create](/cli/azure/group#az_group_create) | Hiermee wordt een resourcegroep gemaakt waarin alle resources worden opgeslagen. |
| [az postgres server create](/cli/azure/postgres/server#az_postgres_server_create) | Hiermee wordt een PostgreSQL-server gemaakt waar de SQL-database wordt gehost. |
| [az postgres server configuration list](/cli/azure/postgres/server/configuration#az_postgres_server_configuration_list) | Hiermee wordt een lijst gemaakt van de configuraties van een Azure Database for PostgreSQL-server. |
| [az postgres server configuration set](/cli/azure/postgres/server/configuration#az_postgres_server_configuration_set) | Hiermee wordt de configuratie van een Azure Database for PostgreSQL-server bijgewerkt. |
| [az postgres server configuration show](/cli/azure/postgres/server/configuration#az_postgres_server_configuration_show) | Hiermee wordt de configuratie van een Azure Database for PostgreSQL-server weergegeven. |
| [az group delete](/cli/azure/group#az_group_delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle geneste resources. |

## <a name="next-steps"></a>Volgende stappen
- Lees de [documentatie van Azure CLI](/cli/azure) voor meer informatie over de Azure CLI.
- Meer scripts om te proberen: [Azure CLI-voorbeelden voor Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)
- Zie voor meer informatie over serverparameters [Serverparameters configureren in Azure-portal](../howto-configure-server-parameters-using-portal.md).
