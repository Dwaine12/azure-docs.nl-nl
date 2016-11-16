---
title: Overzicht van Azure Virtual Network (VNET)
description: Meer informatie over virtuele netwerken (VNEt&quot;s) in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: e08966567a8545c1b37ec856f836b976b5a9ab2a


---
# <a name="virtual-network-overview"></a>Overzicht van Virtual Network
Een virtueel Azure-netwerk (VNET) is een weergave van uw eigen netwerk in de cloud.  Het is een logische isolatie van de Azure-cloud die is toegewezen aan uw abonnement. U kunt de IP-adresblokken, DNS-instellingen, beveiligingsbeleidsregels en routetabellen binnen dit netwerk volledig beheren. U kunt uw VNET ook verder segmenteren in subnetten en Azure IaaS virtuele machines (VM's) en/of [Cloudservices (PaaS-rolexemplaren)](../cloud-services/cloud-services-choose-me.md). Hiermee kunt u het virtuele netwerk via een van de beschikbare [verbindingsopties](../vpn-gateway/vpn-gateway-about-vpngateways.md#site-to-site-and-multi-site) in Azure verbinden met uw on-premises netwerk. In wezen kunt u uw netwerk uitbreiden naar Azure met behoud van de volledige controle over IP-adresblokken en de schaalvoordelen van Azure voor ondernemingen.

Zie de onderstaande afbeelding van een vereenvoudigd on-premises netwerk om meer inzicht te krijgen in VNET's.

![On-premises netwerk](./media/virtual-networks-overview/figure01.png)

In de bovenstaande afbeelding ziet u een on-premises netwerk dat is verbonden met internet via een router. U ziet ook een firewall tussen de router en een DMZ die fungeert als host voor een DNS-server en een webserverfarm. In de webserverfarm worden taken verdeeld met load balancer-hardware die wordt blootgesteld aan internet en bronnen van het interne subnet gebruikt. Het interne subnet is van de DMZ gescheiden met een andere firewall en fungeert als host voor Active Directory-domeincontrollerservers, databaseservers en toepassingsservers.

Hetzelfde netwerk kan worden gehost in Azure, zoals wordt weergegeven in de afbeelding hieronder.

![Azure Virtual Network](./media/virtual-networks-overview/figure02.png)

Zie hoe de Azure-infrastructuur de rol van de router overneemt en zo de toegang van uw VNET tot internet regelt zonder dat u iets hoeft te configureren. Firewalls kunnen worden vervangen door netwerkbeveiligingsgroepen (NSG's, Network Security Groups) die worden toegepast op elk afzonderlijk subnet. En fysieke load balancers worden vervangen door internetgerichte en interne load balancers in Azure.

> [!NOTE]
> Er zijn twee implementatiemodi in Azure: de klassieke modus (ook wel bekend als Service Management) en Azure Resource Manager (ARM). Klassieke VNET's kunnen worden toegevoegd aan een affiniteitsgroep of worden gemaakt als een regionaal VNET. Als u een VNET in een affiniteitsgroep hebt, wordt u aangeraden om het te [migreren naar een regionaal VNET](virtual-networks-migrate-to-regional-vnet.md).
> 
> 

## <a name="virtual-network-benefits"></a>Voordelen van Virtual Network
* **Isolatie**. VNET's zijn volledig geïsoleerd van elkaar. Hierdoor kunt u onafhankelijke netwerken met dezelfde CIDR-adresblokken maken voor ontwikkeling, testen en productie.
* **Toegang tot internet**. Alle IaaS virtuele machines en PaaS-rolexemplaren in een VNET hebben standaard toegang tot internet. U kunt de toegang beheren met behulp van netwerkbeveiligingsgroepen (NSG's).
* **Toegang tot VM's binnen het VNET**. PaaS-rolexemplaren en IaaS VM's kunnen worden gestart in hetzelfde virtuele netwerk en met elkaar verbinding maken via privé-IP-adressen, zelfs als ze zich in verschillende subnetten bevinden. U hoeft hiervoor geen gateway te configureren of openbare IP-adressen te gebruiken.
* **Naamomzetting**. Azure bevat functionaliteit voor interne naamomzetting voor IaaS VM's en PaaS-rolexemplaren die in uw VNET zijn geïmplementeerd. U kunt ook uw eigen DNS-servers implementeren en het VNET daarvoor configureren.
* **Beveiliging**. Binnenkomend en uitgaand verkeer van de virtuele machines en PaaS-rolexemplaren in een VNET kan worden beheerd met behulp van netwerkbeveiligingsgroepen.
* **Connectiviteit**. VNets kunnen met elkaar worden verbonden met netwerkgateways of via VNet-peering. VNets kunnen worden verbonden met on-premises datacenters via site-naar-site-VPN-netwerken of Azure ExpressRoute. Ga naar [Informatie over VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md#site-to-site-and-multi-site) voor meer informatie over site-naar-site-VPN-connectiviteit. Ga naar [Technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) voor meer informatie over ExpressRoute. Ga naar [VNet-peering](virtual-network-peering-overview.md) voor meer informatie over VNet-peering.
  
  > [!NOTE]
  > Maak een VNET voordat u IaaS VM's of PaaS-rolexemplaren implementeert in uw Azure-omgeving. Voor VM's op basis van ARM is een VNET vereist. Als u geen bestaand VNET opgeeft, wordt in Azure een standaard-VNET gemaakt met een CIDR-adresblok dat mogelijk conflicteert met uw on-premises netwerk. In dat geval kunt u uw VNET niet verbinden met uw on-premises netwerk.
  > 
  > 

## <a name="subnets"></a>Subnetten
Een subnet is een bereik met IP-adressen in het VNET. U kunt u een VNET onderverdelen in meerdere subnetten voor organisatie- en beveiligingsdoeleinden. Tussen VM's en PaaS-rolexemplaren die in (dezelfde of verschillende) subnetten in een VNET zijn geïmplementeerd, is communicatie mogelijk zonder extra configuratie. U kunt ook routetabellen en NSG's configureren voor een subnet.

## <a name="ip-addresses"></a>IP-adressen
Er kunnen twee soorten IP-adressen worden toegewezen aan bronnen in Azure: *openbare* en *privé* IP-adressen. Openbare IP-adressen worden gebruikt om Azure-bronnen te laten communiceren met internet en andere openbare Azure-services, zoals [Azure Redis Cache](https://azure.microsoft.com/services/cache/) en [Azure Event Hubs](https://azure.microsoft.com/documentation/services/event-hubs/). Privé IP-adressen worden gebruikt voor communicatie tussen bronnen in een virtueel netwerk, samen met bronnen die verbonden zijn via een VPN, zonder gebruik te maken van via internet routeerbare IP-adressen.

Ga naar [IP-adressen in het virtuele netwerk](virtual-network-ip-addresses-overview-arm.md) voor meer informatie over IP-adressen in Azure

## <a name="azure-load-balancers"></a>Azure load balancers
Virtuele machines en cloudservices in een virtueel netwerk kunnen worden blootgesteld aan internet met behulp van Azure load balancers. Voor interne bedrijfstoepassingen kan de taakverdeling worden uitgevoerd met interne load balancers.

* **Externe load balancer**. U kunt een externe load balancer gebruiken voor maximale beschikbaarheid van IaaS VM's en PaaS-rolexemplaren met toegang via internet.
* **Interne load balancer**. U kunt een interne load balancer gebruiken voor maximale beschikbaarheid van IaaS VM's en PaaS-rolexemplaren met toegang via andere services uw VNET.

Ga naar [Overzicht van Load balancer](../load-balancer/load-balancer-overview.md) voor meer informatie over taakverdeling en load balancers.

## <a name="network-security-group-nsg"></a>Netwerkbeveiligingsgroep (NSG)
U kunt NSG's maken voor het beheer van binnenkomende en uitgaande toegang tot netwerkinterfaces (NIC's), VM's en subnetten. Elke NSG bevat een of meer regels waarmee wordt bepaald of verkeer wordt goedgekeurd of afgewezen op basis van het bron-IP-adres, de bronpoort, het doel-IP-adres en de doelpoort. Ga naar [Wat is een netwerkbeveiligingsgroep](virtual-networks-nsg.md) voor meer informatie over NSG's.

## <a name="virtual-appliances"></a>Virtuele apparaten
Een virtueel apparaat is gewoon een virtuele machine in uw VNET met een softwarefunctie, zoals firewall, WAN-optimalisatie of inbraakdetectie. U kunt in Azure een route maken waarmee uw VNET-verkeer door een virtueel apparaat wordt geleid om gebruik te maken van de mogelijkheden van dat apparaat.

U kunt uw VNET bijvoorbeeld beveiligen met NSG's. Met NSG's wordt een toegangsbeheerlijst (ACL) van laag 4 toegepast op binnenkomende en uitgaande pakketten. Voor een beveiligingsmodel van laag 7 moet u een firewall-apparaat gebruiken.

Virtuele apparaten zijn afhankelijk van [door de gebruiker gedefinieerde routes en doorsturen via IP](virtual-networks-udr-overview.md).

## <a name="limits"></a>Limieten
Er gelden limieten voor het maximum aantal toegestane virtuele netwerken in een abonnement. Zie [Netwerklimieten in Azure](../azure-subscription-service-limits.md#networking-limits) voor meer informatie.

## <a name="pricing"></a>Prijzen
Er worden geen extra kosten in rekening gebracht voor het gebruik van virtuele netwerken in Azure. De Compute-exemplaren die binnen het VNET worden opgestart, worden in rekening gebracht tegen standaardtarieven zoals beschreven in [Prijzen van Azure VM](https://azure.microsoft.com/pricing/details/virtual-machines/). Ook de [VPN-gateways](https://azure.microsoft.com/pricing/details/vpn-gateway/) en [openbare IP-adressen](https://azure.microsoft.com/pricing/details/ip-addresses/) die in het VNET worden gebruikt, worden in rekening gebracht tegen standaardtarieven.

## <a name="next-steps"></a>Volgende stappen
* [Een VNET maken](virtual-networks-create-vnet-arm-pportal.md) en subnetten maken.
* [Een VM in een VNET maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md).
* Meer informatie over [NSG's](virtual-networks-nsg.md).
* Meer informatie over [door de gebruiker gedefinieerde routes en doorsturen via IP](virtual-networks-udr-overview.md).




<!--HONumber=Nov16_HO2-->


