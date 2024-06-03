---

copyright:
  years: 2021, 2024

lastupdated: "2024-05-16"

keywords: VPN connections, IKE policies, IPsec policies, vpnaas, VPC VPN, VPN as a service

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# VPN connections
{: #VPN-connections}

{{site.data.keyword.powerSysFull}} offers a robust Virtual Private Network (VPN) solution that is tailored with security and seamless connectivity for businesses with diverse networking requirements. The VPN for {{site.data.keyword.powerSys_notm}} establishes a private and encrypted communication channel between [client-managed environment]{: tag-teal} environments and the virtual server instances that are deployed on IBM Cloud.

There is a new method for creating a VPN connection - [Creating a Virtual Private Cloud VPN connection](/docs/allowlist/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) [Recommended]{: tag-teal}

The following deprecated method is also currently supported - [Creating a {{site.data.keyword.powerSys_notm}} VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections-deprecated) [Deprecated]{: tag-red}

## Creating a Virtual Private Cloud VPN connection
{: #vpc-vpn}

The Virtual Private Cloud's (VPC) Virtual Private Network (VPN) service allows using a dedicated VPN for a one-cloud experience, improved reliability and high availability.

If you are using the {{site.data.keyword.powerSys_notm}} VPN, upgrading to IBM Cloud VPC VPN is encouraged before March 2024 with the end of service on 14 July 2025. After 18 January 2025, IBM won't provide standard support for the legacy {{site.data.keyword.powerSys_notm}} VPNaaS. If you need any assistance on upgrading or migration, open a [support ticket](https://www.ibm.com/cloud/support){: external} or engage with your Customer Support Manager (CSM).
{: note}


When you complete the VPC VPN set-up, you can:
-	Ensure a private and low-cost connectivity to IBM Cloud services.
-	Access your virtual server instances through the private IP address by using Secure Shell (SSH) and other [client-managed]{: tag-teal} applications running on your host.

IBM Cloud offers the following two VPN options:
* _VPN for VPC_ for site-to-site gateways to safely and securely connect from [client-managed environment]{: tag-teal} to resources in VPC, Power, and Classic infrastructure
* _Client VPN for VPC_ for client-to-site servers allowing remote devices to secretly connect to the VPC network in a secure manner.

To learn more on the VPN options you get, see the VPC documentation on [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview).

This topic provides you with guidance on how to create or use the VPC VPN. Following are the steps for creating a VPC VPN:
1.	Create a VPC resource.
2.	Create a Site-to-Site VPN gateway in VPC
3.	Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace by using one of the following methods:
     -	In PER workspace through TGW
     -	In non-PER workspace through Cloud connection.

It is recommended that you create a direct cloud connection between the VPC and the {{site.data.keyword.powerSys_notm}}. Adding in the Transit Gateway is viable, but it incurs extra charges. The cloud connection set-up is not required in a PER-enabled workspace.
{: note}

### Architecture diagram
{: #arc-diag-vpcvpn}

### Configuring VPC VPN in a PER workspace
{: #arch-per}

![VPC VPN in PER architecture diagram](./images/vpc_vpn_per.svg "Configuring VPC VPN in a PER workspace"){: caption="Figure 1. Configuring VPC VPN in a PER workspace" caption-side="bottom"}

1. Define the [client-managed ]{: tag-teal} subnet in the address prefix for the VPC.
2. Define a routing table with Transit Gateway and VPN gateway.

### Configuring VPC VPN in a non-PER workspace
{: #arch-nonper}

![VPC VPN in non-PER architecture diagram](./images/vpc_vpn_legacy.svg "Configuring VPC VPN in a non-PER workspace"){: caption="Figure 1. Configuring VPC VPN in a non-PER workspace" caption-side="bottom"}

1. Define the [client-managed]{: tag-teal} subnet in the address prefix for the VPC.
2. Define a routing table with Direct Link and VPN gateway.
3. Attach Direct Link to workspace subnet.
4. You can choose to attach a Transit Gateway along with the Direct Link, but it incurs extra charges.

**Procedure**

1. Create a VPC resource. Complete the steps that are documented in [Using the IBM Cloud console to create VPC resources](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

2. Create a Site-to-Site VPN gateway in VPC. Complete the steps documented in [About site-to-site VPN gateways](/docs/vpc?topic=vpc-using-vpn).

     While creating a VPN connection, use a policy-based VPN.
     {: note}

3. Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace. Use one of the following procedures that suit your needs:
   - For a PER-enabled workspace, see: [Attaching Transit Gateway to a PER workspace](/docs/allowlist/power-iaas?topic=power-iaas-per#attaching-transit-gateway-to-a-per-workspace).
   - For a non-PER enabled workspace, see: [Creating IBM Cloud connections](/docs/allowlist/power-iaas?topic=power-iaas-cloud-connections).

### Considerations
{: #vpcvpn-cons}

1. The VPN connection that is used in all the configurations are policy-based VPN.
2. Subnets that are created in {{site.data.keyword.powerSys_notm}} needs to be added to Local CIDR list of IBM Cloud VPC and Peer CIDR list of [VPC in your client-managed environment]{: tag-teal}.
3. In the routing table of IBM Cloud VPC, you must enable VPN Gateway and traffic source for Direct Link and Transit Gateway (in Edit Traffic window).
4. Choose the Direct Link with Transit Gateway enabled or disable configuration for different {{site.data.keyword.powerSys_notm}} workspaces that are in the same region.


### Additional information
{: #vpcvpn-add-info}

- [Connecting IBM VPC to IBM {{site.data.keyword.powerSys_notm}}s and IBM Cloud Object Storage](https://www.ibm.com/blog/connecting-ibm-vpc-to-ibm-power-virtual-servers-and-ibm-cloud-object-storage/){: external}.
