---
title: 'Zelfstudie: Azure Active Directory-integratie met ThousandEyes | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: b6af7a3322b1a01c1d822df78d827121c19e21e1
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39444399"
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Zelfstudie: Azure Active Directory-integratie met ThousandEyes

In deze zelfstudie leert u hoe u ThousandEyes integreren met Azure Active Directory (Azure AD).

ThousandEyes integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot ThousandEyes heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij ThousandEyes (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts in één centrale locatie - Azure portal beheren

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met ThousandEyes, moet u de volgende items:

- Een Azure AD-abonnement
- Een ThousandEyes eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. ThousandEyes uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-thousandeyes-from-the-gallery"></a>ThousandEyes uit de galerie toe te voegen
Voor het configureren van de integratie van ThousandEyes in Azure AD, moet u ThousandEyes uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen ThousandEyes uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

1. Typ in het zoekvak **ThousandEyes**.

    ![Het maken van een Azure AD-testgebruiker](./media/thousandeyes-tutorial/tutorial_thousandeyes_search.png)

1. Selecteer in het deelvenster resultaten **ThousandEyes**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Het maken van een Azure AD-testgebruiker](./media/thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test Azure AD eenmalige aanmelding met ThousandEyes op basis van een testgebruiker 'Julia steen' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in ThousandEyes is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in ThousandEyes tot stand worden gebracht.

In ThousandEyes, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met ThousandEyes, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD eenmalige aanmelding](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Het maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Het maken van een testgebruiker ThousandEyes](#creating-a-thousandeyes-test-user)**  : als u wilt een equivalent van Britta Simon in ThousandEyes die is gekoppeld aan de Azure AD-weergave van de gebruiker hebben.
1. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#testing-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw toepassing ThousandEyes.

**Voor het configureren van Azure AD eenmalige aanmelding met ThousandEyes, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **ThousandEyes** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.

    ![Eenmalige aanmelding configureren](./media/thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

1. Op de **ThousandEyes domein en URL's** sectie, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    In de **aanmeldings-URL** tekstvak, een URL als: `https://app.thousandeyes.com/login/sso`

1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **Certificate(Base64)** en slaat u het certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/thousandeyes-tutorial/tutorial_thousandeyes_certificate.png)

1. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/thousandeyes-tutorial/tutorial_general_400.png)

1. Op de **ThousandEyes configuratie** sectie, klikt u op **configureren ThousandEyes** openen **aanmelding configureren** venster. Kopiëren de **afmelding-URL, SAML-entiteit-ID en Single Sign-On Service URL voor SAML-** uit de **Naslaggids sectie.**

    ![Eenmalige aanmelding configureren](./media/thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

1. In een ander browservenster aanmelden bij uw **ThousandEyes** bedrijf site als beheerder.

1. Klik in het menu aan de bovenkant op **instellingen**.

    ![Instellingen voor](./media/thousandeyes-tutorial/ic790066.png "instellingen")

1. Klik op **Account**

    ![Account](./media/thousandeyes-tutorial/ic790067.png "Account")

1. Klik op de **beveiliging & verificatie** tabblad.

    ![Beveiliging en verificatie](./media/thousandeyes-tutorial/ic790068.png "beveiligings- en -verificatie")

1. In de **Setup Single Sign-On** sectie, voert u de volgende stappen uit:

    ![Instellen van eenmalige aanmelding](./media/thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")

    a. Selecteer **eenmalige aanmelding inschakelen**.

    b. In **aanmeldings-URL van pagina** tekstvak plakken **Single Sign-On Service URL voor SAML**, die u hebt gekopieerd vanuit Azure portal.

    c. In **afmeldings-URL van pagina** tekstvak plakken **afmelding URL**, die u hebt gekopieerd vanuit Azure portal.

    d. **Identity Provider Issuer** tekstvak plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure portal.

    e. In **verificatiecertificaat**, klikt u op **bestand kiezen**, en upload het certificaat dat u hebt gedownload vanuit Azure portal.

    f. Klik op **Opslaan**.

### <a name="creating-an-azure-ad-test-user"></a>Het maken van een Azure AD-testgebruiker
Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Het maken van een Azure AD-testgebruiker](./media/thousandeyes-tutorial/create_aaduser_01.png) 

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klikt u op **alle gebruikers**.
    
    ![Het maken van een Azure AD-testgebruiker](./media/thousandeyes-tutorial/create_aaduser_02.png) 

1. Om te openen de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.

    ![Het maken van een Azure AD-testgebruiker](./media/thousandeyes-tutorial/create_aaduser_03.png)

1. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Het maken van een Azure AD-testgebruiker](./media/thousandeyes-tutorial/create_aaduser_04.png)

    a. In de **naam** tekstvak, type **BrittaSimon**.

    b. In de **gebruikersnaam** tekstvak, type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.

### <a name="creating-a-thousandeyes-test-user"></a>Het maken van een testgebruiker ThousandEyes

Het doel van deze sectie is het maken van een gebruiker met de naam van Britta Simon in ThousandEyes. ThousandEyes ondersteunt automatisch gebruikers inrichten, dit is standaard ingeschakeld. Meer informatie vindt u [hier](thousandeyes-provisioning-tutorial.md) voor het automatisch inrichten van gebruikers configureren.

**Als u moet de gebruiker handmatig hebt gemaakt, voert u de volgende stappen uit:**

1. Meld u in uw bedrijf ThousandEyes site als beheerder.

1. Klik op **instellingen**.

    ![Instellingen voor](./media/thousandeyes-tutorial/IC790066.png "instellingen")

1. Klik op **Account**.

    ![Account](./media/thousandeyes-tutorial/IC790067.png "Account")

1. Klik op de **Accounts en gebruikers** tabblad.

    ![Accounts en gebruikers](./media/thousandeyes-tutorial/IC790073.png "Accounts en gebruikers")

1. In de **gebruikers toevoegen en Accounts** sectie, voert u de volgende stappen uit:

    ![Gebruikersaccounts toevoegen](./media/thousandeyes-tutorial/IC790074.png "gebruikersaccounts toevoegen")

    a. In **naam** tekstvak typt u de naam van gebruiker, zoals **Britta Simon**.

    b. In **e** tekstvak, typ het e-mailadres van gebruiker, zoals **brittasimon@contoso.com**.

    b. Klik op **nieuwe gebruiker toevoegen aan het Account**.

    > [!NOTE]
    > De houder van Azure Active Directory-account ontvangt een e-mailbericht ook een koppeling om te bevestigen en activeren van het account.

> [!NOTE]
> U kunt elke andere ThousandEyes gebruiker account hulpmiddelen voor het maken of API's geleverd door ThousandEyes voor het inrichten van Azure Active Directory-gebruikersaccounts.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen aan de gebruiker van de test Azure AD

In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen aan ThousandEyes.

![Gebruiker toewijzen][200] 

**Als u wilt Britta Simon aan ThousandEyes toewijst, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **ThousandEyes**.

    ![Eenmalige aanmelding configureren](./media/thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie maakt testen u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Wanneer u op de tegel ThousandEyes in het toegangsvenster, u moet u automatisch aangemeld bij uw toepassing ThousandEyes.

Zie voor meer informatie over het toegangsvenster, [Inleiding tot het toegangsvenster](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)
* [Inrichten van gebruikers configureren](thousandeyes-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/thousandeyes-tutorial/tutorial_general_203.png
