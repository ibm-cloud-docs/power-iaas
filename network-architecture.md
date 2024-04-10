---

copyright:
  years: 2019, 2023

lastupdated: "2023-11-30"

keywords: networking diagrams, network architecture, private ssl, private ipsec, direct link connect, colocation, data center, cloud connect, megaport

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network architecture diagrams
{: #network-architecture-diagrams}

This topic describes typical network architectures that are used in the {{site.data.keyword.powerSysShort}} network architecture and is not an exhaustive list of {{site.data.keyword.powerSys_notm}} connection methods.
{: shortdesc}

## {{site.data.keyword.powerSys_notm}} networking environment
{: #networking-environment}

When you create a {{site.data.keyword.powerSys_notm}}, you can select a private or public network interface. For more information, see [Public and Private networks](/docs/power-iaas?topic=power-iaas-about-virtual-server#public-private-networks).  

{{site.data.keyword.powerSys_notm}} network architectures consist of one or more of the following networks:

- IBM Cloud infrastructure networks - While the following infrastructure network environments offer different features and are managed separately, they can be connected to each other to provide layer-3 IPv4 traffic flow: 
    - Classic - Classic network resources include VLANs, subnets, and SSL Virtual Private Network (VPN) access. See [Network security architecture](https://www.ibm.com/cloud/architecture/architectures/network-security-arch/){: external} for a description of the classic network components. Bring Your Own IP (BYOIP) is not supported. 
    - Virtual Private Cloud (VPC) - VPC network resources include subnets, floating IPs, security groups, and VPN gateways. For more information, see [About networking](/docs/vpc?topic=vpc-about-networking-for-vpc). See [Advanced networking for IBM Cloud VPC](https://www.ibm.com/cloud/architecture/content/course/advanced-networking-for-vpc/){: external} for a one-hour course on VPC networking. BYOIP is supported.  
    - Power Systems - Network resources include subnets. BYOIP is supported.
- Overlay networks - These networks exist in the IBM Cloud VMware Shared and VMware Dedicated offerings. While technically hosted in the IBM Cloud classic infrastructure environment, these networks are implemented in VMware NSX and under your direct control, including the IP addressing schema. BYOIP is supported. Therefore, overlay networks cannot be routed by the IBM Cloud infrastructure networks; access is through tunnels. 
- External:
    - Internet - Access the internet through resources that are hosted in any of these three infrastructure environments.
    - Remote - Connect remote networks to your IBM Cloud networks. You can use the following services to connect to a remote network:
        - Internet VPN - Uses the public internet to connect remote networks and their IBM Cloud networks through a VPN. The VPN is terminated on gateway devices or a service within IBM Cloud.
        - {{site.data.keyword.dl_short}} - {{site.data.keyword.dl_short}} is a suite of offerings that enable the creation of direct, private connections between your remote, on-premises network and IBM Cloud, without traversing the public internet. For more information, see [Getting started with IBM Cloud {{site.data.keyword.dl_short}} (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl). 

      You can connect {{site.data.keyword.dl_short}}s to either a local or remote {{site.data.keyword.tg_full_notm}}, which allows the on-premises network to access all networks that are connected to the {{site.data.keyword.tg_full_notm}}.
      {: note}

## Power Edge Router use cases
{: #per-use-cases}

Using a Power Edge Router (PER) enabled workspace provides the following benefits:

* Improved performance with aggregated bandwidth of 400 Gbps.
* Direct access to IBM cloud services from {{site.data.keyword.powerSys_notm}} workspace.
* Direct access to {{site.data.keyword.powerSys_notm}} from on-premises environment by using a Direct Link connect or Direct Link dedicated.

The following are some of the use cases of a PER-enabled {{site.data.keyword.powerSys_notm}} workspace:
1. [Connecting an on-premises data center](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-on-orem)
2. [Connecting to classic infrastructure](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-classic)
3. [Connecting to Virtual Private Cloud](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-vpc)
4. [Connecting to IBM Cloud services](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-cloud-services)
5. [Connecting multiple workspaces](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-accross-dc)

The above are base capability use cases. These base capabilities use cases can be customized to meet any specific requirement.
{: important}

### Connecting an on-premises data center
{: #per-on-orem}

1. In this depiction, the on-premises data center uses a direct link connection to attach to the transit gateway. 

2. A PER-enabled {{site.data.keyword.powerSys_notm}} workspace can be attached to the same transit gateway, which in turn enables connectivity to the on-premises data center via the incoming direct link that is interconnected through this transit gateway.
3. You will pay for the Direct Link connection that you use  to connect your on-premises with the transit gateway. There is no cost involved for using upto 4 connections on a local transit gateway. For more information on transit gateway pricing, see: [Pricing for Power Edge Router](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-power-edge-router).

![Connecting on-premises with a PER-enabled workspace](./images/2_PER_Onprem.svg "Connecting on-premises with a PER-enabled workspace"){: caption="Figure 9. Connecting on-premise with a PER-enabled {{site.data.keyword.powerSys_notm}}" caption-side="bottom"}

### Connecting to classic infrastructure
{: #per-classic}

1. Establish a connection between PER-enabled {{site.data.keyword.powerSys_notm}} workspace and the classic infrastructure by using local routing of transit gateway.
2. Involves no additional transit gateway charges. For such connection the following conditions should be satisfied:
    - The workspace and the classic infrastructure should be in the same region.
    - The workspace should be connected to a transit gateway.

For more information on transit gateway pricing, see: [Pricing for Power Edge Router](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-power-edge-router).

![Connecting PER workspace with classic with custom IP](./images/1_PER_classic.svg "Connecting PER workspace with classic infrastructure with/without custom IP"){: caption="Figure 10. Connecting PER workspace with classic" caption-side="bottom"}



Here are the following two scenarios for connecting to classic that are differentiated based on GRE tunnel requirement:

**When a GRE tunnel is not needed.**

A Generic Routing Encapsulation (GRE) tunnel is not required when you want to establish a connection from your PER-enabled workspace with classic infrastructure provided you do not have any custom IP address on your workspaces.

   - The Backend Customer Router (BCR) allows an IBM Cloud IP address (`10.0.0.0/8`) only to pass through.
   - If you use any other IP address other than `10.0.0.0/8`, you might need to configure a GRE tunnel.

**When a GRE tunnel is needed.**

A GRE tunnel is required when you want to establish a connection from your PER-enabled workspace with classic infrastructure that uses a custom IP address.

   - The classic subnet is located behind the Backend Connect Router (BCR) router.
   - The custom IP address for example `172.X.X.X` that originates from your workspace is dropped and not allowed to pass through to classic subnet by the Backend Customer Router (BCR).
   - The BCR allows an IBM Cloud IP address (`10.0.0.0/8`) only to pass through.

Hence, if you have a custom IP address in your PER-enabled workspace, you need a GRE tunnel that wraps the custom IP address with another header. This GRE tunnel needs to be attached with the transit gateway.

For detailed steps, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-cloud-connections#configure-gre-tunnel).

### Connecting to Virtual Private Cloud
{: #per-vpc}

1. Establish a connection between PER-enabled {{site.data.keyword.powerSys_notm}} workspace and Virtual Private Cloud (VPC) using the transit gateway.
2. You can also connect the classic infrastructure with the same transit gateway to create a multi-connection network. This establishes a three-way communication. 
3. Thus, the PER-enabled workspace, VPC, and classic infrastructure can establish connection with each other.

The pricing for this connection depends upon the local or global transit gateway usage. See: [Pricing for Power Edge Router](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-power-edge-router).

![Connecting PER workspace with VPC](./images/3.PER_VPC.svg "Connecting PER workspace with VPC"){: caption="Figure 11. Connecting PER workspace with VPC" caption-side="bottom"}

### Connecting to IBM Cloud (Classic) services via Secure Endpoint (SE)
{: #per-cloud-services-se}

A PER-enabled {{site.data.keyword.powerSys_notm}} workspace can by default connect to IBM Cloud Service Endpoints (CSE), and can also seamlessly connect with the Secure Endpoints (SE) in the Classic Infrastructure environment when using a Transit Gateway.

1. A PER-enabled {{site.data.keyword.powerSys_notm}} workspace is connected to the Classic Infrastructure environment using a Transit Gateway.
2. A {{site.data.keyword.powerSys_notm}} can then connect to the Secure Endpoint (SE) of the IBM Cloud (Classic) services.
    
    On a PER-enabled workspace that uses a custom IP address, the network is routed through a Network Address Translator (NAT) device that converts the custom IP address into an IBM Cloud supported IP address. 

For information on transit gateway pricing, see: [Pricing for Power Edge Router](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-power-edge-router).

![Connecting PER workspace to IBM Cloud (Classic) services via Secure Endpoint (SE)](./images/4_PER_Cloudservices.svg "Connecting PER workspace to IBM Cloud (Classic) services via Secure Endpoint (SE)"){: caption="Figure 12. Connecting PER workspace to IBM Cloud (Classic) services via Secure Endpoint (SE)" caption-side="bottom"}

### Connecting multiple workspaces across a data center
{: #per-accross-dc}

1. Use the local transit gateway to connect multiple {{site.data.keyword.powerSys_notm}} workspaces that are across different zones but in the same region.
    A PER-enabled workspace needs to be attached with the transit gateway that can exchange routes between two workspaces. 
2. When the workspaces are present in different regions, use a global transit gateway to inter-connect them.

To know more about the transit gateway charges for local and global routing, see: [Pricing for Power Edge Router](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-power-edge-router).

![Connecting workspaces in different regions](./images/5_PER_PER.svg "Connecting workspaces in different regions"){: caption="Figure 13. Connecting workspaces in different regions" caption-side="bottom"}