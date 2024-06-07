---

copyright:
  years: 2023, 2024

lastupdated: "2024-06-07"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}} as a service, private cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network requirements
{: #network-requirements}

[On-premises]{: tag-red}

To facilitate the {{site.data.keyword.powerSysFull}} pod infrastructure connectivity, you must evaluate the following network requirements:
* The data center site must provide network cables to connect the IBM {{site.data.keyword.powerSys_notm}} Private Cloud network infrastructure and the data network at the site.
* The site must provide two uplink cables to connect the IBM {{site.data.keyword.powerSys_notm}} Private Cloud network infrastructure to the IBM Cloud region through IBM Direct Link connections or through VPN connections.
* Contract with a service provider to:
    * Provide redundant connections to the IBM Direct Link connection or VPN connection.
    * Provide the last mile connection from the point-of-presence (PoP) of your service provider to the customer data center.  

For network architecture diagrams, see [Network architecture diagrams](/docs/power-iaas?topic=power-iaas-network-private-cloud#netwok-architecture-diagrams).

Setting up a network has two parts:
* [Control plane network](/docs/power-iaas?topic=power-iaas-network-private-cloud#control-plane-network) - for communication between IBM Cloud and the pod.
* [Data plane network](/docs/power-iaas?topic=power-iaas-network-private-cloud#data-plane-network) - for accessing virtual servers.

<!--## Control plane network
{: #control-plane-network}

The private cloud network architecture requires connectivity between two entities, IBM Cloud and the pod that is located in your private cloud data center. This connectivity is the main communication channel and is known as control plane network. For more information, see [Control plane network](/docs/power-iaas?topic=power-iaas-network_overview-on-premises&interface=api#control-plane-network){: external}.

Direct Link 2.0 Connect can be viewed as an alternative to a traditional site-to-site VPN solution that can provide security and privacy, consistent, and higher-throughput connectivity between a remote network and IBM Cloud environments. For more information about Direct Link Connect, see [Getting started with IBM Cloud Direct Link](https://cloud.ibm.com/docs/dl?topic=dl-get-started-with-ibm-cloud-dl){: external}

VPN connection can be established using one of the following methods:
* [site-to-site VPN Connectivity](/docs/power-iaas?topic=power-iaas-network_overview-on-premises&interface=api#vpn){: external}
* [connectivity using IBM Cloud classic environment](/docs/power-iaas?topic=power-iaas-network_overview-on-premises&interface=api#vpn){: external}

Provide the required network-specific information before the pod installation so that either the Direct Link 2.0 connection or VPN connection can be established. For example:
* Autonomous system numbers (ASN)
* Service key
* IP addresses and gateway for the Aggregation Services Router (ASR)
* Network connectivity ports
* Firewall access and permission

## Data plane network
{: #data-plane-network}

The Data Plane Network is enabled when the pods in your data center are connected to your private cloud network infrastructure. Using this connectivity you can access the virtual servers (logical partitions) in the pod through your network instead of IBM Cloud. As part of the network planning, you can review the [Network overview](/docs/power-iaas?topic=power-iaas-network-private-cloud) and available use cases in the [Network use cases](/docs/power-iaas?topic=power-iaas-network_use_cases) sections and identify the use cases that are applicable to you. You can communicate about such requirements before the installation so that you do not have to open separate support tickets to implement those use-cases and configuration.-->
