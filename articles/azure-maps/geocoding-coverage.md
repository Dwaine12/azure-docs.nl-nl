---
title: Dekking voor geocodering van Azure Maps | Microsoft Docs
description: Meer informatie over de dekking voor Geocodering van Azure Maps
author: dsk-2015
ms.author: dkshir
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: 664d52a96f1e724502f82f5f72567f87c74e716b
ms.sourcegitcommit: 5aed7f6c948abcce87884d62f3ba098245245196
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/28/2018
ms.locfileid: "52444253"
---
# <a name="azure-maps-geocoding-coverage"></a>Azure Maps-dekking voor geocodering

Wanneer u een locatie met Azure Maps zoekt, wordt de search-service neemt van uw zoektermen en retourneert de breedtegraad en lengtegraad coördinaten, een proces dat geocodering wordt genoemd. Maps hoeft echter niet dezelfde mate van informatie en de nauwkeurigheid van de gegevens voor alle regio's en andere landen. Gebruik dit artikel om te bepalen wat voor soort locaties kunt u op betrouwbare wijze zoeken naar in elke regio. 

De mogelijkheid om geocode in een land/regio is afhankelijk van de gegevens onderweg dekking en de nauwkeurigheid van de geocodering van de service voor geocodering. De volgende categorieën worden gebruikt. Geef het niveau van ondersteuning voor geocodering in elk land.
* **Adres van de punten** -adressen gegevens kan worden omgezet in een breedtegraad/lengtegraad coördinaat binnen de adres-pakket (eigenschap grens). Soms aangeduid als 'Dakantenne' nauwkeurige. Dit is de hoogste mate van nauwkeurigheid is beschikbaar voor adressen. 
* **Getallen bevatten** -adressen zijn geïnterpoleerde naar een breedtegraad/lengtegraad-coördinaat op straat.
* **Naam van de straat niveau** -adressen worden omgezet in de breedtegraad/lengtegraad-coördinaat van de straat die het adres bevat. Het huisnummer kan niet worden verwerkt.
* **Niveau plaats** -plaats het geocoderen van plaatsnamen worden ondersteund.

## <a name="americas"></a>Noord- en Zuid-Amerika

| Regio             | Adres verwijst | Huis cijfers | Naam van de straat niveau | Niveau plaats | Punten van belang zijn |
|-----------------------------------------------------|:---------------:|:--------------:|:------------:|:----------:|:------------------:|
| Anguilla                                            |                 |                |              |      ✓     |          ✓         |
| Antarctica                                          |                 |                |              |      ✓     |          ✓         |
| Antigua en Barbuda                                 |                 |                |       ✓      |      ✓     |          ✓         |
| Argentinië                                           |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Aruba                                               |                 |                |              |      ✓     |          ✓         |
| Bahama's                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Barbados                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Belize                                              |                 |                |              |      ✓     |          ✓         |
| Bermuda                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Bolivia                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Bonaire, Sint Eustatius en Saba|                 |                |              |      ✓     |          ✓         |
| Brazilië                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Canada                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Kaaimaneilanden                                      |                 |                |       ✓      |      ✓     |          ✓         |
| Chili                                               |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Clipperton-eiland                                   |                 |                |              |      ✓     |                    |
| Colombia                                            |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Costa Rica                                          |                 |                |       ✓      |      ✓     |          ✓         |
| Cuba                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Dominica                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Dominicana                                          |                 |                |       ✓      |      ✓     |          ✓         |
| Ecuador                                             |                 |                |       ✓      |      ✓     |          ✓         |
| El Salvador                                         |                 |                |       ✓      |      ✓     |          ✓         |
| Falklandeilanden                                    |                 |                |              |      ✓     |          ✓         |
| Frans-Guyana                                       |                 |                |       ✓      |      ✓     |          ✓         |
| Grenada                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Guadeloupe|                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Guam                                                |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Guatemala                                           |                 |                |       ✓      |      ✓     |          ✓         |
| Guyana        |                |             |           |      ✓     |                 |
| Haiti                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Honduras                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Jamaica                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Martinique                                          |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Mexico                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Montserrat                                          |                 |                |              |      ✓     |          ✓         |
| Nicaragua                                           |                 |                |       ✓      |      ✓     |          ✓         |
| Panama                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Paraguay                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Peru                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Puerto Rico                                         |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Saint-Barthélemy                                    |                 |                |       ✓      |      ✓     |          ✓         |
| Saint Kitts en Nevis                               |                 |                |       ✓      |      ✓     |          ✓         |
| Saint Lucia                                         |                 |                |              |      ✓     |          ✓         |
| Saint-Martin                                        |                 |                |       ✓      |      ✓     |          ✓         |
| Saint-Pierre en Miquelon|                 |                |       ✓      |      ✓     |          ✓         |
| Saint Vincent en de Grenadines                    |                 |                |              |      ✓     |          ✓         |
| Sint Maarten                                        |                 |                |       ✓      |      ✓     |          ✓         |
| Zuid-Georgia en de Zuidelijke Sandwicheilanden        |                 |                |              |      ✓     |          ✓         |
| Suriname                                            |                 |                |              |      ✓     |          ✓         |
| Trinidad en Tobago                                 |                 |                |       ✓      |      ✓     |          ✓         |
| Amerikaanse ondergeschikte afgelegen eilanden                |                 |                |              |      ✓     |          ✓         |
| Verenigde Staten van Amerika                            |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Uruguay                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Venezuela                                           |                 |                |       ✓      |      ✓     |          ✓         |
| Britse Maagdeneilanden - Groot-Brittannië                            |                 |                |              |      ✓     |          ✓         |
| Britse Maagdeneilanden - Verenigde Staten                      |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |

