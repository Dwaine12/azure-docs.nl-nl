---
title: 'Zelfstudie: Azure Active Directory-integratie met samenloop SAML SSO door Microsoft | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en samenloop SAML SSO door Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/05/2018
ms.author: jeedes
ms.openlocfilehash: 2e254faae0289cd00c7e66d430ec3148fccb364a
ms.sourcegitcommit: 02ce0fc22a71796f08a9aa20c76e2fa40eb2f10a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/08/2018
ms.locfileid: "51288149"
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>Zelfstudie: Azure Active Directory-integratie met samenloop SAML SSO door Microsoft

In deze zelfstudie leert u hoe u samenloop SAML SSO door Microsoft integreren met Azure Active Directory (Azure AD).

Samenloop SAML SSO door Microsoft integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot samenloop SAML SSO door Microsoft heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij samenloop SAML SSO door Microsoft (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts in één centrale locatie - Azure portal beheren.

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md)

## <a name="description"></a>Beschrijving:

Uw Microsoft Azure Active Directory-account met Atlassian samenloop server gebruiken voor eenmalige aanmelding inschakelen. Op deze manier alle gebruikers in uw organisatie kunnen de Azure AD-referenties aan te melden bij de toepassing samenloop gebruiken. Deze invoegtoepassing maakt gebruik van SAML 2.0 voor Federatie.

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met samenloop SAML SSO door Microsoft, moet u de volgende items:

- Een Azure AD-abonnement
- De servertoepassing samenloop geïnstalleerd op een Windows 64-bits-server (on-premises of in de cloud-IaaS-infrastructuur)
- Samenloop-server is HTTPS-functionaliteit
- Houd er rekening mee dat de ondersteunde versies samenloop-invoegtoepassing worden vermeld in onderstaande sectie.
- Samenloop server bereikbaar is op internet met name naar Azure AD-aanmeldingspagina voor verificatie en moet kunnen ontvangen van het token uit Azure AD
- Referenties van een beheerder worden ingesteld in samenloop
- WebSudo is uitgeschakeld in samenloop
- Testgebruiker gemaakt in de servertoepassing samenloop

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving van samenloop. De integratie in ontwikkelings- of faseringsomgeving van de toepassing eerst te testen en gebruik vervolgens de productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-confluence"></a>Ondersteunde versies van samenloop

Vanaf nu de volgende versies van samenloop worden ondersteund:

- Samenloop: 5.0 naar versie 5.10
- Samenloop: 6.0.1
- Samenloop: 6.1.1
- Samenloop: 6.2.1
- Samenloop: 6.3.4
- Samenloop: 6.4.0
- Samenloop: 6.5.0
- Samenloop: 6.6.2
- Samenloop: 6.7.0
- Samenloop: 6.8.1
- Samenloop: 6.9.0
- Samenloop: 6.10.0
- Samenloop: 6.11.0
- Samenloop: 6.12.0

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Samenloop SAML SSO door Microsoft uit de galerie toe te voegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a>Samenloop SAML SSO door Microsoft uit de galerie toe te voegen

Voor het configureren van de integratie van samenloop SAML SSO door Microsoft in Azure AD, moet u samenloop SAML SSO door Microsoft uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen samenloop SAML SSO door Microsoft uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]

3. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop nieuwe toepassing][3]

