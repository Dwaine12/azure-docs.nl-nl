---
title: 'Zelfstudie: Azure Key Vault gebruiken met Azure Windows Virtual Machine in Python | Microsoft Docs'
description: 'Zelfstudie: Een ASP.NET Core-toepassing configureren voor het lezen van een geheim uit Key Vault'
services: key-vault
documentationcenter: ''
author: prashanthyv
manager: rajvijan
ms.assetid: 0e57f5c7-6f5a-46b7-a18a-043da8ca0d83
ms.service: key-vault
ms.workload: key-vault
ms.topic: tutorial
ms.date: 09/05/2018
ms.author: pryerram
ms.custom: mvc
ms.openlocfilehash: 26b5b16e3eb016edbe53c3526e51c3aa44f307b5
ms.sourcegitcommit: 56d20d444e814800407a955d318a58917e87fe94
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/29/2018
ms.locfileid: "52583581"
---
# <a name="tutorial-how-to-use-azure-key-vault-with-azure-windows-virtual-machine-in-python"></a>Zelfstudie: Azure Key Vault gebruiken met Azure Windows Virtual Machine in Python

Azure Key Vault helpt u bij het beveiligen van geheimen zoals API-sleutels, databaseverbindingsreeksen die nodig zijn voor toegang tot uw toepassingen, services en IT-resources.

In deze zelfstudie voert u de stappen uit die nodig zijn om een Azure-webtoepassing gegevens te laten lezen uit Azure Key Vault met behulp van beheerde identiteiten voor Azure-resources. Deze zelfstudie is gebaseerd op [Azure Web Apps](../app-service/app-service-web-overview.md). Hieronder leert u:

> [!div class="checklist"]
> * Een sleutelkluis maken.
> * Een geheim opslaan in de sleutelkluis.
> * Een geheim ophalen uit de sleutelkluis.
> * Een virtuele Azure-machine maken.
> * Een [beheerde identiteit](../active-directory/managed-identities-azure-resources/overview.md) inschakelen voor de virtuele machine.
> * De vereiste machtigingen verlenen aan de consoletoepassing om gegevens te lezen uit de sleutelkluis.
> * Geheimen lezen uit Key Vault