## <a name="asia-pacific"></a>Azië en Stille Oceaan

| Regio             | Adres verwijst |Huis cijfers | Naam van de straat niveau | Niveau plaats | Punten van belang zijn |
|-----------------------------------------------------|:---------------:|:--------------:|:------------:|:----------:|:------------------:|
| Amerikaans-Samoa                                      |                 |                |       ✓      |      ✓     |          ✓         |
| Australië                                           |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Bangladesh                                          |                 |                |              |      ✓     |          ✓         |
| Bhutan                                              |                 |                |              |      ✓     |          ✓         |
| Brits Indische Oceaanterritorium                      |                 |                |              |      ✓     |          ✓         |
| Brunei                                              |        ✓        |                |       ✓      |      ✓     |          ✓         |
| Cambodja                                            |                 |                |              |      ✓     |          ✓         |
| China |                 |                |              |      ✓     |          ✓         |
| Christmaseiland                                    |        ✓        |                |       ✓      |      ✓     |          ✓         |
| Cocos-Keeling-eilanden|                 |                |              |      ✓     |          ✓         |
| Comoren|                 |                |              |      ✓     |          ✓         |
| Cookeilanden                                        |                 |                |              |      ✓     |          ✓         |
| Fiji |                 |                |              |      ✓     |          ✓         |
| Frans-Polynesië                                    |                 |                |              |      ✓     |          ✓         |
| Heard- en McDonald-eilanden                   |                 |                |              |      ✓     |          ✓         |
| Hongkong                                           |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Indonesië                                           |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| India       |        ✓        |        ✓       |       ✓      |      ✓     |                   |
| Japan                                               |                 |                |              |      ✓     |          ✓         |
| Kiribati                                            |                 |                |              |      ✓     |          ✓         |
| Laos                                                |                 |                |              |      ✓     |          ✓         |
| Macao                                               |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Maleisië                                            |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Micronesia |                 |                |              |      ✓     |          ✓         |
| Mongolië                                            |                 |                |              |      ✓     |          ✓         |
| Nauru                                               |                 |                |              |      ✓     |          ✓         |
| Napal|                 |                |              |      ✓     |          ✓         |
| Nieuw-Caledonië                                       |                 |                |              |      ✓     |          ✓         |
| Nieuw-Zeeland                                         |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Niue                                                |                 |                |              |      ✓     |          ✓         |
| Norfolkeiland                                      |                 |                |              |      ✓     |          ✓         |
| Noord-Korea                                         |                 |                |              |      ✓     |          ✓         |
| Noordelijke Marianen                            |                 |                |       ✓      |      ✓     |          ✓         |
| Pakistan                                            |                 |                |              |      ✓     |          ✓         |
| Palau |                 |                |              |      ✓     |          ✓         |
| Papoea-Nieuw-Guinea                                    |                 |                |              |      ✓     |          ✓         |
| Paracel-eilanden                                     |                 |                |              |      ✓     |                    |
| Filipijnen                                         |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Pitcairn                                            |                 |                |              |      ✓     |          ✓         |
| Samoa                                               |                 |                |              |      ✓     |          ✓         |
| Senkaku-eilanden                                     |        ✓        |                |              |      ✓     |          ✓         |
| Singapore                                           |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Salomonseilanden                                     |                 |                |              |      ✓     |          ✓         |
| Zuid-Korea                                         |                 |                |              |      ✓     |          ✓         |
| Zuidelijke Kurils                                     |        ✓        |                |              |      ✓     |          ✓         |
| Spratly eilanden                                     |                 |                |              |      ✓     |                    |
| Sri Lanka                                           |                 |                |              |      ✓     |          ✓         |
| Taiwan                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Thailand                                            |        ✓        |                |       ✓      |      ✓     |          ✓         |
| Tokelau                                             |                 |                |              |      ✓     |          ✓         |
| Tonga                                               |                 |                |              |      ✓     |          ✓         |
| Turks- en Caicoseilanden                            |                 |                |              |      ✓     |          ✓         |
| Tuvalu                                              |                 |                |              |      ✓     |          ✓         |
| Vanuatu                                             |                 |                |              |      ✓     |          ✓         |
| Vietnam                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Wallis en Futuna|                 |                |              |      ✓     |          ✓         |

