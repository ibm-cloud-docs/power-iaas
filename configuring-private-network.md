---

copyright:
  years: 2019

lastupdated: "2019-05-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Configuring Power Systems Virtual Servers with a private network
{: #cpn-configuring}

You can use a private network with {{site.data.keyword.powerSysFull}} to securely connect your on-premises environment with the off-premises {{site.data.keyword.cloud_notm}} environment. In a private network, you can access {{site.data.keyword.cloud_notm}} resources and interconnect with other virtual servers.
{:shortdesc}

You can use one of the following options to create a private network that connects your on-premises environment with the {{site.data.keyword.cloud_notm}} environment:

1. **{{site.data.keyword.cloud_notm}} SSL VPN with jump server**
   * You can use the {{site.data.keyword.cloud_notm}} SSL VPN service to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use a {{site.data.keyword.cloud_notm}} virtual machine (VM) as a jump server to connect to your {{site.data.keyword.powerSys_notm}} instance.
   * You must use a jump server because you cannot use a VPN connection to directly connect to the {{site.data.keyword.powerSys_notm}} instance.
   * This option is typically used to manage your environments. This option is not recommended for production workloads.
   * For more information on how to configure this option, see [Set up SSL VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

2. **{{site.data.keyword.cloud_notm}} IPSec VPN with IBM Cloud Virtual Router Appliance**
   * You can use the {{site.data.keyword.cloud_notm}} IPSec VPN service to connect into your existing {{site.data.keyword.cloud_notm}} network. Inside the {{site.data.keyword.cloud_notm}} network, you can use the IBM Cloud Virtual Router Appliance (VRA) to connect to your {{site.data.keyword.powerSys_notm}} instance.
   * You must use a VRA because you cannot use a VPN connection to directly connect to the {{site.data.keyword.powerSys_notm}} instance.
   * This option is typically used to manage your environments. This option is not recommended for production workloads.
   * For more information on how to configure this option, see [Set up IPSec VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) and [Ordering a Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra).

3. **Direct Link Connect with IBM Cloud Virtual Router Appliance**
   * You can order the Direct Link Connect service from IBM that connects your on-premises network to the IBM Cloud network by using the IBM Cloud Virtual Router Appliance (VRA).
   * This option provides high performance between the on-premises and the IBM Cloud network.
   * To order a Direct Link Connect, complete the steps in the [Ordering IBM Cloud Direct Link Connect from the UI Console](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect) topic.
   * There are specific IP addresses that you cannot use with a Direct Link Connect service. For more information, see [Strict limitations on IP assignments](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments).
