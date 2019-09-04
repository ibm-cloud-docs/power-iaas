---

copyright:
  years: 2019

lastupdated: "2019-08-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}

# Configuring IBM Power Systems Virtual Servers
{: #cpn-configuring}

You can configure your subnet to interact with the {{site.data.keyword.cloud}} after establishing [Direct Link connectivity](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect). To get your IBM Cloud Direct Link connection working, you need to perform some basic network configuration and set up Border Gateway Protocol (BGP). During the setup process, an IBM professional works with you to enable your network to use the required Virtual Routing Function (VRF) capability. For more information, see [Configuring IBM Cloud Direct Link](https://cloud.ibm.com/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link).

## Connecting to the IBM Cloud classic infrastructure
{: #cpn-connect-classic}

You can use one of the following options to connect to the IBM Cloud classic infrastructure:

**Using an SSL VPN with a jump server and a VRA**

You can use the {{site.data.keyword.cloud_notm}} **SSL VPN service** to connect to your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use a {{site.data.keyword.cloud_notm}} virtual machine (VM) as a jump server to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connections are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a jump server.
* For more information, see [Setting up SSL VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

**Using a IPSec VPN and a VRA**

You can use the {{site.data.keyword.cloud_notm}} **IPSec VPN service** to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use the IBM Cloud VRA to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must have a Direct Link connection.
* This option is typically used to manage environments and is not recommended for production workloads.
* Because VPN connects are unable to connect directly to the {{site.data.keyword.powerSys_notm}} instance, you must use a VRA.
* For more information, see [Setting up IPSec VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

You cannot use the same private subnet for both IBM Cloud classic and IBM Cloud Power instances. These offerings are not colocated and their networks are not linked. You must order a DirectLink Connection.
{: important}

## Connecting to the IBM Cloud Power infrastructure
{: #cpn-connect-power}

After establishing a connection to the IBM Cloud classic infrastructure, you must use a separate Direct Link connection to connect to the IBM Cloud Power infrastructure.

* You can choose from several Direct Link Connect services to connect to the IBM Cloud Power infrastructure. For more information, see [Direct Link connectivity](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).
* This option provides high performance between the on-premises network and the IBM Cloud Power infrastructure.
* There are specific IP addresses that you cannot use with a Direct Link Connect service. For more information, see [Strict limitations on IP assignments](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).

## Using Megaport to directly connect to the IBM Cloud Power infrastructure
{: #cpn-connect-megaport}

You can connect directly to the IBM Cloud Power infrastructure through [Megaport](https://www.megaport.com/) exchange. You must engage Megaport directly to procure the bandwidth. You must also open a secondary ticket with IBM Power to perform the connection.
