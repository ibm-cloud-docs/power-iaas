---

copyright:
  years: 2021, 2022

lastupdated: "2022-06-13"

keywords: Cloud connections, subnet, VPC, IBM cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing {{site.data.keyword.cloud_notm}} connections
{: #cloud-connections}

You can use {{site.data.keyword.cloud}} connections to automatically connect your {{site.data.keyword.powerSys_notm}} instances to {{site.data.keyword.cloud_notm}} resources on {{site.data.keyword.cloud_notm}} classic network and Virtual Private Cloud (VPC) infrastructures. {{site.data.keyword.cloud_notm}} connections create a {{site.data.keyword.dl_short}} (2.0) Connect instance to connect your {{site.data.keyword.powerSys_notm}} instances to the {{site.data.keyword.cloud_notm}} resources. The speed and reliability of the {{site.data.keyword.dl_short}} connection extends the network of your organization data center and offers more consistent and higher-throughput connectivity, while keeping network traffic within the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

You can have a maximum of two {{site.data.keyword.cloud_notm}} connections per account.
{: important}

## Support for Power Systems Virtual Servers service instances with {{site.data.keyword.cloud_notm}} connections
{: #powervs-support-cloud-connections}

{{site.data.keyword.powerSys_notm}} supports multiple service instances from the same account. However, any given {{site.data.keyword.cloud_notm}} connection can be used by only one service instance. If you want to configure a setup with multiple service instances for the same account and if you want these service instances to share an {{site.data.keyword.cloud_notm}} connection, open an [IBM Support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

When you perform multiple {{site.data.keyword.cloud_notm}} connection tasks, actions within a task can time out. When the timeout occurs, the tasks are completed in the background and the status might not change immediately.
{: note}

## Creating {{site.data.keyword.cloud_notm}} connections
{: #create-cloud-connections}

To create an {{site.data.keyword.cloud_notm}} connection, complete the following steps:

1. Go to the Power Systems Virtual Server user interface and click **Cloud connections**.
1. On the Cloud connections page, click **Create connection**.
1. In the **Resource details** section, complete the following:
   1. Specify a connection name and select a connection speed. Follow these guidelines for setting the speed:
      - Maximum connection speed is 10 Gbps. 
      - You can select 10 Gbps speed only when you are creating a new connection.
      - If you select 10 Gbps as the required speed, the GRE tunneling option is unavailable. 
      - You cannot modify a Cloud connection with 10 Gbps to be GRE capable by reducing the speed.  
      - You cannot modify the speed of an IBM Cloud connection when the speed is set to 10 Gbps at the time of creation.
   1. Select **Enable global routing** if you need access to other data centers outside your Power Systems Virtual Server region. For example, you can use global routing to share workloads between dispersed {{site.data.keyword.cloud_notm}} resources, such as Dallas to Tokyo, or Dallas to Frankfurt.
   1. Select **Enable IBM Transit Gateway** to interconnect your Power Systems Virtual Servers to the {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC) infrastructures, keeping traffic within {{site.data.keyword.cloud_notm}}. IBM Cloud Transit Gateway connects the private networks, such as classic, VPC, and {{site.data.keyword.dl_short}}. For more information, see [Getting started with IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started&interface=ui).
1. In the **Virtual connections** section, you can establish a connection between multiple Power Systems Virtual Server services across different data centers by using a transit gateway. You can create virtual connections that are directly attached to the Direct Link gateway, or you can choose to connect a transit gateway and then create a connection from it to your networks (VPC, classic). You must create an [IBM Cloud Transit Gateway](https://cloud.ibm.com/login?redirect=%2Finterconnectivity%2Ftransitconnection){: external} to enable the virtual connections. Select the checkbox to continue. This setting is required if you selected the **Enable IBM Transit Gateway** checkbox in the previous step.
1. In the **Subnets** section, click **Attach existing** to attach an existing subnet to the connection. A GRE tunnel requires that a connection be attached to a subnet. You can create a new subnet. If you enable IBM Cloud Transit Gateway, you must configure the GRE tunnel by using the IBM Cloud Transit Gateway interface. For more information, see [Configuring subnets](/docs/power-iaas?topic=power-iaas-configuring-subnet). The table in this topic lists all the subnets that are attached to the IBM Cloud connection.

   If you want to attach a subnet to an IBM Cloud connection, the network traffic is routed over the connection. You must route Power Systems Virtual Server private network subnets over IBM Cloud Direct Link to allow connectivity between Power Systems Virtual Server instances and the IBM Cloud network.
   {: note}

1. Review the summary and the terms and conditions. Then, click **Create** to create an IBM Cloud connection.

IBM Cloud connections are not supported on the `WDC06` data center. If you don't have the authorization to create an IBM Cloud connection, a direct link is created. This direct link is not operational, and must be authorized by the IBM Cloud account user who has the required authority. Two direct links cannot be created under one account, even from different regions.
{: note}

## Modifying IBM Cloud connections
{: #configure-Cloud-connections}

When you create or edit a subnet, you can attach an existing IBM Cloud connection to the subnet. For more information, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).

To view or edit IBM Cloud connections, complete the following steps:

1. From the Power Systems Virtual Services dashboard, click **Cloud connections** in the left navigation pane.
1. Click the Cloud connection that you want to configure. The corresponding **Connection details** page appears.
1. If a transit gateway is enabled for the connection, you can view the **Managed with IBM Transit Gateway** details. 
1. Click the **Edit details** icon.

   If you have an existing IBM Cloud connection with a speed of 5 Gbps or less, you cannot increase the speed limit to 10 Gbps. Also, you cannot modify an IBM Cloud connection with 10 Gbps to be GRE-capable by reducing the speed.
   {: note}

1. Modify the details, review the pricing changes, and click **Save edits**.

## Deleting an IBM Cloud connection
{: #delete-cloud-connection}

To delete an IBM Cloud connection, complete the following steps:

1. From the Power Systems Virtual Services dashboard, click **Cloud connections** in the left navigation window.
   
   You can see the list of IBM Cloud connections that are currently configured. 
   
 1. To delete a specific IBM Cloud connection, click the **Delete** icon in the last column of the table.

   If you delete the IBM Cloud connection, subnets that are attached to the connection are automatically detached.
   {: note}

## Setting up high availability over IBM Cloud connections
{: #ha-availability-cloud-connections}

By default, IBM Cloud Direct Link (2.0) is not a redundant service. You must order a separate Direct Link (2.0) Connect instance for redundancy.

To set up high availability to the IBM Cloud network by using Direct Link Connect, complete the following steps:

1. Create two IBM Cloud connections for your Power Systems Virtual Server.
1. Attach subnets to the primary and redundant IBM Cloud connections.

When subnets are attached to IBM Cloud connections, the Power Systems Virtual Server supports routing the subnets over the IBM Cloud connections and Border Gateway Protocol (BGP) configuration, which provides the redundant paths.

## Configuring a Generic Routing Encapsulation (GRE) tunnel
{: #configure-gre-tunnel}

A Generic Routing Encapsulation (GRE) tunnel connects two endpoints (a firewall or a router and another network appliance) in a point-to-point logical link. Power Systems Virtual Servers use GRE tunnels to enable connectivity to IBM Cloud VMware networks and other destinations by using a router appliance. A GRE tunnel enables Bring Your Own IP (BYOIP) functionality, as well as the ability for data to transit through the IBM Cloud classic network.

GRE tunnel configuration requires a tunnel source IP (Power Systems Virtual Server router end), GRE subnet, and destination IP address. For more information, see [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections).  

A GRE tunnel subnet supports addressing for GRE tunnels. It is used for the tunnel source IP, local IP, and remote IP. The first half of the subnet IP range (`s1`) is used for source IPs and the second half (`s2`) is used for local and remote IPs. GRE tunnels use the first IP from `s1` as the source IP. The local IP is first IP of `s2` and the remote IP is the second IP of `s2`.

### GRE configuration example
{: #gre-configuration-example}

Suppose you choose `10.148.252.83` as your destination IP address, which is a private IP of your vRealize Automation (VRA -IBM Cloud vSRX, Vyatta, or VMWare NSX Edge) and `172.16.3.0/29` as the GRE subnet:

```text
GRE Destination IP: 10.148.252.83 (VRA private IP)
GRE Subnet:       : 172.16.3.0/29 (GRE subnet that you chose)
PowerVS source IP : 172.16.3.1 mask 255.255.255.255
PowerVS tunnel IP : 172.16.3.5
```
{: codeblock}

Then, you must configure the GRE tunnel in your VRA as follows:

```text
GRE Destination IP: 172.16.3.1/32 (PowerVS Tunnel End-point Destination IP)
VRA source IP     : 10.148.252.83
VRA tunnel IP     : 172.16.3.6
VRA ASN           : 64880
PowerVS ASN       : 64999
```
{: codeblock}

You must configure the VRA with BGP protocol for route advertising so that the subnets can reach through the GRE tunnel. The ASN numbers are pre-assigned in the Power Systems Virtual Servers and you can't choose another number.

## Migrating an existing network configuration
{: #migrate-existing-configuration}

You can continue to have your existing configuration managed using the Power Systems Virtual Server IBM Support case process. You are not required to migrate to a Power Systems Virtual Server network. 
{: note}

If you want to use the new features that are offered by network automation, you can migrate your existing network configuration by creating a Power Systems Virtual Server operations IBM Support case.

### Considerations for network configuration migration
{: #pre-req-migration-to-network}

When planning for migration, review the following considerations:

* Be sure to factor a maintenance window into your schedule.
* Migration might require configuration changes to an on-premises configuration.
