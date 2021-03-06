---
title: Zelfstudie over het voorbereiden van Azure Portal voor de implementatie van Data Box Edge | Microsoft Docs
description: De eerste zelfstudie voor het implementeren van Azure Data Box Edge omvat het voorbereiden van Azure Portal.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 10/08/2018
ms.author: alkohli
Customer intent: As an IT admin, I need to understand how to prepare the portal to deploy Data Box Edge so I can use it to transfer data to Azure.
ms.openlocfilehash: 35ac28d687c8bc6636a7d8e10f54ffb5b219a776
ms.sourcegitcommit: c282021dbc3815aac9f46b6b89c7131659461e49
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/12/2018
ms.locfileid: "49167457"
---
# <a name="tutorial-prepare-to-deploy-azure-data-box-edge-preview"></a>Zelfstudie: implementatie voorbereiden van Azure Data Box Edge (Preview-versie)


Dit is de eerste zelfstudie in de reeks zelfstudies voor implementatie, die noodzakelijk zijn voor het voltooien van de implementatie van uw Azure Data Box Edge. In deze zelfstudie wordt beschreven hoe u Azure Portal voorbereidt voor de implementatie van de Data Box Edge-resource. 

U hebt beheerdersbevoegdheden nodig om het installatie- en configuratieproces uit te voeren. Het voorbereiden van de portal duurt minder dan 10 minuten.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een nieuwe resource maken
> * De activeringssleutel ophalen

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.


