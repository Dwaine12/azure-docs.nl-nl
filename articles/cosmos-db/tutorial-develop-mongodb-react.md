---
title: Zelfstudie voor MongoDB, React en Node.js voor Azure
description: Leer aan de hand van deze reeks zelfstudies op video een MongoDB-app maken met React en Node.js op Azure Cosmos DB met precies dezelfde APIs die u gebruikt voor MongoDB.
services: cosmos-db
author: johnpapa
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 09/05/2017
ms.author: jopapa
ms.custom: mvc
ms.openlocfilehash: bd72aad51d2649ba6f110ab07b3f85d58da2a09d
ms.sourcegitcommit: b0f39746412c93a48317f985a8365743e5fe1596
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52867032"
---
# <a name="create-a-mongodb-app-with-react-and-azure-cosmos-db"></a>Een MongoDB-app maken met React en Azure Cosmos DB  

In deze meerdelige zelfstudie op video wordt gedemonstreerd hoe u een app voor het volgen van hero's maakt met een React-frontend. De app gebruikt Node en Express voor de server, maakt verbinding met Azure Cosmos DB met de [MongoDB API](mongodb-introduction.md), en verbindt vervolgens de React-frontend met het servergedeelte van de app. In deze zelfstudie wordt ook gedemonstreerd hoe u met aanwijzen en klikken schaling uitvoert van Azure Cosmos DB in Azure Portal en hoe u de app implementeert met internet, zodat gebruikers hun favoriete hero's kunnen volgen. 

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) ondersteunt MongoDB-clientverbindingen, zodat u Azure Cosmos DB kunt gebruiken in plaats van MongoDB, maar dezelfde code die u gebruikt voor MongoDB-apps, maar met extra voordelen, zoals eenvoudige cloudimplementatie, schaling en supersnel lezen en schrijven.  

Deze meerdelige zelfstudie behandelt de volgende taken:

> [!div class="checklist"]
> * Inleiding
> * Het project instellen
> * De gebruikersinterface bouwen met React
> * Een Azure Cosmos DB-account maken in Azure Portal
> * Mongoose gebruiken om verbinding te maken met Azure Cosmos DB
> * De bewerkingen React, Create, Update en Delete aan de app toevoegen

Wilt u dezelfde app bouwen met Angular? Zie de [videoserie met zelfstudies van Angular](tutorial-develop-mongodb-nodejs.md).

## <a name="prerequisites"></a>Vereisten
* [Node.js](https://www.nodejs.org)

### <a name="finished-project"></a>Voltooid project
Download de voltooide app [op GitHub](https://github.com/Azure-Samples/react-cosmosdb).

## <a name="introduction"></a>Inleiding 

In deze video geeft Burke Holland een inleiding tot Azure Cosmos DB en wordt u door de app begeleid die in deze videoserie wordt gemaakt. 

> [!VIDEO https://www.youtube.com/embed/58IflnJbYJc]

## <a name="project-setup"></a>Instellen van het project

In deze video ziet u hoe u Express en React in hetzelfde project instelt. Burke geeft u vervolgens een kijkje in de code van het project.

> [!VIDEO https://www.youtube.com/embed/ytFUPStJJds]

## <a name="build-the-ui"></a>De gebruikersinterface bouwen

In deze video ziet u hoe u de gebruikersinterface van de app maakt met React. 

> [!NOTE]
> De CSS waarnaar in deze video wordt verwezen, kunt u vinden in de [react-cosmosdb GitHub-opslagplaats](https://github.com/Azure-Samples/react-cosmosdb/blob/master/src/index.css).

> [!VIDEO https://www.youtube.com/embed/SzHzX0fTUUQ]

## <a name="connect-to-azure-cosmos-db"></a>Verbinding maken met Azure Cosmos DB

In deze video ziet u hoe u een Azure Cosmos DB-account maakt in Azure Portal, de MongoDB- en Mongoose-pakketten installeert, en vervolgens de app verbinding laat maken met het nieuwe account met behulp van de Azure Cosmos DB-verbindingsreeks. 

> [!VIDEO https://www.youtube.com/embed/0U2jV1thfvs]

## <a name="read-and-create-heroes-in-the-app"></a>Hero's in de app lezen en maken

In deze video ziet u hoe u hero's leest en hero's maakt in de Cosmos DB-database, en hoe u deze methoden test in Postman en de React-gebruikersinterface. 

> [!VIDEO https://www.youtube.com/embed/AQK9n_8fsQI] 

## <a name="delete-and-update-heroes-in-the-app"></a>Hero's in de app bijwerken en uit de app verwijderen

In deze video ziet u hoe u hero's uit de app verwijdert en in de app bijwerkt en de updates in de gebruikersinterface kunt weergeven. 

> [!VIDEO https://www.youtube.com/embed/YmaGT7ztTQM] 

## <a name="complete-the-app"></a>De app voltooien

In deze video ziet u hoe u de app voltooit en de gebruikersinterface ten slotte verbindt met de backend-API. 

> [!VIDEO https://www.youtube.com/embed/TcSm2ISfTu8]

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze app verder niet gaat gebruiken, kunt u met de volgende stappen alle resources verwijderen die met deze zelfstudies in Azure Portal zijn gemaakt. 

1. Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt. 
2. Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]
> * Een app maken met React, Node, Express en Azure Cosmos DB 
> * Maak een Azure Cosmos DB-account
> * De app verbinding laten maken met het Azure Cosmos DB-account
> * De app testen in Postman
> * De app uitvoeren en hero's toevoegen aan de database

Kom hier terug voor een aanvullende video in deze serie zelfstudies, waarin de implementatie van de app en het globaal repliceren van uw gegevens aan de orde komt.

U kunt doorgaan met de volgende zelfstudie om te leren hoe u MongoDB-gegevens in Azure Cosmos DB importeert.  

> [!div class="nextstepaction"]
> [MongoDB-gegevens importeren in Azure Cosmos DB](mongodb-migrate.md)
 