Lees voordat we verdergaan de [basisconcepten](key-vault-whatis.md#basic-concepts).

## <a name="prerequisites"></a>Vereisten
* Alle platformen:
  * Git ([downloaden](https://git-scm.com/downloads)).
  * Een Azure-abonnement. Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.
  * [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) versie 2.0.4 of hoger. Deze is beschikbaar voor Windows, Mac en Linux.

In deze zelfstudie wordt Managed Service Identity gebruikt

## <a name="what-is-managed-service-identity-and-how-does-it-work"></a>Wat is Managed Service Identity en hoe werkt het?
Voordat we verder gaan, moeten we het over MSI hebben. Azure Key Vault kan referenties veilig opslaan zodat ze zich niet in uw code bevinden, maar om ze op te halen moet u zich authenticeren bij Azure Key Vault. En om u te authenticeren bij Key Vault, hebt u een referentie nodig! Een klassiek bootstrap-probleem. Door de magie van Azure en Azure AD biedt MSI een 'bootstrap-identiteit' die het veel eenvoudiger maakt om dingen op gang te brengen.

Het werkt als volgt. Wanneer u MSI inschakelt voor een Azure-service zoals Virtual Machines, App Service of Functions, maakt Azure een [service-principal](key-vault-whatis.md#basic-concepts) voor de instantie van de service in Azure Active Directory, en injecteert de referenties voor de service-principal in de instantie van de service. 

![MSI](media/MSI.png)

Vervolgens roept uw ​​code een lokale metadataservice aan die beschikbaar is op de Azure-resource om een ​​toegangstoken te verkrijgen.
Uw code gebruikt het toegangstoken dat wordt verkregen van het lokale MSI_ENDPOINT zich te authenticeren bij een Azure Key Vault-service. 

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.

Als u zich bij Azure wilt aanmelden met de Azure CLI, voert u het volgende in:

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een resourcegroep met de opdracht [az group create](/cli/azure/group#az-group-create). Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.

Selecteer de naam van een resourcegroep en vul de tijdelijke aanduiding in.
In het volgende voorbeeld wordt een resourcegroep gemaakt in de regio US - west:

```azurecli
# To list locations: az account list-locations --output table
az group create --name "<YourResourceGroupName>" --location "West US"
```

De resourcegroep die u net hebt gemaakt, wordt overal in dit artikel gebruikt.

## <a name="create-a-key-vault"></a>Een sleutelkluis maken

Vervolgens maakt u een sleutelkluis in de resourcegroep die u in de vorige stap hebt gemaakt. Geef de volgende informatie op:

* Naam van de sleutelkluis: de naam moet een tekenreeks zijn met 3-24 tekens en mag alleen (0-9, a-z, A-Z en -) bevatten.
* Naam van de resourcegroep.
* Locatie: **US - west**.

```azurecli
az keyvault create --name "<YourKeyVaultName>" --resource-group "<YourResourceGroupName>" --location "West US"
```
Vanaf dit punt is uw Azure-account nu als enige gemachtigd om bewerkingen op deze nieuwe kluis uit te voeren.

## <a name="add-a-secret-to-the-key-vault"></a>Een geheim toevoegen aan de sleutelkluis

We gaan een geheim toevoegen om te laten zien hoe dit werkt. U wilt bijvoorbeeld een SQL-verbindingsreeks opslaan of andere gegevens die u veilig wilt bewaren, maar wel beschikbaar wilt stellen aan uw toepassing.

Typ de volgende opdrachten om een geheim te maken in de sleutelkluis met de naam **AppGeheim**. Met dit geheim wordt de waarde **MijnGeheim** opgeslagen.

```azurecli
az keyvault secret set --vault-name "<YourKeyVaultName>" --name "AppSecret" --value "MySecret"
```

## <a name="create-a-virtual-machine"></a>Een virtuele machine maken
Volg de onderstaande koppelingen om een virtuele Windows-machine te maken

[Azure-CLI](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-cli) 

[Powershell](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-powershell)

[Portal](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal)

## <a name="assign-identity-to-virtual-machine"></a>Identiteit toewijzen aan een virtuele machine
In deze stap wijzen we een door het systeem toegewezen identiteit toe aan de virtuele machine met de volgende opdracht in Azure CLI

```
az vm identity assign --name <NameOfYourVirtualMachine> --resource-group <YourResourceGroupName>
```

Hieronder wordt de door het systeem toegewezen identiteit (systemAssignedIdentity) weergegeven. De uitvoer van de bovenstaande opdracht ziet er als volgt uit 

```
{
  "systemAssignedIdentity": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "userAssignedIdentities": {}
}
```

## <a name="give-virtual-machine-identity-permission-to-key-vault"></a>Identiteit van virtuele machine machtigen voor Key Vault
Nu kunnen we de hierboven gemaakte identiteit machtigen voor Key Vault met de volgende opdracht

```
az keyvault set-policy --name '<YourKeyVaultName>' --object-id <VMSystemAssignedIdentity> --secret-permissions get list
```

## <a name="login-to-the-virtual-machine"></a>Aanmelden bij de virtuele machine

U kunt deze [zelfstudie](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon) volgen

## <a name="create-and-run-sample-python-app"></a>Python-voorbeeld-app maken en uitvoeren

Het volgende bestand is slechts een voorbeeldbestand met de naam 'Sample.py'. Hierbij wordt gebruikgemaakt van de bibliotheek [requests](http://docs.python-requests.org/master/) (aanvragen) voor HTTP GET-aanroepen.

## <a name="edit-samplepy"></a>Sample.py bewerken
Nadat u Sample.py hebt gemaakt, opent u het bestand en kopieert u de onderstaande code

```
The below is a 2 step process. 
1. Fetch a token from the local MSI endpoint on the VM which in turn fetches a token from Azure Active Directory
2. Pass the token to Key Vault and fetch your secret 
```
    # importing the requests library 
    import requests 

    # Step 1: Fetch an access token from a Managed Identity enabled azure resource      
    # Note that the resource here is https://vault.azure.net for public cloud and api-version is 2018-02-01
    MSI_ENDPOINT = "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net"
    r = requests.get(MSI_ENDPOINT, headers = {"Metadata" : "true"}) 
      
    # extracting data in json format 
    # This request gets a access_token from Azure Active Directory using the local MSI endpoint
    data = r.json() 
    
    # Step 2: Pass the access_token received from previous HTTP GET call to Key Vault
    KeyVaultURL = "https://prashanthwinvmvault.vault.azure.net/secrets/RandomSecret?api-version=2016-10-01"
    kvSecret = requests.get(url = KeyVaultURL, headers = {"Authorization": "Bearer " + data["access_token"]})
    
    print(kvSecret.json()["value"])
```

By running you should see the secret value 
```
python Sample.py
```

The above code shows you how to do operations with Azure Key Vault in an Azure Windows Virtual Machine. 

## Next steps

> [!div class="nextstepaction"]
> [Azure Key Vault REST API](https://docs.microsoft.com/rest/api/keyvault/)
