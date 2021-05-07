---

copyright:
  years: 2020

lastupdated: "2021-03-02"

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

# Cloud connections
{: Cloud-connections}

Cloud connections provide an automated way to connect your {{site.data.keyword.powerSys_notm}} instances to the IBM Cloud resources that include Classic and VPC network. Cloud connections create a Direct Link Connect (2.0) offering instance to connect your {{site.data.keyword.powerSys_notm}} instances to the IBM Cloud resources. The speed and reliability of the Direct Link connection extends the network of your organization data center and offers more consistent, higher-throughput connectivity, keeping traffic within the IBM Cloud network.

Maximum number of Cloud connections per account is limited to 2 connections.
{: important}

## Power Systems Virtual Servers service instances support with Cloud connections
{: powervs-support-cloud-connections}

Power Systems Virtual Server supports multiple services under the same account. Cloud Connections support only one service to utilize a Cloud connection. If you want a configuration where multiple service instances are created under same account and the multiple service instances must share a Cloud connection, the configuration can be requested by opening a [Service Ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Creating Cloud connections
{: #create-cloud-connections}

If you are creating a new service, you automatically receive two Cloud connections of up to 10 Gbps network transmission speed at no cost. After the first two connections, charges apply based on speed and number of connections that you choose to have.
{: note}

Use the following command to create a Cloud connection:

```
ibmcloud pi connection-create CONNECTION_NAME -speed SPEED [--vps ] [--classic] [<--gre-tunnel "CIDR DEST-IP SOURCE-IP">] ...[--global-routing GLOBAL-ROUTING] [<--vpcID "ID">] [--json]
```
{: codeblock}

Cloud connections provide connectivity to IBM Cloud Classic network in addition to VPC network. You can access all of the Classic network locations irrespective of Direct Link 2.0 gateway in local or global routing attribute. You must use the global routing attribute to reach VPC network outside the local region.

For more information on parameters, see [Create a Cloud connection](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-connection).

Cloud connections is available in all current locations except Toronto 1, Montreal 1, and São Paulo 1 
{: note}

## Configuring Cloud connections
{: #configure-Cloud-connections}

If you created a Power Systems Virtual Servers service that contains two default Cloud connections, you have an initial subnet that is connected to those connections. You can view the attached subnets and add or remove subnets in the Cloud Connection details page. When you create or edit a subnet, you can also attach an existing Cloud connection. For information about adding a private network subnet, see [Configuring and adding a private network subnet](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-configuring-subnet).

Any changes to bandwidth might affect pricing.
{: note}

You can configure Cloud connections by using the following commands:

1. Use the following command to list all the Cloud connections:

```
ibmcloud pi connections [--long] [--json]
```
{: codeblock}

2. Use the following command to get the information about the network that is attached to your Cloud connection:

```
ibmcloud pi connection-network CONNECTION_ID --network NETWORK_ID [--json]
```
{: codeblock}

3. Use the following command to update the Cloud connection:

```
ibmcloud pi conu CONNECTION_NAME [--speed SPEED] [--type TYPE[<--gre-tunnel "CIDR DEST-IP SOURCE-IP">] ...[--global-routing GLOBAL-ROUTING] [<--vpc "NAME, VPC-ID">] [--json]
```
{: codeblock}

For more information on parameters, see [Update a Cloud connection](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#connection-update).

## Attaching subnets to Cloud connections
{: #attach-subnet}

You must route Power Systems Virtual Server private network subnets over IBM Cloud Direct Link to allow connectivity between Power Systems Virtual Server instances and the IBM Cloud network.

- Use the following command to attach a subnet to Cloud connection:

```
ibmcloud pi connection-attach-network CONNECTION_ID --network NETWORK_ID [--json]
```
{: codeblock}

When you create a subnet or edit details of a subnet, you can attach an existing Cloud connection to the subnet. For steps to create a subnet, see [Configuring and adding a private network subnet](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-configuring-subnet).

## Configuring and adding a private network subnet
{: #congure-add-private-network}

You can configure a private network subnet when you create an IBM Power Systems Virtual Server instance. You must use Classless inter-domain routing (CIDR) notation when you choose the IP ranges for your private network subnet. CIDR notation is defined in [RFC 1518](https://tools.ietf.org/html/rfc1518) and [RFC 1519](https://tools.ietf.org/html/rfc1519).

```
<IPv4 address>/<number>
```
{: codeblock}

The first IP address is always reserved for the gateway in all data centers. The second and third IP addresses are reserved for gateway high-availability (HA) in only the *WDC04* Power IaaS locations. The subnet address and subnet broadcast address are reserved in all Power IaaS locations.
{: important}

You can create and configure a private network subnet by using the following command:

```
ibmcloud pi network-create-private NETWORK_NAME --cidr-block CIDR --ip-range "startIP-endIP[,startIP-endIP]" [--dns-servers "DNS1 DNS2"] [--gateway GATEWAY] [--json]
```
{: codeblock}

A DNS server value of 9.9.9.9 might not be reachable if you do not have a public IP. This can cause the LPAR to hang during startup. Use the default DNS server value of 127.0.0.1 to avoid this issue. Currently, you can add up to 20 DNS servers. The DNS IP addresses must be separated by commas.

## Deleting a Cloud connection
{: #delte-Cloud-connection}

Use the following command to delete the Cloud connection:

```
ibmcloud pi connection-delete CONNECTION_ID
```
{: codeblock}

If you delete the Cloud connection, subnets that are attached to Cloud connection are automatically detached.
{: note}

## Setting up high availability over Cloud Connections
{: #ha-availability-cloud-connections}

IBM Cloud Direct Link (2.0) is not a redundant service by default. You must order a separate Direct Link Connect (2.0) instance for redundancy.

To set up highly available connectivity to the IBM Cloud network by using Direct Link Connect, complete the following steps:

1. Create two Cloud connections for your Power Systems Virtual Server.
2. Attach subnets to the primary and redundant Cloud connections.

When subnets are attached to Cloud connections, the Power Systems Virtual Server supports routing the subnets over the Cloud connections and BGP configuration, which provides the redundant paths.

## Configuring Generic Routing Encapsulation (GRE) tunnel
{: #configure-gre-tunnel}

A Generic Routing Encapsulation (GRE) tunnel connects two endpoints (a firewall or a router and another network appliance) in a point-to-point logical link. Power Systems Virtual Servers use GRE tunnel to enable connectivity to IBM Cloud VMware network and other destinations by using a router appliance.

GRE tunnel configuration requires tunnel source IP (Power Systems Virtual Server router end) and destination IP. To configure GRE tunnel and associated IPs, destination IP and GRE subnet are required.

GRE tunnel subnet supports addressing for GRE tunnels. It is used for tunnel source IP, local IP, and remote IP. First half of the subnet IP range (s1) is used for source IPs and second half for local and remote IPs (s2). GRE tunnel uses first IP from s1 for source IP, local IP is first IP of s2 and remote IP is second IP of s2.

### GRE configuration example
{: gre-configuration-example}

If you choose your destination IP address as 10.148.252.83, which is private IP of your VRA (VRA -IBM Cloud vSRX, Vyatta or VMWare NSX Edge) and GRE subnet as 172.16.3.0/29:

GRE Destination IP: 10.148.252.83 (VRA private IP)
GRE Subnet:       : 172.16.3.0/29 (GRE subnet that you choose)
Power VS source IP: 172.16.3.1 mask 255.255.255.255
PowerVS tunnel IP: 172.16.3.5

You must configure the GRE tunnel in your VRA as follows:

GRE Destination IP: 172.16.1.1/32 (PowerVS Tunnel End-point Destination IP)
VRA source IP     : 10.148.252.83
VRA tunnel IP     : 172.16.3.6
VRA ASN           : 64880
PowerVS ASN       : 64999

You must configure VRA with BGP protocol for route advertising for the subnets to reach over the GRE tunnel.

<!--GRE tunnel BGP ASNs are as follows:

- Power ASR side ASN is 64995 in WDC(64999 for Nexus in WDC).
- For other ASRs ASN number is 64999.
- Customer ASN for GRE BGP is 64880.-->

## Migrating existing configuration
{: migrate-existing-configuration}

Your existing network configuration can continue to be managed by using Power Systems Virtual Server support ticket process and is not required to be migrated to Power Systems Virtual Server network.

If you want to use the new features that are offered by network automation, you can migrate by creating a Power Systems Virtual Server operations support ticket.

### Pre-requisites for network configuration migration
{: pre-req-migration-to-network}

1. If you want to migrate your network configuration, you might need a maintenance window.
2. Network configuration migration might require network configuration changes in on-premises configuration.

