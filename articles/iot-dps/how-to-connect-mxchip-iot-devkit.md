---
title: Het gebruik van automatische inrichting van Azure IoT Hub Device Provisioning Service voor het registreren van de MXChip IoT DevKit met IoT Hub | Microsoft Docs
description: Het gebruik van automatische inrichting van Azure IoT Hub Device Provisioning Service voor het registreren van de MXChip IoT DevKit met IoT Hub.
author: liydu
ms.author: liydu
ms.date: 04/04/2018
ms.topic: conceptual
ms.service: iot-dps
services: iot-dps
manager: jeffya
ms.openlocfilehash: d8912a5da8c4df2069d8bc53454748b5fb3d5c39
ms.sourcegitcommit: 3f8f973f095f6f878aa3e2383db0d296365a4b18
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2018
ms.locfileid: "42054723"
---
# <a name="use-azure-iot-hub-device-provisioning-service-auto-provisioning-to-register-the-mxchip-iot-devkit-with-iot-hub"></a>Gebruik automatische inrichting van Azure IoT Hub Device Provisioning Service voor het registreren van de MXChip IoT DevKit met IoT Hub

In dit artikel wordt beschreven hoe u Azure IoT Hub Device Provisioning Service [automatische inrichting](concepts-auto-provisioning.md), de MXChip IoT DevKit registreren bij Azure IoT Hub. In deze zelfstudie leert u het volgende:

