---
title: Systeemvereisten voor Microsoft Azure Data Box Edge | Microsoft Docs
description: Meer informatie over de software en netwerkvereisten voor uw Azure Data Box-Edge
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: article
ms.date: 11/06/2018
ms.author: alkohli
ms.openlocfilehash: 7f03953739eebc63c57b30750e15329f24a00537
ms.sourcegitcommit: da3459aca32dcdbf6a63ae9186d2ad2ca2295893
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/07/2018
ms.locfileid: "51263580"
---
# <a name="azure-data-box-edge-system-requirements-preview"></a>Systeemvereisten voor Azure Data Box Edge (preview)

Dit artikel beschrijft de belangrijke systeemvereisten voor uw Microsoft Azure Data Box Edge-oplossing en de clients die verbinding maken met Azure Data Box Edge. Het is raadzaam dat u de informatie voordat u uw Data Box-Edge implementeren zorgvuldig te controleren. U kunt raadplegen tot deze gegevens zo nodig tijdens de implementatie en het volgende gebruik.

De systeemvereisten voor de Data Box-rand zijn onder andere:

- **Softwarevereisten voor hosts** -beschrijving van de ondersteunde platforms, browsers voor de lokale configuratie-UI, SMB-clients en eventuele bijkomende vereisten voor de clients die toegang het apparaat tot.
- **Netwerkvereisten voor het apparaat** -vindt u informatie over eventuele netwerkvereisten voor de werking van het fysieke apparaat.

