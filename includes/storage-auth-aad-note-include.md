---
title: bestand opnemen
description: bestand opnemen
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 10/09/2018
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: 2d641287bcf095f13719667a91b7f61295309b5d
ms.sourcegitcommit: 707bb4016e365723bc4ce59f32f3713edd387b39
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/19/2018
ms.locfileid: "49430354"
---
> [!NOTE]
> - De Preview-versie van Azure AD-verificatie voor blobs en wachtrijen is bedoeld voor gebruik in alleen niet-productieomgevingen. Productie service level agreements (Sla's) zijn momenteel niet beschikbaar. Als Azure AD-verificatie wordt nog niet ondersteund voor uw scenario, echter ook doorgaan met de gedeelde sleutel autorisatie of SAS-tokens in uw toepassingen.
>
> - Tijdens de Preview-versie duurt RBAC-roltoewijzingen tot vijf minuten worden doorgegeven.
>
> - U moet HTTPS gebruiken om te verifiëren met Azure AD bij het aanroepen van blob- en wachtrijservices bewerkingen.
>
> - De Azure-portal biedt nu ondersteuning voor het gebruik van Azure AD-referenties om te lezen en schrijven van blob-gegevens als onderdeel van de preview-versie.
> 
> - De Azure-portal ondersteunt momenteel geen Azure AD-referenties gebruiken om te lezen en schrijven van wachtrijgegevens. Wachtrijgegevens wordt benaderd via de sleutels van uw storage-account.
>
> - [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) gebruikt momenteel de sleutel van uw opslagaccount voor het openen van blob- en wachtrijservices.
>
> - Azure Files biedt ondersteuning voor verificatie met Azure AD via SMB voor domein-VM's alleen (preview). Zie voor meer informatie over het gebruik van Azure AD voor Azure Files via SMB, [overzicht van Azure Active Directory-verificatie voor Azure Files (preview) via SMB](../articles/storage/files/storage-files-active-directory-overview.md).



