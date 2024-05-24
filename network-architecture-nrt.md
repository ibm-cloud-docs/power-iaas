---

copyright:
  years: 2019, 2023

lastupdated: "2021-06-23"

keywords: networking diagrams, network architecture, private ssl, private ipsec, direct link, colocation, data center, cloud connect, megaport

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Network architecture diagrams
{: #network-reference-architecture}

This documentation describes typical network architectures used in {{site.data.keyword.powerSysShort}} network architecture and is not an exhaustive list of {{site.data.keyword.powerSys_notm}} connection methods.
{: shortdesc}

IBM Cloud Connect is only available to IBM clients within the US. IBM clients can always contact Megaport connectivity services directly to procure their services.
{: important}

{{site.data.keyword.powerSysShort}} network architectures consist of one or more of the following:

* IBM Cloud infrastructure environment networks - While the three infrastructure environment networks offer different features and are managed separately, they can be connected to each other to provide layer 3 IPv4 traffic flow.
     * Classic - network resources include VLANs, subnets and SSL VPN access, however, bring your own IP is not supported. See [Network security architecture](https://www.ibm.com/cloud/architecture/architectures/network-security-arch/){: external} for a description of the Classic network components.
     * Virtual Private Cloud - network resources include subnets, floating IPs, security groups and VPN gateways, see [About networking](/docs/vpc?topic=vpc-about-networking-for-vpc). Bring your own IP is supported. See [Advanced networking for IBM Cloud VPC](https://www.ibm.com/cloud/architecture/content/course/advanced-networking-for-vpc/){: external} for a one hour course on VPC networking.
     * IBM Power - network resources include subnets and bring your own IP is supported.
* Overlay - Overlay networks exist in the IBM Cloud VMware Shared and VMware Dedicated offerings and while technically they are hosted in the IBM Cloud classic infrastructure environment, they are implemented in VMware NSX and, therefore, under your direct control, including the IP addressing schema, so bring your own IP is supported. Overlay networks cannot be routed by the IBM Cloud infrastructure environment networks, therefore, access is via tunnels.
* External:
    * Internet - The Internet can be accessed via resources hosted in any of the three infrastructure environments.
    * Remote - Remote networks are networks that you want to connect to your IBM Cloud networks and can be connected using:
       * Internet VPN - Uses the public internet to connect customer remote networks and their IBM Cloud networks, via a Virtual Private Network (VPN). The VPN is terminated on gateway devices or a service within IBM Cloud.
       * Direct Link - Direct Link is a suite of solutions that enables customers to create direct, private connections between their remote network environments and their IBM Cloud networks, without using the public internet. See [Getting started with IBM Cloud Direct Link (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) for further information. For locations not supported by Direct Link (2.0), see [Getting started with IBM Cloud Direct Link on Classic](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link).

This documentation describes the following network deployment topologies:

* Connect to private cloud - A typical use case for this topology is that you require access to your {{site.data.keyword.powerSys_notm}} from your external networks, such as networks on your premises. This topology uses Megaport services or IBM Cloud Connect.
* Connecting {{site.data.keyword.powerSys_notm}} environments - This topology connects two or more {{site.data.keyword.powerSys_notm}} environments together using Megaport services or IBM Cloud Connect. Connecting two or more environments together enables use cases such as disaster recovery.
* Connect to IBM Cloud Classic - Typical use cases for this topology include:
    * Leverage IBM Cloud Classic x86 resources to create tiered applications across different hardware platforms i.e. x86 application servers and Power database servers.
    * Build a backup and restore environment based on [IBM Spectrum Protect Cloud Blueprints](https://www.ibm.com/support/pages/ibm-spectrum-protect-cloud-blueprints) for both IBM Spectrum Protect and IBM Spectrum Protect Plus topologies. Also see, [AIX Backups with IBM Power Virtual Server](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Backups_Tutorial_v1.pdf).
* Connect to IBM Cloud Virtual Private Cloud - Typical use cases for this topology include:
    * Leverage IBM Cloud VPC x86 resources to create tiered applications across different hardware platforms i.e. x86 application servers and Power database servers.
* Private SSL connection - This is a specific use case for connecting to the classic environment so that the SSL VPN connection can be used to access your Power VS servers for operations and administration tasks.
* Private IPsec connection - This is a specific use case for connecting to the classic environment so that an IPsec VPN connection can be used to access your classic and Power VS servers. This network architecture is typically used for small production environments or proof-of-concept, development, and test purposes.
* Private Direct-Link connection - A Direct Link enables your remote networks to connect to IBM Cloud over a private connection that does not use public networks.

Multiple deployment topologies, described in this document, can be layered to create the desired topology required.

## Connect to private cloud
{: #network-reference-architecture-onprem}

In this deployment topology [Megaport](https://www.megaport.com/){: external} or IBM Cloud Connect is used to provide connectivity from your remote networks to your Power subnets.

![Connect to private cloud](./images/network-connect-to-onprem.svg "Connect to private cloud"){: caption="Figure 1. Connect to private cloud" caption-side="bottom"}

The key features of this connect to classic topology are as follows:

* Your {{site.data.keyword.powerSys_notm}} are hosted on your Power subnets. The IP address schema for these subnets is defined by you and should not overlap with your remote networks.
* The Power router is the default gateway for your {{site.data.keyword.powerSys_notm}} instances. The Power router is operated by the IBM Cloud team and you have no direct access or control.
* You extend your remote networks into the Megaport network, see [Connecting directly to the {{site.data.keyword.powerSys_notm}} environment by using Megaport connectivity services](/docs-draft/power-iaas?topic=power-iaas-configuring-power#connecting-megaport):
    * Megaport operates a global network infrastructure which enables on-demand connectivity to hundreds of global services in Asia Pacific, North America, Europe, and the Middle East.
    * A port is the physical point of connection between your organization’s network and the Megaport network. While a single data center connection is possible, best practice is to select two different port locations to provide redundancy.
    * Megaport has a number of Cloud Service Providers including IBM Cloud.
    * Virtual Cross Connects (VXCs) provide connections between any of the locations and services on the Megaport network. Ordering a VXC, via the Megaport Portal or Megaport API, allows you to connect into the {{site.data.keyword.powerSys_notm}} environment and  optionally the classic/VPC infrastructure environments or other clouds.

## Connecting {{site.data.keyword.powerSys_notm}} environments
{: #network-reference-architecture-pvs2pvs}

In this deployment topology [Megaport](https://www.megaport.com/){: external} or IBM Cloud Connect is used to provide connectivity between {{site.data.keyword.powerSys_notm}} environments.

![Connecting {{site.data.keyword.powerSys_notm}} environments](./images/network-connect-to-pvs2pvs.svg "Connecting {{site.data.keyword.powerSys_notm}} environments"){: caption="Figure 2. Connecting {{site.data.keyword.powerSys_notm}} environments" caption-side="bottom"}

The key features of this connect to classic topology are as follows:

* Your {{site.data.keyword.powerSys_notm}} are hosted on your Power subnets. The IP address schema for these subnets is defined by you and should not overlap between environments.
* The Power routers are the default gateways for your {{site.data.keyword.powerSys_notm}} instances. The Power routers are operated by the IBM Cloud team and you have no direct access or control.
* You connect your Power subnets to the Megaport network, see [Connecting directly to the {{site.data.keyword.powerSys_notm}} environment by using Megaport connectivity services](/docs-draft/power-iaas?topic=power-iaas-configuring-power#connecting-megaport):
    * Megaport operates a global network infrastructure which enables on-demand connectivity to hundreds of global services in Asia Pacific, North America, Europe, and the Middle East.
    * Virtual Cross Connects (VXCs) provide connections between any of the locations and services on the Megaport network. Ordering a VXC, via the Megaport Portal or Megaport API, allows you to connect two {{site.data.keyword.powerSys_notm}} environments.

## Connect to Classic
{: #network-reference-architecture-classic}

In this deployment topology, a Direct Link 2.0 is used to connect your {{site.data.keyword.powerSysShort}} networks to your resources hosted in your IBM Cloud Classic infrastructure environment. See [Ordering Direct Link Connect 2.0](/docs-draft/power-iaas?topic=power-iaas-ordering-direct-link-connect) for details on how to order this connection.

![Connect to Classic](./images/network-connect-to-classic.svg "Connect to Classic"){: caption="Figure 3. Connect to Classic" caption-side="bottom"}

The key features of this connect to classic topology are as follows:

* Your {{site.data.keyword.powerSys_notm}} are hosted on your Power subnets. The IP address schema for these subnets is defined by you and should not overlap with your classic private subnets or the IP addressing schema used for the services networks.
* The Power router is the default gateway for your {{site.data.keyword.powerSys_notm}} instances. The Power router is operated by the IBM Cloud team and you have no direct access or control.
* During the ordering process of your Direct Link, it is connected to the Power router and the Cross Connect Router (XCR). During this process BGP is configured:
    * The Power router advertises your Power subnets to the XCR.
    * The XCR advertises only your classic private subnets to the Power router.
* The XCR is operated by the IBM Cloud team and you have no direct access or control. The XCR will filter the following networks from the BGP advertisements from the Power router as they are used by the services networks: 10.0.0.0/14, 10.198.0.0/15, 10.200.0.0/14, 169.254.0.0/16, 224.0.0.0/4 and any IP ranges assigned to your classic private subnets.
* The Main Services Router (MSR) uses Access Control Lists (ACLs) which restricts access to the services networks to resources on your classic private subnets only. The IBM Cloud services networks are not accessible directly from your {{site.data.keyword.powerSys_notm}} instances.
* The Backend Customer Router (BCR) is the default gateway for bare metal or virtual server instances hosted on your classic private subnets.
* The Classic private subnets IP address schema is assigned to you when a subnet is ordered.
* IBM Cloud Direct Link Connect requires you to use a VRF (Virtual Routing and Forwarding) instance.
    * This VRF instance connects all the XCRs, BCRs and MSRs in all data centers and points of presence across the global IBM Cloud backbone.
    * VRFs allows multiple instances of a routing table to exist in a router and to work simultaneously. With VRF, each IBM Cloud account classic environment network is segmented within its own routing table. See [Virtual routing and forwarding on IBM Cloud](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).

Each IBM Cloud Direct Link service is not redundant, however, diversity can be engineered using multiple direct links and BGP. See [Models for diversity and redundancy in Direct Link (2.0)](/docs/dl?topic=dl-models-for-diversity-and-redundancy-in-direct-link)

## Connect to VPC
{: #network-reference-architecture-vpc}

In this deployment topology, a Direct Link 2.0 is used to connect your {{site.data.keyword.powerSysShort}} networks to your resources hosted in your IBM Cloud VPC infrastructure environment. See [Ordering Direct Link Connect 2.0](/docs-draft/power-iaas?topic=power-iaas-ordering-direct-link-connect) for details on how to order this connection.

![Connect to VPC](./images/network-connect-to-vpc.svg "Connect to VPC"){: caption="Figure 4. Connect to VPC" caption-side="bottom"}

The key features of this connect to classic topology are as follows:

* Your {{site.data.keyword.powerSys_notm}}s are hosted on your Power subnets. The IP address schema for these subnets is defined by you and should not overlap with your VPC subnets or the IP addressing schema used for the endpoint networks.
* The Power router is the default gateway for your {{site.data.keyword.powerSys_notm}} instances. The Power router is operated by the IBM Cloud team and you have no direct access or control.
* During the ordering process of your Direct Link, it is connected to the Power router and the Cross Connect Router (XCR). During this process BGP is configured:
    * The Power router advertises your Power subnets to the XCR.
    * The XCR advertises your VPC subnets to the Power router.
* The XCR is operated by the IBM Cloud team and you have no direct access or control:
    * The XCR will filter the following networks from the BGP advertisements from the Power router as they are used by the endpoint networks: 169.254.0.0/16, 224.0.0.0/4, 166.9.0.0/16 and any IP ranges assigned to your VPC subnets.
* The implicit router function in VPC provides routing functions to each VPC and allows each VPC to have access to its own copy of the IPv4 address space. The MPLS VPN allows for federating Direct Link, and Classic infrastructure environment. See [Network isolation, data packet flow, and the role of an implicit router in a VPC](https://www.ibm.com/cloud/architecture/content/course/advanced-networking-for-vpc/design-develop-and-deploy/){: external} for a full description.
* Endpoint networks - Service and infrastructure services endpoint networks are not accessible from your Power subnets. Virtual private endpoints are also not accessible from your Power subnets:
    * Service endpoints - allow connection to IBM Cloud services available through DNS names in the cloud.ibm.com domain and resolve to 166.9.x.x addresses.
    * Infrastructure services - allow connection to IBM Cloud services from the adn.networklayer.com domain and resolve to 161.26.0.0/16 addresses. Services that you can reach include:
      * DNS resolvers - 161.26.0.10 and 161.26.0.11 (Windows VS seems to be setup with 161.26.0.7 and Linux with 161.26.0.7 and 161.26.0.8)
      * Ubuntu and Debian mirrors - mirrors.adn.networklayer.com or 161.26.0.6
      * NTP - time.adn.networklayer.com or 161.26.0.6. This is the same IP address as the Ubuntu and Debian mirrors.
      * IBM Cloud Object Storage.
    * Virtual Private Endpoints - enables the connection to supported IBM Cloud services by using the IP addresses allocated from a subnet within your VPC. See [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services). Two infrastructure services of interest are; NTP and IBM Cloud Object Storage.

While endpoint networks cannot be accessed directly from your Power subnets, it is possible to use VPC virtual server instances to proxy these services. For example a virtual server running Nginx can proxy HTTPS to and from IBM Cloud Object Storage. A virtual server running NTP services, synchronized with time.adn.networklayer.com, could be used as a time source for PowerVS instances.

Each IBM Cloud Direct Link service is not redundant, however, diversity can be engineered using multiple direct links and BGP. See [Models for diversity and redundancy in Direct Link (2.0)](/docs/dl?topic=dl-models-for-diversity-and-redundancy-in-direct-link)

## Private SSL connection
{: #network-reference-architecture-privatessl}

The IBM Cloud SSL VPN service is a feature of the classic infrastructure environment and enables you to manage your classic resources, remotely, over the IBM Cloud private network. A SSL VPN connection from your location to the private network allows for out-of-band management and server rescue through an encrypted VPN tunnel. See [About VPN](/docs/iaas-vpn?topic=iaas-vpn-about-iaas-vpn).

The IBM Cloud SSL VPN service can only access your classic private IP subnets, therefore, you will not be able to use the SSL VPN feature to access your PowerVS instances directly from your workstation, so a jump box or bastion server is used.

![SSL VPN](./images/network-ssl-vpn.svg "SSL VPN"){: caption="Figure 5. SSL VPN" caption-side="bottom"}

The key features of this SSL VPN topology are as follows:

* This deployment topology builds upon the [Connect to Classic](/docs-draft/power-iaas?topic=power-iaas-network-reference-architecture-classic) so refer to that section as well.
* Your IBM Cloud account needs to have the required permissions, a VPN password configured, and you have access to the subnets hosting your resources, see [Activating or deactivating SSL VPN access for a user](/docs/iaas-vpn?topic=iaas-vpn-activate-or-deacivate-ssl-vpn-access-for-a-user).
* Your workstation or laptop at your location has the stand-alone VPN client installed. [Stand-alone VPN clients (Windows, Linux, and Mac OS X)](/docs/iaas-vpn?topic=iaas-vpn-standalone-vpn-clients)
* You have Internet access and the stand-alone client has a connection to the endpoint for the location hosting your classic resources, see [Available VPN endpoints](/docs/iaas-vpn?topic=iaas-vpn-available-vpn-endpoints).
* A jump server or bastion host with the OS of your choice has been deployed. Via RDP or SSH, you connect from your workstation or laptop at your location to the private IP address of your jump server or bastion server. On the jump server or bastion host SSH to your Power instances.

## Internet IPsec VPN connection
{: #network-reference-architecture-privateipsec}

Individual {{site.data.keyword.powerSys_notm}} can have Internet access, see [Public and private networks](/docs-draft/power-iaas?topic=power-iaas-about-power-iaas#public-private-networks), however, there is no site-to-site IPsec VPN service that connects your Power subnets to your remote networks, currently available.

![IPsec VPN](./images/network-ipsec-vpn.svg "SSL VPN"){: caption="Figure 6. IPsec VPN" caption-side="bottom"}

The key features of this IPsec VPN topology are as follows:

* This deployment topology leverages the IBM Cloud classic infrastructure gateway appliance to provide an Internet connected IPsec VPN gateway to enable a site-to-site VPN connection to your Power VS resources. See [Getting started with IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started).
    * The IBM Cloud gateway appliance allows you to selectively route private and public network traffic through a full-featured, enterprise level firewall powered by the software features of; VyOS, JunOS or any other operating system (Bring Your own Appliance (BYOA)) you choose.
    * All appliance features are customer-managed.
    * Via the IBM Cloud UI/CLI/API, you select your VLANs and hence, the associated subnets, that you want to associate with your gateway appliance. Associating a VLAN with a gateway appliance re-routes, or trunks, that VLAN and all of its subnets to your appliance, giving you control over filtering, forwarding, and protection.
    * A gateway appliance is attached to two non-removable transit VLANs, one each for your public and private networks.
* The Classic infrastructure environment VRF will contain the following routes, it will **NOT** contain routes to your remote networks:
    * Subnets assigned to you by IBM Cloud for use in your classic environment.
    * Your Power subnets advertised by the Power router.
* A site-to-site IPSec VPN is configured between a gateway in your remote network and the gateway appliance.
* Static routes or a routing protocol, such as BGP, is used to share routes between your gateway on your remote network and the gateway appliance. The routes that are advertised by the gateway appliance include your Power subnets.
* A Generic Routing Encapsulation (GRE) tunnel is required between the gateway appliance and the Power router as the Power router will not have routes for your remote networks advertised to it from the XCR. Within the GRE tunnel, static routes are configured between the Power router and the gateway appliance. See [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs-draft/power-iaas?topic=power-iaas-managing-cloud-connections#configure-gre-tunnel)

For a tutorial on site-to-site VPN connectivity, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.

While not shown on the diagram, x86 servers can be deployed onto the subnets contained within the associated and non-associated VLANs to build complex topologies such as 3 tier architectures.

## Private Direct-Link connection
{: #network-reference-architecture-directlink}

To connect your external networks to your Power subnets, you can use the IBM Cloud Direct Link service, however, you can not use this connectivity for a direct connection as both your Power subnets and your remote networks are considered to be external networks to the VRF and direct external to external traffic is prohibited. Therefore, in this deployment topology, a gateway appliance and GRE tunnels are used to provide connectivity.

This topology focuses on Direct Link (2.0) service which has the following offerings:

* Direct Link Dedicated - A single-tenant, fiber-based, cross-connect into the IBM Cloud Private network.
* Direct Link Connect - Uses a service provider who are already connected to the IBM Cloud private network to deliver multi-tenant, high capacity links, also known as network-to-network interfaces.

Direct Link (2.0)is not currently available in all locations, see [Locations](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-dedicated#dedicated-locations) for details about the IBM Cloud data centers where Direct Link Dedicated is available and [Providers and locations](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect#connect-locations) for Direct Link Connect.

If Direct Link (2.0) is not available at a suitable location then see
[Getting started with IBM Cloud Direct Link on Classic](/docs/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link).

![Direct Link](./images/network-dl-gre.svg "Direct Link"){: caption="Figure 7. Direct Link" caption-side="bottom"}

The key features of this Direct Link topology are as follows:

* This deployment topology leverages the IBM Cloud classic infrastructure gateway appliance to provide a GRE gateway. See [Getting started with IBM Cloud Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started).
    * The IBM Cloud gateway appliance allows you to selectively route private and optionally public network traffic through a full-featured, enterprise level firewall powered by the software features of; VyOS, JunOS or any other operating system (Bring Your own Appliance (BYOA)) you choose.
    * All appliance features are customer-managed.
    * Via the IBM Cloud UI/CLI/API, you select your VLANs and hence, the associated subnets, that you want to associate with your gateway appliance. Associating a VLAN with a gateway appliance re-routes, or trunks, that VLAN and all of its subnets to your appliance, giving you control over filtering, forwarding, and protection.
    * A gateway appliance is attached to a non-removable private transit VLAN, and optionally a non-removable public transit VLAN.
* The Classic infrastructure environment VRF will prohibit the direct routing of Power subnets to external networks traffic and vice versa.
* A GRE tunnel is required between the gateway appliance and the Power router as the Power router will not have routes for your remote networks advertised to it from the XCR. Within the GRE tunnel, static routes are configured between the Power router and the gateway appliance. See [Configuring Generic Routing Encapsulation (GRE) tunnel](/docs-draft/power-iaas?topic=power-iaas-managing-cloud-connections#configure-gre-tunnel)
* A GRE tunnel is required between the gateway appliance and a tunnel endpoint connected to your external networks to enable the remote network to remote network connectivity.
* See [Getting started with IBM Cloud Direct Link (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl), however, key elements of IBM Cloud Direct Link (2.0) include the following:
    * Requires BGP to establish the routes to a customer's remote network.
    * Each IBM Cloud Direct Link service is not redundant, however, diversity can be enabled over multiple direct links along with BGP.
    * Ensure that IP subnet overlaps do not exist between the infrastructure environments, remote networks and the services network.
    * The IBM Cloud services network isn't accessible directly from remote networks including your Power subnets.
* The services networks are only accessible from your subnets assigned to you in your Classic infrastructure environment. The services networks are not accessible from your external networks or your Power subnets.

For some tutorials based on some of the topologies described above, see [IBM Power Virtual Server Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}:.