> [!IMPORTANT]
> Data Box Edge is in de preview-fase. Lees de [gebruiksvoorwaarden voor de preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voordat u deze oplossing implementeert.

## <a name="supported-os-for-clients-connected-to-device"></a>Ondersteund besturingssysteem voor clients die zijn verbonden met het apparaat

[!INCLUDE [Supported OS for clients connected to device](../../includes/data-box-edge-gateway-supported-client-os.md)]

## <a name="supported-protocols-for-clients-accessing-device"></a>Ondersteunde protocollen voor toegang tot apparaat-clients

[!INCLUDE [Supported protocols for clients accessing device](../../includes/data-box-edge-gateway-supported-client-protocols.md)]

## <a name="supported-storage-accounts"></a>Ondersteunde opslagaccounts

[!INCLUDE [Supported storage accounts](../../includes/data-box-edge-gateway-supported-storage-accounts.md)]

## <a name="supported-storage-types"></a>Ondersteunde opslagtypen

[!INCLUDE [Supported storage types](../../includes/data-box-edge-gateway-supported-storage-types.md)]

## <a name="supported-browsers-for-local-web-ui"></a>Ondersteunde browsers voor de lokale web-UI

[!INCLUDE [Supported browsers for local web UI](../../includes/data-box-edge-gateway-supported-browsers.md)]

## <a name="port-configuration-for-data-box-edge"></a>Poortconfiguratie voor de gegevens in Microsoft Edge

De volgende tabel staan de poorten die moeten worden geopend in uw firewall om toe te staan voor SMB en de cloud en het beheer van verkeer. In deze tabel *in* of *inkomende* verwijst naar de richting van welke binnenkomende client aanvragen toegang tot uw apparaat. *Uit* of *uitgaande* verwijst naar de richting waarin uw gegevens in het Edge-apparaat gegevens extern, na de implementatie, bijvoorbeeld, uitgaand naar het internet verzendt.

[!INCLUDE [Port configuration for device](../../includes/data-box-edge-gateway-port-config.md)]

## <a name="port-configuration-for-iot-edge"></a>Poortconfiguratie voor de IoT Edge

Azure IoT Edge kunt uitgaande communicatie tussen een on-premises Edge-apparaat en Azure-cloud met ondersteunde protocollen van IoT-Hub. Binnenkomende communicatie is alleen vereist voor specifieke scenario's waar Azure IoT Hub moeten zijn om berichten naar de Azure IoT Edge-apparaat (bijvoorbeeld Cloud naar apparaatmessaging).

Gebruik de volgende tabel voor de configuratie van de poort voor de servers die als host fungeert voor Azure IoT Edge-runtime:

| Poort niet. | In- of uitschalen | Poort-bereik | Vereist | Richtlijnen |
|----------|-----------|------------|----------|----------|
| TCP 5671 (AMQP)| Uit       | WAN        | Ja      | Standaard communicatieprotocol voor IoT Edge. Moet zijn geopend als Azure IoT Edge is niet geconfigureerd voor andere ondersteunde protocollen of AMQP het gewenste communicatieprotocol is. <br>5672 voor AMQP wordt niet ondersteund door de IoT Edge. <br>Deze poort blokkeren wanneer Azure IoT Edge maakt gebruik van een andere IoT-Hub ondersteund protocol. |
| TCP 443 (HTTPS)| Uit       | WAN        | Ja      | Uitgaande open voor IoT Edge wordt ingericht. Als u een transparante gateway met leaf-apparaten die methodeaanvragen kunnen worden verzonden hebt. Poort 443 hoeft in dit geval niet te worden geopend voor externe netwerken te verbinden met IoT Hub uw IoT Hub-services via Azure IoT Edge. De binnenkomende regel kan zo worden beperkt tot alleen openen binnenkomend verkeer van het interne netwerk. |
| TCP 5671 (AMQP) | In        |            | Nee       | Binnenkomende verbindingen moeten worden geblokkeerd.|
| TCP 443 (HTTPS) | In        |            | In sommige gevallen opmerkingen bekijken | Binnenkomende verbindingen moeten alleen voor specifieke scenario's worden geopend. Als niet-HTTP-protocollen, zoals AMQP-, MQTT kan niet worden geconfigureerd, kunnen de berichten worden verzonden via WebSockets met behulp van poort 443. |

Voor meer informatie gaat u naar [Firewall en configuratieregels poort voor de implementatie van IoT Edge](https://docs.microsoft.com/azure/iot-edge/troubleshoot).

## <a name="url-patterns-for-firewall-rules"></a>URL-patronen voor firewall-regels

Netwerkbeheerders kunnen vaak geavanceerde firewall-regels op basis van de URL-patronen voor het filteren van de inkomende en uitgaande verkeer configureren. Uw gegevens in het Edge-apparaat en de service, is afhankelijk van andere Microsoft-toepassingen, zoals Azure Service Bus, toegangsbeheer van Azure Active Directory, opslagaccounts en Microsoft Update-servers. De URL-patronen die zijn gekoppeld aan deze toepassingen kunnen worden gebruikt om de firewall-regels configureren. Het is belangrijk om te begrijpen dat de URL-patronen die zijn gekoppeld aan deze toepassingen kunnen wijzigen. Deze wijzigingen vereisen de netwerkbeheerder om te controleren en firewallregels bijwerken voor uw gegevens in Edge als en wanneer dat nodig is.

U wordt aangeraden dat u uw firewall-regels voor uitgaand verkeer, op basis van gegevens in Edge vaste IP-adressen, opneemt in de meeste gevallen hebt ingesteld. Echter, kunt u de onderstaande informatie om in te stellen van geavanceerde firewallregels die nodig zijn om beveiligde omgevingen te maken.

> [!NOTE]
> - Het apparaat (bron) IP-adressen moet altijd worden ingesteld op alle netwerkinterfaces ingeschakeld voor de cloud.
> - De IP-adressen moet worden ingesteld op bestemming [Azure datacenter IP-adresbereiken](https://www.microsoft.com/download/confirmation.aspx?id=41653).

|     URL-patroon                                                                                                                                                                                                                                                                                                                                                                                                                                       |     Onderdeel of functionaliteit                                                                             |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
|    https://*.databoxedge.azure.com/*<br>https://*.servicebus.windows.net/*<br>https://login.windows.net                                                                                                                                                                                                                                                                                                        |    Azure Data Box-Edge-service<br>Azure Service Bus<br>Verificatieservice    |
|    http://*.Backup.windowsazure.com                                                                                                                                                                                                                                                                                                                                                                                                                   |    Activering van apparaat                                                                                    |
|    http://crl.microsoft.com/pki/*   http://www.microsoft.com/pki/*                                                                                                                                                                                                                                                                                                                                                                                    |    Het intrekken van certificaten                                                                               |
|    https://*.core.windows.net/* https://*. data.microsoft.com http://*. msftncsi.com                                                                                                                                                                                                                                                                                                                                                                |    Azure storage-accounts en bewaking                                                                |
|    http://windowsupdate.microsoft.com<br>http://*. windowsupdate.microsoft.com<br>https://*. windowsupdate.microsoft.com<br>http://*. update.microsoft.com<br>https://*. update.microsoft.com<br>http://*. windowsupdate.com<br>http://download.microsoft.com<br>http://*. download.windowsupdate.com<br>http://wustat.windows.com<br>http://ntservicepack.microsoft.com<br>http://*. ws.microsoft.com<br>https://*. ws.microsoft.com<br>http://*.MP.Microsoft.com        |    Microsoft Update-servers                                                                             |
|    http://*.Deploy.akamaitechnologies.com                                                                                                                                                                                                                                                                                                                                                                                                             |    Akamai CDN                                                                                           |
|    https://*.partners.extranet.microsoft.com/*                                                                                                                                                                                                                                                                                                                                                                                                        |    Ondersteuningspakket                                                                                      |
|    http://*.Data.Microsoft.com                                                                                                                                                                                                                                                                                                                                                                                                                        |    Telemetrieservice in Windows, Zie de update voor de gebruikerservaring en diagnostische telemetrie      |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                         |

## <a name="internet-bandwidth"></a>Internet-bandbreedte

[!INCLUDE [Internet bandwidth](../../includes/data-box-edge-gateway-internet-bandwidth.md)]

## <a name="next-step"></a>Volgende stap

* [Uw Azure Data Box-Edge implementeren](data-box-Edge-deploy-prep.md)
