---

copyright:
  years: 2019, 2023

lastupdated: "2023-11-30"

keywords: networking diagrams, network architecture, private ssl, private ipsec, direct link connect, colocation, data center, cloud connect, megaport

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network architecture diagrams for non-PER
{: #network-architecture-diagrams-former}

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
