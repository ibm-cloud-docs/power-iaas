---

copyright:
  years: 2020, 2023

lastupdated: "2023-12-04"

keywords: VPC VPN, VPNaaS,

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

# Creating a VPC VPN
{: #vpn-connectivity}

The Virtual Private Cloud's (VPC) Virtual Private Network (VPN) service enables you to use a dedicated VPN that is a more robust service than the legacy {{site.data.keyword.powerSysFull}} VPN service. 

It is recommended that you migrate from {{site.data.keyword.powerSys_notm}} VPN to the latest VPC VPN.
{: important}

When you complete the VPC VPN set up, you can:
-	Ensure a private and low-cost connectivity to IBM Cloud services.
-	Access your virtual server instances through the private IP address using Secure Shell (SSH) and other on-premises applications running on your host.

This topic provides you guidance on how to create or use the VPC VPN. Here is the summarized steps for creating a VPC VPN:
1.	[Create a VPC resource](/docs/power-iaas?topic=power-iaas-vpn-connectivity#step-1).
2.	[Create a Site-to-Site VPN gateway in VPC](/docs/power-iaas?topic=power-iaas-vpn-connectivity#step-2)
3.	Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace using one of the following methods:
  -	[In PER workspace through TGW](/docs/power-iaas?topic=power-iaas-vpn-connectivity#step-3)
  -	[In non-PER workspace through Cloud connection](/docs/power-iaas?topic=power-iaas-vpn-connectivity#step-3)

It is recommended that you create a direct cloud connection between the VPC and the {{site.data.keyword.powerSys_notm}}. Adding in the trasit gateway is viable, but it incurs additional charges. The cloud connection set up is not required in a PER-enabled workspace.
{: note}

## Architecture diagram
{: arc-diag-vpcvpn}

### Configuring VPC VPN in a PER workspace
{: arch-per}

![VPC VPN in PER architecture diagram](./images/vpc_vpn_per "Configuring VPC VPN in a PER workspace"){: caption="Figure 1. Configuring VPC VPN in a PER workspace" caption-side="bottom"}

1. Define the on-premises subnet in the address prefix for the VPC.
2. Define a routing table with Transit Gateway and VPN gateway.

### Configuring VPC VPN in a non-PER workspace
{: arch-nonper}

![VPC VPN in non-PER architecture diagram](./images/vpc_vpn_legacy "Configuring VPC VPN in a non-PER workspace"){: caption="Figure 1. Configuring VPC VPN in a non-PER workspace" caption-side="bottom"}

1. Define the on-premises subnet in the address prefix for the VPC.
2. Define a routing table with Direct Link and VPN gateway.
3. Attach Direct Link to workspace subnet.
4. You can choose to attach a trasit gateway along with the Direct Link, but it will incur additional charges.

## Step 1
{: vpc-vpn-1}

**Create a VPC resource.** \n
Complete the steps documented in [Using the IBM Cloud console to create VPC resources](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

## Step 2
{: vpc-vpn-2}

**Create a Site-to-Site VPN gateway in VPC** \n
Complete the steps documented in [About site-to-site VPN gateways](/docs/vpc?topic=vpc-using-vpn).


## Step 3
{: vpc-vpn-3}

**Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace**. \n

Use one the following procedures that suit your needs:
  -	For a PER enabled workspace, see: [Attaching Transit Gateway to a PER workspace](/docs/power-iaas?topic=power-iaas-per#attaching-transit-gateway-to-a-per-workspace).
  -	For a non-per enabled workspace, see: [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

## Considerations
{: vpcvpn-cons}

1.	Subnets created in {{site.data.keyword.powerSys_notm}} needs to be added to Local CIDR list of IBM Cloud VPC and Peer CIDR list of On-premises VPC.
2.	In routing table of IBM Cloud VPC, you must enable VPN Gateway and traffic source for Direct Link and Transit Gateway (in Edit Traffic panel).
3.	Choose the Direct Link with Transit Gateway enabled or disable configuration for different {{site.data.keyword.powerSys_notm}} workspaces that are in the same region.  


## Additional information
{: vpcvpn-add-info}

- [Connecting IBM VPC to IBM {{site.data.keyword.powerSys_notm}}s and IBM Cloud Object Storage](https://www.ibm.com/blog/connecting-ibm-vpc-to-ibm-power-virtual-servers-and-ibm-cloud-object-storage/){: external}.