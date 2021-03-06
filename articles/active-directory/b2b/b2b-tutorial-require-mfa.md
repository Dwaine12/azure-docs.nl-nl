---
title: 'Zelfstudie: Multi-Factor Authentication afdwingen voor B2B-gastgebruikers van Azure AD'
description: Leer hoe u Multi-Factor Authentication (MFA) kunt afdwingen wanneer u Azure AD B2B gebruikt om samen te werken met externe gebruikers en partnerorganisaties.
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: tutorial
ms.date: 06/25/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 34ca5667b5bf47bec8c48a7e5836b7d51ad08724
ms.sourcegitcommit: 776b450b73db66469cb63130c6cf9696f9152b6a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2018
ms.locfileid: "45986814"
---
# <a name="tutorial-enforce-multi-factor-authentication-for-b2b-guest-users"></a>Zelfstudie: Multi-Factor Authentication afdwingen voor B2B-gastgebruikers

Wanneer u met externe B2B-gastgebruikers samenwerkt, is het raadzaam om uw apps te beschermen met beleid voor Multi-Factor Authentication (MFA). Externe gebruikers hebben dan meer nodig dan alleen een gebruikersnaam en wachtwoord om toegang te krijgen tot uw resources. In Azure Active Directory (Azure AD) kunt u dit realiseren door middel van een voorwaardelijk toegangsbeleid waarbij MFA is vereist voor toegang. MFA-beleid kan worden afgedwongen op het niveau van de tenant, app of individuele gastgebruiker, op dezelfde manier als voor leden van uw eigen organisatie.

Voorbeeld:

![B2B-app waarbij MFA is vereist](media/tutorial-mfa/aad-b2b-mfa-example.png)

1.  Een beheerder of medewerker van bedrijf A nodigt een gastgebruiker uit om een cloud- of on-premises toepassing te gebruiken die zodanig is geconfigureerd dat MFA nodig is voor toegang.
2.  De gastgebruiker meldt zich aan met de identiteit van zijn eigen werk, school of organisatie. 
3.  De gebruiker wordt gevraagd om een MFA-controle in te vullen. 
4.  De gebruiker configureert de MFA voor bedrijf A en kiest hun MFA-optie. De gebruiker krijgt toegang tot de toepassing.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * De aanmeldingservaring testen vóór de MFA-configuratie.
> * Een voorwaardelijk toegangsbeleid maken waarbij MFA is vereist voor toegang tot een cloud-app in uw omgeving. In deze zelfstudie gebruiken we de Microsoft Azure Management-app om het proces toe te lichten.
> * Het What If-hulpprogramma gebruiken om de aanmelding bij MFA te simuleren.
> * Uw beleid voor voorwaardelijke toegang testen.
> * Testgebruiker en beleid opschonen.

Als u nog geen abonnement op Azure hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="prerequisites"></a>Vereisten

Voor het voltooien van het scenario in deze zelfstudie hebt u het volgende nodig:

 - **Toegang tot de Azure AD Premium-editie**, die mogelijkheden voor voorwaardelijk toegangsbeleid bevat. Om MFA af te dwingen, moet u in Azure AD een voorwaardelijk toegangsbeleid maken. Merk op dat MFA-beleid altijd wordt afgedwongen bij uw organisatie, ongeacht of de partner MFA-mogelijkheden heeft. Als u MFA instelt voor uw organisatie, moet u ervoor zorgen dat u over voldoende Azure AD Premium-licenties voor uw gastgebruikers beschikt. 
 - **Een geldig extern e-mailaccount** dat u aan uw tenant-directory als gastgebruiker kunt toevoegen en voor aanmelding kunt gebruiken. Als u niet weet hoe u een gastaccount kunt maken, bekijkt u dan [Een B2B-gastgebruiker toevoegen in de Azure-portal](add-users-administrator.md).

## <a name="create-a-test-guest-user-in-azure-ad"></a>Een test-gastgebruiker toevoegen in Azure AD

1. Meld u als een Azure AD-administrator aan bij de [Azure Portal](https://portal.azure.com/).
2. Selecteer de knop **Azure Active Directory** in het linkerdeelvenster.
3.  Onder **Beheren**, selecteer **Gebruikers**.
4.  Selecteer **Nieuwe gastgebruiker**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-user-3.png)

5.  Onder **Gebruikersnaam**, voer het e-mailadres van de externe gebruiker in. U kunt optioneel een welkomstbericht toevoegen. 

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-user-4.png)

6.  Selecteer **Uitnodigen** voor het automatisch verzenden van de uitnodiging voor de gastgebruiker. Het bericht **Gebruiker is uitgenodigd** verschijnt. 
7.  Nadat u de uitnodiging verzendt, wordt het gebruikersaccount automatisch toegevoegd aan de map als gast.