## <a name="europe"></a>Europa

| Regio             | Adres verwijst |Huis cijfers | Naam van de straat niveau | Niveau plaats | Punten van belang zijn |
|-----------------------------------------------------|:---------------:|:--------------:|:------------:|:----------:|:------------------:|
| Albanië                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Andorra                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Armenië                                             |                 |                |              |      ✓     |          ✓         |
| Oostenrijk                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Azerbeidzjan                                          |                 |                |              |      ✓     |          ✓         |
| België                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Bosnië en Herzegovina                              |                 |                |       ✓      |      ✓     |          ✓         |
| Bulgarije                                            |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Belarus|                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Kroatië                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Cyprus                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Tsjechië                                      |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Denemarken                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Estland                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Faeröer                                       |                 |                |              |      ✓     |          ✓         |
| Finland                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Frankrijk                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Georgië                                             |                 |                |              |      ✓     |          ✓         |
| Duitsland                                             |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Gibralter                                           |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Griekenland                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Groenland                                           |                 |                |              |      ✓     |          ✓         |
| Guernsey                                            |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Hongarije                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| IJsland                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Ierland (Republiek)                               |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Isle Of Man                                         |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Italië                                               |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Jan Mayen                                           |        ✓        |                |              |      ✓     |          ✓         |
| Jersey                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Kazachstan                                          |        ✓        |                |       ✓      |      ✓     |          ✓         |
| Kosovo                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Kirgizië                                          |                 |                |              |      ✓     |          ✓         |
| Letland                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Liechtenstein                                       |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Litouwen                                           |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Luxemburg                                          |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Macedonië                                           |                 |                |       ✓      |      ✓     |          ✓         |
| Malta                                               |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Moldavië                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Monaco                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Montenegro                                          |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Nederland                                         |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Noorwegen                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Polen                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Portugal                                            |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Roemenië                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Russische Federatie                                  |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| San Marino                                          |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Servië                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Slowakije                                            |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Slovenië                                            |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Spanje                                               |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Spitsbergen                                            |        ✓        |                |       ✓      |      ✓     |          ✓         |
| Zweden                                              |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Zwitserland                                         |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Tadzjikistan                                          |                 |                |              |      ✓     |          ✓         |
| Turkije                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Turkmenistan                                        |                 |                |              |      ✓     |          ✓         |
| Oekraïne                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Verenigd Koninkrijk                                      |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Oezbekistan                                          |                 |                |              |      ✓     |          ✓         |
| Vaticaanstad                                        |                 |                |       ✓      |      ✓     |          ✓         |


## <a name="middle-east-and-africa"></a>Midden-Oosten en Afrika

