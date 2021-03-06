---
title: Een Windows IoT Core-apparaat verbinden met uw Azure IoT Central-toepassing | Microsoft Docs
description: Leer hoe u een apparaat MXChip IoT DevKit verbinden met uw Azure IoT Central-toepassing als een apparaat-ontwikkelaar.
author: miriambrus
ms.author: miriamb
ms.date: 04/09/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 7d593a992d0ff189d23185b3422dee86a55308d1
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53309447"
---
# <a name="connect-a-windows-iot-core-device-to-your-azure-iot-central-application"></a>Een Windows IoT Core-apparaat verbinden met uw Azure IoT Central-toepassing

Dit artikel wordt beschreven hoe u als ontwikkelaar apparaat een Windows IoT Core-apparaat verbinden met uw Microsoft Azure IoT Central-toepassing.

## <a name="before-you-begin"></a>Voordat u begint

U hebt het volgende nodig om de stappen in dit artikel uit te voeren:

1. Een Azure IoT Central-toepassing gemaakt op basis van de **voorbeeld Devkits** toepassingssjabloon. Zie voor meer informatie de [snelstart over het maken van een toepassing](quick-deploy-iot-central.md).
2. Een apparaat met het besturingssysteem Windows 10 IoT Core. Voor dit scenario gebruiken we een Raspberry Pi.


## <a name="sample-devkits-application"></a>**Voorbeeld van een Devkits** toepassing

Een toepassing gemaakt op basis van de **voorbeeld Devkits** toepassingssjabloon bevat een **Windows IoT Core** apparaat sjabloon met de volgende kenmerken: 

- Telemetrie waarin de metingen voor het apparaat **vochtigheid**, **temperatuur** en **druk te verlichten**. 
- Instellingen van **ventilatorsnelheid**.
- Eigenschappen van de apparaateigenschappen **die nummer** en **locatie** eigenschap in de cloud.


