---
title: Informatie over VPN-apparaten voor verbinding met site-naar-site-VPN-gateways voor Azure Virtual Network| Microsoft Docs
description: Dit artikel gaat over VPN-apparaten en IPSec-parameters voor S2S VPN Gateway-verbindingen en bevat koppelingen naar configuratie-instructies en voorbeelden.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: ''
tags: azure-resource-manager, azure-service-management

ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/13/2016
ms.author: yushwang;cherylmc

---
# Informatie over VPN-apparaten voor verbinding met site-naar-site-VPN-gateways
U hebt een VPN-apparaat nodig om een S2S-VPN-verbinding (site-naar-site) te configureren. S2S-verbindingen kunnen worden gebruikt om een hybride oplossing te maken of wanneer u een beveiligde verbinding wilt maken tussen uw on-premises netwerk en het virtuele netwerk. In dit artikel komen compatibele VPN-apparaten en configuratieparameters aan bod. 

> [!NOTE]
> Wanneer u een S2S-verbinding configureert, hebt u een openbaar IPv4-adres voor het VPN-apparaat nodig.                                                                                                                                                                               
> 
> 

Zie het gedeelte [Niet-gevalideerde VPN-apparaten](#additionaldevices) als het apparaat niet voorkomt in de tabel [Gevalideerde VPN-apparaten](#devicetable) van dit artikel. Het is mogelijk dat het apparaat toch werkt met Azure. Voor ondersteuning van VPN-apparaten neemt u contact op met de fabrikant van uw apparaat.

**Waar u op moet letten wanneer u de tabellen bekijkt:**

* Er is een terminologiewijziging voor statische en dynamische routering. Waarschijnlijk komt u beide termen tegen. Er is geen wijziging in functionaliteit, alleen de benaming is veranderd.
  * Statische routering = PolicyBased
  * Dynamische routering = RouteBased
* De specificaties voor een VPN-gateway met hoge prestaties en een RouteBased VPN-gateway zijn hetzelfde, tenzij anders wordt vermeld. Zo zijn de gevalideerde VPN-apparaten die compatibel zijn met RouteBased VPN-gateways ook compatibel met de Azure VPN-gateway met hoge prestaties. 

## <a name="devicetable"></a>Gevalideerde VPN-apparaten
We hebben samen met apparaatleveranciers een reeks standaard VPN-apparaten gevalideerd. Alle apparaten in de apparaatfamilies die in onderstaande lijst zijn opgenomen, kunnen met Azure VPN-gateways worden gebruikt. Zie [VPN-gateways](vpn-gateway-about-vpngateways.md) om het type gateway te verifiëren dat u moet maken voor de oplossing die u wilt configureren. 

Voor hulp bij de configuratie van uw VPN-apparaat, raadpleegt u de koppelingen die overeenkomen met de betreffende apparaatstuurprogrammafamilie. Voor ondersteuning van VPN-apparaten neemt u contact op met de fabrikant van uw apparaat.

| **Leverancier** | **Apparaatfamilie** | **Minimale versie van het besturingssysteem** | **PolicyBased** | **RouteBased** |
| --- | --- | --- | --- | --- |
| Allied Telesis |VPN-routers uit AR-serie |2.9.2 |Binnenkort beschikbaar |Niet compatibel |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall F-serie |PolicyBased: 5.4.3, RouteBased: 6.2.0 |[Configuratie-instructies](https://techlib.barracuda.com/NGF/AzurePolicyBasedVPNGW) |[Configuratie-instructies](https://techlib.barracuda.com/NGF/AzureRouteBasedVPNGW) |
| Barracuda Networks, Inc. |Barracuda NextGen Firewall X-serie |Barracuda Firewall 6.5 |[Barracuda Firewall](https://techlib.barracuda.com/BFW/ConfigAzureVPNGateway) |Niet compatibel |
| Brocade |Vyatta 5400 vRouter |Virtual Router 6.6R3 GA |[Configuratie-instructies](http://www1.brocade.com/downloads/documents/html_product_manuals/vyatta/vyatta_5400_manual/wwhelp/wwhimpl/js/html/wwhelp.htm#href=VPN_Site-to-Site%20IPsec%20VPN/Preface.1.1.html) |Niet compatibel |
| Check Point |Security Gateway |R75.40, R75.40VS |[Configuratie-instructies](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |[Configuratie-instructies](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk101275) |
| Cisco |ASA |8.3 |[Cisco-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASA) |Niet compatibel |
| Cisco |ASR |iOS 15.1 (PolicyBased), iOS 15.2 (RouteBased) |[Cisco-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |[Cisco-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ASR) |
| Cisco |ISR |iOS 15.0 (PolicyBased), iOS 15.1 (RouteBased*) |[Cisco-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |[Cisco-voorbeelden*](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Cisco/Current/ISR) |
| Citrix |NetScaler MPX, SDX, VPX |10.1 en hoger |[Integratie-instructies](https://docs.citrix.com/en-us/netscaler/11-1/system/cloudbridge-connector-introduction/cloudbridge-connector-azure.html) |Niet compatibel |
| Dell SonicWALL |TZ-serie, NSA-serie, SuperMassive-serie, e-klasse van NSA-serie |SonicOS 5.8.x, [SonicOS 5.9.x](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide/supported-platforms?ParentProduct=850), [SonicOS 6.x](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide/supported-platforms?ParentProduct=646) |[Instructies - SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646) [Instructies - SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |[Instructies - SonicOS 6.2](http://documents.software.dell.com/sonicos/6.2/microsoft-azure-configuration-guide?ParentProduct=646) [Instructies - SonicOS 5.9](http://documents.software.dell.com/sonicos/5.9/microsoft-azure-configuration-guide?ParentProduct=850) |
| F5 |BIG-IP-serie |12.0 |[Configuratie-instructies](https://devcentral.f5.com/articles/connecting-to-windows-azure-with-the-big-ip) |[Configuratie-instructies](https://devcentral.f5.com/articles/big-ip-to-azure-dynamic-ipsec-tunneling) |
| Fortinet |FortiGate |FortiOS 5.2.7 |[Configuratie-instructies](http://docs.fortinet.com/d/fortigate-configuring-ipsec-vpn-between-a-fortigate-and-microsoft-azure) |[Configuratie-instructies](http://docs.fortinet.com/d/fortigate-configuring-ipsec-vpn-between-a-fortigate-and-microsoft-azure) |
| Internet Initiative Japan (IIJ) |SEIL-serie |SEIL/X 4.60, SEIL/B1 4.60, SEIL/x86 3.20 |[Configuratie-instructies](http://www.iij.ad.jp/biz/seil/ConfigAzureSEILVPN.pdf) |Niet compatibel |
| Juniper |SRX |JunOS 10.2 (PolicyBased), JunOS 11.4 (RouteBased) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SRX) |
| Juniper |J-serie |JunOS 10.4r9 (PolicyBased), JunOS 11.4 (RouteBased) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/JSeries) |
| Juniper |ISG |ScreenOS 6.3 (PolicyBased en RouteBased) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/ISG) |
| Juniper |SSG |ScreenOS 6.2 (PolicyBased en RouteBased) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |[Juniper-voorbeelden](https://github.com/Azure/Azure-vpn-config-samples/tree/master/Juniper/Current/SSG) |
| Microsoft |Routering en Remote Access-Service |Windows Server 2012 |Niet compatibel |[Microsoft-voorbeelden](http://go.microsoft.com/fwlink/p/?LinkId=717761) |
| Open Systems AG |Mission Control Security Gateway |N.v.t. |[Installatiehandleiding](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |[Installatiehandleiding](https://www.open.ch/_pdf/Azure/AzureVPNSetup_Installation_Guide.pdf) |
| Openswan |Openswan |2.6.32 |(binnenkort beschikbaar) |Niet compatibel |
| Palo Alto Networks |Alle apparaten waarop PAN-OS wordt uitgevoerd |PAN-OS 6.1.5 of hoger (PolicyBased), PAN-OS 7.0.5 of hoger (RouteBased) |[Configuratie-instructies](https://live.paloaltonetworks.com/t5/Configuration-Articles/How-to-Configure-VPN-Tunnel-Between-a-Palo-Alto-Networks/ta-p/59065) |[Configuratie-instructies](https://live.paloaltonetworks.com/t5/Integration-Articles/Configuring-IKEv2-VPN-for-Microsoft-Azure-Environment/ta-p/60340) |
| Watchguard |Alle |Fireware XTM v11.x |[Configuratie-instructies](http://customers.watchguard.com/articles/Article/Configure-a-VPN-connection-to-a-Windows-Azure-virtual-network/) |Niet compatibel |

(*) Routers uit de ISR 7200-serie bieden alleen ondersteuning voor PolicyBased VPN-verbindingen.

## <a name="additionaldevices"></a>Niet-gevalideerde VPN-apparaten
Als uw apparaat niet in de tabel met gevalideerde VPN-apparaten wordt vermeld, werkt het misschien toch met een site-naar-site-verbinding. Controleer of uw VPN-apparaat voldoet aan de minimale vereisten die worden beschreven in de sectie Gatewayvereisten van het artikel [About VPN Gateways](vpn-gateway-about-vpngateways.md#gateway-requirements) (Over VPN-gateways). Apparaten die voldoen aan de minimumvereisten zouden ook met VPN-gateways moeten werken. Neem contact op met de fabrikant van uw apparaat voor aanvullende ondersteuning en configuratie-instructies.

## Voorbeelden van het bewerken van apparaatconfiguraties
Nadat u het bij het VPN-apparaat meegeleverde configuratievoorbeeld hebt gedownload, moet u enkele waarden veranderen zodat ze overeenkomen met de instellingen voor uw omgeving. 

**U bewerkt een voorbeeld als volgt:**

1. Open het voorbeeld met Kladblok. 
2. Zoek alle <*tekst*>-tekenreeksen en vervang ze door de waarden die betrekking hebben op uw omgeving. Zorg dat u < en > opneemt. Als u een naam opgeeft, moet deze uniek zijn. Als een opdracht niet werkt, raadpleeg dan de documentatie van de fabrikant van uw apparaat.

| **Voorbeeldtekst** | **Wijzig in** |
| --- | --- |
| &lt;RP_OnPremisesNetwork&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myOnPremisesNetwork |
| &lt;RP_AzureNetwork&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myAzureNetwork |
| &lt;RP_AccessList&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myAzureAccessList |
| &lt;RP_IPSecTransformSet&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myIPSecTransformSet |
| &lt;RP_IPSecCryptoMap&gt; |De naam die u voor dit object hebt gekozen. Voorbeeld: myIPSecCryptoMap |
| &lt;SP_AzureNetworkIpRange&gt; |Geef het bereik op. Voorbeeld: 192.168.0.0 |
| &lt;SP_AzureNetworkSubnetMask&gt; |Geef het subnetmasker op. Voorbeeld: 255.255.0.0 |
| &lt;SP_OnPremisesNetworkIpRange&gt; |Geef het on-premises bereik op. Voorbeeld: 10.2.1.0 |
| &lt;SP_OnPremisesNetworkSubnetMask&gt; |Geef het on-premises subnetmasker op. Voorbeeld: 255.255.255.0 |
| &lt;SP_AzureGatewayIpAddress&gt; |Deze informatie is specifiek voor uw virtuele netwerk en u vindt deze in de beheerportal als **IP-adres van gateway**. |
| &lt;SP_PresharedKey&gt; |Deze informatie is specifiek voor uw virtuele netwerk en u vindt deze in de beheerportal onder Sleutel beheren. |

## IPsec-parameters
> [!NOTE]
> Hoewel de waarden in de volgende tabel worden ondersteund door de Azure VPN-gateway, is er momenteel geen enkele manier waarop u vanuit de Azure VPN-gateway een specifieke combinatie kunt opgeven of selecteren. U moet eventuele beperkingen vanuit het on-premises VPN-apparaat opgeven. Bovendien moet u MSS vastzetten op 1350.
> 
> 

### Configuratie IKE fase 1
| **Eigenschap** | **PolicyBased** | **RouteBased en standaard VPN-gateway of VPN-gateway met hoge prestaties** |
| --- | --- | --- |
| IKE-versie |IKEv1 |IKEv2 |
| Diffie-Hellman-groep |Groep 2 (1024 bits) |Groep 2 (1024 bits) |
| Verificatiemethode |Vooraf gedeelde sleutel |Vooraf gedeelde sleutel |
| Versleutelingsalgoritmen |AES256 AES128 3DES |AES256 3DES |
| Hash-algoritme |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Levensduur (tijd) van beveiligingskoppeling (SA) fase 1 |28.800 seconden |10.800 seconden |

### Configuratie IKE fase 2
| **Eigenschap** | **PolicyBased** | **RouteBased en standaard VPN-gateway of VPN-gateway met hoge prestaties** |
| --- | --- | --- |
| IKE-versie |IKEv1 |IKEv2 |
| Hash-algoritme |SHA1(SHA128) |SHA1(SHA128) |
| Levensduur beveiligingskoppeling (SA) fase 2 (tijd) |3.600 seconden |3.600 seconden |
| Levensduur beveiligingskoppeling (SA) fase 2 (doorvoer) |102.400.000 kB |- |
| IPSec-SA-codering en -verificatieaanbiedingen (in volgorde van voorkeur) |1. ESP-AES256 2. ESP-AES128 3. ESP-3DES 4. N.v.t. |Zie *Aanbiedingen voor IPsec-beveiligingskoppelingen (SA) voor RouteBased gateways* (hieronder) |
| Perfect Forward Secrecy (PFS) |Nee |Nee (*) |
| Dead Peer Detection |Niet ondersteund |Ondersteund |

(*) Azure Gateway als IKE-responder accepteert PFS DH-groep 1, 2, 5, 14, 24.

### Aanbiedingen voor IPsec-beveiligingskoppelingen (SA) voor RouteBased gateways
In de volgende tabel staan aanbiedingen voor IPSec-SA-versleuteling en -verificatie. De aanbiedingen staan in volgorde van voorkeur waarin de aanbieding is gepresenteerd of geaccepteerd.

| **Aanbiedingen voor IPSec-SA-codering en -verificatie** | **Azure-gateway als initiator** | **Azure-Gateway als antwoorder** |
| --- | --- | --- |
| 1 |ESP AES_256 SHA |ESP AES_128 SHA |
| 2 |ESP AES_128 SHA |ESP 3_DES MD5 |
| 3 |ESP 3_DES MD5 |ESP 3_DES SHA |
| 4 |ESP 3_DES SHA |AH SHA1 met ESP AES_128, null HMAC |
| 5 |AH SHA1 met ESP AES_256, null HMAC |AH SHA1 met ESP 3_DES, null HMAC |
| 6 |AH SHA1 met ESP AES_128, null HMAC |AH MD5 met ESP 3_DES, met null HMAC, geen voorgestelde levensduur |
| 7 |AH SHA1 met ESP 3_DES, null HMAC |AH-SHA1 met ESP 3_DES SHA1, geen levensduur |
| 8 |AH MD5 met ESP 3_DES, met null HMAC, geen voorgestelde levensduur |AH MD5 met ESP 3_DES MD5, geen levensduur |
| 9 |AH-SHA1 met ESP 3_DES SHA1, geen levensduur |ESP DES MD5 |
| 10 |AH MD5 met ESP 3_DES MD5, geen levensduur |ESP DES SHA1, geen levensduur |
| 11 |ESP DES MD5 |AH SHA1 met ESP DES, null HMAC, geen voorgestelde levensduur |
| 12 |ESP DES SHA1, geen levensduur |AH MD5 met ESP DES, null HMAC, geen voorgestelde levensduur |
| 13 |AH SHA1 met ESP DES, null HMAC, geen voorgestelde levensduur |AH SHA1 met ESP DES SHA1, geen levensduur |
| 14 |AH MD5 met ESP DES, null HMAC, geen voorgestelde levensduur |AH MD5 met ESP DES MD5, geen levensduur |
| 15 |AH SHA1 met ESP DES SHA1, geen levensduur |ESP SHA, geen levensduur |
| 16 |AH MD5 met ESP DES MD5, geen levensduur |ESP MD5, geen levensduur |
| 17 |- |AH SHA, geen levensduur |
| 18 |- |AH MD5, geen levensduur |

* U kunt IPsec ESP NULL-versleuteling opgeven met RouteBased VPN-gateways en VPN-gateways met hoge prestaties. Op null gebaseerde versleuteling biedt geen beveiliging voor gegevens tijdens de overdracht. Dit mag alleen worden gebruikt wanneer maximale doorvoer en minimale latentie zijn vereist.  Clients kunnen ervoor kiezen dit te gebruiken voor communicatie tussen VNET's of wanneer elders in de oplossing versleuteling wordt toegepast.
* Gebruik voor cross-premises connectiviteit via internet de standaardinstellingen voor Azure VPN-gateways met versleuteling en hash-algoritmen die in de tabel hierboven worden vermeld, om beveiliging van uw kritieke communicatie te waarborgen.

<!--HONumber=Sep16_HO3-->


