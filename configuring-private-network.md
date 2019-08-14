---

copyright:
  years: 2019

lastupdated: "2019-08-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Configuring Power Systems Virtual Servers
{: #cpn-configuring}

## Direct Link offerings
{: #cpn-dl}

{{site.data.keyword.cloud}} Direct Link is a suite of four offerings from the IBM Cloud Network, with availability in locations around the globe. Each one enables customers to create direct, private connections between their remote network environments and their IBM Cloud deployments--without touching the public internet. Most commonly, these offerings are implemented to support hybrid workloads, cross-provider workloads, large or frequent data transfers, private workloads, or to ease administration of the {{site.data.keyword.cloud_notm}} environment.

* **IBM Cloud Direct Link Exchange** allows customers to utilize an Exchange provider to deliver connectivity to their IBM Cloud. An Exchange provider is a co-location or data center provider that is already connected to the {{site.data.keyword.cloud_notm}} network, using multi-tenant, high capacity links (also known as a network-to-network interface, or NNI). Customers typically can purchase a virtual circuit at this provider, bringing connectivity at a reduced cost, because the physical connectivity from {{site.data.keyword.cloud_notm}} to the Exchange provider is in place already, shared amongst other customers.

* **IBM Cloud Direct Link Connect** allows customers to utilize a connection through our Carrier partners who own and operate a facility-based network. A Connect provider is a network service provider (NSP) that is already connected to the {{site.data.keyword.cloud_notm}} network, using multi-tenant, high capacity links (also known as a network-to-network interface, or NNI). Customers typically can purchase a virtual circuit at this provider, bringing connectivity at a reduced cost, because the physical connectivity from {{site.data.keyword.cloud_notm}} to the Connect provider is in place already, shared among other customers.

* **IBM Cloud Direct Link Dedicated** allows customers to terminate a single-tenant, fiber-based cross-connect into the {{site.data.keyword.cloud_notm}} network. This offering can be utilized by customers with co-location premises that are adjacent to IBM Cloud PoPs and data centers; as well as network service providers that deliver circuits to customer premises or other data centers.

* **IBM Cloud Direct Link Dedicated** Hosting provides connectivity similar to {{site.data.keyword.cloud_notm}} Direct Link Dedicated, but the connection point is adjacent to a {{site.data.keyword.cloud_notm}} data center, which improves latency for higher-performance use cases. {{site.data.keyword.cloud_notm}} offers a variety of customizable co-location services with this solution.

## Connecting to the IBM Power environment by using the IBM Cloud
{: #cpn-connect-cloud}

You can use one of the following options to connect to the IBM Power enviornment:

**{{site.data.keyword.cloud_notm}} SSL VPN with jump server**

You can use the {{site.data.keyword.cloud_notm}} SSL VPN service to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use a {{site.data.keyword.cloud_notm}} virtual machine (VM) as a jump server to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must use a jump server because you cannot use a VPN connection to directly connect to the {{site.data.keyword.powerSys_notm}} instance.
* This option is typically used to manage your environments. This option is not recommended for production workloads.
* For more information on how to configure this option, see [Set up SSL VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

**{{site.data.keyword.cloud_notm}} IPSec VPN with IBM Cloud Virtual Router Appliance**

You can use the {{site.data.keyword.cloud_notm}} IPSec VPN service to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use the IBM Cloud Virtual Router Appliance (VRA) to connect to your {{site.data.keyword.powerSys_notm}} instance.

* You must use a VRA because you cannot use a VPN connection to directly connect to the {{site.data.keyword.powerSys_notm}} instance.
* This option is typically used to manage your environments. This option is not recommended for production workloads.
* For more information on how to configure this option, see [Set up IPSec VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

## Connecting to the IBM Power environment from an on-premises network
{: #cpn-connect-onprem}

You can connect directly to the IBM Power environment from an on-premises network:

**Direct Link Connect with IBM Cloud Virtual Router Appliance**

You can order the Direct Link Connect service from IBM that connects your on-premises network to the IBM Cloud network by using the IBM Cloud Virtual Router Appliance (VRA).

* This option provides high performance between the on-premises and the IBM Cloud network.
* To order a Direct Link Connect, complete the steps in the [Ordering IBM Cloud Direct Link Connect from the UI Console](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect) topic.
* There are specific IP addresses that you cannot use with a Direct Link Connect service. For more information, see [Strict limitations on IP assignments](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
