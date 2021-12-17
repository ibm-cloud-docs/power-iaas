---

copyright:
  years: 2019, 2021

lastupdated: "2021-05-12"

keywords: connectivity, configuring network, direct link, classic infrastructure, power infrastructure, network, megaport, vxc, gre tunneling

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Configuring connectivity to {{site.data.keyword.powerSys_notm}}
{: #configuring-power}

You can configure your subnet to interact with the {{site.data.keyword.cloud}} after you establish [Direct Link connectivity](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). To get your IBM Cloud Direct Link connection to work, you need to perform some basic network configuration. For more information, see [Direct Link Connect for Power Systems Virtual Servers](/docs/direct-link?topic=direct-link-configure-ibm-cloud-direct-link). If you have two or more virtual machines (VMs), do not use an external IP for communication between them. You must use an internal IP.
{: shortdesc}

To connect directly to the {{site.data.keyword.powerSys_notm}} environment, see [Connecting directly to the {{site.data.keyword.powerSys_notm}} environment by using Megaport connectivity services](#connecting-megaport).
{: note}

## Connecting to the IBM Cloud classic environment
{: #connecting-classic}

You can use one of the following options to connect to the IBM Cloud classic environment. You can then use a secondary Direct Link connection to access the {{site.data.keyword.powerSys_notm}} environment. Your {{site.data.keyword.powerSys_notm}} private subnet cannot be in the `169.254.0.0/16`, or `224.0.0.0/4` ranges. These ranges are blocked. For more information, see [IBM Cloud IP Ranges](/docs/security-groups?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges).

You can use the `10.x.x.x` range if there is not a conflict with an {{site.data.keyword.cloud_notm}} backend `10.x.x.x` service. You must contact support if you'd like to use *NAT'ing* or IP aliasing to resolve the IP conflict. That being said, IBM does not recommend using the `10.x.x.x` range when you create a new network.
{: important}

### Using an SSL VPN with a jump server
{: #using-ssl-jump-server}

You can use the {{site.data.keyword.cloud_notm}} **SSL VPN service** to connect to your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use an {{site.data.keyword.cloud_notm}} virtual machine (VM) as a jump server to connect to your {{site.data.keyword.powerSysShort}} instance.

* This option is typically used to manage infrastructures and is not recommended for production workloads.
* Because VPN connections are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a jump server.
* See [Setting up an SSL VPN](/docs/iaas-vpn?topic=iaas-vpn-setup-ssl-vpn-connections) and [Ordering a Virtual Router Appliance](/docs/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

### Using an IPSec VPN and a VRA (customer implementation)
{: #using-ipsec-vpn-vra}

You can use your own **IPSec VPN** to connect to your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use a Direct Link Connect connection to connect to your {{site.data.keyword.powerSys_notm}} instance. You must use a [VRA](/docs/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra) as VPN connects are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance.

The IPSec VPN referenced here is not the one offered by IBM.
{: note}

You cannot use the same private subnet for both IBM Cloud Classic and {{site.data.keyword.powerSys_notm}} instances. These offerings are not colocated and their networks are not linked. You must order a Direct Link Connection.

### Using a Direct Link Connect connection and a VRA (customer implementation)
{: #using-dl-vra}

You can use a **Direct Link Connect connection and a VRA** to connect to your existing {{site.data.keyword.cloud_notm}} network. You must use a second Direct Link Connect connection to connect to the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Ordering IBM Cloud Direct Link Connect](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect).


## Connecting to the {{site.data.keyword.powerSys_notm}} environment
{: #connecting-power}

After you establish a connection to the IBM Cloud Classic environment, you must use a separate Direct Link Connect connection to connect to the {{site.data.keyword.powerSys_notm}} environment. You must use [Direct Link Connect](/docs/dl?topic=dl-dl-about) to connect to the {{site.data.keyword.powerSys_notm}} environment. This option provides high performance between the on-premises network and the {{site.data.keyword.powerSys_notm}} environment.

## Connecting directly to the {{site.data.keyword.powerSys_notm}} environment by using Megaport connectivity services
{: #connecting-megaport}

You can connect directly to the {{site.data.keyword.powerSys_notm}} environment by using **IBM {{site.data.keyword.powerSys_notm}} NNI Private Ports @ Megaport** connectivity services. Before you engage [Megaport](https://portal.megaport.com){: external} to procure the connection (VxC) to **{{site.data.keyword.powerSys_notm}} Port @ Megaport**, IBM provides a Service ID (VxC identifier). You must also open a [secondary ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support) against {{site.data.keyword.powerSys_notm}} to perform the network configuration. Remember to include the following pieces of information in your support ticket:

```text
Customer name and contact:
Customer account ID
Service ID (VxC Identifier):

Customer network subnet:
Customer router IP Address:
Power Systems Virtual Server customer network IP address:
Power Systems Virtual Server network ASN: 64999 for WDC04 and 64997 for DAL13
Customer Network ASN:

Customer subnets to be advertised:
Power Systems Virtual Server customer Private Network ID (1):
Power Systems Virtual Server customer Private Network ID (2):
Power Systems Virtual Server customer Private Network ID (3):
```
{: codeblock}

Megaport connectivity services are available in WDC04, DAL13, DAL12, LON06, TOR01, FRA05, SYD05, and OSA21 data centers.
{: important}

## Generic Routing Encapsulation (GRE) tunneling
{: #gre-tunneling}

You can optionally request a GRE tunnel configuration by adding the request to the {{site.data.keyword.powerSys_notm}} support case. The GRE capability is available on **IBM Power Virtual Server** Direct Link Connect only. This information applies when you are configuring GRE tunnels manually. If you are using Cloud connections, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-managing-cloud-connections#configure-gre-tunnel).

```text
GRE Tunnel Configuration Request:
Customer name:
Customer account ID:
GRE Tunnel source (Power VS) IP:
GRE Tunnel destination (IBM Cloud VRA) IP:
GRE Tunnel interface (Power VS) IP:
GRE Tunnel interface (IBM Cloud VRA) IP:
Private Networks to be routed over GRE:
Private Network ID (1):
Private Network ID (2):
Private Network ID (3):
```
{: codeblock}
