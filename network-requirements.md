---

copyright:
  years: 2023, 2024

lastupdated: "2024-07-24"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}} as a service, private cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network requirements
{: #network-requirements}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

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


