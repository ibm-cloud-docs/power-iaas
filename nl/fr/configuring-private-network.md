---

copyright:
  years: 2019

lastupdated: "2019-07-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Configuration de Power Systems Virtual Servers avec un réseau privé
{: #cpn-configuring}

Vous pouvez utiliser un réseau privé avec {{site.data.keyword.powerSysFull}} pour vous connecter en toute sécurité à votre environnement sur site avec l'environnement {{site.data.keyword.cloud_notm}} hors site. Dans un réseau privé, vous pouvez accéder aux ressources {{site.data.keyword.cloud_notm}} et effectuer l'interconnexion avec d'autres serveurs virtuels.
{:shortdesc}

Vous pouvez utiliser l'une des options suivantes pour créer un réseau privé qui connecte votre environnement sur site à l'environnement {{site.data.keyword.cloud_notm}} :

1. **{{site.data.keyword.cloud_notm}} SSL VPN avec serveur intermédiaire**
   * Vous pouvez utiliser le service {{site.data.keyword.cloud_notm}} SSL VPN pour vous connecter à votre réseau {{site.data.keyword.cloud_notm}} existant. Dans le réseau {{site.data.keyword.cloud_notm}}, vous pouvez utiliser une machine virtuelle (VM) {{site.data.keyword.cloud_notm}} comme serveur intermédiaire pour vous connecter à votre instance {{site.data.keyword.powerSys_notm}}.
   * Vous devez utiliser un serveur intermédiaire car vous ne pouvez pas utiliser une connexion VPN pour vous connecter directement à l'instance {{site.data.keyword.powerSys_notm}}.
   * Cette option est utilisée en principe pour gérer vos environnements. Elle n'est pas recommandée pour les charges de travail en environnement de production.
   * Pour savoir comment configurer cette option, voir [Configuration de connexions VPN SSL](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) et [Commande d'un dispositif Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

2. **{{site.data.keyword.cloud_notm}} IPSec VPN avec IBM Cloud Virtual Router Appliance**
   * Vous pouvez utiliser le service {{site.data.keyword.cloud_notm}} IPSec VPN pour vous connecter à votre réseau {{site.data.keyword.cloud_notm}} existant. Dans le réseau {{site.data.keyword.cloud_notm}}, vous pouvez utiliser IBM Cloud Virtual Router Appliance (VRA) pour vous connecter à votre instance {{site.data.keyword.powerSys_notm}}.
   * Vous devez utiliser un dispositif de routeur virtuel (VRA) car vous ne pouvez pas utiliser une connexion VPN pour vous connecter directement à l'instance {{site.data.keyword.powerSys_notm}}.
   * Cette option est utilisée en principe pour gérer vos environnements. Elle n'est pas recommandée pour les charges de travail en environnement de production.
   * Pour plus d'informations sur la configuration de cette option, voir [Configuration d'un VPN IPSec](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) et [Commande d'un dispositif Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

3. **Direct Link Connect avec IBM Cloud Virtual Router Appliance**
   * Vous pouvez commander le service Direct Link Connect auprès d'IBM qui connecte votre réseau sur site au réseau IBM Cloud à l'aide d'IBM Cloud Virtual Router Appliance (VRA).
   * Cette option offre de hautes performances entre le réseau sur site et le réseau IBM Cloud.
   * Pour commander un service Direct Link Connect, suivez les étapes indiquées dans la rubrique [Commande d'IBM Cloud Direct Link Connect à partir de la console de l'interface utilisateur](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).
   * Il existe des adresses IP spécifiques que vous ne pouvez pas utiliser avec un service Direct Link Connect. Pour plus d'informations, voir [Limitations strictes pour les affectations d'adresse IP](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
