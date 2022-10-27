---

copyright:
  years: 2019, 2022

lastupdated: "2022-09-15"

keywords: networking diagrams, network architecture, private ssl, private ipsec, direct link connect, colocation, data center, cloud connect, megaport

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network architecture diagrams
{: #network-architecture-diagrams}

This topic describes typical network architectures that are used in the {{site.data.keyword.powerSysShort}} network architecture and is not an exhaustive list of {{site.data.keyword.powerSys_notm}} connection methods.
{: shortdesc}

{{site.data.keyword.dl_full_notm}} (2.0) Connect is available in all current locations. IBM clients can always contact Megaport connectivity services directly to procure their services.
{: important}

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

## Use cases
{: #networking-use-cases}

These use cases describe the following deployment topologies:

* Connecting {{site.data.keyword.powerSys_notm}} to IBM Cloud classic infrastructure by using IBM Cloud {{site.data.keyword.dl_short}} (2.0). Typical use cases for this topology are as follows:
    - Use IBM Cloud classic x86 resources to create tiered applications across different hardware platforms, that is, x86 application servers and Power database servers.
    - Build a backup and restore environment based on [IBM Spectrum Protect Cloud Blueprints](https://www.ibm.com/support/pages/ibm-spectrum-protect-cloud-blueprints) for both IBM Spectrum Protect and IBM Spectrum Protect Plus topologies. Also, see [AIX Backups with {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Backups_Tutorial_v1.pdf).
* Connecting {{site.data.keyword.powerSys_notm}} to the IBM Cloud VPC infrastructure environment by using {{site.data.keyword.dl_short}} (2.0) Connect. A typical use case for this topology is to use IBM Cloud VPC x86 resources to create tiered applications across different hardware platforms, that is, x86 application servers and Power database servers.
* Connecting {{site.data.keyword.powerSys_notm}} to on-premises network by using Megaport or {{site.data.keyword.dl_short}} (2.0) Connect. A typical use case for this topology is that you require access to your Power virtual servers from your external networks, such as networks on your on-premises. This topology uses Megaport services or {{site.data.keyword.dl_short}} (2.0) Connect.
* Connecting two {{site.data.keyword.powerSys_notm}} environments by using Megaport or {{site.data.keyword.dl_short}} Connect. This topology connects two or more Power virtual server environments together by using Megaport services or {{site.data.keyword.dl_short}} (2.0) Connect. Connecting two or more environments together enables use cases, such as disaster recovery.
* Connecting {{site.data.keyword.powerSys_notm}} to an on-premises network through the IBM classic infrastructure by using private SSL connection and a jump server. This is a specific use case for connecting to the classic environment so that the SSL VPN connection can be used to access your {{site.data.keyword.powerSys_notm}}s for operations and administration tasks.
* Connecting {{site.data.keyword.powerSys_notm}} to an on-premises network through the IBM Cloud classic infrastructure by using an internet IPsec VPN connection.  This use case describes how to connect to the classic environment so that an IPsec VPN connection can be used to access your classic and {{site.data.keyword.powerSys_notm}}s. Typically, this network architecture is used for small production environments or proof-of-concept, development, and test purposes.
* Connecting {{site.data.keyword.powerSys_notm}} to an on-premises network through an IBM Cloud classic infrastructure by using a private {{site.data.keyword.dl_short}}. A {{site.data.keyword.dl_short}} enables your remote networks to connect to IBM Cloud over a private connection that does not use public networks.
<!--* Connecting two {{site.data.keyword.powerSys_notm}} through an IBM Cloud classic infrastructure by using {{site.data.keyword.tg_full_notm}}. A connection through {{site.data.keyword.tg_full_notm}} is used to provide connectivity between {{site.data.keyword.powerSys_notm}} environments located at two different data centers-->

Multiple topologies, described in this document, can be layered to create a topology that suits your deployment needs.

## Connecting to classic infrastructure by using {{site.data.keyword.dl_short}} (2.0)
{: #network-reference-architecture-classic}

In this deployment topology, a {{site.data.keyword.dl_short}} is used to connect your {{site.data.keyword.powerSys_notm}} networks to IBM Cloud resources hosted in a classic infrastructure environment. You can either [order {{site.data.keyword.dl_short}} (2.0) Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect) connections, or use IBM Cloud connections. 

![Connecting {{site.data.keyword.powerSys_notm}} to IBM Cloud classic infrastructure by using IBM {{site.data.keyword.dl_short}} (2.0)](./images/network-connect-to-classic.svg "Connect to Classic"){: caption="Figure 1. Connect to classic infrastructure with {{site.data.keyword.dl_short}} (2.0)" caption-side="bottom"}

Complete the following steps to implement this scenario:

1. Define the IP address schema of your {{site.data.keyword.powerSys_notm}} subnets in your {{site.data.keyword.powerSys_notm}} environment. Your {{site.data.keyword.powerSys_notm}} instances are hosted on these subnets. Ensure that you do not overlap the subnets with your IBM Cloud classic private subnets, or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Order [{{site.data.keyword.dl_short}} (2.0) Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0), or provision an [IBM Cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections) instance from the {{site.data.keyword.powerSys_notm}} interface to connect the {{site.data.keyword.powerSys_notm}} router to the IBM Cloud classic infrastructure. This connection is established and operated by the IBM Cloud team and you have no direct access or control. 

   Consider the following information before you proceed:

    - Ensure that you select the virtual routing and forwarding (VRF) option when you provision a {{site.data.keyword.dl_short}}. The VRF option allows multiple instances of a routing table to exist in a router and to work simultaneously. With VRF, each IBM Cloud account classic environment network is segmented within its own routing table. For more information, see [Virtual routing and forwarding on IBM Cloud](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud). 
    - When this connection is established, the Border Gateway Protocol (BGP) is configured automatically by the IBM Cloud team in the following way:
        - The {{site.data.keyword.powerSys_notm}} router advertises your {{site.data.keyword.powerSys_notm}} subnets to the classic infrastructure environment. 
        - The classic infrastructure advertises only your IBM Cloud classic private subnets to the {{site.data.keyword.powerSys_notm}} router. 
        - The classic infrastructure filters the following networks from the BGP advertisements coming from the {{site.data.keyword.powerSys_notm}} router because these IP addresses are used by the services networks: `10.0.0.0/14`, `10.198.0.0/15`, `10.200.0.0/14`, `169.254.0.0/16`, `224.0.0.0/4` and any IP ranges that are assigned to your IBM Cloud classic private subnets.
        
          You can use the `10.x.x.x` range if there is no conflict with an IBM Cloud back-end `10.x.x.x` service. You must contact IBM Support if you want to use NAT'ing or IP aliasing to resolve the IP conflict. However, IBM does not recommend using the `10.x.x.x` range when you create a network.
          {: important}

3. Identify the IBM Cloud classic private subnets and the IP address schema that is assigned to you when you ordered bare metal or virtual server instances that are hosted on your IBM Cloud classic private subnets. Connect to the required resources and services.

    All the routers in all classic infrastructure data centers and PoPs across the global IBM Cloud backbone are connected to the {{site.data.keyword.powerSys_notm}} router by using the {{site.data.keyword.dl_short}} Connect VRF-enabled connection. 

    Each IBM Cloud {{site.data.keyword.dl_short}} workspace is not redundant. However, diversity can be engineered using multiple {{site.data.keyword.dl_short}}s and BGP. For more information, see [Models for diversity and redundancy in {{site.data.keyword.dl_short}} (2.0)](/docs/dl?topic=dl-models-for-diversity-and-redundancy-in-direct-link).
    {: note}

## Connecting to VPC by using {{site.data.keyword.dl_short}} Connect
{: #network-reference-architecture-vpc}

In this deployment topology, a {{site.data.keyword.dl_short}} (2.0) is used to connect your {{site.data.keyword.powerSys_notm}} networks to resources that are hosted in the IBM Cloud VPC infrastructure.

![Connect to VPC](./images/network-connect-to-vpc.svg "Connect to VPC"){: caption="Figure 2. Connect to VPC" caption-side="bottom"}

Complete the following steps to implement this scenario:

1. Define the IP address schema of your {{site.data.keyword.powerSys_notm}} subnets in your {{site.data.keyword.powerSys_notm}} environment. Your {{site.data.keyword.powerSys_notm}} instances are hosted on these subnets. Ensure that you do not overlap these subnets with your IBM Cloud classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Order [{{site.data.keyword.dl_short}} (2.0) Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0), or provision an [IBM Cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections) instance from the {{site.data.keyword.powerSys_notm}} interface to connect the {{site.data.keyword.powerSys_notm}} router to the IBM Cloud classic infrastructure. This connection is established and operated by the IBM Cloud team and you have no direct access or control.

    When this connection is established, the BGP is configured by the IBM Cloud team in the following way:
    - The {{site.data.keyword.powerSys_notm}} router advertises your {{site.data.keyword.powerSys_notm}} subnets to the router in the VPC infrastructure.
        - The router in the VPC infrastructure advertises only your IBM Cloud VPC subnets to the {{site.data.keyword.powerSys_notm}} router.
        - The router in the VPC infrastructure filters the following networks from the BGP advertisements coming from the {{site.data.keyword.powerSys_notm}} router because these IP addresses are used by the endpoint networks: `169.254.0.0/16`, `224.0.0.0/4`, `166.9.0.0/16`, and any IP ranges that are assigned to your IBM Cloud VPC subnets.
3. Identify the IBM Cloud VPC subnets and the IP address schema that is assigned to you when you ordered VPC services. The XCR connects to the endpoint networks by using the VPC implicit router that provides routing functions to each VPC, and allows each VPC to have access to its own copy of the IPv4 address space. The Multi-Protocol Label Switching (MPLS) VPN works with {{site.data.keyword.dl_short}} and classic infrastructure environments. For more information, see [Network isolation, data packet flow, and the role of an implicit router in a VPC](https://www.ibm.com/cloud/architecture/content/course/advanced-networking-for-vpc/design-develop-and-deploy/){: external}.
    You cannot access endpoint networks (services and infrastructure services) and Virtual Private Endpoints (VPEs) from your {{site.data.keyword.powerSys_notm}} subnets. The types of endpoint networks are as follows:
    - Service endpoints - Allows connection to IBM Cloud services available through DNS names in the cloud.ibm.com domain and resolves to `166.9.x.x` addresses.
    - Infrastructure services - Allows connection to IBM Cloud services from the adn.networklayer.com domain and resolves to `161.26.0.0/16` addresses. Services that you can reach include:
      - DNS resolvers - `161.26.0.10` and `161.26.0.11` (Windows VS is set up with `161.26.0.7`; Linux with `161.26.0.7` and `161.26.0.8`)
      - Ubuntu and Debian mirrors - mirrors.adn.networklayer.com or `161.26.0.6`
      - NTP - time.adn.networklayer.com or `161.26.0.6`. This is the same IP address as the Ubuntu and Debian mirrors.
      - IBM Cloud Object Storage
    - VPEs - Enables connection to supported IBM Cloud services by using the IP addresses allocated from a subnet within your VPC. For more information, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services). Two infrastructure services of interest are NTP and IBM Cloud Object Storage.
4. If you want to access the endpoint network, use a VPC virtual server instance to proxy the endpoint services. For example, a virtual server that is running Nginx can proxy HTTPS to and from IBM Cloud Object Storage. A virtual server that is running NTP services (synchronized with time.adn.networklayer.com) can be used as a time source for {{site.data.keyword.powerSys_notm}} instances.

Each IBM Cloud {{site.data.keyword.dl_short}} service is not redundant, however, diversity can be engineered by using multiple {{site.data.keyword.dl_short}}s and BGP. For more information, see [Models for diversity and redundancy in {{site.data.keyword.dl_short}} (2.0)](/docs/dl?topic=dl-models-for-diversity-and-redundancy-in-direct-link).

<!--
## Connecting to IBM Cloud services
{: #network-architecture-cloud-services}

TBD-->

## Connecting to on-premises by using Megaport
{: #network-reference-architecture-onprem}

In this deployment topology, [Megaport](https://www.megaport.com/){: external} or {{site.data.keyword.dl_short}} Connect is used to provide connectivity from your on-premises (remote) networks to your {{site.data.keyword.powerSys_notm}} subnets.

![Connect to on-premises](./images/network-connect-to-onprem.svg "Connect to on-premises"){: caption="Figure 3. Connect to on-premises" caption-side="bottom"}

IBM Cloud Connect is a managed network service that uses Megaport services. This service is available only in the United States. You can also use Megaport to connect your on-premises network to {{site.data.keyword.powerSys_notm}} directly.

Review the following characteristics about Megaport connectivity services:
    * Megaport operates a global network infrastructure that enables on-demand connectivity to hundreds of global services in Asia Pacific, North America, Europe, and the Middle East.
    * A port is the physical point of connection between your organization’s network and the Megaport network. While a single data center connection is possible, best practice is to select two different port locations to provide redundancy.
    * Megaport has a number of cloud service providers including IBM Cloud.
    * Virtual Cross Connects (VXCs) provide connections between any of the locations and services on the Megaport network. Ordering a VXC (by using the Megaport portal or API) allows you to connect into the Power virtual server environment and, optionally, the classic/VPC infrastructure environments or other clouds.

Megaport connectivity services are available in WDC04, DAL13, DAL12, LON06, TOR01, FRA05, SYD05, and OSA21 data centers.
{: important}

Complete the following steps to implement this scenario:

1. Define the IP address schema of your {{site.data.keyword.powerSys_notm}} subnets in your {{site.data.keyword.powerSys_notm}} environment. Your {{site.data.keyword.powerSys_notm}} instances are hosted on these subnets. Ensure that you do not overlap these subnets with your IBM Cloud classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Procure the [Megaport](https://www.megaport.com/){: external} VXC connections to connect your on-premises (remote) networks to the Megaport network.
    - Open an IBM Support case against {{site.data.keyword.powerSys_notm}} to receive a service ID or a virtual cross-connect (VxC) identifier from IBM.
    - Engage with Megaport to procure the connection (VxC) to {{site.data.keyword.powerSys_notm}} Port @ Megaport.
        Although a single data center connection between the on-premises network and Megaport network is possible, best practice is to select two different port locations to provide redundancy.
3. Open an IBM Support case against the {{site.data.keyword.powerSys_notm}} team to configure the Megaport network to the {{site.data.keyword.powerSys_notm}} router by using VXCs. Remember to include the following pieces of information in your case:
    
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
    
The {{site.data.keyword.powerSys_notm}} router is the default gateway for your Power virtual server instances. This router is operated by the {{site.data.keyword.powerSys_notm}} team and you have no direct access or control.
    

## Connecting two Power virtual server environments
{: #network-reference-architecture-pvs2pvs}

In this deployment topology, [Megaport](https://www.megaport.com/){: external} or {{site.data.keyword.dl_short}} (2.0) Connect is used to provide connectivity between Power virtual server environments located at two different data centers.

![Connecting Power virtual server environments](./images/network-connect-to-pvs2pvs.svg "Connecting Power virtual server environments"){: caption="Figure 4. Connecting Power virtual server environments" caption-side="bottom"}

IBM Cloud Connect is a managed network service that uses Megaport services. This service is available only in the United States. You can also use Megaport to connect your on-premises network to {{site.data.keyword.powerSys_notm}} directly.

The key features of this Connect-to-classic topology are as follows:

1. Define the IP address schema of your {{site.data.keyword.powerSys_notm}} subnets in your {{site.data.keyword.powerSys_notm}} environment. Your {{site.data.keyword.powerSys_notm}} instances are hosted on these subnets. Ensure that you do not overlap these subnets with your IBM Cloud classic private subnets or the IP addressing schema that is used for the services network. For instructions, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).
2. Procure the [Megaport](https://www.megaport.com/){: external} VXC connections to connect your on-premises (remote) networks to the Megaport network.
      - Open an IBM Support case against {{site.data.keyword.powerSys_notm}} to receive a service ID or a virtual cross-connect (VxC) identifier from IBM.
      - Engage with Megaport to procure the connection (VxC) to {{site.data.keyword.powerSys_notm}} Port @ Megaport.
        When connecting a Power IaaS Location-1 to Power IaaS Location-2 by using Megaport, you might need a [Megaport Cloud Router (MCR)](https://docs.megaport.com/mcr/creating-mcr/){: external} unless network connectivity is through a customer router. Consult a {{site.data.keyword.dl_short}} Connect or Megaport representative for specific network requirements.
3. Open an IBM Support case against the {{site.data.keyword.powerSys_notm}} team to perform the network configuration to connect the Megaport network to the {{site.data.keyword.powerSys_notm}} router by using VXCs. Remember to include the following pieces of information in your case:

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
The {{site.data.keyword.powerSys_notm}} router is the default gateway for your Power virtual server instances. This router is operated by the IBM Cloud team and you have no direct access or control.

## Connecting to an on-premises network by using a private SSL connection and a jump server
{: #network-reference-architecture-privatessl}   

The IBM Cloud SSL VPN service is a feature of the IBM Cloud classic infrastructure, which enables you to manage your classic resources, remotely, over the IBM Cloud Private network. An SSL VPN connection from your location to the private network allows out-of-band management and server rescue through an encrypted VPN tunnel. For more information, see [About VPN](/docs/iaas-vpn?topic=iaas-vpn-about-iaas-vpn).

The IBM Cloud SSL VPN service can access only your classic private IP subnets. Therefore, you cannot use the SSL VPN feature to access your {{site.data.keyword.powerSys_notm}} instances directly from your workstation. Instead, a jump server or bastion host is used to access your {{site.data.keyword.powerSys_notm}} instances from your on-premises network. 

![SSL VPN deployment scenario](./images/network-ssl-vpn.svg "SSL VPN"){: caption="Figure 5. SSL VPN deployment scenario" caption-side="bottom"}

This deployment topology builds on the [Connect-to-classic](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#network-reference-architecture-classic) architecture.
{: note}

Complete the following steps to implement this scenario:

1. Ensure that you meet the following prerequisites:
      * Ensure that your IBM Cloud account has the required permissions, a VPN password is configured, and you have access to the subnets that are hosting your resources. For instructions, see [Activating or deactivating SSL VPN access for a user](/docs/iaas-vpn?topic=iaas-vpn-activate-or-deacivate-ssl-vpn-access-for-a-user).
      * Ensure that your workstation or laptop at your on-premises location has the stand-alone VPN client installed. For instructions, see [standalone VPN clients (Windows, Linux, and Mac OS X)](/docs/iaas-vpn?topic=iaas-vpn-standalone-vpn-clients)
      * Ensure that you have internet access and the stand-alone client has a connection to the endpoint for the location that is hosting your classic resources. For a complete list, see [Available VPN endpoints](/docs/iaas-vpn?topic=iaas-vpn-available-vpn-endpoints).
2. Deploy a jump server or bastion host with your preferred operating system. You can connect from your workstation or laptop at your location to the private IP address of your jump server or bastion host by using Remote Desktop Protocol (RDP) or Secure Shell Protocol (SSH). 
3. Establish a connection from the jump server or bastion host to your {{site.data.keyword.powerSys_notm}} instances by using SSH. 

This option is typically used to manage infrastructures and is not recommended for production workloads.
{: note}

## Connecting to an on-premises network by using an internet IPsec VPN connection
{: #network-reference-architecture-privateipsec}

Although individual {{site.data.keyword.powerSys_notm}} instances can have internet access, there is no site-to-site IPsec VPN service that connects your {{site.data.keyword.powerSys_notm}} subnets to your remote networks currently available.

![IPsec VPN deployment scenario](./images/network-ipsec-vpn.svg "SSL VPN"){: caption="Figure 6. IPsec VPN deployment scenario" caption-side="bottom"}

This deployment topology leverages the IBM Cloud classic infrastructure gateway appliance to provide an internet-connected IPsec VPN gateway to enable a site-to-site VPN connection to your {{site.data.keyword.powerSys_notm}} resources.

- The IBM Cloud gateway appliance allows you to selectively route private and public network traffic through a full-featured, enterprise-level firewall that is powered by the software features of VyOS, JunOS, or any other operating system (Bring Your Own Appliance) that you choose.
- All appliance features are customer-managed.
- By using the IBM Cloud UI, CLI, or API, you can select your VLANs, and hence, the associated subnets, that you want to associate with your gateway appliance. Associating a VLAN with a gateway appliance reroutes (or trunks) that VLAN and all of its subnets to your appliance, giving you control over filtering, forwarding, and protection.
- A gateway appliance is attached to two nonremovable transit VLANs, one each for your public, and private networks. 

Complete the following steps to implement this scenario:

1. [Set up an IBM Cloud gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started) to establish an IPsec VPN connection from your remote location to the IBM Cloud classic infrastructure.
2. Complete all steps that are mentioned in [Connect to classic infrastructure by using IBM Cloud (2.0) {{site.data.keyword.dl_short}}](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#network-reference-architecture-classic). This includes configuring {{site.data.keyword.powerSys_notm}} private subnets and provisioning a {{site.data.keyword.dl_short}} (2.0) Connect or an IBM Cloud connection instance with the VRF option.

   The IBM Cloud classic infrastructure environment VRF contains the following routes:
    - Subnets that are assigned to you by IBM Cloud for use in your classic environment.
    - Your {{site.data.keyword.powerSys_notm}} subnets advertised by the {{site.data.keyword.powerSys_notm}} router.

   However, it does not contain routes to your remote networks. Static routes or a routing protocol, such as BGP, shares routes between your remote network and the gateway appliance. The routes that are advertised by the gateway appliance include your {{site.data.keyword.powerSys_notm}} subnets.
   
3. Configure a Generic Routing Encapsulation (GRE) tunnel between the gateway appliance and the {{site.data.keyword.powerSys_notm}} router as this router doesn't have routes for your remote networks that are advertised to it through the IBM Cloud-side router. Within the GRE tunnel, static routes are configured between the {{site.data.keyword.powerSys_notm}} router and the gateway appliance. For detailed steps, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-cloud-connections#configure-gre-tunnel).

For a tutorial on site-to-site VPN connectivity, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.

Additionally, the x86 servers can be deployed on to the subnets contained within the associated and nonassociated VLANs to build complex topologies, such as three-tier architectures.

## Connecting to an on-premises network by using a private {{site.data.keyword.dl_short}} connection
{: #network-reference-architecture-directlink}

To connect your external networks to your {{site.data.keyword.powerSys_notm}} subnets, you can use the {{site.data.keyword.dl_short}} service; however, you cannot use this connectivity for a direct connection as both your {{site.data.keyword.powerSys_notm}} subnets and your remote networks are considered to be external networks to the VRF and direct external-to-external traffic is prohibited. Therefore, in this deployment topology, a gateway appliance and GRE tunnels are used to provide connectivity.

This topology focuses on {{site.data.keyword.dl_short}} (2.0) service that has the following offerings:

* {{site.data.keyword.dl_short}} Dedicated - A single-tenant, fiber-based, cross-connect into the IBM Cloud Private network.
* {{site.data.keyword.dl_short}} Connect - Uses a service provider who is already connected to the IBM Cloud Private network to deliver multi-tenant, high capacity links, also known as network-to-network interfaces.

Currently, {{site.data.keyword.dl_short}} (2.0) is not available in all locations. For more information, see [Locations and providers](/docs/dl?topic=dl-locations).

If {{site.data.keyword.dl_short}} (2.0) is not available at a suitable location, then see
[Getting started with IBM Cloud {{site.data.keyword.dl_short}} on Classic](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link).

![{{site.data.keyword.dl_short}} on Classic deployment scenario](./images/network-dl-gre.svg "{{site.data.keyword.dl_short}}"){: caption="Figure 7. {{site.data.keyword.dl_short}} on Classic deployment scenario" caption-side="bottom"}

This deployment topology leverages the IBM Cloud classic infrastructure gateway appliance to provide a GRE gateway. For more information, see [Getting started with IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started).
    - The IBM Cloud gateway appliance allows you to selectively route private and, optionally, public network traffic through a full-featured, enterprise-level firewall that is powered by the software features of; VyOS, JunOS, or any other operating system (Bring Your Own Appliance) you choose.
    - All appliance features are customer-managed.
    - By using the IBM Cloud UI, CLI, or API, you can select your VLANs, and hence, the associated subnets that you want to associate with your gateway appliance. Associating a VLAN with a gateway appliance reroutes (or trunks) that VLAN and all of its subnets to your appliance, giving you control over filtering, forwarding, and protection.
    - A gateway appliance is attached to two nonremovable transit VLANs, one each for your public and private networks.

Complete the following steps to implement this scenario:

1. [Set up an IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started).
2. Complete all steps that are mentioned in [Connect-to-classic infrastructure by using IBM {{site.data.keyword.dl_short}}](/docs/gateway-appliance?topic=power-iaas-network-architecture-diagrams#network-reference-architecture-privatessl). It includes configuring {{site.data.keyword.powerSys_notm}} private subnets and provisioning a {{site.data.keyword.dl_short}} (2.0) Connect or an IBM Cloud connection instance with the VRF option.
3. The IBM Cloud classic infrastructure environment VRF contains the following routes:
    - Subnets that are assigned to you by IBM Cloud for use in your classic environment.
    - Your {{site.data.keyword.powerSys_notm}} subnets advertised by the {{site.data.keyword.powerSys_notm}} router.

   However, it does not contain routes to your remote networks. Static routes or a routing protocol, such as BGP, shares routes between your remote network and the gateway appliance. The routes that are advertised by the gateway appliance include your {{site.data.keyword.powerSys_notm}} subnets.
4. Configure a GRE tunnel between the gateway appliance and the {{site.data.keyword.powerSys_notm}} router as this router doesn't have routes for your remote networks that are advertised to it through the IBM Cloud-side router. Within the GRE tunnel, static routes are configured between the {{site.data.keyword.powerSys_notm}} router and the gateway appliance. For more information, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-cloud-connections#configure-gre-tunnel).
5. Set up a separate {{site.data.keyword.dl_short}} (2.0) connection between your remote network (on-premises) and the IBM Cloud classic infrastructure. See [Getting started with IBM Cloud {{site.data.keyword.dl_short}} (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl), however, key elements of IBM Cloud {{site.data.keyword.dl_short}} (2.0) include the following:
    - Requires BGP to establish the routes to a customer's remote network.
    - Each IBM Cloud {{site.data.keyword.dl_short}} service is not redundant, however, diversity can be enabled over multiple {{site.data.keyword.dl_short}}s along with BGP.
    - Ensure that IP subnet overlaps do not exist between the infrastructure environments and the remote networks.
6. Configure a GRE tunnel between the gateway appliance and a tunnel endpoint that is connected to your external network to enable the remote network connectivity. For more information, see [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs/power-iaas?topic=power-iaas-cloud-connections#configure-gre-tunnel).

For tutorials based on some of the topologies described, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.

## Connecting two {{site.data.keyword.powerSys_notm}} environments by using IBM Cloud Transit Gateway
{: #network-reference-architecture-tgw}

In this deployment topology, a connection through IBM Cloud Transit Gateway is used to provide connectivity between Power virtual server environments located at two different data centers. With IBM Cloud Transit Gateway, you can also interconnect your {{site.data.keyword.powerSys_notm}}s to the IBM Cloud classic and VPC infrastructures, keeping traffic within the IBM Cloud network. Transit Gateway enables you to connect your otherwise disconnected private networks, such as classic, VPC, and {{site.data.keyword.dl_short}}. In addition, you can establish connection between multiple {{site.data.keyword.powerSys_notm}} workspaces across different data centers.

The following network architecture allows connectivity between multiple {{site.data.keyword.powerSys_notm}} locations with high availability (HA) and disaster recovery (DR) solutions.

![Transit Gateway deployment scenario](./images/network-tgw.svg "Transit Gateway"){: caption="Figure 8. Transit Gateway deployment scenario" caption-side="bottom"}

Key features are as follows:

   - Access and connectivity between two different {{site.data.keyword.powerSys_notm}} locations in the same region (for example DAL12 to DAL13) to support HA through replication. 
   - Access and connectivity between two different {{site.data.keyword.powerSys_notm}} locations in different regions (for example DAL12 to WDC06) to support DR through replication. 

Complete the following steps to implement this scenario:

1.	Create an [IBM Cloud Transit Gateway](https://cloud.ibm.com/interconnectivity/transit/provision){: external} to enable the virtual connections.
2.	[Create an IBM Cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections#create-cloud-connections) with Transit Gateway enabled.
3.	Connect your {{site.data.keyword.powerSys_notm}}s that are located in data center 1 and data center 2 through the IBM Cloud network by using a transit gateway. 

After the transit gateway connection is established, different IBM Cloud networks are connected to each other.