Raadpleeg voor volledige informatie van de configuratie van de sjabloon apparaat [details van de sjabloon Windows IoT Core-apparaat](howto-connect-windowsiotcore.md#windows-iot-core-device-template-details)

## <a name="add-a-real-device"></a>Echt apparaat toevoegen

Voeg in uw Azure IoT Central-toepassing een echt apparaat uit de **Windows IoT Core** apparaat sjabloon en maak een notitie van de verbindingsreeks van het apparaat. Zie voor meer informatie, [een echt apparaat toevoegen aan uw Azure IoT Central toepassing](tutorial-add-device.md).

### <a name="prepare-the-windows-iot-core-device"></a>Bereid het apparaat Windows IoT Core

Voor het instellen van een apparaat met Windows IoT Core Volg de stapsgewijze handleiding bij [instellen van een apparaat met Windows IoT Core](https://github.com/Azure/iot-central-firmware/tree/master/WindowsIoT#setup-a-physical-device).

### <a name="add-a-real-device"></a>Echt apparaat toevoegen

Voeg in uw Azure IoT Central-toepassing een echt apparaat uit de **Windows IoT Core** apparaat sjabloon en maak een notitie van de verbindingsgegevens van het apparaat (**bereik-ID, apparaat-ID, primaire sleutel**). Zie voor meer informatie, [een echt apparaat toevoegen aan uw Azure IoT Central toepassing](tutorial-add-device.md).

 > [!NOTE]
   > Azure IoT Central is overgeschakeld naar het gebruik van Azure IoT Hub Device Provisioning service (DPS) voor alle apparaatverbindingen, volgt u deze instrustions naar [de apparaat-verbindingsreeks ophalen](concepts-connectivity.md#getting-device-connection-string) en Ga door met de rest van de zelfstudie.

## <a name="prepare-the-windows-10-iot-core-device"></a>Het Windows 10 IoT Core-apparaat voorbereiden

### <a name="what-youll-need"></a>Wat u nodig hebt

Als u een fysiek apparaat met Windows 10 IoT Core instelt, moet u eerst een apparaat met Windows 10 IoT Core hebben. Meer informatie over het instellen van een apparaat met Windows 10 IoT Core [hier](https://docs.microsoft.com/windows/iot-core/tutorials/quickstarter/devicesetup).

U moet ook een clienttoepassing die met Azure IoT Central communiceren kan. U kunt uw eigen aangepaste toepassing met behulp van de Azure SDK bouwen en implementeren op uw apparaat met behulp van Visual Studio, maar u kunt downloaden een [vooraf gemaakte voorbeeld](https://developer.microsoft.com/windows/iot/samples) gewoon implementeren en uitvoeren op het apparaat. 

### <a name="deploying-the-sample-client-application"></a>De voorbeeldtoepassing van de client implementeren

De clienttoepassing uit de vorige stap op uw Windows 10 IoT-apparaat om te kunnen voorbereiden implementeren:

**Zorg ervoor dat de verbindingsreeks is opgeslagen op het apparaat voor de clienttoepassing te gebruiken**
* Sla de verbindingsreeks in een tekstbestand met de naam connection.string.iothub op het bureaublad.
* Kopieer het tekstbestand naar de map document van het apparaat: `[device-IP-address]\C$\Data\Users\DefaultAccount\Documents\connection.string.iothub`

Zodra u dat hebt gedaan, moet u opent de [Windows Device Portal](https://docs.microsoft.com/windows/iot-core/manage-your-device/deviceportal) door te typen in http://[device-IP-address]:8080 in elke browser.

Vanaf daar en, zoals weergegeven in de als hieronder, moet u doen:
1. Vouw het knooppunt 'Apps' aan de linkerkant.
2. Klik op 'voorbeelden snel uitvoeren'.
3. Klik op 'Azure IoT Hub-Client'.
4. Klik op 'Implementeren en uitvoeren'.

![Afbeelding van Azure IoT Hub-Client op Windows Device Portal](./media/howto-connect-windowsiotcore/iothubapp.gif)

Als dat lukt, wordt de toepassing starten op het apparaat en wordt er als volgt uit:

![Schermopname van Azure IoT Hub-Client-app](./media/howto-connect-windowsiotcore/IoTHubForegroundClientScreenshot.png)

In Azure IoT Central, kunt u zien hoe de code die wordt uitgevoerd op de Raspberry Pi communiceert met de toepassing:

* Op de **metingen** pagina voor uw echte apparaten, kunt u de telemetrie bekijken.
* Op de **eigenschappen** pagina, ziet u de waarde van het gerapporteerde aantal Die eigenschap.
* Op de **instellingen** pagina, kunt u verschillende instellingen op de Raspberry Pi zoals spanning- en fan-snelheid.

## <a name="download-the-source-code"></a>De broncode downloaden

Als u wilt verkennen en te wijzigen van de broncode voor de clienttoepassing, kunt u deze downloaden vanuit GitHub [hier](https://github.com/Microsoft/Windows-iotcore-samples/tree/develop/Samples/Azure/IoTHubClients). Als u van plan bent om te wijzigen van de code, moet u deze instructies in het Leesmij-bestand [hier](https://github.com/Microsoft/Windows-iotcore-samples) voor uw besturingssysteem voor desktopcomputers.

> [!NOTE]
> Als **git** is niet geïnstalleerd in uw ontwikkelingsomgeving, u kunt dit ook downloaden via [ https://git-scm.com/download ](https://git-scm.com/download).

## <a name="windows-iot-core-device-template-details"></a>Details van de sjabloon Windows IoT Core-apparaat

Een toepassing gemaakt op basis van de **voorbeeld Devkits** toepassingssjabloon bevat een **Windows IoT Core** apparaat sjabloon met de volgende kenmerken:

### <a name="telemetry-measurements"></a>Telemetrie-metingen

| Veldnaam     | Eenheden  | Minimum | Maximum | Aantal decimalen |
| -------------- | ------ | ------- | ------- | -------------- |
| vochtigheid       | %      | 0       | 100     | 0              |
| TEMP           | ° C     | -40     | 120     | 0              |
| pressure       | hPa    | 260     | 1260    | 0              |

### <a name="settings"></a>Instellingen

Numerieke instellingen

| Weergavenaam | Veldnaam | Eenheden | Aantal decimalen | Minimum | Maximum | Oorspronkelijk |
| ------------ | ---------- | ----- | -------------- | ------- | ------- | ------- |
| Snelheid van ventilator    | fanSpeed   | RPM   | 0              | 0       | 1000    | 0       |


### <a name="properties"></a>Properties

| Type            | Weergavenaam | Veldnaam | Gegevenstype |
| --------------- | ------------ | ---------- | --------- |
| Apparaateigenschappen | Aantal die   | dieNumber  | getal    |
| Tekst            | Locatie     | location   | N/A       |
