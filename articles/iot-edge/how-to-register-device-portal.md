---
title: Registreren van een nieuw apparaat vanuit Azure portal - Azure IoT Edge | Microsoft Docs
description: De Azure portal gebruiken voor een nieuwe IoT Edge-apparaat registreren en de verbindingsreeks op te halen
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 06/05/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.custom: seodec18
ms.openlocfilehash: da93541339ac1c199d3ba0a220fbfff6bbb8bf9c
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53082116"
---
# <a name="register-a-new-azure-iot-edge-device-from-the-azure-portal"></a>Registreer een nieuwe Azure IoT Edge-apparaat vanuit de Azure-portal

Voordat u uw IoT-apparaten met Azure IoT Edge gebruiken kunt, moet u hen registreert bij uw IoT-hub. Wanneer u een apparaat hebt geregistreerd, ontvangt u een verbindingsreeks die kan worden gebruikt voor het instellen van uw apparaat voor Edge-werkbelastingen. 

In dit artikel bevat informatie over het registreren van een nieuwe IoT Edge-apparaat met behulp van de Azure portal.

## <a name="prerequisites"></a>Vereisten

* Een [IoT-hub](../iot-hub/iot-hub-create-through-portal.md) in uw Azure-abonnement. 

## <a name="create-a-device"></a>Een apparaat maken

IoT Edge-apparaten zijn gemaakt en afzonderlijk beheerd vanaf apparaten die verbinding maken met uw IoT-hub, maar niet met het edge-functionaliteit in de Azure-portal. 

1. Aanmelden bij de [Azure-portal](https://portal.azure.com) en navigeer naar uw IoT-hub. 
2. Selecteer **IoT Edge** in het menu.
3. Selecteer **IoT Edge-apparaat toevoegen**. 
4. Geef een beschrijvende apparaat-ID. 
5. Selecteer **Opslaan**. 

## <a name="view-all-devices"></a>Alle apparaten weergeven

Alle de edge-apparaten die verbinding met uw IoT-hub maken worden weergegeven op de **IoT Edge** pagina. 

## <a name="retrieve-the-connection-string"></a>De verbindingsreeks ophalen

Wanneer u klaar bent om uw apparaat instellen, moet u de verbindingsreeks die is gekoppeld aan uw fysieke apparaat met de identiteit van de IoT-hub.

1. Uit de **IoT Edge** pagina in de portal, klikt u op de apparaat-ID in de lijst van Edge-apparaten. 
2. Kopieer de waarde van een van beide **verbindingsreeks (primaire sleutel)** of **verbindingsreeks (secundaire sleutel)**. 

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het [modules implementeren op een apparaat met de Azure-portal](how-to-deploy-modules-portal.md)