4. Typ in het zoekvak **samenloop SAML SSO door Microsoft**, selecteer **samenloop SAML SSO door Microsoft** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Samenloop SAML SSO door Microsoft in de lijst met resultaten](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en Azure AD eenmalige aanmelding testen

In deze sectie maakt u configureert en test Azure AD eenmalige aanmelding met samenloop SAML SSO door Microsoft op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in de SAML SSO-samenloop door Microsoft is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in samenloop SAML SSO door Microsoft tot stand worden gebracht.

Om te configureren en testen van Azure AD eenmalige aanmelding met samenloop SAML SSO door Microsoft, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD eenmalige aanmelding](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Het maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Het maken van samenloop SAML SSO door Microsoft testgebruiker](#creating-confluence-saml-sso-by-microsoft-test-user)**  : als u wilt een equivalent van Britta Simon in samenloop SAML SSO door Microsoft en die is gekoppeld aan de Azure AD-weergave van de gebruiker hebben.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Eenmalige aanmelding testen](#testing-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw samenloop SAML SSO door toepassing van Microsoft.

**Voor het configureren van Azure AD eenmalige aanmelding met samenloop SAML SSO door Microsoft, kunt u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **samenloop SAML SSO door Microsoft** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op de **selecteert u een methode voor eenmalige aanmelding** dialoogvenster, klikt u op **Selecteer** voor **SAML** modus voor eenmalige aanmelding inschakelen.

    ![Eenmalige aanmelding configureren](common/tutorial_general_301.png)

3. Op de **instellen van eenmalige aanmelding met SAML** pagina, klikt u op **bewerken** pictogram openen **SAML-basisconfiguratie** dialoogvenster.

    ![Eenmalige aanmelding configureren](common/editconfigure.png)

4. Op de **SAML-basisconfiguratie** sectie, voert u de volgende stappen uit:

    ![Samenloop SAML SSO door Microsoft Domain en URL's één aanmeldings-informatie](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    a. In de **aanmeldings-URL** tekstvak, een URL met behulp van het volgende patroon: `https://<domain:port>/plugins/servlet/saml/auth`

    b. In de **id** tekstvak, een URL met behulp van het volgende patroon: `https://<domain:port>/`

    c. In de **antwoord-URL** tekstvak, een URL met behulp van het volgende patroon: `https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE]
    > Deze waarden zijn niet echt. Werk deze waarden met de werkelijke-id, de antwoord-URL en aanmeldings-URL. Poort is optioneel als een URL met de naam is. Deze waarden zijn ontvangen tijdens de configuratie van samenloop-invoegtoepassing, die later in de zelfstudie wordt uitgelegd.

5. Op de **SAML-handtekeningcertificaat** pagina, in de **SAML-handtekeningcertificaat** sectie, klikt u op de knop kopiëren om te kopiëren **App-Url voor federatieve metagegevens** en plak deze in Kladblok.

    ![De downloadkoppeling certificaat](./media/confluencemicrosoft-tutorial/tutorial_metadataurl.png)

6. In een ander browservenster aanmelden bij uw samenloop exemplaar als beheerder.

7. Beweeg de muisaanwijzer op het tandwiel en klikt u op de **invoegtoepassingen**.

    ![Eenmalige aanmelding configureren](./media/confluencemicrosoft-tutorial/addon1.png)

8. Download de invoegtoepassing van [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56503). Handmatig uploaden van de invoegtoepassing die is opgegeven met behulp van Microsoft **invoegtoepassing uploaden** menu. Het downloaden van de invoegtoepassing wordt gedekt onder [Microsoft-serviceovereenkomst](https://www.microsoft.com/servicesagreement/).

    ![Eenmalige aanmelding configureren](./media/confluencemicrosoft-tutorial/addon12.png)

9. Zodra de invoegtoepassing is geïnstalleerd, wordt deze weergegeven **gebruiker geïnstalleerd** invoegtoepassingen-sectie van **beheren invoegtoepassing** sectie. Klik op **configureren** het configureren van de nieuwe-invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/confluencemicrosoft-tutorial/addon13.png)

10. Voert u de volgende stappen uit op de configuratiepagina:

    ![Eenmalige aanmelding configureren](./media/confluencemicrosoft-tutorial/addon52.png)

    > [!TIP]
    > Zorg ervoor dat er slechts één certificaat toegewezen op basis van de app, zodat er geen fout is opgetreden bij het oplossen van de metagegevens. Als er meerdere certificaten, haalt de beheerder een fout opgetreden bij het oplossen van de metagegevens.

    a. In de **metagegevens-URL** tekstvak plakken **App-Url voor federatieve metagegevens** waarde die u hebt gekopieerd uit de Azure portal en klik op de **oplossen** knop. Leest de IdP metagegevens-URL en wordt alle informatie van de velden ingevuld.

    b. Kopiëren de **-id, de antwoord-URL en de aanmeldings-URL** waarden en plak deze in **-id, de antwoord-URL en de aanmeldings-URL** respectievelijk in tekstvakken **samenloop SAML SSO door Microsoft Domain en URL's**  sectie in Azure portal.

    c. In **aanmeldingsnaam van de knop** Typ de naam van uw organisatie wil dat de gebruikers om te zien op het aanmeldingsscherm knop.

    d. In **SAML-ID gebruikerslocaties**, selecteert u **gebruikers-ID is in de NameIdentifier-element van het onderwerp overzicht** of **gebruikers-ID is in een kenmerkelement**.  Deze ID is de samenloop gebruikers-id. Als de gebruikers-id niet overeen komt, klikt u vervolgens systeem niet toestaan dat gebruikers zich aanmelden. 

    > [!Note]
    > De standaardlocatie voor de SAML-gebruikers-ID is naam-id. U kunt dit wijzigen in een kenmerk-optie en geef de juiste naam.
    
    e. Als u selecteert **gebruikers-ID is in een kenmerkelement** optie, klikt u vervolgens in **kenmerknaam** tekstvak typt u de naam van het kenmerk waar gebruikers-Id wordt verwacht. 

    f. Als u van de federatief domein (zoals ADFS enz.) met Azure AD gebruikmaakt, klikt u op de **inschakelen start Realm detectie** optie en configureer de **domeinnaam**.
    
    g. In **domeinnaam** typt u de domeinnaam hier in het geval van de aanmelding op basis van een AD FS.

    h. Controleer **eenmalige aanmelding inschakelen om** als u Meld u wilt af bij Azure AD wanneer een gebruiker zich afmeldt van samenloop. 

    i. Klik op **opslaan** knop de instellingen op te slaan.

    > [!NOTE]
    > Voor meer informatie over de installatie en probleemoplossing, gaat u naar [MS samenloop SSO-Connector-beheerdershandleiding](../ms-confluence-jira-plugin-adminguide.md) en er is ook [Veelgestelde vragen over](../ms-confluence-jira-plugin-faq.md) voor uw hulp

### <a name="creating-an-azure-ad-test-user"></a>Het maken van een Azure AD-testgebruiker

Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

1. Selecteer in de Azure portal, in het linkerdeelvenster **Azure Active Directory**, selecteer **gebruikers**, en selecteer vervolgens **alle gebruikers**.

    ![Azure AD-gebruiker maken][100]

2. Selecteer **nieuwe gebruiker** aan de bovenkant van het scherm.

    ![Het maken van een Azure AD-testgebruiker](common/create_aaduser_01.png) 

3. In de eigenschappen van de gebruiker de volgende stappen uitvoeren.

    ![Het maken van een Azure AD-testgebruiker](common/create_aaduser_02.png)

    a. In de **naam** veld **BrittaSimon**.
  
    b. In de **gebruikersnaam** veld, typt u **brittasimon@yourcompanydomain.extension**  
    Bijvoorbeeld: BrittaSimon@contoso.com

    c. Selecteer **eigenschappen**, selecteer de **Show wachtwoord** selectievakje en noteer de waarde die wordt weergegeven in het wachtwoord.

    d. Selecteer **Maken**.

### <a name="creating-confluence-saml-sso-by-microsoft-test-user"></a>Samenloop SAML SSO door Microsoft testgebruiker maken

Om Azure AD-gebruikers zich aanmelden met samenloop on-premises server, moeten deze in samenloop SAML SSO worden ingericht door Microsoft. Voor samenloop SAML SSO door Microsoft is het inrichten van een handmatige taak.

**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**

1. Meld u aan bij uw samenloop on-premises-server aan als beheerder.

2. Beweeg de muisaanwijzer op het tandwiel en klikt u op de **Gebruikersbeheer**.

    ![Werknemer toevoegen](./media/confluencemicrosoft-tutorial/user1.png) 

3. Klik onder de sectie gebruikers op **gebruikers toevoegen** tabblad. Op de **toevoegen van een gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Werknemer toevoegen](./media/confluencemicrosoft-tutorial/user2.png) 

    a. In de **gebruikersnaam** tekstvak typt u het e-mailadres van gebruiker, zoals Britta Simon.

    b. In de **volledige naam** tekstvak typt u de volledige naam van gebruiker, zoals Britta Simon.

    c. In de **e** tekstvak, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.

    d. In de **wachtwoord** tekstvak typt u het wachtwoord voor Britta Simon.

    e. Klik op **wachtwoord bevestigen** het wachtwoord opnieuw invoeren.

    f. Klik op **toevoegen** knop.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen aan de gebruiker van de test Azure AD

In deze sectie schakelt u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen aan samenloop SAML SSO door Microsoft.

1. Selecteer in de Azure portal, **bedrijfstoepassingen**, selecteer **alle toepassingen**.

    ![Gebruiker toewijzen][201]

2. Selecteer in de lijst met toepassingen, **samenloop SAML SSO door Microsoft**.

    ![Eenmalige aanmelding configureren](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png)

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. In de **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst met gebruikers, en klik op de **Selecteer** knop aan de onderkant van het scherm.

6. In de **toevoegen toewijzing** dialoogvenster Selecteer de **toewijzen** knop.

### <a name="testing-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie maakt testen u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Wanneer u op de samenloop SAML SSO door Microsoft-tegel in het toegangsvenster, u moet u automatisch aangemeld bij uw samenloop SAML SSO door toepassing van Microsoft.
Zie voor meer informatie over het toegangsvenster, [Inleiding tot het toegangsvenster](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)

<!--Image references-->

[1]: common/tutorial_general_01.png
[2]: common/tutorial_general_02.png
[3]: common/tutorial_general_03.png
[4]: common/tutorial_general_04.png

[100]: common/tutorial_general_100.png

[201]: common/tutorial_general_201.png
[202]: common/tutorial_general_202.png
[203]: common/tutorial_general_203.png
