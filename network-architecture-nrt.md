---

copyright:
  years: 2019, 2021

lastupdated: "2021-06-23"

keywords: networking diagrams, network architecture, private ssl, private ipsec, direct link, colocation, data center, cloud connect, megaport

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

# Network architecture diagrams
{: #network-architecture-diagrams}

## Overview
{: #network-architecture-overview}

This topic describes typical network architectures that are used in {{site.data.keyword.powerSysShort}} (PowerVS) network architecture and is not an exhaustive list of {{site.data.keyword.powerSys_notm}} connection methods.
{: shortdesc}

IBM Cloud Connect is only available to IBM clients within the US. IBM clients can always contact Megaport connectivity services directly to procure their services.
{: important}

## IBM PowerVS networking environment
{: #networking-environment}

When you create a Power Systems Virtual Server, you can select a private or public network interface. For more information, see [Public and Private networks](/docs/vpc?topic=power-iaas-about-virtual-server#public-private-networks){: external}. Refer to the [Glossary](/docs/overview?topic=overview-glossary){: external} topic for any new terms. 

{{site.data.keyword.powerSysShort}} network architectures consist of one or more of the following networks:

- IBM Cloud infrastructure environment networks - While the following infrastructure network environments offer different features and are managed separately, they can be connected to each other to provide layer 3 IPv4 traffic flow: 
    - Classic - Network resources include VLANs, subnets and SSL VPN access, however, bring your own IP is not supported. See [Network security architecture](https://www.ibm.com/cloud/architecture/architectures/network-security-arch/){: external} for a description of the Classic network components.
    - Virtual Private Cloud - Network resources include subnets, floating IPs, security groups and VPN gateways, see [About networking](/docs/vpc?topic=vpc-about-networking-for-vpc). Bring your own IP is supported. See [Advanced networking for IBM Cloud VPC](https://www.ibm.com/cloud/architecture/content/course/advanced-networking-for-vpc/){: external} for a 1 hour course on VPC networking.
    - IBM Cloud Services – 
    - Power Systems - Network resources include subnets and bring your own IP is supported.
- Overlay - Overlay networks exist in the IBM Cloud VMware&trade Shared and VMware&trade Dedicated offerings and while technically they are hosted in the IBM Cloud classic infrastructure environment, they are implemented in VMware&trade NSX and, therefore, under your direct control, including the IP addressing schema, so bring your own IP is supported. Therefore, overlay networks cannot be routed by the IBM Cloud infrastructure environment networks access is via tunnels. 
- External:
    - Internet - The Internet can be accessed via resources that are hosted in any of the three infrastructure environments.
    - Remote - Remote networks are networks that you want to connect to your IBM Cloud networks and can be connected by using:
        - Internet VPN - Uses the public internet to connect customer remote networks and their IBM Cloud networks, via a Virtual Private Network (VPN). The VPN is terminated on gateway devices or a service within IBM Cloud.
        -  Direct Link - Direct Link is a suite of solutions that enables customers to create direct, private connections between their remote network environments and their IBM Cloud networks, without using the public internet. See [Getting started with IBM Cloud Direct Link (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) for further information. For locations not supported by Direct Link (2.0), see [Getting started with IBM Cloud Direct Link on Classic](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link).

## Use Cases
{: #networking-use-cases}

This documentation describes the following network deployment topologies:

* Connecting IBM PowerVS to IBM Cloud Classic infrastructure by using IBM Direct Link 2.0 - Typical use cases for this topology are as follows:
    - Use IBM Cloud Classic x86 resources to create tiered applications across different hardware platforms, that is, x86 application servers and Power database servers.
    - Build a backup and restore environment based on [IBM Spectrum Protect Cloud Blueprints](https://www.ibm.com/support/pages/ibm-spectrum-protect-cloud-blueprints) for both IBM Spectrum Protect and IBM Spectrum Protect Plus topologies. Also, see, [AIX Backups with IBM Power Virtual Server](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Backups_Tutorial_v1.pdf).
* Connecting IBM PowerVS to IBM Cloud VPC infrastructure environment by using Direct Link Connect - TTypical use cases for this topology are as follows: 
    - Use IBM Cloud VPC x86 resources to create tiered applications across different hardware platforms, that is, x86 application servers and Power database servers.
* Connecting PowerVS to on-premises network by using Megaport or IBM Cloud Connect- A typical use case for this topology is that you require access to your Power virtual servers from your external networks, such as networks on your premises. This topology uses Megaport services or IBM Cloud Connect.
* Connecting two Power Systems Virtual Server environments by using Megaport or IBM Cloud Connect- This topology connects two or more Power virtual server environments together by using Megaport services or IBM Cloud Connect. Connecting two or more environments together enables use cases such as disaster recovery.
* Connecting PowerVS to on-premises network via IBM Classic Infrastructure environment by using private SSL connection and a jump server- This is a specific use case for connecting to the classic environment so that the SSL VPN connection can be used to access your Power VS servers for operations and administration tasks.
* Connecting PowerVS to on-premises network via IBM Cloud Classic Infrastructure by using an internet IPsec VPN connection- This is a specific use case for connecting to the classic environment so that an IPsec VPN connection can be used to access your classic and Power VS servers. This network architecture is typically used for small production environments or proof-of-concept, development, and test purposes.
* Connecting PowerVS to on-premises network through IBM Cloud Classic Infrastructure by using a Private Direct-Link connection- A Direct Link enables your remote networks to connect to IBM Cloud over a private connection that does not use public networks.

Multiple deployment topologies, described in this document, can be layered to create the desired topology required.

## Connecting to Classic infrastructure by using IBM Direct Link (2.0)
{: #network-reference-architecture-classic}

In this deployment topology, a Direct Link 2.0 is used to connect your {{site.data.keyword.powerSysShort}} networks to your resources hosted in your IBM Cloud Classic infrastructure environment. You can either [order a Direct Link Connect (2.0)](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect) connections or use Cloud connections. 

![Connecting IBM PowerVS to IBM Cloud Classic infrastructure by using IBM Direct Link (2.0)](./images/network-connect-to-classic.svg "Connect to Classic"){: caption="Figure 3. Connect to Classic" caption-side="bottom"}

Complete the following steps to implement this scenario:

1. Define the IP address schema of your PowerVS subnets in your PowerVS environment. Your PowerVS instances are hosted on these PowerVS subnets. Ensure that you do not overlap the PowerVS subnets with your IBM Cloud Classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Order a [Direct Link Connect (2.0)](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0) or provision a [Cloud Connection](/docs/power-iaas?topic=power-iaas-cloud-connections) instance from the PowerVS interface to connect the PowerVS router to the IBM Cloud Classic infrastructure environment. This connection is established and operated by the IBM Cloud team and you have no direct access or control. Consider the following information before you proceed:
    - Ensure that you select the virtual routing and forwarding (VRF) option when you provision a Direct-Link connection. The VRF option allows multiple instances of a routing table to exist in a router and to work simultaneously. With VRF, each IBM Cloud account Classic environment network is segmented within its own routing table. For more information, see [Virtual routing and forwarding on IBM Cloud](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).
    - When this connection is established, the Border Gateway Protocol (BGP) is configured automatically by the IBM Cloud team in the following way:
        - The PowerVS router advertises your PowerVS subnets to the Classic infrastructure environment. 
        - The Classic infrastructure advertises only your IBM Cloud Classic private subnets to the PowerVS router. 
        - The Classic infrastructure filters the following networks from the BGP advertisements coming from the PowerVS router because these IP addresses are used by the services networks: 10.0.0.0/14, 10.198.0.0/15, 10.200.0.0/14, 169.254.0.0/16, 224.0.0.0/4 and any IP ranges that are assigned to your IBM Cloud Classic private subnets.
          You can use the 10.x.x.x range if there is not a conflict with an IBM Cloud backend 10.x.x.x service. You must contact support if you want to use NAT'ing or IP aliasing to resolve the IP conflict. However, IBM does not recommend using the 10.x.x.x range when you create a new network.
          {: important}

3. Identify the IBM Cloud Classic private subnets and the IP address schema that is assigned to you when you ordered bare metal or virtual server instances that are hosted on your IBM Cloud Classic private subnets and connect to the required resources and services.
    All the routers in all Classic infrastructure data centers and points of presence across the global IBM Cloud backbone are connected to the PowerVS router by using the Direct Link Connect VRF-enabled connection. 

    Each IBM Cloud Direct Link service is not redundant. However, diversity can be engineered using multiple direct links and BGP. See [Models for diversity and redundancy in Direct Link (2.0)](/docs/dl?topic=dl-models-for-diversity-and-redundancy-in-direct-link)
    {: note}

## Connecting to VPC by using Direct Link Connect
{: #network-reference-architecture-vpc}

In this deployment topology, a Direct Link 2.0 is used to connect your {{site.data.keyword.powerSysShort}} networks to your resources that are hosted in the IBM Cloud VPC infrastructure environment.

![Connect to VPC](./images/network-connect-to-vpc.svg "Connect to VPC"){: caption="Figure 4. Connect to VPC" caption-side="bottom"}

Complete the following steps to implement this scenario:

1. Define the IP address schema of your PowerVS subnets in your PowerVS environment. Your PowerVS instances are hosted on these PowerVS subnets. Ensure that you do not overlap the PowerVS subnets with your IBM Cloud Classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).

2. Order a [Direct Link Connect (2.0)](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0) or provision a [Cloud Connection](/docs/power-iaas?topic=power-iaas-cloud-connections) instance from the PowerVS interface to connect the PowerVS router to the IBM Cloud Classic infrastructure environment. This connection is established and operated by the IBM Cloud team and you have no direct access or control.
    When this connection is established, the Border Gateway Protocol (BGP) is configured by the IBM Cloud team in the following way:
        - The PowerVS router advertises your PowerVS subnets to the router in the VPC infrastructure environment.
        - The router in the VPC infrastructure environment advertises only your IBM Cloud VPC subnets to the PowerVS router.
        - The router in the VPC infrastructure environment filters the following networks from the BGP advertisements coming from the PowerVS router because these IP addresses are used by the endpoint networks: 169.254.0.0/16, 224.0.0.0/4, 166.9.0.0/16 and any IP ranges that are assigned to your IBM Cloud VPC subnets.

3. Identify the IBM Cloud VPC subnets and the IP address schema that is assigned to you when you ordered VPC services. The XCR connects to the endpoint networks by using the VPC implicit router that provides routing functions to each VPC and allows each VPC to have access to its own copy of the IPv4 address space. The Multi-Protocol Label Switching (MPLS) VPN works with Direct Link and Classic infrastructure environment. For more information, see [Network isolation, data packet flow, and the role of an implicit router in a VPC](https://www.ibm.com/cloud/architecture/content/course/advanced-networking-for-vpc/design-develop-and-deploy/){: external}.
    You cannot access endpoint networks (services and infrastructure services) and virtual private endpoints (VPE) from your PowerVS subnets. The types of endpoint networks are as follows:
    - Service endpoints - allow connection to IBM Cloud services available through DNS names in the cloud.ibm.com domain and resolve to 166.9.x.x addresses.
    - Infrastructure services - allow connection to IBM Cloud services from the adn.networklayer.com domain and resolve to 161.26.0.0/16 addresses. Services that you can reach include:
      - DNS resolvers - 161.26.0.10 and 161.26.0.11 (Windows VS seems to be set up with 161.26.0.7 and Linux with 161.26.0.7 and 161.26.0.8)
      - Ubuntu and Debian mirrors - mirrors.adn.networklayer.com or 161.26.0.6
      - NTP - time.adn.networklayer.com or 161.26.0.6. This is the same IP address as the Ubuntu and Debian mirrors.
      - IBM Cloud Object Storage.
    - Virtual Private Endpoints - enables the connection to supported IBM Cloud services by using the IP addresses allocated from a subnet within your VPC. See [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services). Two infrastructure services of interest are; NTP and IBM Cloud Object Storage.
4. If you want to access the endpoint network, use a VPC virtual server instance to proxy the endpoint services. For example, a virtual server that is running Nginx can proxy HTTPS to and from IBM Cloud Object Storage. A virtual server that is running NTP services, which are synchronized with time.adn.networklayer.com, can be used as a time source for PowerVS instances.

Each IBM Cloud Direct Link service is not redundant, however, diversity can be engineered by using multiple direct links and BGP. See [Models for diversity and redundancy in Direct Link (2.0)](/docs/dl?topic=dl-models-for-diversity-and-redundancy-in-direct-link)

## Connecting to IBM Cloud Services
{: #network-architecture-cloud-services}

TBD

## Connecting to on-premises by using Megaport
{: #network-reference-architecture-onprem}

In this deployment topology [Megaport](https://www.megaport.com/){: external} or IBM Cloud Connect is used to provide connectivity from your on-premises (remote) networks to your PowerVS subnets.

![Connect to on-premises](./images/network-connect-to-onprem.svg "Connect to on-premises"){: caption="Figure 1. Connect to on-premise" caption-side="bottom"}

IBM Cloud Connect is a managed network service that uses Megaport services. This service is available only in the United States. You can also use MegaPort or Cloud Connect to connect your on-premises network to PowerVS directly.

Review the following characteristics about Megaport connectivity services:
    * Megaport operates a global network infrastructure that enables on-demand connectivity to hundreds of global services in Asia Pacific, North America, Europe, and the Middle East.
    * A port is the physical point of connection between your organization’s network and the Megaport network. While a single data center connection is possible, best practice is to select two different port locations to provide redundancy.
    * Megaport has a number of Cloud Service Providers including IBM Cloud.
    * Virtual Cross Connects (VXCs) provide connections between any of the locations and services on the Megaport network. Ordering a VXC, via the Megaport Portal or Megaport API, allows you to connect into the Power virtual server environment and optionally the classic/VPC infrastructure environments or other clouds.

Megaport connectivity services are available in WDC04, DAL13, DAL12, LON06, TOR01, FRA05, SYD05, and OSA21 data centers.
{: important}

Complete the following steps to implement this scenario:
1. Define the IP address schema of your PowerVS subnets in your PowerVS environment. Your PowerVS instances are hosted on these PowerVS subnets. Ensure that you do not overlap the PowerVS subnets with your IBM Cloud Classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Procure the [Megaport](https://www.megaport.com/){: external} VXC connections to connect your on-premises (remote) networks to the Megaport network.
    - Open a support ticket against Power Systems Virtual Server to receive a service ID or a virtual cross-connect (VxC) identifier from IBM.
    - Engage with Megaport to procure the connection (VxC) to Power Systems Virtual Server Port @ Megaport.
        Although a single data center connection between the on-premises network and Megaport network is possible, best practice is to select two different port locations to provide redundancy.
3. Open a support ticket against Power Systems Virtual Server team to perform the network configuration to connect the Megaport network to the PowerVS router by using VXCs. Remember to include the following pieces of information in your support ticket:
    
    ```text
    Customer name and contact:
    Customer account ID
    Service ID (VxC Identifier):

    Customer network subnet:
    Customer router IP Address:
    Power Systems Virtual Server customer network IP address:
    Power Systems Virtual Server network ASN: 64999 for WDC04 and 64997 for DAL13
    Customer Network ASN:

    Customer subnets to be advertised:
    Power Systems Virtual Server customer Private Network ID (1):
    Power Systems Virtual Server customer Private Network ID (2):
    Power Systems Virtual Server customer Private Network ID (3):
    ```
 The PowerVS router is the default gateway for your Power virtual server instances. The PowerVS router is operated by the IBM PowerVS team and you have no direct access or control.
    

## Connecting two Power virtual server environments
{: #network-reference-architecture-pvs2pvs}

In this deployment topology [Megaport](https://www.megaport.com/){: external} or IBM Cloud Connect is used to provide connectivity between Power virtual server environments located at two different data centers.

![Connecting Power virtual server environments](./images/network-connect-to-pvs2pvs.svg "Connecting Power virtual server environments"){: caption="Figure 2. Connecting Power virtual server environments" caption-side="bottom"}

IBM Cloud Connect is a managed network service that uses Megaport services. This service is available only in the United States. You can also use MegaPort or Cloud Connect to connect your on-premises network to PowerVS directly.

The key features of this connect to classic topology are as follows:

1. Define the IP address schema of your PowerVS subnets in your PowerVS environment. Your PowerVS instances are hosted on these PowerVS subnets. Ensure that you do not overlap the PowerVS subnets with your IBM Cloud Classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Procure the [Megaport](https://www.megaport.com/){: external} VXC connections to connect your on-premises (remote) networks to the Megaport network.
      - Open a support ticket against Power Systems Virtual Server to receive a service ID or a virtual cross-connect (VxC) identifier from IBM.
      - Engage with Megaport to procure the connection (VxC) to Power Systems Virtual Server Port @ Megaport.
        When connecting a Power IaaS Loaction-1 to Power IaaS Location-2 by using Megaport, you might need a [Megaport Cloud Router (MCR)](https://docs.megaport.com/mcr/creating-mcr/){: external} unless network connectivity is through a customer router. Consult an IBM Cloud Connect or Megaport representative for specific network requirements.
3. Open a support ticket against Power Systems Virtual Server team to perform the network configuration to connect the Megaport network to the PowerVS router by using VXCs. Remember to include the following pieces of information in your support ticket:
    ```text
    Customer name and contact:
    Customer account ID
    Service ID (VxC Identifier):

    Customer network subnet:
    Customer router IP Address:
    Power Systems Virtual Server customer network IP address:
    Power Systems Virtual Server network ASN: 64999 for WDC04 and 64997 for DAL13
    Customer Network ASN:

    Customer subnets to be advertised:
    Power Systems Virtual Server customer Private Network ID (1):
    Power Systems Virtual Server customer Private Network ID (2):
    Power Systems Virtual Server customer Private Network ID (3):
    ```
The PowerVS router is the default gateway for your Power virtual server instances. The PowerVS router is operated by the IBM Cloud team and you have no direct access or control.

## Connecting to on-premises network by using private SSL connection and a jump server
{: #network-reference-architecture-privatessl}

The IBM Cloud Secure Sockets Layer (SSL) VPN service is a feature of the IBM Cloud Classic infrastructure environment and enables you to manage your Classic resources, remotely, over the IBM Cloud Private network. An SSL VPN connection from your location to the private network allows out-of-band management and server rescue through an encrypted VPN tunnel. For more information about VPN, see [About VPN](/docs/iaas-vpn?topic=iaas-vpn-about-iaas-vpn).

The IBM Cloud SSL VPN service can only access your Classic private IP subnets, therefore, you cannot use the SSL VPN feature to access your PowerVS instances directly from your workstation, so a jump server or bastion host is used to access your PowerVS instances from your on-premises network. 

![SSL VPN](./images/network-ssl-vpn.svg "SSL VPN"){: caption="Figure 5. SSL VPN" caption-side="bottom"}

This deployment topology builds upon the [Connect to Classic](/docs/power-iaas?topic=power-iaas-network-reference-architecture-classic).
{: note}

Complete the following steps to implement this scenario:

1. Ensure that you meet the following prerequisites:
      * Ensure that your IBM Cloud account has the required permissions, a VPN password that is configured, and you have access to the subnets that are hosting your resources. For detailed instructions, see [Activating or deactivating SSL VPN access for a user](/docs/iaas-vpn?topic=iaas-vpn-activate-or-deacivate-ssl-vpn-access-for-a-user).
      * Ensure that your workstation or laptop at your on-premises location has the stand-alone VPN client installed. For detailed instructions, see [stand-alone VPN clients (Windows, Linux, and Mac OS X)](/docs/iaas-vpn?topic=iaas-vpn-standalone-vpn-clients)
      * Ensure that you have internet access and the stand-alone client has a connection to the endpoint for the location that is hosting your Classic resources. For a complete list, see [Available VPN endpoints](/docs/iaas-vpn?topic=iaas-vpn-available-vpn-endpoints).
2. Deploy a jump server or bastion host with your preferred operating system. You can connect from your workstation or laptop at your location to the private IP address of your jump server or bastion host by using Remote Desktop Protocol (RDP) or Secure Shell Protocol (SSH). 
3. Establish a connection from the jump server or bastion host to your PowerVS instances by using SSH. 

This option is typically used to manage infrastructures and is not recommended for production workloads.
{: note}

## Connecting to on-premises network by using an internet IPsec VPN connection
{: #network-reference-architecture-privateipsec}

Although, individual PowerVS instances can have internet access [Public and private networks](/docs/power-iaas?topic=power-iaas-about-virtual-server#public-private-networks), there is no site-to-site IPsec VPN service that connects your PowerVS subnets to your remote networks, currently available.

![IPsec VPN](./images/network-ipsec-vpn.svg "SSL VPN"){: caption="Figure 6. IPsec VPN" caption-side="bottom"}

This deployment topology leverages the IBM Cloud Classic infrastructure gateway appliance to provide an Internet-connected IPsec VPN gateway to enable a site-to-site VPN connection to your Power VS resources.

- The IBM Cloud gateway appliance allows you to selectively route private and public network traffic through a full-featured, enterprise-level firewall that is powered by the software features of VyOS, JunOS, or any other operating system (Bring Your own Appliance (BYOA)) you choose.
- All appliance features are customer-managed.
- By using the IBM Cloud UI, CLI, or API, you can select your VLANs, and hence, the associated subnets, that you want to associate with your gateway appliance. Associating a VLAN with a gateway appliance reroutes, or trunks, that VLAN and all of its subnets to your appliance, giving you control over filtering, forwarding, and protection.
- A gateway appliance is attached to two nonremovable transit VLANs, one each for your public, and private networks.

Complete the following steps to implement this scenario:

1. [Set up an IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started) to establish an IPsec VPN connection from your remote location to IBM Cloud Classic infrastructure.
2. Complete all the steps that are mentioned in the [Connect to Classic infrastructure by using IBM Direct-Link](/docs/gateway-appliance?topic=network-architecture-diagrams#network-reference-architecture-privatessl) topic. It includes configuring PowerVS private subnets and provisioning a Direct Link Connect 2.0 or a Cloud Connection instance with VRF option.
   The IBM Cloud Classic infrastructure environment VRF contains the following routes:
    - Subnets that are assigned to you by IBM Cloud for use in your Classic environment.
    - Your PowerVS subnets advertised by the PowerVS router.

   However, it does not contain routes to your remote networks. Static routes or a routing protocol, such as BGP, shares routes between your remote network and the gateway appliance. The routes that are advertised by the gateway appliance include your PowerVS subnets.
3. Configure a Generic Routing Encapsulation (GRE) tunnel between the gateway appliance and the PowerVS router as the PowerVS router will not have routes for your remote networks that are advertised to it through the IBM Cloud-side router. Within the GRE tunnel, static routes are configured between the PowerVS router and the gateway appliance. For detailed steps, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-managing-cloud-connections#configure-gre-tunnel).

For a tutorial on site-to-site VPN connectivity, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.

Additionally, the x86 servers can also be deployed on to the subnets contained within the associated and nonassociated VLANs to build complex topologies such as three tier architectures.

## Connecting to on-premises network by using a Private Direct-Link connection
{: #network-reference-architecture-directlink}

However, to connect your external networks to your PowerVS subnets, you can use the IBM Cloud Direct Link service you cannot use this connectivity for a direct connection as both your PowerVS subnets and your remote networks are considered to be external networks to the VRF and direct external to external traffic is prohibited. Therefore, in this deployment topology, a gateway appliance and GRE tunnels are used to provide connectivity.

This topology focuses on Direct Link (2.0) service that has the following offerings:

* Direct Link Dedicated - A single-tenant, fiber-based, cross-connect into the IBM Cloud Private network.
* Direct Link Connect - Uses a service provider who is already connected to the IBM Cloud Private network to deliver multi-tenant, high capacity links, also known as network-to-network interfaces.

Direct Link (2.0) is not currently available in all locations, see [Locations](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-dedicated#dedicated-locations) for details about the IBM Cloud data centers where Direct Link Dedicated is available and [Providers and locations](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect#connect-locations) for Direct Link Connect.

If Direct Link (2.0) is not available at a suitable location, then see
[Getting started with IBM Cloud Direct Link on Classic](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link).

![Direct Link](./images/network-dl-gre.svg "Direct Link"){: caption="Figure 7. Direct Link" caption-side="bottom"}

This deployment topology leverages the IBM Cloud classic infrastructure gateway appliance to provide a GRE gateway. See [Getting started with IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started).
    - The IBM Cloud gateway appliance allows you to selectively route private and optionally public network traffic through a full-featured, enterprise-level firewall that is powered by the software features of; VyOS, JunOS, or any other operating system (Bring Your own Appliance (BYOA)) you choose.
    - All appliance features are customer-managed.
    - By using the IBM Cloud UI, CLI, or API, you can select your VLANs, and hence, the associated subnets, that you want to associate with your gateway appliance. Associating a VLAN with a gateway appliance reroutes, or trunks, that VLAN and all of its subnets to your appliance, giving you control over filtering, forwarding, and protection.
    - A gateway appliance is attached to two nonremovable transit VLANs, one each for your public and private networks.

Complete the following steps to implement this scenario:

1. [Set up an IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started).
2. Complete all the steps that are mentioned in the [Connect to Classic infrastructure by using IBM Direct-Link](/docs/gateway-appliance?topic=network-architecture-diagrams#network-reference-architecture-privatessl) topic. It includes configuring PowerVS private subnets and provisioning a Direct Link Connect 2.0 or a Cloud Connection instance with VRF option.
   The IBM Cloud Classic infrastructure environment VRF contains the following routes:
    - Subnets that are assigned to you by IBM Cloud for use in your Classic environment.
    - Your PowerVS subnets advertised by the PowerVS router.

   However, it does not contain routes to your remote networks. Static routes or a routing protocol, such as BGP, shares routes between your remote network and the gateway appliance. The routes that are advertised by the gateway appliance include your PowerVS subnets.
3. Configure a Generic Routing Encapsulation (GRE) tunnel between the gateway appliance and the PowerVS router as the PowerVS router will not have routes for your remote networks that are advertised to it through the IBM Cloud-side router. Within the GRE tunnel, static routes are configured between the PowerVS router and the gateway appliance. For detailed steps, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-managing-cloud-connections#configure-gre-tunnel).
4. Set up a separate Direct Link 2.0 connection between your remote network (on-premises) and IBM Cloud Classic infrastructure environment. See [Getting started with IBM Cloud Direct Link (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl), however, key elements of IBM Cloud Direct Link (2.0) include the following:
    - Requires BGP to establish the routes to a customer's remote network.
    - Each IBM Cloud Direct Link service is not redundant, however, diversity can be enabled over multiple direct links along with BGP.
    - Ensure that IP subnet overlaps do not exist between the infrastructure environments and the remote networks.
5.	Configure a GRE tunnel between the gateway appliance and a tunnel endpoint that is connected to your external network to enable the remote network connectivity. For detailed steps, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-managing-cloud-connections#configure-gre-tunnel).

For some tutorials based on some of the topologies described above, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.

## Connecting two Power virtual server environments by using Transit Gateway
{: #network-reference-architecture-tgw}

In this deployment topology Cloud connection through IBM Transit Gateway is used to provide connectivity between Power virtual server environments located at two different data centers. With Transit Gateway you can also interconnect your Power Systems Virtual Servers to the IBM Cloud classic and Virtual Private Cloud (VPC) infrastructures, keeping traffic within the IBM Cloud network. IBM Transit Gateway enables you to connect your otherwise disconnected private networks such as classic, VPC, Direct Link. In addition, you can establish connection between multiple Power Systems Virtual Server services across different data centers.

The following network architecture allows connectivity between multiple Power Systems Virtual Server locations with high availability (HA) and disaster recovery (DR) solutions.

![Transit Gateway](./images/network-tgw.svg "Transit Gateway"){: caption="Figure 8. Transit Gateway" caption-side="bottom"}

The key features of this topology are as follows:

   - Access and connectivity between two different PowerVS locations in the same region (for example DAL12 to DAL13) to support HA via replication. 
   - Access and connectivity between two different PowerVS locations in different regions (for example DAL12 to WDC06) to support DRvia replication. 
   - Access and connectivity between on-premises and PowerVS locations by using GRE Tunneling.

Complete the following steps to implement this scenario:
1.	Create an [IBM Cloud Transit Gateway](https://cloud.ibm.com/login?redirect=%2Finterconnectivity%2Ftransitconnection){: external} to enable the virtual connections.
2.	[Create a Cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections) with Transit Gateway enabled.
3.	Connect your Power Systems Virtual Servers that are located in Data center 1 and Data center 2 through the IBM Cloud network by using Transit Gateway. 
4.	Once the Transit Gateway connection is established different Cloud networks are connected to each other.
