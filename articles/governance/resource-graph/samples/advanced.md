---
title: Geavanceerde query's van Azure Resource Graph
description: Gebruik Azure Resource Graph om een aantal geavanceerde query's uit te voeren.
services: resource-graph
author: DCtheGeek
ms.author: dacoulte
ms.date: 10/22/2018
ms.topic: quickstart
ms.service: resource-graph
manager: carmonm
ms.custom: mvc
ms.openlocfilehash: 43cf9f5ec0f9c265efa0e59eadbf6c9bbe4f7c3f
ms.sourcegitcommit: db2cb1c4add355074c384f403c8d9fcd03d12b0c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/15/2018
ms.locfileid: "51682876"
---
# <a name="advanced-resource-graph-queries"></a>Geavanceerde query's van Resource Graph

Om inzicht te krijgen in query's met Azure Resource Graph moet u eerst enige basiskennis hebben van de [querytaal](../concepts/query-language.md). Als u nog geen ervaring hebt met [Azure Data Explorer](../../../data-explorer/data-explorer-overview.md), is het raadzaam om eerst de basisbeginselen door te nemen, zodat u weet hoe u aanvragen opstelt voor de resources die u zoekt.

We nemen de volgende geavanceerde query's door:

> [!div class="checklist"]
> - [VMSS-capaciteit en -grootte opvragen](#vmss-capacity)
> - [Een lijst weergeven van alle tagnamen](#list-all-tags)
> - [Virtuele machines zoeken met reguliere expressies](#vm-regex)

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free) aan voordat u begint.

## <a name="language-support"></a>Taalondersteuning

Azure CLI (met een extensie) en Azure PowerShell (met een module) ondersteunen Azure Resource Graph. Controleer voordat u een van de volgende query's uitvoert, of uw omgeving gereed is. Zie [Azure CLI](../first-query-azurecli.md#add-the-resource-graph-extension) en [Azure PowerShell](../first-query-powershell.md#add-the-resource-graph-module) voor stappen voor het installeren en valideren van uw gewenste shellomgeving.

## <a name="vmss-capacity"></a>Capaciteit en grootte van een virtuele-machineschaalset ophalen

Met deze query zoekt u virtuele-machineschaalsetresources en verkrijgt u diverse informatie, waaronder de grootte van de virtuele machines en de capaciteit van de schaalset. Deze query maakt gebruik van de functie `toint()` om de capaciteit te converteren naar een waarde die kan worden gesorteerd. Ten slotte worden de namen van de kolommen gewijzigd in eigenschappen met aangepaste namen.

```Query
where type=~ 'microsoft.compute/virtualmachinescalesets'
| where name contains 'contoso'
| project subscriptionId, name, location, resourceGroup, Capacity = toint(sku.capacity), Tier = sku.name
| order by Capacity desc
```

```azurecli-interactive
az graph query -q "where type=~ 'microsoft.compute/virtualmachinescalesets' | where name contains 'contoso' | project subscriptionId, name, location, resourceGroup, Capacity = toint(sku.capacity), Tier = sku.name | order by Capacity desc"
```

```azurepowershell-interactive
Search-AzureRmGraph -Query "where type=~ 'microsoft.compute/virtualmachinescalesets' | where name contains 'contoso' | project subscriptionId, name, location, resourceGroup, Capacity = toint(sku.capacity), Tier = sku.name | order by Capacity desc"
```

## <a name="list-all-tags"></a>Een lijst weergeven van alle tagnamen

Deze query start met de tag en bouwt een JSON-object dat alle unieke tagnamen en hun overeenkomende typen vermeldt.

```Query
project tags
| summarize buildschema(tags)
```

```azurecli-interactive
az graph query -q "project tags | summarize buildschema(tags)"
```

```azurepowershell-interactive
Search-AzureRmGraph -Query "project tags | summarize buildschema(tags)"
```

## <a name="vm-regex"></a>Virtuele machines zoeken met reguliere expressies

Deze query zoekt virtuele machines die overeenkomen met een [reguliere expressie](/dotnet/standard/base-types/regular-expression-language-quick-reference) (ook wel _regex_ genoemd).
Met de **reguliere overeenkomstexpressie @** kunt u de betreffende reguliere expressie definiëren. Deze is `^Contoso(.*)[0-9]+$`. De definitie van deze reguliere expressie wordt als volgt uitgelegd:

- `^`: Overeenkomst moet beginnen aan het begin van de tekenreeks.
- `Contoso`: De hoofdlettergevoelige reeks.
- `(.*)`: Een subexpressieovereenkomst:
  - `.`: Komt overeen met een willekeurig teken (met uitzondering van een nieuwe regel).
  - `*`: Komt nul keer of vaker overeen met vorig element.
- `[0-9]`: Tekengroepovereenkomst met de cijfers 0 t/m 9.
- `+`: Komt één keer of vaker overeen met vorig element.
- `$`: Overeenkomst met het vorige element moet voorkomen aan het einde van de tekenreeks.

Na de vergelijking op naam worden de namen in oplopende volgorde weergegeven.

```Query
where type =~ 'microsoft.compute/virtualmachines' and name matches regex @'^Contoso(.*)[0-9]+$'
| project name
| order by name asc
```

```azurecli-interactive
az graph query -q "where type =~ 'microsoft.compute/virtualmachines' and name matches regex @'^Contoso(.*)[0-9]+$' | project name | order by name asc"
```

```azurepowershell-interactive
Search-AzureRmGraph -Query "where type =~ 'microsoft.compute/virtualmachines' and name matches regex @'^Contoso(.*)[0-9]+$' | project name | order by name asc"
```

## <a name="next-steps"></a>Volgende stappen

- Voorbeelden uit [Starter query's](starter.md) bekijken
- Meer informatie over de [querytaal](../concepts/query-language.md)
- [Resources verkennen](../concepts/explore-resources.md)