* De globale-eindpunt van de Device Provisioning-service configureren op een apparaat.
* Gebruik een unieke apparaat-geheim (ud's) voor het genereren van een X.509-certificaat.
* Een afzonderlijk apparaat inschrijven.
* Controleer of dat het apparaat is geregistreerd.

De [MXChip IoT DevKit](https://aka.ms/iot-devkit) is een alles-in-een Arduino-compatibel bord met uitgebreide randapparatuur en sensoren. U kunt voor het ontwikkelen met behulp van de [Visual Studio Code-extensie voor Arduino](https://aka.ms/arduino). De DevKit wordt geleverd met een groeiend [projecten catalogus](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) om u te helpen uw prototype Internet of Things (IoT)-oplossingen die van Azure-services profiteren.

## <a name="before-you-begin"></a>Voordat u begint

Als u wilt de stappen in deze zelfstudie hebt voltooid, moet u eerst de volgende taken uitvoeren:

* Voorbereiden van uw DevKit met de volgende stappen in [IoT DevKit AZ3166 verbinding maken met Azure IoT Hub in de cloud](/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started).
* Een upgrade uitvoeren naar de meest recente firmware (1.3.0 of hoger) met de [firmware-Update DevKit](https://microsoft.github.io/azure-iot-developer-kit/docs/firmware-upgrading/) zelfstudie.
* Maken en koppelen van een IoT-Hub met een exemplaar van Device Provisioning service met de volgende stappen in [instellen van de IoT Hub Device Provisioning Service met de Azure-portal](/azure/iot-dps/quick-setup-auto-provision).

## <a name="build-and-deploy-auto-provisioning-registration-software-to-the-device"></a>Bouwen en implementeren van software voor apparaatregistratie automatische inrichting op het apparaat

De DevKit verbinden met de op Device Provisioning service-exemplaar dat u hebt gemaakt:

1. Selecteer in de Azure portal, de **overzicht** deelvenster van de Device Provisioning service en noteert u de **Global device endpoint** en **ID-bereik** waarden.
  ![Device Provisioning Service Global Endpoint en ID-bereik](./media/how-to-connect-mxchip-iot-devkit/dps-global-endpoint.png)

2. Zorg ervoor dat u hebt `git` op uw computer geïnstalleerd en dat deze wordt toegevoegd aan de omgevingsvariabelen die toegankelijk zijn voor het opdrachtvenster. Zie [Git-clienttools van Software Freedom](https://git-scm.com/download/) naar de meest recente versie hebt geïnstalleerd.

3. Open een opdrachtprompt. Kloon de GitHub-opslagplaats voor de Device Provisioning service-voorbeeldcode:
  ```bash
  git clone https://github.com/DevKitExamples/DevKitDPS.git
  ```

4. Open Visual Studio Code, de DevKit verbinden met uw computer en open vervolgens de map met de code die u hebt gekloond.

5. Open **DevKitDPS.ino**. Zoeken en vervangen `[Global Device Endpoint]` en `[ID Scope]` door de waarden die u zojuist hebt genoteerd.
  ![Device Provisioning Service-eindpunt](./media/how-to-connect-mxchip-iot-devkit/endpoint.png) kunt u de **registratie-id** leeg. De toepassing genereert een voor u op basis van de MAC-adres en firmware-versie. Als u aanpassen van de registratie-ID wilt, moet u gebruik alleen alfanumerieke tekens, kleine letters en afbreekstreepjes combinaties met een maximum van 128 tekens. Zie voor meer informatie, [apparaatregistraties beheren met Azure portal](https://docs.microsoft.com/azure/iot-dps/how-to-manage-enrollments).

6. Snel openen in VS Code gebruiken (Windows: `Ctrl+P`, Mac OS: `Cmd+P`) en het type *taak van apparaat-upload* bouwen en de code uploaden naar de DevKit.

7. Het uitvoervenster laat zien of de taak voltooid is.

## <a name="save-a-unique-device-secret-on-an-stsafe-security-chip"></a>Een unieke apparaat-geheim opslaan op een STSAFE security-chip

Automatische inrichting kan worden geconfigureerd op een apparaat, gebaseerd op van het apparaat [attestation-mechanisme](concepts-security.md#attestation-mechanism). Maakt gebruik van de MXChip IoT DevKit de [apparaat Identity Composition Engine](https://trustedcomputinggroup.org/wp-content/uploads/Foundational-Trust-for-IOT-and-Resource-Constrained-Devices.pdf) uit de [Trusted Computing Group](https://trustedcomputinggroup.org). Een *unieke apparaat-geheim* (ud's) die zijn opgeslagen in een beveiligingsgroep STSAFE chip op de DevKit wordt gebruikt voor het genereren van het apparaat met de unieke [X.509-certificaat](concepts-security.md#x509-certificates). Het certificaat wordt later gebruikt voor het registratieproces in de Device Provisioning service en tijdens de registratie tijdens runtime.

Een typische unieke apparaat-geheim is een 64-tekenreeks, zoals te zien is in het volgende voorbeeld:

```
19e25a259d0c2be03a02d416c05c48ccd0cc7d1743458aae1cb488b074993eae
```

De tekenreeks wordt opgedeeld naar paren met tekens die worden gebruikt in de berekening van de beveiliging. Het voorgaande voorbeeld ud's wordt omgezet in: `0x19`, `0xe2`, `0x5a`, `0x25`, `0x9d`, `0x0c`, `0x2b`, `0xe0`, `0x3a`, `0x02`, `0xd4`, `0x16` , `0xc0`, `0x5c`, `0x48`, `0xcc`, `0xd0`, `0xcc`, `0x7d`, `0x17`, `0x43`, `0x45`, `0x8a`, `0xae`, `0x1c`, `0xb4`, `0x88`, `0xb0`, `0x74`, `0x99`, `0x3e`, `0xae`.

Een unieke apparaat-geheim opslaan op de DevKit:

1. Open de seriële monitor met behulp van een hulpprogramma zoals Putty. Zie [gebruik configuratiemodus](https://microsoft.github.io/azure-iot-developer-kit/docs/use-configuration-mode/) voor meer informatie.

2. Met de DevKit op uw computer is aangesloten, houdt u de **A** knop en druk vervolgens op en laat de **opnieuw** om in te voeren van de configuratiemodus. Het scherm ziet u de DevKit-ID en de configuratie.

3. Het voorbeeld ud's tekenreeks en wijzigt u een of meer tekens in andere waarden tussen nemen `0` en `f` voor uw eigen ud's.

4. Typ in het venster seriële monitor *set_dps_uds [your_own_uds_value]* en selecteer Enter.
  > [!NOTE]
  > Bijvoorbeeld, als u uw eigen ud's instellen door het veranderen van de laatste twee tekens dat moet worden `f`, moet u de opdracht als volgt opgeven: `set_dps_uds 19e25a259d0c2be03a02d416c05c48ccd0cc7d1743458aae1cb488b074993eff`.

5. Zonder de seriële monitorvenster sluit, drukt u op de **opnieuw** knop op de DevKit.

6. Noteer de **DevKit MAC-adres** en **DevKit firmwareversie** waarden.
  ![Firmwareversie](./media/how-to-connect-mxchip-iot-devkit/firmware-version.png)

## <a name="generate-an-x509-certificate"></a>Genereren van een X.509-certificaat

Nu moet u een certificaat X.609 genereren. 

### <a name="windows"></a>Windows

1. Open File Explorer en Ga naar de map met de Device Provisioning Service-voorbeeldcode die u eerder hebt gekloond. In de **.build** map, zoeken en kopiëren **DPS.ino.bin** en **DPS.ino.map**.
  ![Gegenereerde bestanden](./media/how-to-connect-mxchip-iot-devkit/generated-files.png)
  > [!NOTE]
  > Als u hebt gewijzigd de `built.path` configuratie voor Arduino naar een andere map, moet u deze bestanden vinden in de map die u hebt geconfigureerd.

2. Plak deze twee bestanden in de **extra** map op hetzelfde niveau met de **.build** map.

3. Run **dps_cert_gen.exe**. Volg de aanwijzingen om in te voeren uw **ud's**, wordt de **MAC-adres** voor de DevKit en de **firmwareversie** voor het genereren van het X.509-certificaat.
  ![Dps-certificaat-gen.exe uitvoeren](./media/how-to-connect-mxchip-iot-devkit/dps-cert-gen.png)

4. Nadat het X.509-certificaat wordt gegenereerd, een **.pem** certificaat wordt opgeslagen in dezelfde map.

## <a name="create-a-device-enrollment-entry-in-the-device-provisioning-service"></a>Een vermelding voor apparaatinschrijving maken in de Device Provisioning service

1. In de Azure-portal, gaat u naar uw Device Provisioning service-exemplaar. Selecteer **registraties beheren**, en selecteer vervolgens de **afzonderlijke inschrijvingen** tabblad. ![Afzonderlijke inschrijvingen](./media/how-to-connect-mxchip-iot-devkit/individual-enrollments.png)

2. Selecteer **Toevoegen**.

3. 'Registratie toevoegen' in het venster:

   - Selecteer **X.509** onder **mechanisme**.
   - Klik op 'Een bestand selecteren' onder **primaire PEM- of cer-certificaatbestand**.
   - In het dialoogvenster bestand openen, gaat u naar en upload het **.pem** zojuist gegenereerde certificaat.
   - Laat de overige als standaard en klik op **opslaan**.

   ![Certificaat uploaden](./media/how-to-connect-mxchip-iot-devkit/upload-cert.png)

  > [!NOTE]
  > Als er een fout opgetreden bij dit bericht:
  >
  > `{"message":"BadRequest:{\r\n \"errorCode\": 400004,\r\n \"trackingId\": \"1b82d826-ccb4-4e54-91d3-0b25daee8974\",\r\n \"message\": \"The certificate is not a valid base64 string value\",\r\n \"timestampUtc\": \"2018-05-09T13:52:42.7122256Z\"\r\n}"}`
  >
  > Open het certificaatbestand **.pem** als tekst (open met Kladblok of een teksteditor), de regels en verwijderen:
  >
  > `"-----BEGIN CERTIFICATE-----"` en `"-----END CERTIFICATE-----"`.
  >

## <a name="start-the-devkit"></a>Start de DevKit

1. VS Code en de seriële monitor openen.

2. Druk op de **opnieuw** knop op uw DevKit.

Ziet u het begin DevKit de registratie bij Device Provisioning service.

![VS Code-uitvoer](./media/how-to-connect-mxchip-iot-devkit/vscode-output.png)

## <a name="verify-that-the-devkit-is-registered-with-azure-iot-hub"></a>Controleer of dat de DevKit is geregistreerd bij Azure IoT Hub

Nadat het apparaat wordt opgestart, worden de volgende acties uitgevoerd:

1. Vanaf het apparaat wordt een registratie-aanvraag verzonden naar Device Provisioning Service.
2. De Device Provisioning service teruggestuurd een registratie-uitdaging waarop het apparaat reageert.
3. Registratie is gelukt verzendt de Device Provisioning-service de IoT Hub-URI, apparaat-ID en de versleutelde sleutel terug naar het apparaat.
4. De IoT Hub-clienttoepassing op het apparaat verbinding maakt met uw hub.
5. U ziet het apparaat worden weergegeven in de IoT Hub Device Explorer op geslaagde verbinding met de hub.
  ![Apparaat is geregistreerd](./media/how-to-connect-mxchip-iot-devkit/device-registered.png)

## <a name="problems-and-feedback"></a>Problemen en feedback

Als u problemen ondervindt, raadpleegt u de Iot DevKit [Veelgestelde vragen over](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/), of contact opnemen met de volgende kanalen voor ondersteuning:

* [Gitter.IM](http://gitter.im/Microsoft/azure-iot-developer-kit)
* [StackOverflow](https://stackoverflow.com/questions/tagged/iot-devkit)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u geleerd om een apparaat veilig met de Device Provisioning Service met behulp van de apparaat Identity Composition Engine, schrijven, zodat het apparaat automatisch met Azure IoT Hub registreren kan. 

Kortom, hebt u geleerd hoe u:

> [!div class="checklist"]
> * De globale-eindpunt van de Device Provisioning-service configureren op een apparaat.
> * Gebruik een unieke apparaat-geheim voor het genereren van een X.509-certificaat.
> * Een afzonderlijk apparaat inschrijven.
> * Controleer of dat het apparaat is geregistreerd.

Meer informatie over het [een gesimuleerd apparaat maken en inrichten](./quick-create-simulated-device.md).

