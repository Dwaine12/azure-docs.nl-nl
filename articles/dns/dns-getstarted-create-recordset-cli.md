---
title: Een recordset en records voor een DNS-zone maken met CLI| Microsoft Docs
description: Hostrecords voor Azure DNS maken. Recordsets en records instellen met CLI
services: dns
documentationcenter: na
author: sdwheeler
manager: carmonm
editor: 
ms.assetid: 02b897d3-e83b-4257-b96d-5c29aa59e843
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: sewhee
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 40accee35eca32eefd4afc2315c70d51e0edcdcd


---
# <a name="create-dns-record-sets-and-records-by-using-cli"></a>DNS-recordsets en records maken met CLI
> [!div class="op_single_selector"]
> * [Azure Portal](dns-getstarted-create-recordset-portal.md)
> * [PowerShell](dns-getstarted-create-recordset.md)
> * [Azure CLI](dns-getstarted-create-recordset-cli.md)
> 
> 

In dit artikel wordt uitgelegd hoe u records en recordsets maakt met CLI. Nadat u de DNS-zone hebt gemaakt, moet u de DNS-records voor uw domein toevoegen. Als u dit wilt doen, moet u eerst goed begrijpen wat DNS-records en recordsets zijn.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

## <a name="create-a-record-set-and-record"></a>Een recordset en record maken
In deze sectie leert u hoe u een recordset en records maakt. In dit voorbeeld maakt u een recordset met de relatieve naam www in de DNS-zone contoso.com. De volledig gekwalificeerde naam van de records is www.contoso.com. Het recordtype is A en deTTL (Time to Live) is 60 seconden. Nadat deze stap is voltooid, hebt u een lege recordset gemaakt.

Als u een record in de apex van de zone wilt maken (in dit geval contoso.com), gebruikt u de recordnaam "@",, inclusief de aanhalingstekens. Dit is een algemene DNS-conventie.

### <a name="1-create-a-record-set"></a>1. Een recordset maken
Gebruik `azure network dns record-set create` om een recordset te maken. Geef de resourcegroep, de zonenaam, de relatieve naam van de recordset, het recordtype en de TTL op. Als de parameter `--ttl` niet is gedefinieerd, wordt de standaardwaarde vier (in seconden) gebruikt. Nadat deze stap is voltooid, hebt u een lege recordset (www) gemaakt.

*Gebruik: network dns record-set create <resource-group> <dns-zone-name> <name> <type> <ttl>*

    azure network dns record-set create myresourcegroup  contoso.com  www A  60

### <a name="2-add-records"></a>2. Records toevoegen
Als u de nieuwe www-recordset wilt gebruiken, moet u records aan de set toevoegen. U voegt records aan de recordsets toe met `azure network dns record-set add-record`.

De parameters voor het toevoegen van records aan een recordset variëren afhankelijk van het type recordset. Als u bijvoorbeeld een recordset van type A gebruiken, kunt alleen records opgeven met de parameter `-a <IPv4 address>`.

U kunt de volgende opdracht gebruiken om IPv4 *A*-records voor de www-record toe te voegen:

*Gebruik: network dns record-set add-record <resource-group> <dns-zone-name> <record-set-name> <type>*

    azure network dns record-set add-record myresourcegroup contoso.com  www A  -a 134.170.185.46

## <a name="additional-record-type-examples"></a>Aanvullende voorbeelden van recordtypen
De volgende voorbeelden tonen u hoe u een recordset van elk recordtype kunt maken. Elke recordset bevat één record.

[!INCLUDE [dns-add-record-cli-include](../../includes/dns-add-record-cli-include.md)]

## <a name="next-steps"></a>Volgende stappen
Zie [DNS-records en -recordsets beheren met CLI](dns-operations-recordsets-portal.md) voor meer informatie over het beheren van uw recordset en records.

Zie [Overzicht van Azure DNS-overzicht](dns-overview.md) voor meer informatie over Azure DNS.




<!--HONumber=Nov16_HO2-->


