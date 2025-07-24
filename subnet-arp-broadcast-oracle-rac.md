---

copyright:
  years: 2025

lastupdated: "2025-07-24"

keywords: ARP Broadcast, subnet ARP, subnet ARP Broadcast, Subnet ARP Broadcast Oracle RAC, Oracle RAC

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Configuring the {{site.data.keyword.arp-broadcast}} in {{site.data.keyword.powerSys_notm}} subnets
{: #subnet-arp-oracle-rac}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

---



The Address Resolution Protocol (ARP) is a network protocol that is used to map IP addresses to physical Media Access Control (MAC) addresses in a network. The IP address mapping must be established to enable the communication between endpoints in subnets or in a local network.







The **{{site.data.keyword.arp-broadcast}}** is a switch that is provided on a subnet page of a {{site.data.keyword.powerSys_notm}} workspace. You can set **{{site.data.keyword.arp-broadcast}}** to **Enabled** or **Disabled**. When you set **{{site.data.keyword.arp-broadcast}}** to **Enabled**, the ARP request is broadcast across the subnet. You can use the broadcast request for ARP to distribute the ARP traffic in the {{site.data.keyword.powerSys_notm}} network fabric similar to how ARP is managed in conventional networks. A Gratuitous ARP (GARP) request can update the host ARP caches when an IP address has a different MAC address. To accomplish GARP requests, you must broadcast an ARP request across the subnet. For example, when **{{site.data.keyword.arp-broadcast}}** is used with cluster software, the network traffic is routed to the active cluster node.
{: shortdesc}


The **{{site.data.keyword.arp-broadcast}}** option is not available if you are using Cloud Connections. For more information, see [IBM Power Virtual Server Cloud Connections](/docs/power-iaas?topic=power-iaas-cloud-connections).
{: note}

## Benefits of the {{site.data.keyword.arp-broadcast}} in {{site.data.keyword.powerSys_notm}} subnets
{: #arp-enabl-benefit}

To get the benefits of the **{{site.data.keyword.arp-broadcast}}**, you must set the option to **Enabled** for a subnet of a {{site.data.keyword.powerSys_notm}} workspace on the Subnet page. The ARP request is broadcast across the subnet and the following changes in the subnet are determined:

- Identify the change in the MAC address of a device that is mapped to an IP address
- Identify a MAC address of an IP address that frequently moves from one MAC addresses to another
- Identify the current IP address of a silent IP address in the subnet

In the {{site.data.keyword.powerSys_notm}} network fabric, when an IP address is reassigned to a different host without notifying the network fabric is called as a silent IP address. When you set the **{{site.data.keyword.arp-broadcast}}** to **Enabled**, the host with the silent IP address responds to the ARP request. The {{site.data.keyword.powerSys_notm}} network fabric updates the MAC address of the silent IP address with the MAC address of the host that responded to the ARP request.





If the **{{site.data.keyword.arp-broadcast}}** option is disabled, the {{site.data.keyword.powerSys_notm}} network fabric continues to forward the ARP request to the MAC address that is saved in the network fabric. The network fabric continues to forward the ARP request until the silent IP address endpoint exists. Also, the network traffic flow is optimized as the ARP request is sent to the MAC address associated with the silent IP address. The IP address moves to the new host through GARP or other requests. The endpoint then notifies the network fabric about the change in the current host.


## Enabling or disabling the {{site.data.keyword.arp-broadcast}}
{: #arp-enabl-metds}


To enable the {{site.data.keyword.arp-broadcast}} option when you create a new subnet, set **{{site.data.keyword.arp-broadcast}}** to **Enabled** on the Create subnet page. By default, the **{{site.data.keyword.arp-broadcast}}** option is set to **Disabled**. For more information, see [Configuring a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet). You can enable or disable the subnet ARP option by using the UI, CLI, or API interfaces.

To change the status of the **{{site.data.keyword.arp-broadcast}}** option for an existing subnet on the **{{site.data.keyword.powerSys_notm}}** page, complete the following steps:

1. Sign in to the [IBM Cloud Portal](https://cloud.ibm.com/){: external}.
2. Search for **{{site.data.keyword.powerSys_notm}}** in the search box for IBM Cloud catalog.
3. Select **Workspace** from the left menu.
4. Select the workspace for which you want to edit the subnet details.
5. Select **Subnets** under Networking from the left menu.
6. Select the subnet for which you want to enable the **{{site.data.keyword.arp-broadcast}}** option. The **Subnet ARP Broadcast** field is set as **Enabled** or **Disabled**.
7. Click **Edit Subnet** in the Subnet details section.
8. Set **Subnet ARP Broadcast** to **Enabled** or **Disabled** on the Edit Subnets pane.

To change the status of the **{{site.data.keyword.arp-broadcast}}** option for an existing subnet, use the following API or CLI commands:

* **API**: To enable or disable the broadcast of ARP when you create a subnet, use the [Create a new Network](/apidocs/power-cloud?loginMethod=federated#pcloud-networks-post) API. To enable or disable the broadcast of ARP when you update a subnet, use the [Update a Network](/apidocs/power-cloud?loginMethod=federated#pcloud-networks-put) API. Set the `arpBroadcast` parameter to `enable` or `disable` value. By default, the `arpBroadcast` parameter is set to `disable` value.

* **CLI**: To enable or disable the ARP broadcast option when you create a subnet, use the command [ibmcloud pi subnet create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-create). To enable or disable the ARP broadcast option when you update a subnet, use the command [ibmcloud pi subnet update](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-subnet-update). Set the `arpBroadcast` parameter to `enable` or `disable` value. By default, the `arpBroadcast` parameter is set to `disable` value.



