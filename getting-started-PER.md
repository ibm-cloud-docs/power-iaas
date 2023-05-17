---

copyright:
  years: 2023

lastupdated: "2023-05-09"

keywords: PER, Power Edge Router, PER workspace, PER and Transit gateway, IBM PER

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

# Getting Started with Power Edge Router
{: #per}

A Power Edge Router (PER) is a high-performance virtual router offered by IBM Cloud&reg; that provides advanced routing capabilities for {{site.data.keyword.powerSysFull}} users.
{: shortdesc}

PER improves network communication across different parts of IBM network. This new system will replace the current Direct Link-based network connectivity.

The PER system will create a direct connection to the IBM Cloud MPLS (Multi Protocol Label Switching) backbone, making it easier for different parts of IBM network to communicate with each other. Specifically, IBM have added a new pair of routers to each {{site.data.keyword.powerSys_notm}} pod (a collection of virtual servers instance) with an aggregate connectivity of 400 Gbps.

These new routers (PERs) will associate specific {{site.data.keyword.powerSys_notm}} networks (which are like individual workspaces) with unique MPLS route distinguishers (RDs), making it easier for different networks to communicate with each other across the IBM Cloud MPLS backbone.

To facilitate communication between {{site.data.keyword.powerSys_notm}} instances and other parts of the network, such as Classic, VPC, and remote {{site.data.keyword.powerSys_notm}} instances, Transit Gateway (TGW) is used.

One of the benefits of the PER system is that it will make it easier for {{site.data.keyword.powerSys_notm}} instances user to access other IBM Cloud services, such as IBM Cloud DNS, NTP, Cloud Object Storage, etc. You'll be able to connect to these services without having to use proxies or virtual routers, as the PER system includes a NAT solution that simplifies the process.

The following network architecture diagrams explains how the PER is integrated in the IBM Cloud environment:

![Power Edge Router network architechture diagram](./images/per-network-arch-diag.svg "Power Edge Router network architechture diagram"){: caption="Figure 1. Power Edge Router network architechture diagram" caption-side="bottom"}

The network traffic in a PER environment can flow in the following two ways:
- Accessing classisc infrastructure thruogh Transit Gateway.
  `1` - Traffic from ACI tenants is forwarded to the PER.
  `2` - PER forwards the traffic to classic infrastructure services using Transit Gateway
   
- Accessing cloud services and pinging each other
  `1`	- Traffic from ACI tenants is forwarded to the PER.
  `4`	- Traffic from PER is forwarded to the NAT services provided by Cisco Catalyst 8300 Service Gateway routers for translation of destination addresses to ADN and CSE networks.
  `3`	- The translated traffic from NAT is forwarded to PER which performs SR/MPLS handoff to exchange information for all prefixes in all VRFs via BGP EVPN session. 
<!-- what is the full form of PPR? -->
  `2` - Traffic from PER is now  forwarded to IBM Cloud PPRs for final delivery.

The automation of ACI, PER, and NAT Services provisioning in IBM data centers is carried out by Cisco as per the intent defined by the IBM {{site.data.keyword.powerSys_notm}} team. 

## Creating a PER workspace
{:create-per-workspace}

<!-- Q: Does a user gets the option to choose b/w PER or a non-PER workspace? -->
A PER workspace is same as the non-PER workspace except that the PER workspace will have two additional attributes as follows:
1.	Route distinguisher (RD)
2.	Route target (RT)
<!-- Q: How do I check back that my workspace have these 2 attr? -->

These attributes are automatically created when you create a workspace in the data center where PER is deployed.

To create a PER workspace follow the steps mentioned in [Creating a Power Systems Virtual Server workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and choose DAL10 as the data center.
<!-- Q: Pprovide a list of data centers have PER deployed in them: -->
<!-- Q: Is there any TGW API that lists all the PER supported DCs -->
You can check if a workspace is PER enabled by selecting the workspace and view workspace's details. The PER enabled workspace shows an info message on PER and Transit Gateway.
{: note}

You can attach, detach, update network using the subnets page in a PER workspace like a non-PER workspace. Workspaces in the PER enabled data center such as DAL10, leverage upgraded networking technology for higher performance and seamless connectivity.

You must use Transit Gateway only to configure the Virtual connections, as opposed to using cloud connections.

In a PER workspace you can do the following:
1.	Attach a network without any requirement of creating a separate cloud connection such as Direct Link.
2.	Effortlessly attach a connection to IBM cloud network by attaching the Transit Gateway with your virtual server instance.

### Using IBM cloud services in a PER workpace
{: cloud-services-per}

From your PER workspace, you can create a virtual server instance and attach subnets to it. These virtual server instances can then access the IBM Cloud resources such as Cloud Object Storage(COS), Domain Name System (DNS), and other services that use the allocated IP addresses in the range `161.26.0.0` to `161.26.0.16`.

You will need to attach Transit Gateway if you wish to connect your workspace with the Virtual Private Cloud (VPC) and classic infrastructure.
{: important}

### Attaching Transit Gateway to a PER workpace
{: tgw-per}

You will need the Transit Gateway to connect with VPC and classic infrastructure. To attach a virtual server instance from PER workspace with Transit Gateway complete the steps mentioned in [Ordering IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui)

You must select **{{site.data.keyword.powerSys_notm}}** under connection to attach a virtual server instance that was created in a PER enabled workspace. You can also add VPC and Classic infrastructures as connection. 

The multiple connections that you add under Transit Gateway can ping each other. For example, if you add a {{site.data.keyword.powerSys_notm}} workspace and VPC under Transit Gateway connection, they both can access each other resources.
<!-- Check correctness -->

Make sure the classic infrastructure is VRF enabled before you attach it to the Transit Gateway.
{: note}
