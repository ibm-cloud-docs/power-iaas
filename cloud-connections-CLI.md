---

copyright:
  years: 2021, 2024

lastupdated: "2025-05-07"

keywords: Cloud connections, subnet, VPC, IBM cloud

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# IBM {{site.data.keyword.powerSys_notm}} Cloud Connections
{: #cloud-connections}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}



---


---

You can use {{site.data.keyword.powerSys_notm}} Cloud Connections to connect your {{site.data.keyword.powerSys_notm}} instances to {{site.data.keyword.cloud_notm}} resources on {{site.data.keyword.cloud_notm}} classic network and Virtual Private Cloud (VPC) infrastructures. {{site.data.keyword.powerSys_notm}} Cloud Connection creates a {{site.data.keyword.dl_short}} (2.0) Connect instance to connect your {{site.data.keyword.powerSys_notm}} instances to the {{site.data.keyword.cloud_notm}} resources within your account. For cross-account connectivity, use IBM Transit Gateway to interconnect your {{site.data.keyword.powerSys_notm}} to the {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC) infrastructures. The speed and reliability of the {{site.data.keyword.dl_short}} connection extends your {{site.data.keyword.powerSys_notm}} network to the IBM Cloud network and offers more consistent and higher-throughput connectivity, while keeping the network traffic within {{site.data.keyword.cloud_notm}}.
{: shortdesc}

You can have a maximum of two {{site.data.keyword.cloud_notm}} ({{site.data.keyword.powerSys_notm}} Direct Link Connect) per account per {{site.data.keyword.powerSys_notm}} data center. To create a {{site.data.keyword.powerSys_notm}} {{site.data.keyword.cloud_notm}}, you must have the required access to create the connections. For more information, see [Access roles requirements for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-managing-resources-and-users#access-roles-requirement).
{: important}

## Support for {{site.data.keyword.powerSys_notm}} workspaces with {{site.data.keyword.powerSys_notm}} Cloud Connections
{: #powervs-support-cloud-connections}

The {{site.data.keyword.powerSys_notm}} supports multiple workspaces from the same account. However, a specific IBM Cloud connection can be used by only one workspace.

When you perform multiple {{site.data.keyword.powerSys_notm}} Cloud Connection tasks, actions within a task can time out. When the timeout occurs, the tasks are completed in the background and the status might not change immediately.
{: note}

## Creating {{site.data.keyword.powerSys_notm}} Cloud Connections
{: #create-cloud-connections}



The creation of new {{site.data.keyword.powerSys_notm}} Cloud Connections across most of the data centers is disabled. You can create Cloud Connections only in the `MON01` and `CHE01` data centers. If you do not have the authorization and attempt to create a Cloud Connection (Direct Link Connect), a link is generated. Direct Link is not operational until an authorized IBM Cloud account user with the required authority must authorize the connection by using [IBM Cloud Console Direct Link Portal](https://cloud.ibm.com/interconnectivity){: external}.


To create {{site.data.keyword.powerSys_notm}} Cloud Connection from the `MON01` and `CHE01` data centers, complete the following steps:




1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **Cloud connections**.
2. On the Cloud connections page, click **Create connection**.
3. In the **Resource details** section, complete the following steps:

   a. Specify a connection name and select a connection speed. Follow these guidelines for setting the speed:
      - The maximum connection speed is 10 Gbps.
      - You can select 10 Gbps speed only when you are creating a new connection.
      - If you select 10 Gbps as the required speed, the GRE tunneling option is disabled.
      - You cannot modify a Cloud connection with 10 Gbps to be GRE capable by reducing the speed.
      - You cannot modify the speed of an IBM Cloud connection when the speed is set to 10 Gbps at the time of creation.

   b. Select **Enable global routing** if you need access to other data centers outside your {{site.data.keyword.powerSys_notm}} region. For example, you can use global routing to share workloads between dispersed {{site.data.keyword.cloud_notm}} resources, such as Dallas to Tokyo, or Dallas to Frankfurt. If you want to enable IBM Transit Gateway for the Cloud connection, then global routing option is not required.

   c. Select **Enable IBM Transit Gateway** to interconnect your {{site.data.keyword.powerSys_notm}} to the {{site.data.keyword.cloud_notm}} classic and Virtual Private Cloud (VPC) infrastructures and to keep traffic within {{site.data.keyword.cloud_notm}}. {{site.data.keyword.tg_full_notm}} connects the private networks, such as classic, VPC, and {{site.data.keyword.dl_short}}. For more information, see [Getting started with IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started&interface=ui).



   {{site.data.keyword.tg_full_notm}} is available in `WDC04`, `DAL12`, `DAL13`, `DAL14`, `LON04`, `LON06`, `FRA04`, `FRA05`, `SAO01`, `SYD04`, `TOK04`, `TOR01`, `MON01`, `SYD05`, and `OSA21` data centers.





   You need to configure IBM Cloud Transit Gateway in `WDC06` manually. Select **Transit Gateway** as the network connection type instead of **Direct resources** while you create {{site.data.keyword.dl_short}} (2.0) Connect to use IBM Cloud Transit Gateway. Complete your connection by submitting an IBM Support case to the {{site.data.keyword.powerSys_notm}} team. For more information, see [Ordering Direct Link Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0).
   {: note}

4. In the **Virtual connections** section, you can establish a connection between multiple {{site.data.keyword.powerSys_notm}} workspaces across different data centers by using an {{site.data.keyword.tg_full_notm}}. You can create virtual connections that are directly attached to the {{site.data.keyword.dl_short}} gateway, or you can choose to connect an {{site.data.keyword.tg_full_notm}} and then create a connection from it to your network (VPC, classic). You must create an [IBM Cloud Transit Gateway](https://cloud.ibm.com/login?redirect=%2Finterconnectivity%2Ftransitconnection){: external} to enable virtual connections. Select the virtual connections checkbox to continue. This setting is required if you selected the **Enable IBM Transit Gateway** checkbox in the previous step.
   

5. In the **Subnets** section, click **Attach existing** to attach an existing subnet to the connection. For A GRE tunnel, a connection must be attached to a subnet. You can create a new subnet. If you enable {{site.data.keyword.tg_full_notm}}, you can configure the GRE tunnel by using the {{site.data.keyword.tg_full_notm}} interface. For more information, see [Configuring subnets](/docs/power-iaas?topic=power-iaas-configuring-subnet). The table `Understanding CIDR notation caption` in the [Configuring subnets](/docs/power-iaas?topic=power-iaas-configuring-subnet) topic lists all the subnets that are attached to the IBM Cloud connection. 

   Attaching a subnet to an IBM Cloud connection is required as the network traffic is routed over the connection. You must route {{site.data.keyword.powerSys_notm}} private network subnets over IBM Cloud {{site.data.keyword.dl_short}} to allow connectivity between {{site.data.keyword.powerSys_notm}} instances and the IBM Cloud network. Attaching a subnet to Cloud connections allows {{site.data.keyword.powerSys_notm}} VM to VM communication and for the VMs that are located in the same subnet or different subnet within the workspace to communicate.
   {: note}

   If the Cloud connection is attached to a Transit Gateway, prepare for [Direct Link](/docs/dl?topic=dl-notification-dl-tgw) and [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-notification-dl-tgw) changes to advertise service network routes.
   {: note}

6. Review the summary and the terms and conditions. Then, click **Create** to create an IBM Cloud connection.


## Modifying IBM Cloud connections
{: #configure-Cloud-connections}

When you create or edit a subnet, you can attach an existing IBM Cloud connection to the subnet. For more information, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).

To view or edit IBM Cloud connections, complete the following steps:

1. From the {{site.data.keyword.powerSys_notm}} dashboard, click **Cloud connections** in the left navigation page.
2. Click the Cloud connection that you want to configure. The corresponding **Connection details** page appears.
3. If a Transit Gateway is enabled for the connection, you can view the **Managed with IBM Transit Gateway** details.
4. Click the **Edit details** icon.

   If you have an existing IBM Cloud connection with a speed of 5 Gbps or less, you cannot increase the speed limit to 10 Gbps. Also, you cannot modify an IBM Cloud connection with 10 Gbps to be GRE-capable by reducing the speed.
   {: note}

5. Modify the details, review the pricing changes, and click **Save edits**.

## Deleting an IBM Cloud connection
{: #delete-cloud-connection}

To delete an IBM Cloud connection, complete the following steps:

1. From the {{site.data.keyword.powerSys_notm}} dashboard, click **Cloud connections** in the left navigation window.

   You can see the list of IBM Cloud connections that are currently configured.

   1. To delete a specific IBM Cloud connection, click the **Delete** icon in the last column of the table.

When you delete a virtual server instance, it deletes the private networks (subnets) and other resources. Review the following considerations before you delete a virtual server instance:
-You must delete the Cloud Connection (Direct Link) from the IBM Cloud Transit Gateway interface before you delete the Cloud Connection.
-When there are more than one virtual server instances that use the Cloud Connection, and you delete one, you can delete the Cloud Connection from the existing server instances.
{: note}

## Setting up high availability over IBM Cloud connections
{: #ha-availability-cloud-connections}

By default, IBM Cloud {{site.data.keyword.dl_short}} (2.0) is not a redundant service. You must order a separate {{site.data.keyword.dl_short}} (2.0) Connect instance for redundancy.

To set up high availability to the IBM Cloud network by using {{site.data.keyword.dl_short}} connect, complete the following steps:

1. Create two IBM Cloud connections for your {{site.data.keyword.powerSys_notm}}.
2. Attach subnets to the primary and redundant IBM Cloud connections.

When subnets are attached to IBM Cloud connections, the {{site.data.keyword.powerSys_notm}} supports routing the subnets over the IBM Cloud connections and Border Gateway Protocol (BGP) configuration, which provides the redundant paths.

## Configuring a Generic Routing Encapsulation (GRE) tunnel
{: #configure-gre-tunnel}

A Generic Routing Encapsulation (GRE) tunnel connects two endpoints (a firewall or a router and another network appliance) in a point-to-point logical link. {{site.data.keyword.powerSys_notm}} use GRE tunnels to enable connectivity to IBM Cloud VMware&trade; networks and other destinations by using a router appliance. A GRE tunnel enables Bring Your Own IP (BYOIP) features and the ability for data to transit through the IBM Cloud classic network.

GRE tunnel configuration requires a tunnel source IP ({{site.data.keyword.powerSys_notm}} router end), GRE subnet, and destination IP address. For more information, see [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections).

A GRE tunnel subnet supports addressings for GRE tunnels. It is used for the tunnel source IP, local IP, and remote IP. The first half of the subnet IP range (`s1`) is used for source IP addresses and the second half (`s2`) is used for local and remote IP addresses. GRE tunnels use the first IP from `s1` as the source IP. The local IP is the first IP of `s2` and the remote IP is the second IP of `s2`.

### GRE configuration example
{: #gre-configuration-example}

Suppose you choose `10.148.252.83` as your destination IP address, which is a private IP of your vRealize Automation (VRA -IBM Cloud vSRX, Vyatta, or VMWare&trade; NSX Edge) and `172.16.3.0/29` as the GRE subnet:

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

In general, the overlay and underlay network must not be on the same subnet, so to make sure your configuration that is stated earlier is valid on your gateway appliance. You can change the subnet mask of the GRE subnet from /29 to /30 so that it excludes 172.16.3.1 from the overlay network.{: note}

By default, gateway appliances send the traffic for the 172 network to the default gateway, which is generally the public subnet gateway of the gateway appliance. Make sure to add a static route for the destination "PowerVS Source IP" to be sent to the private subnet gateway of the gateway appliance.{: note}

You must configure the VRA with BGP protocol for route advertising so that the subnets can reach through the GRE tunnel. The ASN numbers are pre-assigned in the {{site.data.keyword.powerSys_notm}}s and you can't choose another number.

## Migrating an existing network configuration
{: #migrate-existing-configuration}

You can continue to have your existing configuration that is managed by using the {{site.data.keyword.powerSys_notm}} IBM Support case process. You are not required to migrate to a {{site.data.keyword.powerSys_notm}} network.
{: note}

If you want to use the new features that are offered by network automation, you can migrate your existing network configuration by creating a {{site.data.keyword.powerSys_notm}} operations IBM Support case.

### Considerations for network configuration migration
{: #pre-req-migration-to-network}

When you are planning for migration, review the following considerations:

* Be sure to factor a maintenance window into your schedule.
* Migration might require configuration changes to a private cloud configuration.
