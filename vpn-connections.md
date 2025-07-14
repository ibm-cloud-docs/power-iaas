---

copyright:
  years: 2021, 2025

lastupdated: "2025-07-08"

keywords: VPN connections, IKE policies, IPsec policies, vpnaas, VPC VPN, VPN as a service

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# VPN connections
{: #VPN-connections}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---



{{site.data.keyword.powerSysFull}} offers a robust Virtual Private Network (VPN) solution that is tailored with security and seamless connectivity for businesses with diverse networking requirements. The VPN for {{site.data.keyword.powerSys_notm}} establishes a private and encrypted communication channel between the client-managed environment and the virtual server instances that are deployed on IBM Cloud.

For more information about creating a VPN connection, see [Creating a Virtual Private Cloud VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn) [Recommended]{: tag-teal}

The following deprecated method is also currently supported - [Creating a {{site.data.keyword.powerSys_notm}} VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections-deprecated) [Deprecated]{: tag-red}

## Creating a Virtual Private Cloud VPN connection
{: #vpc-vpn}

By using the Virtual Private Cloud (VPC) provided Virtual Private Network (VPN) service, you can use a dedicated VPN for a one-cloud experience and achieve improved reliability and high availability.

If you are using the {{site.data.keyword.powerSys_notm}} VPN as a Service (VPNaaS), you are encouraged to upgrade to the IBM Cloud VPC VPN before March 2024. The end of service for {{site.data.keyword.powerSys_notm}} VPNaaS is on 14 July 2025. IBM will not provide the standard support for the {{site.data.keyword.powerSys_notm}} VPNaaS after 18 January 2025. For assistance to upgrade or migrate to IBM Cloud VPC VPN, open a [support ticket](https://www.ibm.com/cloud/support){: external} or engage with your Customer Support Manager (CSM).
{: note}



When you complete the VPC VPN setup, you get the following benefits:
-	Private and low-cost connectivity to IBM Cloud services.
-	Access to your virtual server instances through the private IP address. You can use Secure Shell (SSH) and other client-managed applications that are running on your host for the access.

IBM Cloud offers the following two VPN options:
* _VPN for VPC_ for site-to-site gateways to safely and securely connect from client-managed environment to resources in VPC, Power, and classic infrastructure.
* _Client VPN for VPC_ for client-to-site servers that allow remote devices to secretly connect to the VPC network in a secure manner.

To learn more on the VPN options you get, see the VPC documentation on [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview).

Complete the following steps for creating a VPC VPN connection:
1.	Create a VPC resource.
2.	Create a Site-to-Site VPN gateway in VPC.
3.	Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace by using one of the following methods:
     -	Use a Transit Gateway in a Power Edge Router (PER) workspace.
     -	Use a Cloud connection in a non-PER workspace.

It is recommended that you create a direct cloud connection between the VPC and the {{site.data.keyword.powerSys_notm}}. Adding a Transit Gateway is feasible, but it incurs extra charges. The cloud connection setup is not required in a PER-enabled workspace.
{: note}






### Architecture diagram
{: #arc-diag-vpcvpn}

### Configuring VPC VPN in a PER workspace
{: #arch-per}

![VPC VPN in PER architecture diagram](./images/vpc_vpn_per.svg "Configuring VPC VPN in a PER workspace"){: caption="Configuring VPC VPN in a PER workspace" caption-side="bottom"}

1. Define the client-managed subnet in the address prefix for the VPC.
2. Define a routing table with Transit Gateway and VPN gateway.

### Configuring VPC VPN in a non-PER workspace
{: #arch-nonper}

![VPC VPN in non-PER architecture diagram](./images/vpc_vpn_legacy.svg "Configuring VPC VPN in a non-PER workspace"){: caption="Configuring VPC VPN in a non-PER workspace" caption-side="bottom"}

1. Define the client-managed subnet in the address prefix for the VPC.
2. Define a routing table with Direct Link and VPN gateway.
3. Attach Direct Link to workspace subnet.
4. You can choose to attach a Transit Gateway along with the Direct Link, but it incurs extra charges.

**Procedure**

1. Create a VPC resource. Complete the steps that are documented in [Using the IBM Cloud console to create VPC resources](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console).

2. Create a Site-to-Site VPN gateway in VPC. Complete the steps documented in [About site-to-site VPN gateways](/docs/vpc?topic=vpc-using-vpn).

     To create a VPN connection, use a policy-based VPN.
     {: note}

3. Attach the VPN connection to the {{site.data.keyword.powerSys_notm}} workspace. Use one of the following procedures that suit your needs:
   - For a PER-enabled workspace, see: [Attaching Transit Gateway to a PER workspace](/docs/power-iaas?topic=power-iaas-per#migrate-per).
   - For a non-PER enabled workspace, see: [Creating IBM Cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections).

### Considerations for configuring VPC VPN in a non-PER workspace
{: #vpcvpn-cons}



To configure VPC VPN in a non-PER workspace, you must consider the following points:

* Use a policy-based VPN in all the configurations of the VPN connection. 
* Add the subnets that are created in the {{site.data.keyword.powerSys_notm}} to the local CIDR list of IBM Cloud VPC and to the peer CIDR list of VPC in your client-managed environment.
* Enable VPN gateway and traffic source for Direct Link and Transit Gateway in the **Edit Traffic** window that is present in the routing table of IBM Cloud VPC.

Select Direct Link that is enabled with Transit Gateway or disable the configuration for different {{site.data.keyword.powerSys_notm}} workspaces that are in the same region.



### Changing from VPNaaS to the VPC VPN service
{: #vpnaas-to-vpcvpn}

To use the VPC VPN service, you must switch from VPNaaS to VPC VPN service. The following example illustrates the steps to set up the VPC VPN connection and \validate the switch from VPNaaS to the VPC VPN service:

1. Create a VPC connection in the same data center as the {{site.data.keyword.powerSys_notm}} by using the same account. Complete the following configurations:

      1. The default routing table must be configured by selecting the `VPN server` and `VPN gateway` values for **Accepts routes from** option. This configuration allows the traffic between the virtual servers that are members of the VPC subnet and the devices on the remote side of the VPN connection.
      2. Create a second routing table to select VPN server, VPN gateway, and Transit Gateway. Under Transit Gateway, select the **Advertise to** option. For more information, see [Getting started with Virtual Private Cloud (VPC)](https://cloud.ibm.com/docs/vpc?topic=vpc-getting-started){: external}.

2. Establish a VPN connection between the VPC and the remote side of the existing VPNaaS. Use the following considerations:

   1. Use a policy-based VPN in all the configurations of the VPN connection.
   2. Subnets for the remote VPN, VPC, and workspace must be distinct. Subnets cannot be shared or overlapped.
   3. Add the workspace CIDRs to the list of local CIDRs in the VPN connection.
   4. Add the workspace CIDRs to the peer CIDRs list in the VPNaaS remote side.

   For more information about VPN options, see [About site-to-site VPN gateways](https://cloud.ibm.com/docs/vpc?topic=vpc-using-vpn){: external}.

3. Create a Transit Gateway by completing the following steps:
   1. Add VPC to Transit Gateway.
   2. Under the **Routes** tab, generate a routing table. You can see the list of VPC, CIDR, and the CIDR for the remote side of the VPN.

   For more information about Transit Gateways, see [Getting started with IBM Cloud Transit Gateway](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-getting-started){: external}.

   The transition to VPC VPN can begin assuming that the following list is true:
   * The connectivity between a virtual server on the VPC and a system on the remote side of the VPN is working.
   * The CIDRs are advertised through to the Transit Gateway.

     The workspace and the remote side of the VPN are not connected until all transition to VPC VPN is completed.
     {: note}

4. Delete the VPNaaS gateway. You must select the VPNaaS connections that are attached to the workspace.

5. Migrate the workspace to PER. You must remove the active Cloud Connections attached to the workspace on other subnets. For more information, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per).

6. Connect to the Transit Gateway after the workspace is PER-enabled.

7. Generate the routing table. The CIDRs for the workspace are listed along with the existing CIDRs.



### Additional information
{: #vpcvpn-add-info}

- [Connecting IBM VPC to IBM {{site.data.keyword.powerSys_notm}}s and IBM Cloud Object Storage](https://www.ibm.com/blog/connecting-ibm-vpc-to-ibm-power-virtual-servers-and-ibm-cloud-object-storage/){: external}.
