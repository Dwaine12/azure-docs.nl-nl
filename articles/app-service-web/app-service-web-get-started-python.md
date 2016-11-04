---
title: Uw eerste Python-web-app in vijf minuten in Azure implementeren | Microsoft Docs
description: Hier ontdekt u door een voorbeeld-app te implementeren hoe eenvoudig het is om web-apps in App Service uit te voeren. U kunt snel een app gaan ontwikkelen en onmiddellijk de resultaten bekijken.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: wpickett
editor: ''

ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 09/16/2016
ms.author: cephalin

---
# Uw eerste Python-web-app in vijf minuten in Azure implementeren
Met deze zelfstudie leert u om uw eerste Python-web-app te implementeren in [Azure App Service](../app-service/app-service-value-prop-what-is.md).
Met App Service kunt u web-apps, [back-ends voor mobiele apps](/documentation/learning-paths/appservice-mobileapps/) en [API-apps](../app-service-api/app-service-api-apps-why-best-platform.md) maken.

U gaat het volgende doen: 

* Een web-app maken in Azure App Service.
* Python-voorbeeldcode implementeren.
* Zien hoe de code live in productie wordt uitgevoerd.
* De web-app op dezelfde manier bijwerken als waarop u [Git-doorvoeracties pusht](https://git-scm.com/docs/git-push).

## Vereisten
* [Installeer Git](http://www.git-scm.com/downloads). Controleer of de installatie is geslaagd door `git --version` uit te voeren vanuit een nieuwe Windows-opdrachtprompt, een PowerShell-venster, Linux-shell of OS X-terminal.
* Verkrijg een Microsoft Azure-account. Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> U kunt [App Service proberen](http://go.microsoft.com/fwlink/?LinkId=523751) zonder een Azure-account. U kunt een beginnerstoepassing maken en hier een uur mee spelen. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

<a name="create"></a>

## Een webtoepassing maken
1. Meld u met uw Azure-account aan bij de [Azure-portal](https://portal.azure.com).
2. Klik in het menu aan de linkerkant op **Nieuw** > **Web en mobiel** > **Web-app**.
   
    ![](./media/app-service-web-get-started-languages/create-web-app-portal.png)
3. Gebruik in de blade voor het maken van de app de volgende instellingen voor de nieuwe app:
   
   * **App-naam**: voer een unieke naam in.
   * **Resourcegroep**: selecteer **Nieuwe maken** en geef de resourcegroep een naam.
   * **App Service-plan/-locatie**: klik hier om te configureren en klik vervolgens op **Nieuwe maken** om als u de naam, locatie en prijscategorie van het App Service-plan wilt instellen. Gebruik gerust de prijscategorie **Gratis**.
     
     Wanneer u klaar bent, ziet de blade voor het maken van de app er als volgt uit:
     
     ![](./media/app-service-web-get-started-languages/create-web-app-settings.png)
4. Klik onderaan op **Maken**. U kunt bovenaan op het **melding**spictogram klikken als u de voortgang wilt bekijken.
   
    ![](./media/app-service-web-get-started-languages/create-web-app-started.png)
5. Wanneer de implementatie is voltooid, ziet u deze melding. Klik op het bericht als u de blade van uw implementatie wilt openen.
   
    ![](./media/app-service-web-get-started-languages/create-web-app-finished.png)
6. Klik in de blade **Implementatie is voltooid** op de koppeling **Resource** om de blade van de nieuwe web-app te openen.
   
    ![](./media/app-service-web-get-started-languages/create-web-app-resource.png)

## Code voor de web-app implementeren
Nu gaat u met Git een stukje code in Azure implementeren.

1. Schuif in de blade van de web-app omlaag naar **Implementatieopties** of zoek deze optie en klik erop. 
   
    ![](./media/app-service-web-get-started-languages/deploy-web-app-deployment-options.png)
2. Klik op **Bron kiezen** > **Lokale Git-opslagplaats** > **OK**.
3. Terug in de blade van de web-app klikt u op **Implementatiereferenties**.
4. Stel uw implementatiereferenties in en klik op **Opslaan**.
5. Terug in de blade van de web-app schuift u omlaag naar **Eigenschappen** of zoekt u deze optie en klikt u erop. Klik naast de **Git-URL** op de knop **Kopiëren**.
   
    ![](./media/app-service-web-get-started-languages/deploy-web-app-properties.png)
   
    Nu kunt u uw code met Git gaan implementeren.
6. Schakel in de opdrachtregelterminal naar een werkmap (`CD`) en ga als volgt te werk om de voorbeeld-app te kopiëren:
   
        git clone https://github.com/Azure-Samples/app-service-web-python-get-started.git
   
    ![Kopieer de voorbeeldcode van de app voor uw eerste web-app in Azure](./media/app-service-web-get-started-languages/python-git-clone.png)
   
    Voor *&lt;github_sample_url>* gebruikt u een van de volgende URL's, afhankelijk van het framework dat u wilt gebruiken:
7. Schakel naar de opslagplaats van uw voorbeeld-app. Bijvoorbeeld: 
   
        cd app-service-web-html-get-started
8. Stel de git remote voor uw Azure-app in op de Git-URL die u enkele stappen eerder hebt gekopieerd vanuit de portal.
   
        git remote add azure <giturlfromportal>
9. Implementeer de voorbeeldcode in de Azure-app op dezelfde manier als waarop u code zou pushen met Git:
   
        git push azure master
   
    ![Code pushen naar uw eerste web-app in Azure](./media/app-service-web-get-started-languages/python-git-push.png)    
   
    Als u een van de taalframeworks hebt gebruikt, ziet u andere uitvoer. Dat komt omdat `git push` niet alleen code in Azure plaatst, maar ook implementatietaken in de implementatie-engine activeert. Als er een requirements.txt-bestand aanwezig is in de hoofdmap (opslagplaats) van uw project, worden de vereiste pakketten hersteld door het implementatiescript. 

Dat is alles. De code wordt nu live uitgevoerd in Azure. Navigeer in uw browser naar http://*&lt;appname>*.azurewebsites.net om de code in actie te zien. 

## Updates aanbrengen in uw app
Nu kunt u met Git op elk moment push-acties uitvoeren vanuit het project (opslagplaats) om een actieve site bij te werken. Dit werkt op dezelfde manier als toen u de code voor het eerst implementeerde. Zo hoeft u telkens wanneer u een nieuwe wijziging wilt pushen die u lokaal hebt getest, alleen de volgende opdrachten uit te voeren vanuit de hoofdmap van het project (opslagplaats):

    git add .
    git commit -m "<your_message>"
    git push azure master

## Volgende stappen
[Maak, configureer en implementeer een Django-web-app via Visual Studio in Azure](web-sites-python-ptvs-django-mysql.md). Door deze zelfstudie te volgen, leert u de basisvaardigheden voor het uitvoeren van een Python-web-app in Azure, zoals:

* Een Python-app maken en implementeren via een sjabloon.
* De Python-versie instellen.
* Virtuele omgevingen maken.
* Verbinding maken met een database.

Of doe meer met uw eerste web-app. Bijvoorbeeld:

* Probeer [andere manieren om uw code in Azure te implementeren](web-sites-deploy.md). Als u bijvoorbeeld wilt implementeren vanuit een van uw GitHub-opslagplaatsen, selecteert u in **Implementatieopties** **GitHub** in plaats van **Lokale Git-opslagplaats**.
* Breng uw Azure-app naar een hoger niveau. Verifieer uw gebruikers. Schaal de app op basis van vraag. Stel prestatiewaarschuwingen in. Dit alles met slechts enkele klikken. Zie [Functionaliteit toevoegen aan uw eerste web-app](app-service-web-get-started-2.md).

<!--HONumber=Sep16_HO3-->


