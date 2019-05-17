---

copyright:
  years: 2019

lastupdated: "2019-05-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Configuring Power Systems Virtual Servers with a private network
{: #cpn-configuring}

You can use a private network with {{site.data.keyword.powerSysFull}} to securely connect your environment (on-premises) with the cloud environment (off-premise).  When you configure a private network, IBM creates a VLAN network to configure the virtual server with the private network.
{:shortdesc}

You can use the following methods to create a secure private network:

* Virtual Private Network (VPN)
  * If your network connection latency is not a priority, you can use a VPN to create a secure connection between your on-premises environment and the {{site.data.keyword.cloud_notm}} network.
  * You cannot use a VPN to directly connect to the {{site.data.keyword.powerSys_notm}}. To access the {{site.data.keyword.powerSys_notm}}, you can create a proxy to tunnel to the {{site.data.keyword.powerSys_notm}} or create a jump server from inside the {{site.data.keyword.cloud_notm}} to access the {{site.data.keyword.powerSys_notm}}.
  * To configure a VPN connection to access the {{site.data.keyword.cloud_notm}} network, see [Getting started with VPN](/docs/infrastructure/iaas-vpn?topic=VPN-gettingstarted-with-virtual-private-networking#gettingstarted-with-virtual-private-networking).

* Direct Link Connect
  * If you want low latency for your connection between your on-premises environment and the {{site.data.keyword.cloud_notm}} network, you can use a Direct Link Connect. Configuring a Direct Link Connect connection can take a few days because you must open a Direct Link Connect request and work with network providers.
  * To order a Direct Link Connect, complete the steps in the [How to order IBM Cloud Direct Link Connect](/docs/infrastructure/direct-link?topic=direct-link-how-to-order-ibm-cloud-direct-link-connect#how-to-order-ibm-cloud-direct-link-connect) topic.
  * There are specific IP address that you cannot use with a Direct Link Connect connection. For more information, see [Strict limitations on IP assignments](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)
