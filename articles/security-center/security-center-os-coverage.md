---
title: Functies en platformen worden ondersteund door Azure Security Center | Microsoft Docs
description: Dit document bevat een lijst met functies en platformen worden ondersteund door Azure Security Center.
services: security-center
documentationcenter: na
author: rkarlin
manager: MBaldwin
editor: ''
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/28/2018
ms.author: rkarlin
ms.openlocfilehash: 4108355415d1230f98db36a4f83497de2fa848f7
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53185576"
---
# <a name="platforms-and-features-supported-by-azure-security-center"></a>Platforms en functies die worden ondersteund door Azure Security Center

Status van beveiligingsbewaking en aanbevelingen zijn beschikbaar voor virtuele machines (VM's) gemaakt met behulp van zowel de klassieke en Resource Manager-implementatiemodel, en computers.

> [!NOTE]
> Meer informatie over de [klassieke en Resource Manager-implementatiemodel](../azure-classic-rm.md) voor Azure-resources.
>
>

## <a name="supported-platforms"></a>Ondersteunde platforms 

Deze sectie vindt u de platforms waarop de Azure Security Center-agent kan worden uitgevoerd en het verzamelen van gegevens.

### <a name="supported-platforms-for-windows-computers-and-vms"></a>Ondersteunde platforms voor Windows-computers en virtuele machines
De volgende Windows-besturingssystemen worden ondersteund:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016


### <a name="supported-platforms-for-linux-computers-and-vms"></a>Ondersteunde platforms voor Linux-computers en virtuele machines
De volgende Linux-besturingssystemen worden ondersteund:

* Ubuntu-versie 12.04 LTS, 14.04 LTS en 16.04 LTS.
* Debian-versie 6, 7, 8 en 9.
* CentOS versie 5, 6 en 7.
* Red Hat Enterprise Linux (RHEL) versie 5, 6 en 7.
* SUSE Linux Enterprise Server (SLES) versie 11 en 12.
* Oracle Linux-versies 5, 6 en 7.
* Amazon Linux 2012.09 tot 2017.
* OpenSSL 1.1.0 wordt alleen ondersteund op 64-bits x86_64 platforms.

> [!NOTE]
> Gedragsanalyse voor virtuele machine zijn nog niet beschikbaar voor Linux-besturingssystemen.
>
>

## <a name="vms-and-cloud-services"></a>Virtuele machines en Cloudservices
Virtuele machines die worden uitgevoerd in een cloudservice worden ook ondersteund. Alleen cloud services web- en werkrollen-rollen die worden uitgevoerd in productiesites worden bewaakt. Zie voor meer informatie over cloudservices, [overzicht van Azure Cloud Services](../cloud-services/cloud-services-choose-me.md).


## <a name="supported-iaas-features"></a>Ondersteunde IaaS-functies

> [!div class="mx-tableFixed"]
> 

|Server|Windows||Linux||
|----|----|----|----|----|
|Omgeving|Azure|Niet-Azure|Azure|Niet-Azure|
|VMBA dagelijks geconstateerde waarschuwingen|✔|✔|✔ (op ondersteunde versies)|✔|
|Waarschuwingen voor detectie van bedreigingen op basis van netwerk|✔|X|✔|X|
|Windows Defender ATP-integratie *|✔ (op ondersteunde versies)|✔|X|X|
|Ontbrekende patches.|✔|✔|✔|✔|
|Beveiligingsconfiguraties|✔|✔|✔|✔|
|Antimalwareprogramma 's|✔|✔|X|X|
|JIT-VM-toegang|✔|X|✔|X|
|Adaptieve toepassingsbesturingselementen|✔|X|X|X|
|FIM|✔|✔|✔|✔|
|Schijfversleuteling|✔|X|✔|X|
|Implementatie van derden|✔|X|✔|X|
|NSG's|✔|X|✔|X|
|Detectie van bedreigingen fileless|✔|✔|X|X|
|Netwerktoewijzingen|✔|X|✔|X|
|Besturingselementen voor adaptieve netwerk|✔|X|✔|X|

\* Deze functies worden momenteel ondersteund in openbare preview.


## <a name="supported-paas-features"></a>Ondersteunde PaaS-functies 


|Service|Aanbevelingen|Detectie van bedreigingen|
|----|----|----|
|SQL|✔| ✔|
|PostGreSQL *|✔| ✔|
|MySQL *|✔| ✔|
|Azure Blob storage-accounts *|✔| ✔|
|App-services|✔| ✔|
|Cloud Services|✔| X|
|VNets|✔| N.v.t.|
|Subnetten|✔| N.v.t.|
|NIC’s|✔| ✔|
|NSG's|✔| N.v.t.|
|Abonnement|✔| ✔|

\* Deze functies worden momenteel ondersteund in openbare preview. 

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het [plannen en de ontwerpoverwegingen die zich conformeerde aan Azure Security Center kennen](security-center-planning-and-operations-guide.md).
- Meer informatie over [gedragsanalyse voor virtuele machine en crash dump analyse van geheugengebruik in Security Center](security-center-alerts-type.md#virtual-machine-behavioral-analysis).
- Zoek [Veelgestelde vragen over het gebruik van Azure Security Center](security-center-faq.md).
- Zoek [blogberichten over de Azure-beveiliging en naleving](https://blogs.msdn.com/b/azuresecurity/).
