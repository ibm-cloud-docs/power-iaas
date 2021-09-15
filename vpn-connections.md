---

copyright:
  years: 2021

lastupdated: "2021-09-08"

keywords: VPN connections, IKE policies, IPsec policies

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Managing VPN connections
{: #VPN-connections}

You can connect an on-premises virtual private network (VPN) gateway to an IBM Cloud™ VPN gateway that is created within a Power Systems Virtual Server VPN gateway by using the VPN service that is provided by IBM Power Systems Virtual Server. You can use VPN to log in to the private network, complete your work securely, and log out. This capability offers you site-to-site IP security (IPsec) VPN between your on-premises location and Power Systems Virtual Servers to enable low-cost secure connectivity.

With VPN access, you can:

- Ensure private and low-cost connectivity to IBM Cloud services.
- Access your Virtual Servers through the primary private IP address by using Secure Shell (SSH) or Remote Desktop Protocol (RDP).
- Connect to your Virtual Server’s Intelligent Platform Management Interface (IPMI) IP address for low-level server management or rescue needs.

The Power Systems Virtual Server infrastructure consists of subnets and virtual server instances (VSIs).  You can use VPN as a service with your existing VSIs and private networks. To create a VSI or a private network, see [Creating a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet). Each of your IBM Cloud accounts can be provided with VPN access and it can be limited to the subnets that need VPN access. Ensure that the VPN access is enabled and a VPN password is specified before you attempt to log in to VPN services. You can use VPN for Virtual Private Cloud (VPC) to securely connect your VPC to an on-premises network through a VPN tunnel. For more information, see [Connecting to your on-premises network](/docs/pvpc?topic=vpc-vpn-onprem-example).

A maximum of four VPN connections are supported for one user account. A maximum of four policies (IKE and IPsec) for a VPN connection is supported.
{: important}

To learn more about using the command-line interface (CLI) for VPN connections, see [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

## Creating VPN connections
{: #creating-VPN-connections}

You can create a new VPN connection by using the `ibmcloud pi vpn-connection-create` command. For creating, viewing, updating, or deleting a VPN connection by using CLI, see [VPN connections](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

You can view allowable and default values for attributes when you are creating Internet Key Exchange (IKE) and IPsec policies for a VPN connection. These values are listed under each command in the CLI.

IKE policy version 2 is not compatible with policy-based VPN connections. If you attempt to add an IKE policy version 2 to a policy-based VPN connection, an error is displayed.
{: important}

## Creating IKE and IPsec policies
{: #creating-IKE-policies}

When you create a VPN connection, you must set the IKE and IPsec policies. IBM provides default IKE and IPsec policies. You can also create custom policies based on your requirements.

### Adding a VPN IKE policy to a VPN connection
{: #adding-IKE-policies}

You can use the default or custom IKE policies to define security parameters that will be used during Phase 1 of IKE negotiation. In this phase, credentials and security policies are exchanged between the VPN and peer device to authenticate with each other and to establish a secure communication channel that will be used for Phase 2 of IKE negotiation.

You can add an IKE policy by using the `ibmcloud pi vpn-ike-policy-add` command. For more information about adding, viewing, updating, or deleting an IKE policy by using CLI, see [VPN IKE policy](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-ike-policy).

### Adding and configuring IPsec policy to a VPN connection
{: #adding-IPsec-policies}

You can use the default or custom IPsec policies to define security parameters that will be used during Phase 2 of IKE negotiation. In this phase, the VPN and peer device use the security association that is established during Phase 1 of IKE negotiation to negotiate what traffic to send and how to authenticate and encrypt that traffic.

You can add an IPsec policy by using the `ibmcloud pi vpn-ipsec-policy-add` command. For more information on adding, viewing, updating, or deleting an IPsec policy by using CLI, see [VPN IPsec policy](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-ike-policy).

## Attaching subnets to VPN connections
{: #attach_subnets_VPN}

If you create a Power Systems Virtual Servers service that contains VPN connections, you must also have Local subnets and Peer subnets that are connected to the VPN connection.

You must route Power Systems Virtual Server private network subnets over VPN connections to allow access to your Power Systems Virtual Server over private network.
When you create a subnet or edit details of a subnet, you can attach an existing VPN connection to the subnet.

For more information about attaching or detaching subnets by using CLI, see [VPN subnets](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connection-local-subnets).
