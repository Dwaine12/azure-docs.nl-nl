---
title: 'Azure AD Domain Services: wachtwoordsynchronisatie inschakelen | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/06/2017
ms.author: maheshu
translationtype: Human Translation
ms.sourcegitcommit: 094729399070a64abc1aa05a9f585a0782142cbf
ms.openlocfilehash: d75f6a9db55595ab6b40052b8609709eacf30d4e
ms.lasthandoff: 03/07/2017


---
# <a name="enable-password-synchronization-to-azure-ad-domain-services"></a>Wachtwoordsynchronisatie inschakelen voor Azure AD Domain Services
In de voorgaande taken hebt u Azure AD Domain Services ingeschakeld voor uw Azure AD-tenant. De volgende taak bestaat uit het inschakelen dat referentie-hashes voor NTLM- en Kerberos-verificatie moeten worden gesynchroniseerd met Azure AD Domain Services. Wanneer de synchronisatie van referenties is ingesteld, kunnen gebruikers zich aanmelden bij het beheerde domein middels hun zakelijke referenties.

De vereiste stappen verschillen, afhankelijk van of uw organisatie een Azure AD-tenant in de cloud heeft of kan synchroniseren met uw on-premises directory via Azure AD Connect.

<br>

> [!div class="op_single_selector"]
> * [Azure AD-tenant in de cloud](active-directory-ds-getting-started-password-sync.md)
> * [Gesynchroniseerde Azure AD-tenant](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-aad-domain-services-for-a-cloud-only-azure-ad-tenant"></a>Taak 5: wachtwoordsynchronisatie met AAD Domain Services inschakelen voor een Azure AD-tenant die zich alleen in de cloud bevindt
Azure AD Domain Services vereist referentie-hashes in een indeling die geschikt is voor NTLM- en Kerberos-verificatie om gebruikers in het beheerde domein te kunnen verifiëren. Tenzij u AAD Domain Services voor uw tenant inschakelt, maakt of bewaart Azure AD geen referentie-hashes in de vereiste indeling voor NTLM- of Kerberos-verificatie. Om veiligheidsredenen slaat Azure AD ook geen referenties op in niet-gecodeerde vorm. Azure AD biedt daarom geen manier voor het genereren van deze NTLM- of Kerberos-referentie-hashes op basis van bestaande referenties van gebruikers.

> [!NOTE]
> Als uw organisatie een Azure AD-tenant in de cloud heeft, moeten gebruikers die Azure AD Domain Services willen gebruiken, hun wachtwoord wijzigen.
>
>

Door deze wachtwoordwijziging worden de referentie-hashes die door Azure AD Domain Services zijn vereist voor Kerberos- en NTLM-verificatie, gegenereerd in Azure AD. U kunt wachtwoorden laten verlopen voor alle gebruikers in de tenant die Azure AD Domain Services moeten gebruiken of aan deze gebruikers doorgeven dat ze hun wachtwoord moeten wijzigen.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-azure-ad-tenant"></a>Het genereren van hashes voor NTLM- en Kerberos-referenties inschakelen voor een Azure AD-tenant in de cloud
Hier vindt u instructies over het wijzigen van het wachtwoord die u moet doorgeven aan eindgebruikers:

1. Ga naar de pagina Azure AD-toegangsvenster voor uw organisatie op [http://myapps.microsoft.com](http://myapps.microsoft.com).
2. Selecteer het tabblad **Profiel** op deze pagina.
3. Klik op de tegel **Wachtwoord wijzigen** op deze pagina.

    ![Maak een virtueel netwerk voor Azure AD Domain Services.](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Als u de optie **Wachtwoord wijzigen** niet ziet op de pagina Toegangsvenster, controleert u of uw organisatie [wachtwoordbeheer in Azure AD](../active-directory/active-directory-passwords-getting-started.md) heeft geconfigureerd.
   >
   >
4. Op de pagina **Wachtwoord wijzigen** voert u uw bestaande (oude) wachtwoord in en voert u een nieuw wachtwoord twee keer in. Klik op **Verzenden**.

    ![Maak een virtueel netwerk voor Azure AD Domain Services.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

Wanneer u uw wachtwoord hebt gewijzigd, kunt u al snel het nieuwe wachtwoord gebruiken in Azure AD Domain Services. U kunt zich na een paar minuten (gemiddeld ongeveer 20) met uw gewijzigde wachtwoord aanmelden bij computers die zijn gekoppeld aan het beheerde domein.

<br>

## <a name="related-content"></a>Gerelateerde inhoud
* [Uw eigen wachtwoord bijwerken](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Aan de slag met wachtwoordbeheer in Azure AD](../active-directory/active-directory-passwords-getting-started.md).
* [Wachtwoordsynchronisatie met AAD Domain Services inschakelen voor een gesynchroniseerde Azure AD-tenant](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [Een virtuele Windows-computer toevoegen aan een beheerd domein van Azure AD Domain Services](active-directory-ds-admin-guide-join-windows-vm.md)
* [Een virtuele Red Hat Enterprise Linux-computer toevoegen aan een beheerd domein van Azure AD Domain Services](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