| Regio             | Adres verwijst |Huis cijfers | Naam van de straat niveau | Niveau plaats | Punten van belang zijn |
|-----------------------------------------------------|:---------------:|:--------------:|:------------:|:----------:|:------------------:|
| Afghanistan                                         |                 |                |              |      ✓     |          ✓         |
| Algerije                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Angola                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Bahrein                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Benin                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Botswana                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Bouveteiland                                       |                 |                |              |      ✓     |          ✓         |
| Burkina Faso                                        |                 |                |       ✓      |      ✓     |          ✓         |
| Burundi                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Kameroen                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Cabo Verde|                 |                |       ✓      |      ✓     |          ✓         |
| Centraal-Afrikaanse Republiek                            |                 |                |       ✓      |      ✓     |          ✓         |
| Tsjaad                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Congo-Brazzaville                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Ivoorkust                                       |                 |                |       ✓      |      ✓     |          ✓         |
| Congo (DRC)                        |                 |                |       ✓      |      ✓     |          ✓         |
| Djibouti                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Egypte                                               |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Equatoriaal-Guinea, Republiek                      |                 |                |       ✓      |      ✓     |          ✓         |
| Eritrea                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Ethiopië                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Franse Zuidelijke Gebieden|                 |                |              |      ✓     |          ✓         |
| Gabon                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Gambia                                              |                 |                |              |      ✓     |          ✓         |
| Ghana                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Guinee                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Guinea-Bissau                                       |                 |                |       ✓      |      ✓     |          ✓         |
| Iran                                                |                 |                |              |      ✓     |          ✓         |
| Irak                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Israël                                              |                 |                |              |      ✓     |          ✓         |
| Jordanië                                              |        ✓        |                |       ✓      |      ✓     |          ✓         |
| Kenia                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Koeweit                                              |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Libanon                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Lesotho                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Liberia                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Libië|                 |                |       ✓      |      ✓     |          ✓         |
| Madagascar                                          |                 |                |       ✓      |      ✓     |          ✓         |
| Malawi                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Maldiven |                 |                |              |      ✓     |          ✓         |
| Mali                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Marshalleilanden |                 |                |              |      ✓     |          ✓         |
| Mauretanië                                          |                 |                |       ✓      |      ✓     |          ✓         |
| Mauritius                                           |                 |                |       ✓      |      ✓     |          ✓         |
| Mayotte                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Marokko                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Mozambique                                          |                 |                |       ✓      |      ✓     |          ✓         |
| Myanmar                                             |                 |                |              |      ✓     |          ✓         |
| Namibië                                             |                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Niger                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Nigeria                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Oman                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Qatar                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Réunion|                 |        ✓       |       ✓      |      ✓     |          ✓         |
| Rwanda                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Sint-Helena                                        |                 |                |              |      ✓     |          ✓         |
| Saoedi-Arabië                                        |                 |                |       ✓      |      ✓     |          ✓         |
| Senegal                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Seychellen                                          |                 |                |       ✓      |      ✓     |          ✓         |
| Sierra Leone                                        |                 |                |       ✓      |      ✓     |          ✓         |
| Somalië                                             |                 |                |              |      ✓     |          ✓         |
| Zuid-Afrika                                        |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Zuid-Sudan                                         |                 |                |       ✓      |      ✓     |          ✓         |
| Soedan                                               |                 |                |       ✓      |      ✓     |          ✓         |
| Swaziland                                           |                 |                |       ✓      |      ✓     |          ✓         |
| Syrië                                               |                 |                |              |      ✓     |          ✓         |
| Sao Tomé en principe, Democratische Republiek       |                 |                |       ✓      |      ✓     |          ✓         |
| Tanzania                                            |                 |                |       ✓      |      ✓     |          ✓         |
| Togo                                                |                 |                |       ✓      |      ✓     |          ✓         |
| Tunesië                                             |                 |                |       ✓      |      ✓     |          ✓         |
| Oeganda                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Verenigde Arabische Emiraten                                |        ✓        |        ✓       |       ✓      |      ✓     |          ✓         |
| Westelijke Jordaanoever                                           |                 |                |              |      ✓     |          ✓         |
| Jemen                                               |                 |                |              |      ✓     |          ✓         |
| Zambia                                              |                 |                |       ✓      |      ✓     |          ✓         |
| Zimbabwe                                            |                 |                |       ✓      |      ✓     |          ✓         |



## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Azure Maps geocodering, de [zoeken](https://docs.microsoft.com/rest/api/maps/search) verwijzen naar pagina's.

Meer informatie over de [dekking gebieden voor de toewijzingen van het verkeer service](traffic-coverage.md). 

