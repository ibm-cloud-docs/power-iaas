---

copyright:
  years: 2023

lastupdated: "2023-06-23"

keywords: PER, Power Edge Router, PER workspace, PER and Transit Gateway, IBM PER

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
<!-- {{site.data.keyword.powerSys_notm}} -->

# Getting started with Power Edge Router
{: #per}

A Power Edge Router (PER) is a high-performance physical router that is offered by IBM Cloud&reg; provides advanced routing capabilities for {{site.data.keyword.powerSysFull}} users.
{: shortdesc}

PER improves network communication across different parts of IBM network. This new system replaces the current Direct Link-based network connectivity.

The PER system creates a direct connection to the IBM Cloud MPLS (Multi Protocol Label Switching) backbone, making it easy for different parts of IBM network to communicate with each other. Specifically, IBM added a pair of routers to each {{site.data.keyword.powerSys_notm}} POD (acronym for Performance Optimized Datacenter that are basically modular datacenters) with an aggregate connectivity of 400 Gbps. 

IBM is sequentially rolling out PER and currently available in only `DAL10`.
{: note}

These new routers (PERs) associate specific {{site.data.keyword.powerSys_notm}} networks with unique MPLS route distinguishers (RDs). This makes it easy for different networks to communicate with each other across the IBM Cloud MPLS backbone.

To facilitate communication between {{site.data.keyword.powerSys_notm}} instances and other parts of the network, such as [Classic infrastructure](/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial), [Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-getting-started), and remote {{site.data.keyword.powerSys_notm}} instances, [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started&interface=ui) is used.

One of the benefits of the PER system is that it makes it easier for {{site.data.keyword.powerSys_notm}} instances user to access other IBM Cloud services, such as IBM Cloud DNS, NTP, Cloud Object Storage. You can connect to these services without having to use proxies or virtual routers, as the PER system includes a NAT solution that simplifies the process.

The following network architecture diagram explains how the PER is integrated in the IBM Cloud environment:

![Power Edge Router network architechture diagram](./images/per-network-arch-diag.svg "Power Edge Router network architecture diagram"){: caption="Figure 1. Power Edge Router network architechture diagram" caption-side="bottom"}

The network traffic in a PER environment can flow in the following two ways:
- Accessing classic infrastructure through Transit Gateway.
  - `1` - Traffic from ACI tenants is forwarded to the PER.
  - `2` - PER forwards the traffic to classic infrastructure services that use Transit Gateway
   
- Accessing cloud services that can access each other's resources.
  - `1`	- Traffic from ACI tenants is forwarded to the PER.
  - `3`	- Traffic from PER is forwarded to the NAT services with Service Gateway routers for conversion of destination addresses to ADN and CSE networks.
  - `4`	- The converted traffic from NAT is forwarded to PER. 
  - `2` - Traffic from PER is now forwarded to IBM Cloud PPRs for final delivery.
  <!-- what is the full form of PPR? POD to POD router. Where a pod is a modular datacenter which are generally organized/kept as racks -->

The automation of ACI, PER, and NAT Services provisioning in IBM data centres is carried with the intent that is defined by the IBM {{site.data.keyword.powerSys_notm}} team. 

## Considerations for using PER
{: leverage-per}

- You cannot create cloud connection and VPN connection on a PER workspace.
- Currently, you can only choose `DAL10` as the datacenter to create a PER workspace. 
- You can establish a connection between collocated workspaces if one colo is PER enabled (`DAL10`) and second colo (`DAL12` / `DAL13`) uses [Direct Link](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). Both collocated workspaces should be connected to the same Transit Gateway.
- When the PER workspace is connected to a Transit Gateway, you can connect a Direct Link to the same Transit Gateway to achieve end to end connectivity from your on-premises network to the PER workspace.
- You can establish a connection between VPC and Classic infrastructure with PER after adding them to the Transit Gateway.
- There is no additional pricing of PER. When you create a new PER workspace, you are charged with regular pricing. To calculate the exact pricing, use the [IBM cost estimator](https://cloud.ibm.com/estimator){: external} in IBM Cloud console.
- When you create private networks in a PER workspace, a maximum of one DNS server can be specified. 

## Miigration to PER
{: migrate-per}

PER is not supported on existing {{site.data.keyword.powerSys_notm}} workspaces. To use PER, create a new workspace with `DAL10` as datacenter.

The automated migration of your existing network is not supported. But if your existing workspaces are in `DAL10` and uses Transit Gateway based Cloud Connection, you are able to easily connect into new PER network instances.

Your existing {{site.data.keyword.powerSys_notm}} workspace continues to support Cloud Connection and VPNaaS.

The existing non-PER workspace continues to utilize existing routers. You will be able to utilize the high-performance routers when you migrate to or create a PER-enabled workspace.

## Creating a PER workspace
{: create-per-workspace}

To create a PER workspace, follow the steps that are mentioned in [Creating a Power Systems Virtual Server workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and choose `DAL10` as the datacenter.

You can check whether a workspace is PER enabled by selecting the workspace and view workspace's details. The PER enabled workspace shows an information message on PER and Transit Gateway.
{: note}

You can create, delete, attach, detach, update private networks by using the Subnets and Virtual server instances pages on a PER workspace the same as a non-PER workspace. However, private networks on PER workspaces in a PER enabled datacenter, such as `DAL10`, use upgraded networking technology for higher performance, and seamless connectivity. See, [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet) to perform a desired operation.

Use Transit Gateway only to configure the Virtual connections, as opposed to using Cloud Connection.

On a PER workspace, **Cloud Connections** and **VPN connections** options are not available in the left navigation of the user interface.
{: note}

On a PER workspace, you can perform the following actions:
1.  Attach a network without any requirement of creating a separate cloud connection such as Direct Link.
2.	Effortlessly attach a connection to IBM cloud network by attaching the Transit Gateway with your PER workspace
3.  Connect to your on-premises network by creating a Direct Link and attaching it with the Transit Gateway present on the PER workspace.

You cannot delete a PER workspaces that have Transit Gateway connections. You must delete the Transit Gateway connections first.

### Using IBM cloud services in a PER workspace
{: cloud-services-per}

From your PER workspace, you can create a virtual server instance and attach subnets to it. These virtual server instances can then access the IBM Cloud resources such as Cloud Object Storage(COS), Domain Name System (DNS), and other services that use the allocated IP addresses in the range `161.26.0.0` to `161.26.0.16`.

You need to attach Transit Gateway if you want to connect your workspace with the VPC and classic infrastructure.
{: important}

### Attaching Transit Gateway on PER workspace
{: tgw-per}

You need the Transit Gateway to connect with VPC and classic infrastructure. To attach a virtual server instance from PER workspace with Transit Gateway, complete the steps that are mentioned in [Ordering IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui)

Select **{{site.data.keyword.powerSys_notm}}** under connection to attach a virtual server instance that was created on a PER enabled workspace. You can also add VPC and Classic infrastructures as connection. 

The multiple connections that you add under Transit Gateway can ping each other. For example, if you add a {{site.data.keyword.powerSys_notm}} workspace and VPC under Transit Gateway connection, they both can access each other resource.

Make sure that the classic infrastructure is Virtual Routing and Forwarding (VRF) enabled before you attach it to the Transit Gateway.
{: note}

## OS support on PER workspace
{: os-per}

AIX, IBM i, and Linux operating systems are supported on a PER workspace.

### AIX and IBM i support on PER
{: aix-ibmi-per}

The AIX and IBM i operating systems operate on PER workspaces in the same way that they do on non-PER workspaces.

### Full Linux support on PER
{: aix-ibmi-per}

See [Full Linux® subscription for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-set-full-Linux) for {{site.data.keyword.powerSys_notm}} to register `RHEL84`, `SLES SP2`, `SLES SP3` images on a non-PER workspace.
{: note}

The full Linux subscription `RHEL86` and `SLES15 SP4` images can be used on a PER workspace for registration. Follow these instructions on a PER-enabled workspace to let the virtual server instance automatically register a full Linux subscription:
1.  Create a private network.
  1.  Open the {{site.data.keyword.powerSys_notm}} user interface from the IBM Cloud console.
  2.  Click **Subnets** under **Networking** in the left navigation menu.
  3.  Click **Create subnet**.
  4.  Enter a unique name and CIDR.
      Make sure the CIDR being used is not the same as another CIDR already in use or a subset of that CIDR. The host server for the satellite server will be unable to resolve a network conflict as a result. 
  5.  Enter `161.26.0.10` in the **DNS server** field.

2. Create a virtual server instance. See, [Configuring a Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) for detailed instructions.
3. Attach the private network that you have created in step 1.
4. Verify if the registration is successful with the following commands:
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

## CLI and API support on PER
{: cli-api-per}

PER uses the existing {{site.data.keyword.powerSys_notm}} networks APIs and CLIs.

See the {{site.data.keyword.powerSys_notm}} documentation on
- API - [Create a new cloud connection](/apidocs/power-cloud#pcloud-cloudconnections-post)
- CLI - [Create a cloud connection](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-connection)