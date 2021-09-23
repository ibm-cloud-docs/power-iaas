---

copyright:
  years: 2021

lastupdated: "2021-08-09"

keywords: Cloud connections, subnet, VPC, IBM cloud

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Managing Cloud connections
{: #cloud-connections}

You can use Cloud connections to automatically connect your {{site.data.keyword.powerSys_notm}} instances to IBM Cloud resources including the IBM Cloud Classic network and the Virtual Private Cloud (VPC) network. Cloud connections create a Direct Link Connect (2.0) instance to connect your {{site.data.keyword.powerSys_notm}} instances to the IBM Cloud resources. The speed and reliability of the Direct Link connection extends the network of your organization data center and offers more consistent and higher-throughput connectivity, while keeping network traffic within the IBM Cloud network.

You can have a maximum of two Cloud connections per account.
{: important}

To perform the following operations by using CLI, see [Create a Cloud connection](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-connection).

## Power Systems Virtual Servers service instances support with Cloud connections
{: #powervs-support-cloud-connections}

Power Systems Virtual Server supports multiple service instances from the same account. However, only a single service instance can use a Cloud connection. If you want to configure a setup with multiple service instances for the same account and if you want these multiple service instances to share a Cloud connection, open a [Service Ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

When you are performing multiple Cloud connection tasks, numerous actions within a task can timeout. When the timeout occurs, the tasks are completed in the background and the changed status might not be reflected immediately. You can run the commands again and the status will be updated to complete.
{: note}

## Creating Cloud connections
{: #create-cloud-connections}

The Cloud connections (network automation) speed is limited to 5 Gbps if you are provisioning a new Power Systems Virtual Server service.
{: note}

To create a Cloud connection, complete the following steps:

1. Go to the Power Systems Virtual Server user interface and click **Cloud connections**.

2. In the <wintitle>Cloud connections</wintitle> page, click **Create connection**.

3. Specify a connection name and select a connection speed. Maximum connection speed is 5 Gbps. If required, 10 Gbps Direct Link can be requested by opening a service ticket. For more information about Direct Link, see [Direct Link Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect).

4. If you need access to other data centers outside your Power Systems Virtual Server region, toggle the **Global routing** switch to the on position.
   For example, you might use global routing to share workloads between dispersed IBM Cloud resources, such Dallas to Tokyo, or Dallas to Frankfurt.

5. Select the **Endpoint destination** as follows to select the network connection to attach to the Direct Link gateway:
   * **Classic Infrastructure**: You can connect to IBM Cloud classic resources. Only one Classic infrastructure connection is allowed per Direct Link gateway. You can also request a Generic Routing Encapsulation (GRE) tunnel configuration by specifying the GRE destination and GRE subnet IP addresses. For more information, see [GRE tunneling](/docs/power-iaas?topic=power-iaas-configuring-power#gre-tunneling).
   * **VPC**: You can connect to your account’s Virtual Private Cloud (VPC) resources. You must select the VPC connection from the list of available connections. You can connect multiple VPCs to a Cloud Connection.
   Cloud connections provide connectivity to IBM Cloud Classic network in addition to the VPC network. You can access all of the Classic network locations irrespective of Direct Link 2.0 gateway in Local Routing or Global Routing attribute. You must use the Global routing option to reach the VPC network that is outside the local region.

6. Click **Attach existing** to attach an existing subnet to the Cloud connection. GRE tunnel requires that a Cloud connection must be attached to a subnet. You can create a new subnet in the **Subnets** window. For more information, see [Configuring subnets](/docs/power-iaas?topic=power-iaas-configuring-subnet). The table lists all the subnets that are attached to the Cloud connection.
If you want to attach a subnet to Cloud connection, the network traffic is routed over the Cloud connection.
You must route Power Systems Virtual Server private network subnets over IBM Cloud Direct Link to allow connectivity between Power Systems Virtual Server instances and the IBM Cloud network.
{: note}

7. Review the summary and the terms and conditions information.

8. Click **Create** to create a Cloud connection.

Cloud connections are available in all current locations except Toronto 1, Montreal 1, São Paulo 1, and Washington 4.
{: note}

## Modifying Cloud connections
{: #configure-Cloud-connections}

When you create or edit a subnet, you can also attach an existing Cloud connection to the subnet. For more information about adding a private network subnet, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).

To view or edit Cloud connections, complete the following steps:

1. In the Power Systems Virtual Services dashboard, click **Cloud connections** in the left navigation pane.

2. Click the Cloud connection that you want to configure. The corresponding **Connection details** page appears.

3. Click the **Edit details** icon.

4. Modify the details, review the pricing changes, and click **Save edits**.

## Deleting a Cloud connection
{: #delte-Cloud-connection}

To delete a Cloud connection, complete the following steps:

1. In the Power Systems Virtual Services dashboard, click **Cloud connections** in the left navigation window.

2. You can see the list of Cloud connections that are currently configured. Click the **Delete** icon in the last column of the table to delete a specific Cloud connection.

If you delete the Cloud connection, subnets that are attached to Cloud connection are automatically detached.
{: note}

## Setting up high availability over Cloud Connections
{: #ha-availability-cloud-connections}

IBM Cloud Direct Link (2.0) is not a redundant service by default. You must order a separate Direct Link Connect (2.0) instance for redundancy.

To set up highly available connectivity to the IBM Cloud network by using Direct Link Connect, complete the following steps:

1. Create two Cloud connections for your Power Systems Virtual Server.
2. Attach subnets to the primary and redundant Cloud connections.

When subnets are attached to Cloud connections, the Power Systems Virtual Server supports routing the subnets over the Cloud connections and Border Gateway Protocol (BGP) configuration, which provides the redundant paths.

## Configuring Generic Routing Encapsulation (GRE) tunnel
{: #configure-gre-tunnel}

A Generic Routing Encapsulation (GRE) tunnel connects two endpoints (a firewall or a router and another network appliance) in a point-to-point logical link. Power Systems Virtual Servers use GRE tunnel to enable connectivity to IBM Cloud VMware network and other destinations by using a router appliance. GRE tunnel enables Bring your own IP addresses (BYOIP) and transiting through IBM Cloud Classic Network.

GRE tunnel configuration requires tunnel source IP (Power Systems Virtual Server router end), GRE subnet, and destination IP. You can configure GRE tunnel when creating a Cloud connection by using the GUI, see [Creating Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections). You can also configure the GRE tunnel by using the CLI when creating the cloud connection. For more information see [Creating Cloud connections](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#connection-update).

GRE tunnel subnet supports addressing for GRE tunnels. It is used for tunnel source IP, local IP, and remote IP. First half of the subnet IP range (s1) is used for source IPs and the second half of the subnet IP range (s2) is used for local and remote IPs. GRE tunnel uses the first IP from s1 for source IP. Local IP is first IP of s2 and remote IP is the second IP of s2.

### GRE configuration example
{: #gre-configuration-example}

If you choose your destination IP address as 10.148.252.83, which is a private IP of your vRealize Automation (VRA) (VRA -IBM Cloud vSRX, Vyatta, or VMWare NSX Edge) and GRE subnet as 172.16.3.0/29:

```
GRE Destination IP: 10.148.252.83 (VRA private IP)
GRE Subnet:       : 172.16.3.0/29 (GRE subnet that you chose)
PowerVS source IP : 172.16.3.1 mask 255.255.255.255
PowerVS tunnel IP : 172.16.3.5
```
{: codeblock}

You must configure the GRE tunnel in your VRA as follows:

```
GRE Destination IP: 172.16.3.1/32 (PowerVS Tunnel End-point Destination IP)
VRA source IP     : 10.148.252.83
VRA tunnel IP     : 172.16.3.6
VRA ASN           : 64880
PowerVS ASN       : 64999
```
{: codeblock}

You must configure VRA with BGP protocol for route advertising for the subnets to reach over the GRE tunnel. The ASN numbers are pre assigned in the Power Systems Virtual Servers and you cannot choose any other number.

<!--GRE tunnel BGP ASNs are as follows:

- Power ASR side ASN is 64995 in WDC(64999 for Nexus in WDC).
- For other ASRs ASN number is 64999.
- Customer ASN for GRE BGP is 64880.-->

## Migrating existing network configuration
{: #migrate-existing-configuration}

Your existing network configuration can continue to be managed by using Power Systems Virtual Server support ticket process and is not required to be migrated to Power Systems Virtual Server network.

If you want to use the new features that are offered by network automation, you can migrate the existing network configuration by creating a Power Systems Virtual Server operations support ticket.

### Considerations for network configuration migration
{: #pre-req-migration-to-network}

* If you want to migrate your network configuration, you might need to plan a maintenance window.
* Network configuration migration might require network configuration changes in on-premises configuration.