---
title: Nuttige operators in Azure Log Analytics-query's | Microsoft Docs
description: Algemene functies te gebruiken voor verschillende scenario's in Log Analytics-query's.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: bwren
ms.openlocfilehash: 060b1e469a31c335f062ccd332157d13e64f9318
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53183979"
---
# <a name="useful-operators-in-log-analytics-queries"></a>Nuttige operators in Log Analytics-query 's

De onderstaande tabel bevat enkele algemene functies te gebruiken voor verschillende scenario's in Log Analytics-query's.

## <a name="useful-operators"></a>Nuttige operatoren

Categorie                                |Functie van de relevante Analytics
----------------------------------------|----------------------------------------
Selectie en in de kolom aliassen            |`project`, `project-away`, `extend`
Tijdelijke tabellen en constanten          |`let scalar_alias_name = …;` <br> `let table_alias_name =  …  …  … ;`| 
Vergelijking en Tekenreeksoperators         |`startswith`, `!startswith`, `has`, `!has` <br> `contains`, `!contains`, `containscs` <br> `hasprefix`, `!hasprefix`, `hassuffix`, `!hassuffix`, `in`, `!in` <br> `matches regex` <br> `==`, `=~`, `!=`, `!~`
Algemene tekenreeksfuncties                 |`strcat()`, `replace()`, `tolower()`, `toupper()`, `substring()`, `strlen()`
Veelgebruikte wiskundige functies                   |`sqrt()`, `abs()` <br> `exp()`, `exp2()`, `exp10()`, `log()`, `log2()`, `log10()`, `pow()` <br> `gamma()`, `gammaln()`
Het parseren van tekst                            |`extract()`, `extractjson()`, `parse`, `split()`
Uitvoer te beperken                         |`take`, `limit`, `top`, `sample`
Datumfuncties                          |`now()`, `ago()` <br> `datetime()`, `datepart()`, `timespan` <br> `startofday()`, `startofweek()`, `startofmonth()`, `startofyear()` <br> `endofday()`, `endofweek()`, `endofmonth()`, `endofyear()` <br> `dayofweek()`, `dayofmonth()`, `dayofyear()` <br> `getmonth()`, `getyear()`, `weekofyear()`, `monthofyear()`
Groeperen en cumulatie-instellingen                |`summarize by` <br> `max()`, `min()`, `count()`, `dcount()`, `avg()`, `sum()` <br> `stddev()`, `countif()`, `dcountif()`, `argmax()`, `argmin()` <br> `percentiles()`, `percentile_array()`
Samenvoegingen en samenvoegingen                        |`join kind=leftouter`, `inner`, `rightouter`, `fullouter`, `leftanti` <br> `union`
Volgorde sorteren                             |`sort`, `order` 
Dynamische object (JSON en matrix)         |`parsejson()` <br> `makeset()`, `makelist()` <br> `split()`, `arraylength()` <br> `zip()`, `pack()`
Logische operators                       |`and`, `or`, `iff(condition, value_t, value_f)` <br> `binary_and()`, `binary_or()`, `binary_not()`, `binary_xor()`
Machine learning                        |`evaluate autocluster`, `basket`, `diffpatterns`, `extractcolumns`


## <a name="next-steps"></a>Volgende stappen

- Ga via een les op de [schrijven van query's in Log Analytics](get-started-queries.md).
