---

copyright:
  years: 2019

lastupdated: "2019-10-18"

keywords: configuring virtual machine, direct link connectivity, classic infrastructure, power infrastructure, network

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

You can configure your subnet to interact with the {{site.data.keyword.cloud}} after you establish [Direct Link connectivity](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect). To get your IBM Cloud Direct Link connection to work, you need to perform some basic network configuration and set up Border Gateway Protocol (BGP). During the setup process, an IBM service representative works with you to enable your network to use the required Virtual Routing Function (VRF) capability. For more information, see [Configuring IBM Cloud Direct Link](https://cloud.ibm.com/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link).
{: shortdesc}

If you have two or more virtual machines (VMs), do not use an external IP for communication between them. You must use an internal IP.
{: note}

## Connecting to the IBM Cloud classic infrastructure
{: #connecting-classic}

You can use one of the following options to connect to the IBM Cloud classic infrastructure:

  You can use the `10.x.x.x` range as long as there is no conflict with an {{site.data.keyword.cloud_notm}} backend `10.x.x.x` service. You must reach out to support if you'd like to use NAT'ing or IP aliasing to resolve the IP conflict. IBM recommends that you not use `10.x.x.x` when starting a new network. Your Power private subnet cannot be in the `169.254.0.0/16`, or `224.0.0.0/4` ranges. These ranges are blocked. For more information, see [IBM Cloud IP Ranges](/docs/infrastructure/security-groups?topic=hardware-firewall-dedicated-ibm-cloud-ip-ranges).
  {: important}

**Using an SSL VPN with a jump server and a VRA**

You can use the {{site.data.keyword.cloud_notm}} **SSL VPN service** to connect to your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use a {{site.data.keyword.cloud_notm}} virtual machine (VM) as a jump server to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connections are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a jump server.
* For more information, see [Setting up an SSL VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

**Using a IPSec VPN and a VRA**

You can use the {{site.data.keyword.cloud_notm}} **IPSec VPN service** to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use the IBM Cloud VRA to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connects are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a VRA.
* For more information, see [Setting up a IPSec VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

You cannot use the same private subnet for both IBM Cloud Classic and IBM Cloud Power instances. These offerings are not colocated and their networks are not linked. You must order a Direct Link Connection.
{: important}

## Connecting to the IBM Cloud Power infrastructure
{: #connecting-power}

After you establish a connection to the IBM Cloud classic infrastructure, you must use a separate Direct Link connection to connect to the IBM Cloud Power infrastructure.

* You can choose from several Direct Link Connect services to connect to the IBM Cloud Power infrastructure. For more information, see [Direct Link connectivity](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).
* This option provides high performance between the on-premises network and the IBM Cloud Power infrastructure.
* There are specific IP addresses that you cannot use with a Direct Link Connect service. For more information, see [Strict limitations on IP assignments](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).

## Using Megaport to directly connect to the IBM Cloud Power infrastructure
{: #cpn-connect-megaport}

You can connect directly to the IBM Cloud Power infrastructure through [Megaport](https://www.megaport.com/services/ibm-cloud/){: new_window}{: external} exchange. You must engage Megaport directly to procure the bandwidth. You must also open a secondary ticket with IBM Power to perform the connection.

When connecting to the IBM Cloud Power infrastucture by using a Direct Link with Megaport, the Virtual Cross Connect (VXC) forms the layer 2 component of the connection. Layer 3 BGP connectivity is established directly between the customer and IBM Cloud.

The benefit to creating IBM Direct Link by using Megaport:

* Reduced latency, increased availability
* Reduce data egress cost
* Secure connectivity

### Creating an IBM Direct Link Connect Virtual Cross Conncect (VXC) by using the Megaport Portal
{: creating-connect-vxc}

To begin, complete the steps in [Direct Link Connect for Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect). After you read the *Master Service Agreement* and create your Direct Link, copy the IBM Cloud ticket number.

### Deploying VXC
{: deploying-vxc}

For more information on deploying a VXC, see [IBM Cloud Direct Link Connect](https://knowledgebase.megaport.com/cloud-connectivity/ibm-cloud-direct-link-connect/){: new_window}{: external}.

1. Open the [Megaport Portal](https://portal.megaport.com/login).

2. Create an IBM Direct Link Connect Virtual Cross Connect (VXC). Provision a VXC in the Portal to your chosen IBM Direct Link Connect peering location. To create an IBM Direct Link VXC in the Portal, click **+Connection** on the Megaport to which you want to attach your VXC.

3. Next, select **Cloud** tile.

4. Type **IBM** into the **Select Provider** search box and select the IBM Direct Link location where the peer will be set up with IBM Cloud. This matches the peer location selected in the IBM console. Click **Next**.

    1. Paste the IBM Cloud ticket number in the **Name your connection** field.
    2. *(Optional)* Note an **Invoice Reference** internal to your records.
    3. Choose a **Rate Limit** speed in 1 Mbps increments up to the Megaport rate size. In most cases, customers choose to match the port speed created in the IBM Console.
    4. The VLAN for this connection that you will receive via the Megaport. This must be a unique VLAN ID on this port. You can also click the toggle to **untag** this VXC. This removes the VLAN tagging for this connection but limits the port to only one VXC.

5. Click **Next** and add the VXC. You can then proceed through the checkout process. IBM will verify the IBM Cloud Ticket number and send you a */30* or */31* Private IP to provision for BGP.

6. See [Configure IBM Cloud Direct Link](https://cloud.ibm.com/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#configure-ibm-cloud-direct-link) to complete your private connection to your IBM Cloud environment.

## Understanding how a Novalink connection on RMC works for AIX
{: #novalink-aix-cloud }

When Novalink is the management partition, each virtual machine on the host is assigned a local IPV6 interface to communicate with Novalink for Resource Monitoring and Control (Secure RMC). For more information, see [Simplified NovaLink RMC Connections](https://developer.ibm.com/powervc/2015/12/10/simplified-novalink-rmc-connections/){: new_window}).
