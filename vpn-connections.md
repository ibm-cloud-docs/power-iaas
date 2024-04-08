---

copyright:
  years: 2021, 2024

lastupdated: "2024-04-08"

keywords: VPN connections, IKE policies, IPsec policies, vpnaas, VPC VPN, VPN as a service

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# VPN connections
{: #VPN-connections}

{{site.data.keyword.powerSysFull}} offers a robust Virtual Private Network (VPN) solution that is tailored with security and seamless connectivity for businesses with diverse networking requirements. The VPN for {{site.data.keyword.powerSys_notm}} establishes a private and encrypted communication channel between on-premises environments and the virtual server instances that are deployed on IBM Cloud.

IBM Cloud offers the following two VPN options:  
* _VPN for VPC_ for site-to-site gateways that allows to safely and securely connect from on-premises to resources in VPC, Power, and Classic infrastructure 
* _Client VPN for VPC_ for client-to-site servers that allows remote devices to secretly connect to the VPC network in a secure manner.

To learn more on the VPN options you get, see the VPC documentation on [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview).

## Deploying an automated VPN on your workspace
{: #auto-vpc-vpn}

Automation projects that use [IBM Cloud Schematics](https://www.ibm.com/products/schematics){: external} are now available on GitHub to create or use an existing IBM {{site.data.keyword.powerSys_notm}} workspace that is connected to a VPC using Transit Gateway. These Terraform Infrastructures as Code (IaC) modules offer VPN connections that allow private communication to your IBM {{site.data.keyword.powerSys_notm}}.

These automations provide one-click deployment. For example, the site-to-site VPN automation reduces deployment time from days to 3 minutes. 

You can download or clone the GitHub repository and use that IaC locally with the terraform command. You can also choose to create a Schematics workspace and point to the project's public GitHub repository. 

To understand the details for general Power Systems communication through VPC, including architecture, and troubleshooting, see the [Power Systems communication through a VPC Transit Hub](/docs/solution-tutorials?topic=solution-tutorials-vpc-transit-power) solution tutorial.

### Site-to-site VPN automation
{: #s2s-auto-vpn}

Use this Terraform module to create a [site-to-site VPN gateway](/docs/vpc?topic=vpc-using-vpn), which allows a secure connection over the internet from your local on-premises network to private resources in a {{site.data.keyword.powerSys_notm}} workspace. This Terraform IaC creates a policy-based VPN gateway and connection with local and peer policies. 

A Transit Gateway and IBM {{site.data.keyword.powerSys_notm}} workspace are created by default, but you can override the default by specifying existing ones. 

If you need to identity support for AIX or IBM i, specify the local and remote identities.
{: note}

The GitHub repository for site-to-site VPN automation is located [here](https://github.com/IBM/power-vpn-gateway/){: external}.

To download the IBM Cloud Schematics repository and learn more about Schematics, see [Getting started: IBM Cloud Schematics](/docs/schematics?topic=schematics-getting-started).

![Power connectivity solutions by using VPN for VPC](https://video.ibm.com/embed/recorded/133346636){: video output="iframe" data-script="none" id="watsonmediaplayer" width="560" height="315" scrolling="no" allowfullscreen webkitallowfullscreen mozAllowFullScreen frameborder="0" style="border: 0 none transparent;"}

### Client-to-site VPN automation 
{: #c2s-auto-vpn}

Use this Terraform module to create a [client-to-site VPN server](/docs/vpc?topic=vpc-vpn-client-to-site-overview), which allows users to safely connect from an onsite or remote device to a Power Virtual Server workspace. This allows users to connect immediately from their device and start working with the IBM Power Virtual Server infrastructure. 

The GitHub repository for client-to-server VPN automation is located [here](https://github.com/IBM/power-vpn-server). 

An OVPN file is generated from Terraform, applied, and then stored in a Cloud Object Storage bucket for the user to import into the OpenVPN desktop client.

To download the IBM Cloud Schematics repository and learn more about Schematics, see [Getting started: IBM Cloud Schematics](/docs/schematics?topic=schematics-getting-started).

## Deploying a manual VPC VPN on your workspace
{: #vpc-vpn}

The Virtual Private Cloud's (VPC) Virtual Private Network (VPN) service allows using a dedicated VPN for a one-cloud experience, improved reliability and high availability.

The manual VPN connection can be set in the following ways:
 - [Creating a Virtual Private Cloud VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) [Recommended]{: tag-teal}
 - [Creating a {{site.data.keyword.powerSys_notm}} VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections-deprecated) [Deprecated]{: tag-red}

If you are using the {{site.data.keyword.powerSys_notm}} VPN, upgrading to IBM Cloud VPC VPN is encouraged before March 2024 with the end of service on 14 July 2025. After 18 January 2025, IBM won't provide standard support for the legacy {{site.data.keyword.powerSys_notm}} VPNaaS. If you need any assistance on upgrading or migration, open a [support ticket](https://www.ibm.com/cloud/support){: external} or engage with your Customer Support Manager (CSM).
{: note}
 

When you complete the VPC VPN set-up, you can:
-	Ensure a private and low-cost connectivity to IBM Cloud services.
-	Access your virtual server instances through the private IP address by using Secure Shell (SSH) and other on-premises applications running on your host.


This topic provides you with guidance on how to create or use the VPC VPN. Following are the steps for creating a VPC VPN:
1.	Create a VPC resource.
2.	Create a Site-to-Site VPN gateway in VPC
3.	Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace by using one of the following methods:
     -	In PER workspace through TGW
     -	In non-PER workspace through Cloud connection.

It is recommended that you create a direct cloud connection between the VPC and the {{site.data.keyword.powerSys_notm}}. Adding in the Transit Gateway is viable, but it incurs extra charges. The cloud connection set-up is not required in a PER-enabled workspace.
{: note}

### Architecture diagram
{: arc-diag-vpcvpn}

### Configuring VPC VPN in a PER workspace
{: arch-per}

![VPC VPN in PER architecture diagram](./images/vpc_vpn_per.svg "Configuring VPC VPN in a PER workspace"){: caption="Figure 1. Configuring VPC VPN in a PER workspace" caption-side="bottom"}

1. Define the on-premises subnet in the address prefix for the VPC.
2. Define a routing table with Transit Gateway and VPN gateway.

### Configuring VPC VPN in a non-PER workspace
{: arch-nonper}

![VPC VPN in non-PER architecture diagram](./images/vpc_vpn_legacy.svg "Configuring VPC VPN in a non-PER workspace"){: caption="Figure 1. Configuring VPC VPN in a non-PER workspace" caption-side="bottom"}

1. Define the on-premises subnet in the address prefix for the VPC.
2. Define a routing table with Direct Link and VPN gateway.
3. Attach Direct Link to workspace subnet.
4. You can choose to attach a Transit Gateway along with the Direct Link, but it incurs extra charges.

**Procedure**

1. Create a VPC resource. Complete the steps that are documented in [Using the IBM Cloud console to create VPC resources](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

2. Create a Site-to-Site VPN gateway in VPC. Complete the steps documented in [About site-to-site VPN gateways](/docs/vpc?topic=vpc-using-vpn).

     While creating a VPN connection, use a policy-based VPN.
     {: note}

3. Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace. Use one of the following procedures that suit your needs:
   - For a PER-enabled workspace, see: [Attaching Transit Gateway to a PER workspace](/docs/power-iaas?topic=power-iaas-per#attaching-transit-gateway-to-a-per-workspace).
   - For a non-PER enabled workspace, see: [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Considerations
{: vpcvpn-cons}

1. The VPN connection that is used in all the configurations are policy-based VPN.
2. Subnets that are created in {{site.data.keyword.powerSys_notm}} needs to be added to Local CIDR list of IBM Cloud VPC and Peer CIDR list of On-premises VPC.
3. In the routing table of IBM Cloud VPC, you must enable VPN Gateway and traffic source for Direct Link and Transit Gateway (in Edit Traffic window).
4. Choose the Direct Link with Transit Gateway enabled or disable configuration for different {{site.data.keyword.powerSys_notm}} workspaces that are in the same region.  


### Additional information
{: vpcvpn-add-info}

- [Connecting IBM VPC to IBM {{site.data.keyword.powerSys_notm}}s and IBM Cloud Object Storage](https://www.ibm.com/blog/connecting-ibm-vpc-to-ibm-power-virtual-servers-and-ibm-cloud-object-storage/){: external}.
