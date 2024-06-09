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

{{site.data.keyword.powerSysFull}} offers a robust Virtual Private Network (VPN) solution that is tailored with security and seamless connectivity for businesses with diverse networking requirements. The VPN for {{site.data.keyword.powerSys_notm}} establishes a private and encrypted communication channel between the client-managed environment<!--Q2 client-managed to be confirmed by Joe--> and the virtual server instances that are deployed on IBM Cloud.

For more information about creating a VPN connection, see [Creating a Virtual Private Cloud VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) [Recommended]{: tag-teal}

The following deprecated method is also currently supported - [Creating a {{site.data.keyword.powerSys_notm}} VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections-deprecated) [Deprecated]{: tag-red}

## Creating a Virtual Private Cloud VPN connection
{: #vpc-vpn}

By using the Virtual Private Cloud (VPC) provided Virtual Private Network (VPN) service, you can use a dedicated VPN for a one-cloud experience and achieve improved reliability and high availability.

If you are using the {{site.data.keyword.powerSys_notm}} VPN as a Service (VPNaaS)<!--was VPN confirm-->, you are encouraged to upgrade to the IBM Cloud VPC VPN before March 2024. The end of service for {{site.data.keyword.powerSys_notm}} VPNaaS is on 14 July 2025. IBM will not provide the standard support for the {{site.data.keyword.powerSys_notm}} VPNaaS after 18 January 2025. For assistance to upgrade or migrate to IBM Cloud VPC VPN, open a [support ticket](https://www.ibm.com/cloud/support){: external} or engage with your Customer Support Manager (CSM).
{: note}

<!--confirm with Mukesh-->

When you complete the VPC VPN setup, you get the following benefits:
-	Private and low-cost connectivity to IBM Cloud services.
-	Access to your virtual server instances through the private IP address. You can use Secure Shell (SSH) and other client-managed<!--Q2 client-managed to be confirmed by Joe--> applications that are running on your host for the access.

IBM Cloud offers the following two VPN options:
* _VPN for VPC_ for site-to-site gateways to safely and securely connect from client-managed environment<!--Q2 client-managed to be confirmed by Joe--> to resources in VPC, Power, and classic infrastructure.
* _Client VPN for VPC_ for client-to-site servers that allow remote devices to secretly connect to the VPC network in a secure manner.

To learn more on the VPN options you get, see the VPC documentation on [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview).

Complete the following steps for creating a VPC VPN connection:
1.	Create a VPC resource.
2.	Create a Site-to-Site VPN gateway in VPC.
3.	Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace by using one of the following methods:
     -	Use a Transit Gateway in a PER workspace.<!--TGW was used-->
     -	Use a Cloud connection in a non-PER workspace.

It is recommended that you create a direct cloud connection between the VPC and the {{site.data.keyword.powerSys_notm}}. Adding a Transit Gateway is feasible<!--viable-->, but it incurs extra charges. The cloud connection setup is not required in a PER-enabled workspace.
{: note}

### Architecture diagram
{: #arc-diag-vpcvpn}

### Configuring VPC VPN in a PER workspace
{: #arch-per}

![VPC VPN in PER architecture diagram](./images/vpc_vpn_per.svg "Configuring VPC VPN in a PER workspace"){: caption="Figure 1. Configuring VPC VPN in a PER workspace" caption-side="bottom"}

1. Define the client-managed<!--Q2 client-managed to be confirmed by Joe--> subnet in the address prefix for the VPC.
2. Define a routing table with Transit Gateway and VPN gateway.

### Configuring VPC VPN in a non-PER workspace
{: #arch-nonper}

![VPC VPN in non-PER architecture diagram](./images/vpc_vpn_legacy.svg "Configuring VPC VPN in a non-PER workspace"){: caption="Figure 1. Configuring VPC VPN in a non-PER workspace" caption-side="bottom"}

1. Define the client-managed<!--Q2 client-managed to be confirmed by Joe--> subnet in the address prefix for the VPC.
2. Define a routing table with Direct Link and VPN gateway.
3. Attach Direct Link to workspace subnet.
4. You can choose to attach a Transit Gateway along with the Direct Link, but it incurs extra charges.

**Procedure**

1. Create a VPC resource. Complete the steps that are documented in [Using the IBM Cloud console to create VPC resources](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

2. Create a Site-to-Site VPN gateway in VPC. Complete the steps documented in [About site-to-site VPN gateways](/docs/vpc?topic=vpc-using-vpn).

     To create a VPN connection, use a policy-based VPN.
     {: note}

3. Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace. Use one of the following procedures that suit your needs:
   - For a PER-enabled workspace, see: [Attaching Transit Gateway to a PER workspace](/docs/power-iaas?topic=power-iaas-per#attaching-transit-gateway-to-a-per-workspace).
   - For a non-PER enabled workspace, see: [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Considerations for configuring VPC VPN in a non-PER workspace
{: #vpcvpn-cons}

Consider the following points for configuring VPC VPN in a non-PER workspace:

* Use a policy-based VPN in all the configurations of the VPN connection. <!--The VPN connection that is used in all the configurations are policy-based VPN.-->
* Add the subnets that are created in the {{site.data.keyword.powerSys_notm}} to the Local CIDR list of IBM Cloud VPC and Peer CIDR list of VPC in your client-managed environment. <!--Q2 client-managed to be confirmed by Joe-->
* Enable VPN Gateway and traffic source for Direct Link and Transit Gateway (in the Edit Traffic window) in the routing table of IBM Cloud VPC.
1. Choose the Direct Link that is enabled with the Transit Gateway or disable the configuration for different {{site.data.keyword.powerSys_notm}} workspaces that are in the same region.


### Additional information
{: #vpcvpn-add-info}

- [Connecting IBM VPC to IBM {{site.data.keyword.powerSys_notm}}s and IBM Cloud Object Storage](https://www.ibm.com/blog/connecting-ibm-vpc-to-ibm-power-virtual-servers-and-ibm-cloud-object-storage/){: external}.
