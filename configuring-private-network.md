---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-27"

keywords: configuring virtual machine, direct link connectivity, classic infrastructure, power infrastructure, network, Megaport, VxC, GRE tunneling

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Configuring IBM Power Systems Virtual Servers
{: #configuring-power}

You can configure your subnet to interact with the {{site.data.keyword.cloud}} after you establish [Direct Link connectivity](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). To get your IBM Cloud Direct Link connection to work, you need to perform some basic network configuration and set up Border Gateway Protocol (BGP). During the setup process, an IBM service representative works with you to enable your network to use the required Virtual Routing Function (VRF) capability. For more information, see [Configuring IBM Cloud Direct Link](/docs/direct-link?topic=direct-link-configure-ibm-cloud-direct-link).
{: shortdesc}

If you have two or more virtual machines (VMs), do not use an external IP for communication between them. You must use an internal IP.
{: note}

To connect directly to the IBM Cloud Power infrastructure, see [Connecting directly to the IBM Cloud Power infrastructure by using Megaport connectivity services](#connecting-megaport).

## Connecting to the IBM Cloud classic infrastructure
{: #connecting-classic}

You can use one of the following options to connect to the IBM Cloud classic infrastructure:

  You can use the `10.x.x.x` range if there is not a conflict with an {{site.data.keyword.cloud_notm}} backend `10.x.x.x` service. You must contact support if you'd like to use *NAT'ing* or IP aliasing to resolve the IP conflict. That being said, IBM does not recommend using the `10.x.x.x` range when you start a new network.
  {: important}

Your Power private subnet cannot be in the `169.254.0.0/16`, or `224.0.0.0/4` ranges. These ranges are blocked. For more information, see [IBM Cloud IP Ranges](/docs/security-groups?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges).

**Using an SSL VPN with a jump server and a VRA**

You can use the {{site.data.keyword.cloud_notm}} **SSL VPN service** to connect to your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use a {{site.data.keyword.cloud_notm}} virtual machine (VM) as a jump server to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connections are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a jump server.
* For more information, see [Setting up an SSL VPN](/docs/iaas-vpn?topic=iaas-vpn-setup-ssl-vpn-connections) and [Ordering a Virtual Router Appliance](/docs/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

**Using a VRA**

Inside the {{site.data.keyword.cloud_notm}} network, you can use the IBM Cloud VRA to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connects are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a VRA.

You cannot use the same private subnet for both IBM Cloud Classic and IBM Cloud Power instances. These offerings are not colocated and their networks are not linked. You must order a Direct Link Connection.
{: note}

**Using a IPSec VPN and a VRA (customer implementation)**

You can use your own IPSec VPN to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use the IBM Cloud VRA to connect to your {{site.data.keyword.powerSys_notm}} instance.

The IPSec VPN referenced here is not the one offered by IBM, but your own.
{: note}

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connects are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a [VRA](/docs/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

## Connecting to the IBM Cloud Power infrastructure
{: #connecting-power}

After you establish a connection to the IBM Cloud classic infrastructure, you must use a separate Direct Link connection to connect to the IBM Cloud Power infrastructure.

* You must use [Direct Link Connect](/docs/direct-link?topic=direct-link-about-ibm-cloud-direct-link#direct-link-connect-solution) to connect to the IBM Cloud Power infrastructure.
* This option provides high performance between the on-premises network and the IBM Cloud Power infrastructure.
* There are specific IP addresses that you cannot use with the Direct Link Connect service. For more information, see [Strict limitations on IP assignments](/docs/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).

## Connecting directly to the IBM Cloud Power infrastructure by using Megaport connectivity services
{: #connecting-megaport}

You can connect directly to the IBM Cloud Power infrastructure by using **IBM Cloud Power NNI Private Ports @ Megaport** connectivity services. Before you engage [Megaport](https://portal.megaport.com){: new_window}{: external} directly to procure the connection (VxC) to **IBM Cloud Power Port @ Megaport**, IBM provides a Service ID (VxC identifier). You must also open a [secondary ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support) with IBM Power to perform the network configuration. Remember to include the following pieces of information in your support ticket:

```
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

## Generic Routing Encapsulation (GRE) tunneling
{: #gre-tunneling}

{{site.data.keyword.powerSysShort}} provides GRE tunneling to customers in the Frankfurt 1 (*FRA04*), Frankfurt 2 (*FRA05*), and London 3 (*LON06*) data centers. Customers can optionally request a GRE tunnel configuration by adding the request to their {{site.data.keyword.powerSys_notm}} support case.

```
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

<!-- ### Using IBM Direct Link Connect via Megaport to connect to the IBM Cloud Power environment
{: creating-connect-vxc}

You can connect to the IBM Cloud Classic and Power infrastructures by using **Direct Link Connect** by using Megaport. To begin, complete the steps in [Direct Link Connect for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). After you read the *Master Service Agreement* and create your Direct Link, copy the IBM Cloud ticket number.

When connecting to the IBM Cloud Power infrastructure by using a Direct Link by using Megaport, the Virtual Cross Connect (VXC) forms the layer 2 component of the connection. Layer 3 BGP connectivity is established directly between the customer and IBM Cloud.

The benefit to creating IBM Direct Link by using Megaport:

* Reduced latency, increased availability
* Reduce data egress cost
* Secure connectivity

### Deploying a VXC
{: deploying-vxc}

For more information, see [IBM Cloud Direct Link Connect](https://knowledgebase.megaport.com/cloud-connectivity/ibm-cloud-direct-link-connect/){: new_window}{: external}.

1. Open the [Megaport Portal](https://portal.megaport.com){: new_window}{: external}.

2. Create an IBM Direct Link Connect Virtual Cross Connect (VXC). Provision a VXC in the Portal to your chosen IBM Direct Link Connect peering location. To create an IBM Direct Link VXC in the Portal, click **+Connection** on the Megaport to which you want to attach your VXC.

3. Next, select the **Cloud** tile.

4. Type **IBM** into the **Select Provider** search box and select the IBM Direct Link location where the peer will be set up with IBM Cloud. This matches the peer location selected in the IBM Cloud console. Click **Next**.

    1. Paste the IBM Cloud ticket number in the **Name your connection** field.
    2. *(Optional)* Note an **Invoice Reference** internal to your records.
    3. Choose a **Rate Limit** speed in 1 Mbps increments up to the Megaport rate size. In most cases, customers choose to match the port speed created in the IBM Cloud console.
    4. The VLAN for this connection that you will receive via the Megaport. This must be a unique VLAN ID on this port. You can also click the toggle to **untag** this VXC. This removes the VLAN tagging for this connection but limits the port to only one VXC.

5. Click **Next** and add the VXC. You can then proceed through the checkout process. IBM will verify the IBM Cloud Ticket number and send you a */30* or */31* Private IP to provision for BGP.

6. See [Configure IBM Cloud Direct Link](https://cloud.ibm.com/docs/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#configure-ibm-cloud-direct-link) to complete your private connection to your IBM Cloud environment. -->