## <a name="test-the-sign-in-experience-before-mfa-setup"></a>De aanmeldingservaring testen vóór de MFA-configuratie
1.  Meld u aan bij de [Azure-portal](https://portal.azure.com/) met uw gebruikersnaam en wachtwoord.
2.  U merkt nu dat u alleen al met uw aanmeldingsgegevens toegang hebt tot de Azure-portal. Er is geen extra verificatie vereist.
3.  Meld u af.

## <a name="create-a-conditional-access-policy-that-requires-mfa"></a>Een voorwaardelijk toegangsbeleid maken waarbij MFA is vereist
1.  Meld u aan bij de [Azure-portal](https://portal.azure.com/) als hoofdbeheerder, beveiligingsbeheerder of beheerder voor voorwaardelijke toegang.
2.  Selecteer in de Azure-portal **Azure Active Directory**. 
3.  Selecteer op de pagina **Azure Active Directory** in de sectie **Beveiliging** de optie **Voorwaardelijke toegang**.
4.  Selecteer op de pagina **Voorwaardelijke toegang** in de werkbalk bovenaan de optie **Nieuw beleid**.
5.  Typ op de pagina **Nieuw** in het tekstvak **Naam** de tekst **MFA afdwingen voor B2B-toegang tot de portal**.
6.  Selecteer in de sectie **Toewijzingen** de optie **Gebruikers en groepen**.
7.  Kies op de pagina **Gebruikers en groepen** de optie **Gebruikers en groepen selecteren** en selecteer vervolgens **Alle gastgebruikers (preview)**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-policy-6.png)
9.  Selecteer **Done**.
10. Selecteer op de pagina **Nieuw** in de sectie **Toewijzingen** de optie **Cloud-apps**.
11. Kies op de pagina **Cloud-apps** de optie **Apps selecteren** en kies vervolgens **Selecteren**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-policy-10.png)

12. Kies op de pagina **Selecteren** de optie **Microsoft Azure Management** en kies vervolgens **Selecteren**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-policy-11.png)

13. Selecteer op de pagina **Cloud-apps** de optie **Gereed**.
14. Selecteer op de pagina **Nieuw** in de sectie **Toegangscontroles** de optie **Verlenen**.
15. Kies op de pagina **Verlenen** de optie **Toegang verlenen**, selecteer het selectievakje **Multi-factor authentication afdwingen** en kies vervolgens **Selecteren**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-policy-13.png)

16. Selecteer onder **Beleid inschakelen** de optie **Aan**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-policy-14.png)

17. Selecteer **Maken**.

## <a name="use-the-what-if-option-to-simulate-sign-in"></a>De What If-optie gebruiken om de aanmelding te simuleren

1.  Selecteer op de pagina **Voorwaardelijke toegang – Beleid** de optie **What If**. 

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-whatif-1.png)

2.  Selecteer **Gebruiker**, kies uw test-gastgebruiker en kies vervolgens **Selecteren**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-whatif-2.png)

3.  Selecteer **Cloud-apps**.
4.  Kies op de pagina **Cloud-apps** de optie **Apps selecteren**  en klik vervolgens op **Selecteren**. Selecteer **Microsoft Azure Management** in de lijst met toepassingen en klik vervolgens op **Selecteren**. 

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-whatif-3.png)

5.  Selecteer op de pagina **Cloud-apps** de optie **Gereed**.
6.  Selecteer **What If** en controleer of uw nieuwe beleid verschijnt onder **Evaluatieresultaten** op het tabblad **Beleid dat van toepassing is**.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/tutorial-mfa-whatif-4.png)

## <a name="test-your-conditional-access-policy"></a>Uw voorwaardelijke toegangsbeleid testen
1.  Meld u aan bij de [Azure-portal](https://portal.azure.com/) met uw gebruikersnaam en wachtwoord.
2.  Als het goed is, krijgt u nu een aanvraag om extra verificatiemethoden te zien. Houd er rekening mee dat het enige tijd kan duren voordat het beleid van kracht wordt.

    ![Selecteer Azure Active Directory](media/tutorial-mfa/mfa-required.png)
 
3.  Meld u af.

## <a name="clean-up-resources"></a>Resources opschonen
Verwijder de testgebruiker en het testbeleid voor voorwaardelijke toegang, wanneer deze niet langer nodig zijn.
1.  Meld u als een Azure AD-administrator aan bij de [Azure Portal](https://portal.azure.com/).
2.  Selecteer de knop **Azure Active Directory** in het linkerdeelvenster.
3.  Onder **Beheren**, selecteer **Gebruikers**.
4.  Selecteer de testgebruiker en selecteer vervolgens **Gebruiker verwijderen**.
5.  Selecteer de knop **Azure Active Directory** in het linkerdeelvenster.
6.  Selecteer onder **Beveiliging** de optie **Voorwaardelijke toegang**.
7.  Selecteer in de lijst **Beleidsnaam** het contextmenu (…) voor uw testbeleid, en selecteer vervolgens **Verwijderen**. Selecteer **Ja** om te bevestigen.
## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u een voorwaardelijk toegangsbeleid gemaakt dat gastgebruikers voorschrijft om MFA te gebruiken wanneer zij zich aanmelden bij een van uw cloud-apps. Zie voor meer informatie over het toevoegen van gastgebruikers voor samenwerking, [Azure Active Directory B2B-samenwerkingsgebruikers in Azure Portal toevoegen](add-users-administrator.md).
