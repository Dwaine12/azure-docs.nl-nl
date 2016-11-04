---
title: Apps publiceren met Azure AD-toepassingsproxy | Microsoft Docs
description: Publiceer on-premises toepassingen naar de cloud met Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''

ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/19/2016
ms.author: kgremban

---
# Toepassingen publiceren met Azure AD-toepassingsproxy
Azure AD-toepassingsproxy helpt u externe werknemers te ondersteunen door on-premises toepassingen te publiceren voor toegang via internet. Inmiddels moet u [toepassingsproxy al hebben ingeschakeld in de klassieke Azure-portal](active-directory-application-proxy-enable.md). Dit artikel beschrijft de stappen voor het publiceren van toepassingen die worden uitgevoerd op uw lokale netwerk en het bieden van beveiligde externe toegang van buiten uw netwerk. Nadat u de stappen in dit artikel hebt uitgevoerd, bent u klaar om de toepassing te configureren met persoonlijke gegevens of beveiligingsvereisten.

> [!NOTE]
> De functie toepassingsproxy is alleen beschikbaar als u een upgrade hebt uitgevoerd naar de Premium- of Basic-editie van Azure Active Directory. Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.
> 
> 

## Een app publiceren met de wizard
1. Meld u als beheerder aan in de [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Ga naar Active Directory en selecteer de directory waarin u toepassingsproxy hebt ingeschakeld.
   
    ![Active Directory - pictogram](./media/active-directory-application-proxy-publish/ad_icon.png)
3. Klik op de tab **Toepassingen** en klik vervolgens op de knop **Toevoegen** onder aan het scherm
   
    ![Toepassing toevoegen](./media/active-directory-application-proxy-publish/aad_appproxy_selectdirectory.png)
4. Selecteer **Een toepassing publiceren die toegankelijk is van buiten uw netwerk**.
   
    ![Een toepassing publiceren die toegankelijk is van buiten uw netwerk](./media/active-directory-application-proxy-publish/aad_appproxy_addapp.png)
5. Geef de volgende informatie over de toepassing op:
   
   * **Naam**: de beschrijvende naam van uw toepassing. Deze naam moet uniek zijn in uw directory.
   * **Interne URL**: het adres dat de connector voor de toepassingsproxy gebruikt om toegang tot de toepassing te verkrijgen vanuit uw particuliere netwerk. U kunt voor het publiceren een specifiek pad opgeven op de back-endserver, terwijl de rest van de server ongepubliceerd blijft. Op deze manier kunt u verschillende sites op dezelfde server publiceren en elke server een eigen naam en toegangsregels geven.
     
     > [!TIP]
     > Als u een pad publiceert, moet u ervoor zorgen dat dit alle benodigde installatiekopieën, scripts en opmaakmodellen voor uw toepassing bevat. Als uw app zich bijvoorbeeld bevindt op het pad https://uwapp/app en gebruikmaakt van installatiekopieën op https://uwapp/media, moet u https://uwapp/ publiceren als het pad.
     > 
     > 
   * **Methode met verificatie vooraf**: de manier waarop gebruikers door de toepassingsproxy worden geverifieerd voordat ze toegang krijgen tot uw toepassing. Kies een van de opties in de vervolgkeuzelijst.
     
     * Azure Active Directory: de gebruikers worden omgeleid met de toepassingsproxy zodat zij zich kunnen aanmelden met Azure AD. Hierbij worden hun machtigingen geverifieerd voor de directory en de toepassing.
     * Passthrough: gebruikers hoeven geen verificatie te doorlopen om toegang te krijgen tot de toepassing.
     
     ![Toepassingseigenschappen](./media/active-directory-application-proxy-publish/aad_appproxy_appproperties.png)  
6. Schakel het selectievakje onder aan het scherm in om de wizard te voltooien. De toepassing is nu gedefinieerd in Azure AD.

## Gebruikers en groepen toewijzen aan de toepassing
U dient uw gebruikers individueel of in groepen toe te wijzen, zodat zij toegang krijgen tot uw gepubliceerde toepassing. (Vergeet niet om ook aan uzelf toegang te verlenen.) Hiervoor moet elke gebruiker beschikken over een licentie voor Azure Basic of hoger. U kunt licenties afzonderlijk of aan groepen toewijzen. Zie [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) (Gebruikers toewijzen aan een toepassing) voor meer informatie. 

Voor apps waarbij verificatie vooraf is vereist, worden hierbij machtigingen verleend voor het gebruik van de app. Voor apps waarbij geen verificatie vooraf is vereist, kunnen gebruikers nog steeds aan de app worden toegewezen zodat deze wordt weergegeven in de lijst met toepassingen, zoals MyApps.

1. Nadat u de wizard App toevoegen hebt voltooid, wordt de pagina Snel starten weergegeven voor uw toepassing. Selecteer **Gebruikers en groepen** om de toegang tot de app te beheren.
   
    ![Toepassingsproxy - gebruikers toewijzen via Snel starten - schermafbeelding](./media/active-directory-application-proxy-publish/aad_appproxy_usersgroups.png)
2. Zoek naar specifieke groepen in uw directory of geef alle gebruikers weer. Klik op het vinkje om de zoekresultaten weer te geven.
   
    ![Zoeken naar groepen of gebruikers - schermafbeelding](./media/active-directory-application-proxy-publish/aad_appproxy_search.png)
3. Selecteer elke gebruiker aan wie of groep waaraan u deze app wilt toewijzen en klik op **Toewijzen**. U wordt gevraagd deze actie te bevestigen.

> [!NOTE]
> Voor apps met geïntegreerde Windows-verificatie kunt u alleen gebruikers en groepen toewijzen die zijn gesynchroniseerd vanuit uw on-premises Active Directory. Gebruikers die zich aanmelden met een Microsoft-account en gasten kunnen niet worden toegewezen aan apps die zijn gepubliceerd met Azure Active Directory-toepassingsproxy. Zorg ervoor dat gebruikers zich aanmelden met de referenties die horen bij hetzelfde domein als de app die u publiceert.
> 
> 

## Uw gepubliceerde toepassing testen
Nadat u uw toepassing hebt gepubliceerd, kunt u deze testen door te navigeren naar de URL die u hebt gepubliceerd. Zorg ervoor dat u toegang toe hebt tot uw toepassing, dat deze correct wordt weergegeven en dat alles werkt zoals verwacht. Als problemen optreden of als een foutbericht wordt weergegeven, raadpleegt u de [gids voor het oplossen van problemen](active-directory-application-proxy-troubleshoot.md).

## Uw toepassing configureren
Op de pagina Configureren kunt u gepubliceerde apps aanpassen of geavanceerde opties instellen. Op deze pagina kunt u uw app aanpassen door de naam te wijzigen of een logo te uploaden. Ook kunt u toegangsregels beheren zoals de methode voor verificatie vooraf of meervoudige verificatie.

![Geavanceerde configuratie](./media/active-directory-application-proxy-publish/aad_appproxy_configure.png)

Nadat u toepassingen hebt gepubliceerd met Azure Active Directory-toepassingsproxy, worden ze weergegeven in de lijst Toepassingen in Azure AD en kunt u ze daar beheren.

Als u de services voor toepassingsproxy uitschakelt nadat u toepassingen hebt gepubliceerd, zijn de toepassingen niet langer toegankelijk van buiten uw particuliere netwerk. Hiermee worden de toepassingen niet verwijderd.

Als u een toepassing wilt bekijken en controleren of deze toegankelijk is, dubbelklikt u op de naam van de toepassing. Als de service voor toepassingsproxy is uitgeschakeld en de toepassing niet beschikbaar is, wordt er boven aan het scherm een waarschuwing weergegeven.

Wilt u een toepassing verwijderen, dan selecteert u de toepassing in de lijst en klikt u op **Verwijderen**.

## Volgende stappen
* [Toepassingen publiceren met uw eigen domeinnaam (Engelstalig artikel)](active-directory-application-proxy-custom-domains.md)
* [Eenmalige aanmelding inschakelen (Engelstalig artikel)](active-directory-application-proxy-sso-using-kcd.md)
* [Voorwaardelijke toegang inschakelen (Engelstalig artikel)](active-directory-application-proxy-conditional-access.md)
* [Working with claims aware applications (Engelstalig)](active-directory-application-proxy-claims-aware-apps.md)

Ga naar het [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/) voor nieuws en updates.

<!--HONumber=Sep16_HO3-->