> [!IMPORTANT]
> Data Box Edge is in de preview-fase. Lees de [Gebruiksvoorwaarden voor de preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voordat u deze oplossing bestelt en implementeert. 

### <a name="get-started"></a>Aan de slag

Raadpleeg de volgende zelfstudies in de voorgeschreven volgorde voor het implementeren van uw Data Box Edge.

| **#** | **In deze stap** | **Gebruikt u deze documenten** |
| --- | --- | --- | 
| 1. |**[Azure Portal voorbereiden voor Data Box Edge](data-box-edge-deploy-prep.md)** |Maak en configureer uw Data Box Edge-resource voordat u een fysiek Data Box Edge-apparaat installeert. |
| 2. |**[Data Box Edge installeren](data-box-edge-deploy-install.md)**|Het fysieke Data Box Edge-apparaat uitpakken, plaatsen en aansluiten.  |
| 3. |**[De Data Box Edge verbinden, instellen en activeren](data-box-edge-deploy-connect-setup-activate.md)** |Maak verbinding met de lokale webinterface, voltooi het instellen van het apparaat en activeer het. Het apparaat is klaar om er SMB- of NFS-shares op in te stellen.  |
| 4. |**[Gegevens overdragen met Data Box Edge](data-box-edge-deploy-add-shares.md)** |Voeg shares toe en maak verbinding met shares via SMB of NFS. |
| 5. |**[Gegevens transformeren met Data Box Edge](data-box-edge-deploy-configure-compute.md)** |Configureer de Edge-modules op het apparaat om gegevens te transformeren wanneer ze naar Azure worden overgezet. |

U kunt nu Azure Portal gaan instellen.

## <a name="prerequisites"></a>Vereisten

Hier vindt u de configuratievereisten voor uw Data Box Edge-resource, uw Data Box Edge-apparaat en het datacenternetwerk.

### <a name="for-the-data-box-edge-resource"></a>Voor de Data Box Edge-resource

Zorg voordat u begint voor het volgende:

* Uw Microsoft Azure-abonnement moet worden ingeschakeld voor de Data Box Edge-resource.
* U hebt een Microsoft Azure Storage-account met toegangsreferenties.

### <a name="for-the-data-box-edge-device"></a>Voor het Data Box Edge-apparaat

Voordat u een fysiek apparaat implementeert, controleert u of:

- Er is één U-sleuf beschikbaar in een normaal 19-inch rek in uw datacenter om het apparaat te plaatsen. 
- Zorg ervoor dat u beschikt over een vlak, stabiel en recht werkoppervlak waar u het apparaat veilig kunt neerleggen.
- Controleer of de locatie waar u het apparaat wilt neerzetten, beschikt over reguliere wisselstroom van een onafhankelijke bron of over een vermogenseenheid (PDU) met noodvoeding (UPS).
- U hebt toegang tot een fysiek apparaat.


### <a name="for-the-datacenter-network"></a>Voor datacenternetwerk

Zorg voordat u begint voor het volgende:

* Het netwerk in uw datacenter is geconfigureerd volgens de netwerkvereisten voor uw Data Box Edge-apparaat. Zie [Systeemvereisten voor Data Box Edge](data-box-gateway-system-requirements.md) voor meer informatie.

* Uw Data Box Edge beschikt te allen tijde over een toegewezen internetbandbreedte van 20 Mbps (of meer). Deze bandbreedte mag niet worden gedeeld met andere toepassingen. Als u gebruikmaakt van bandbreedtebeperking, adviseren we om een bandbreedte van 32 Mbps of meer toe te wijzen om de beperking te laten werken.

## <a name="create-a-new-resource"></a>Een nieuwe resource maken

Voer de volgende stappen uit om een nieuwe Data Box Edge-resource te maken. 

Als u al een Data Box Edge-resource hebt voor het beheer van uw fysieke apparaat, kunt u deze stap overslaan en verdergaan met [Activeringscode ophalen](#get-the-activation-key).

Voer de volgende stappen uit in Azure Portal om een Data Box-resource te maken.

1. Gebruik uw Microsoft Azure-referenties om u aan te melden bij Azure Preview Portal op de volgende URL: [https://aka.ms/databox-edge](https://aka.ms/databox-edge). 

2. Selecteer het abonnement dat u wilt gebruiken voor de preview van Data Box Edge. Selecteer de regio waar u de Data Box Edge-resource wilt implementeren. Klik bij de **Data Box Edge**-optie op **Maken**.

    ![Data Box Edge-service zoeken](media/data-box-edge-deploy-prep/data-box-edge-sku.png)

3. Voer de volgende informatie in of selecteer deze voor de nieuwe resource.
    
    |Instelling  |Waarde  |
    |---------|---------|
    |Resourcenaam   | Een beschrijvende naam om de resource aan te duiden.<br>De resourcenaam is tussen 2 en 50 tekens lang en kan letters, cijfers en afbreekstreepjes bevatten.<br> De naam begint en eindigt met een letter of cijfer.        |
    |Abonnement    |Abonnement is gekoppeld aan uw factureringsrekening. |
    |Resourcegroep  |Maak een nieuwe groep of selecteer een bestaande groep.<br>Meer informatie over [Azure-resourcegroepen](../azure-resource-manager/resource-group-overview.md).     |
    |Locatie     |Voor deze release zijn US - oost, US - west 2, Azië - zuidoost en Europa - west beschikbaar. <br> Kies een locatie die het dichtst bij de geografische regio ligt waar u uw apparaat wilt implementeren.|
    
    ![Data Box Edge-resource maken](media/data-box-edge-deploy-prep/data-box-edge-resource.png)
    
4. Klik op **OK**.
 
Het maken van de resource duurt enkele minuten. Nadat de resource is gemaakt, wordt u daarvan op de hoogte gebracht.


## <a name="get-the-activation-key"></a>De activeringssleutel ophalen

Nadat de Azure Data Box Edge-resource is geactiveerd, hebt u de activeringssleutel nodig. Deze sleutel wordt gebruikt om uw Data Box Edge-apparaat te activeren en te verbinden met de resource. U kunt deze sleutel nu ophalen, terwijl u Azure Portal geopend hebt.

1. Klik op de resource die u hebt gemaakt en klik vervolgens op **Overzicht**.

2. Klik op **Sleutel genereren** om een activeringssleutel te maken. Klik op het kopieerpictogram om de sleutel te kopiëren en op te slaan voor later gebruik.

    ![Activeringssleutel ophalen](media/data-box-edge-deploy-prep/get-activation-key.png)

> [!IMPORTANT]
> - De activeringssleutel verloopt 3 dagen nadat deze is gegenereerd. 
> - Als de sleutel is verlopen, genereert u een nieuwe sleutel. De oudere toegangssleutel is niet langer geldig.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie bent u meer te weten gekomen over verschillende onderwerpen met betrekking tot Data Box Edge, zoals:

> [!div class="checklist"]
> * Een nieuwe resource maken
> * De activeringssleutel ophalen

Ga naar de volgende zelfstudie om te lezen hoe u uw Data Box Edge installeert. 

> [!div class="nextstepaction"]
> [Een Data Box Edge installeren](./data-box-edge-deploy-install.md)



