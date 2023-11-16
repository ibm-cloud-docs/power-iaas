---

copyright:
  years: 2023

lastupdated: "2023-09-29"

keywords: PER, Power Edge Router, PER workspace, PER and Transit Gateway, IBM PER

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Getting started with the Power Edge Router
{: #per}

A Power Edge Router (PER) is a high-performance router that provides advanced routing capabilities for {{site.data.keyword.powerSysFull}} users.
{: shortdesc}

PER improves network communication across different parts of the IBM network. The PER solution creates a direct connection to the IBM Cloud MPLS (Multi Protocol Label Switching) backbone, making it easy for different parts of the IBM network to communicate with each other. The PER solution is consisted of two routers that enable an aggregate connectivity of 400 Gbps to each {{site.data.keyword.powerSys_notm}} POD (acronym for Performance Optimized Data center that is modular data centers). 

The PER solution is available in `DAL10` and `WDC06` data centers. PER will be deployed in other data centers over time.
{: note}

PER associates specific {{site.data.keyword.powerSys_notm}} networks with unique MPLS route distinguishers (RDs). This makes it easy for different networks to communicate with each other across the IBM Cloud MPLS backbone.

To facilitate communication between {{site.data.keyword.powerSys_notm}} instances and other parts of the network, such as [Classic infrastructure](/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial), [Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-getting-started), and remote {{site.data.keyword.powerSys_notm}} instances, [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started&interface=ui) is used.

One of the benefits of the PER solution is that it makes it easier for a {{site.data.keyword.powerSys_notm}} user to access other IBM Cloud services, such as IBM Cloud DNS, NTP, and Cloud Object Storage. You can connect to these services without having to use proxies or virtual routers, as the PER solution includes a Network Address Translation (NAT) device that simplifies the access process.

The following network architecture diagram explains how the PER is integrated into the IBM Cloud environment:

![Power Edge Router network architecture diagram](./images/per-network-arch-diag.svg "Power Edge Router network architecture diagram"){: caption="Figure 1. Power Edge Router network architecture diagram" caption-side="bottom"}

The network traffic in a PER environment can flow in the following two ways:
- Accessing classic infrastructure through Transit Gateway.
  - `1` - Traffic from ACI tenants is forwarded to the PER.
  - `2` - PER forwards the traffic to classic infrastructure services that use Transit Gateway.
   
- Accessing cloud services that can access each other's resources.
  - `1`	- Traffic from ACI tenants is forwarded to the PER.
  - `3`	- Traffic from PER is forwarded to the NAT services with Service Gateway routers for conversion of destination addresses to ADN and CSE networks.
  - `4`	- The converted traffic from NAT is forwarded to PER. 
  - `2` - Traffic from PER is now forwarded to IBM Cloud PPRs for final delivery.
  <!-- what is the full form of PPR? POD to POD router. Where a pod is a modular datacenter which are generally organized/kept as racks -->

The automation of ACI, PER, and NAT Services provisioning in IBM data centers is designed to simplify network integration and accelerate connection time for IBM Power Systems Virtual Server users in the IBM Cloud.

## Considerations when using PER
{: leverage-per}

- You cannot create a Cloud Connection or a VPN connection in a PER workspace.
- Currently, you can only choose `DAL10` as the data center to create a PER workspace. 
- You can establish a connection between collocated workspaces if one colo is PER-enabled (`DAL10`) and the second colo (`DAL12` / `DAL13`) uses [Direct Link](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). Both collocated workspaces should be connected to the same Transit Gateway.
- When a PER workspace is connected to a Transit Gateway, you can connect a Direct Link to the same Transit Gateway to achieve end to end connectivity from your on-premises network to the PER workspace.
- You can establish a connection between VPC and Classic infrastructure with PER after adding them to the Transit Gateway.
- When you create private networks in a PER workspace, a maximum of one DNS server can be specified.
- A GRE (Generic Routing Encapsulation) tunnel is not supported in a PER workspace.
- You cannot create a non-PER workspace in a PER-enabled data center. However, you can still use your old non-PER workspaces that are existing in a PER-enabled data center that are created before PER rollout.
- In certain situations, local connection charges can apply when connecting from an on-premises location to {{site.data.keyword.powerSys_notm}}. To ensure accurate pricing, it is important to use the cost estimator tool. See the [Pricing of Power Edge Router](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-power-edge-router) to learn more about PER pricing.

## Migrating to PER
{: migrate-per}

PER is not supported in existing {{site.data.keyword.powerSys_notm}} workspaces. To use PER, you need to create a new workspace (currently available in `DAL10` ).

The automated migration of your existing network is not supported, but if your existing workspaces are in `DAL10` and use a Transit Gateway based Cloud Connection, you can easily connect to new PER network instances.

Existing {{site.data.keyword.powerSys_notm}} workspaces continue to support Cloud Connection and VPNaaS.

Existing non-PER workspaces continue to use existing routers. To use the PER solution's high-performance routers, you can create a new PER-enabled workspace to deploy in while continuing to use the non-PER-enabled workspace. You can also migrate existing workloads into the new PER-enabled workspace by backing up the data from the existing workspace and restoring the data into the PER-enabled new workspace. 

## Creating a PER workspace
{: create-per-workspace}

To create a PER workspace, follow the steps that are mentioned in [Creating a Power Systems Virtual Server workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and choose `DAL10` as the data center.

You can check whether a workspace is PER-enabled by selecting the workspace and viewing the workspace's details. The PER-enabled workspace shows an information message regarding PER and Transit Gateway.
{: note}

You can create, delete, attach, detach, and update private networks by using the **Subnets** and **Virtual server instances** pages on a PER workspace, the same as with a non-PER workspace. However, private networks on PER workspaces in a PER-enabled data center, such as `DAL10`, use upgraded networking technology for higher performance, and seamless connectivity. See, [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet) to perform a wanted operation.

Use Transit Gateway only to configure the Virtual connections, as opposed to using Cloud Connection.

On a PER workspace, **cloud Connections** and **VPN connections** options are not available in the left navigation of the user interface since they are not required or supported by PER.
{: note}

On a PER workspace, you can perform the following actions:
1.  Attach a network without any requirement of creating a separate Cloud Connection such as Direct Link.
2.	Effortlessly attach a connection to the IBM cloud network by attaching the Transit Gateway with your PER workspace.
3.  Connect to your on-premises network by creating a Direct Link and attaching it with the Transit Gateway present on the PER workspace.

You cannot delete PER workspaces that have Transit Gateway connections. You must delete the Transit Gateway connections first.
{: important}

### Using IBM cloud services in a PER workspace
{: cloud-services-per}

From your PER workspace, you can create a virtual server instance and attach subnets to it. These virtual server instances can then access the IBM Cloud resources such as Cloud Object Storage (COS), Domain Name System (DNS), and other services that use the allocated IP addresses in the range `161.26.0.0/16`. See [IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints) for more information.

You need to attach to the Transit Gateway if you want to connect your workspace with the VPC and classic infrastructure.
{: important}

### Attaching Transit Gateway to a PER workspace
{: tgw-per}

Transit Gateway is required to connect with VPC and classic infrastructure. To attach a virtual server instance from a PER workspace with Transit Gateway, complete the steps that are mentioned in [Ordering IBM Cloud Transit Gateway.](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui)

Select **{{site.data.keyword.powerSys_notm}}** under connection to attach a virtual server instance that was created on a PER-enabled workspace. You can also add VPC and Classic infrastructures as connection. 

The connections that you attach to the Transit Gateway can ping each other. For example, if you add a {{site.data.keyword.powerSys_notm}} workspace and VPC under Transit Gateway connection, they both can access each other resource.

Make sure that the classic infrastructure is Virtual Routing and Forwarding (VRF) enabled before you attach it to the Transit Gateway.
{: note}

## OS support in a PER workspace
{: os-per}

AIX, IBM i, and Linux operating systems are supported in a PER workspace.

### AIX and IBM i support on PER
{: aix-ibmi-per}

AIX and IBM i operating systems operate in PER workspaces in the same way that they do in non-PER workspaces.

### Full Linux Subscription with PER
{: aix-ibmi-per}

See [Full Linux® subscription for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-set-full-Linux) for {{site.data.keyword.powerSys_notm}} to register `RHEL84`, `SLES SP2`, `SLES SP3` images on a non-PER workspace.
{: note}

Full Linux subscription `RHEL86` and `SLES15 SP4` images can be used in a PER workspace. Follow these instructions for a PER-enabled workspace to let the virtual server instance automatically register a full Linux subscription:
1.  Create a private network.
  1.  Open the {{site.data.keyword.powerSys_notm}} user interface from the IBM Cloud console.
  2.  Click **Subnets** under **Networking** in the left navigation menu.
  3.  Click **Create subnet**.
  4.  Enter a unique name and CIDR.
      Make sure the CIDR being used is not the same as another CIDR already in use or a subset of that CIDR. The host server for the satellite server will be unable to resolve a network conflict as a result. 
  5.  Enter `161.26.0.10` in the **DNS server** field.

2. Create a virtual server instance. See, [Configuring a Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) for detailed instructions.
3. Attach the private network that you have created in step 1.
4. Verify whether the registration is successful with the following commands:
  
 For SUSE:
   ```
   SUSEConnect -s
   ```
   {: codeblock}

 For RHEL:
   ```
   subscription-manager status
   ```
   {: codeblock}

## CLI and API support with PER
{: cli-api-per}

PER uses the same existing {{site.data.keyword.powerSys_notm}} network APIs and CLIs.

For more information, refer to the {{site.data.keyword.powerSys_notm}} documentation on:
- API - [Create a new cloud connection](/apidocs/power-cloud#pcloud-cloudconnections-post)
- CLI - [Create a cloud connection](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-connection)

<!-- ## Various sample application scenarios
{: scenarios-per}

There are various application scenarios that can be possible based on your choice of a PER or a non-PER workspace. The table below describes some of the various possible application scenarios:

| Scenarios | {{site.data.keyword.powerSys_notm}} DL without Transit Gateway| {{site.data.keyword.powerSys_notm}} DL with Transit Gateway |{{site.data.keyword.powerSys_notm}} PER workspace|
|-----------|-------------------|---------------------|-------------------|
| IBM Cloud local VPC and Classic resources access (x86 VMs etc.)|	DL local routing [^footnote1] |	TGW local routing	| TGW local routing|
| IBM Cloud remote VPC resource access	| DL global routing [^footnote2] |	TGW global routing	| TGW globa	routing |
| {{site.data.keyword.powerSys_notm}} multi-location connectivity for HA DR etc.	| DL + vSRX [^footnote3] | TGW global routing | 	TGW global routing |
| {{site.data.keyword.powerSys_notm}} multi-location connectivity (unipart)	| DL + classic + VPC	[^footnote7]| TGW global routing (improved connection) |	TGW global routing | 
| {{site.data.keyword.powerSys_notm}} GRS	(Global Replication Service) | DL + Megaport [^footnote6]	| TGW global routing 	(to test) | TGW global routing |
| On-premise to {{site.data.keyword.powerSys_notm}} connectivity	| DL + vSRX [^footnote4] |	TGW global routing | TGW global routing |
|{{site.data.keyword.powerSys_notm}} to Cloud Services (COS, DNS, NTP etc.)	| Use proxy server [^footnote5] | - | Use NAT to reach services |			
| Aggregate Bandwidth shared by all customers, between {{site.data.keyword.powerSys_notm}} and IBM Cloud	| 60 Gb/s [^footnote8]	| 60 Gb/s [^footnote9]	| 400 Gb/s |
|User Experience	| Ok | Better	| Excellent |
{: caption="Table 1. Various application scenarios" caption-side="bottom"}

[^footnote1]: No charges apply.
[^footnote2]: No charges apply.
[^footnote3]: Involves cost, complexity, and low performance. Considering Megaport
is used for DL2DL connection.
[^footnote4]: Involves cost, complexity, and low performance. Other options, includes on-premise over DL to classic to PowerVS over DL to classic
[^footnote5]: Involves cost and complexity
[^footnote6]: Involves high cost
[^footnote7]: Combination no longer in use.
[^footnote8]: Typical speed.
[^footnote9]: Typical speed. -->

