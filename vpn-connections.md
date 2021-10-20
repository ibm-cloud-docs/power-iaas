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

You can connect an on-premises virtual private network (VPN) gateway to an IBM Cloud™ VPN gateway that is created within a Power Systems Virtual Server VPN gateway by using the VPN service that is provided by IBM Power Systems Virtual Server. You can use VPN to connect to the private network, complete your work securely, and log out. This capability offers you site-to-site IP security (IPsec) VPN between your on-premises location and Power Systems Virtual Servers to enable low-cost secure connectivity.

With VPN access, you can:

- Ensure private and low-cost connectivity to IBM Cloud services.
- Access your Virtual Servers through the primary private IP address by using Secure Shell (SSH) and your other on-premises applications that are running on your on-premises host.

The Power Systems Virtual Server infrastructure consists of subnets and virtual server instances (VSIs). You can use VPN as a service with your existing VSIs and private networks. To create a VSI on a private network, see [Creating a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet). Each of your IBM Cloud accounts can be provided with VPN access and it can be limited to the subnets that need VPN access. Ensure that the VPN access is enabled and a VPN password is specified before you attempt to log in to VPN services. You can use VPN to securely connect your Power Virtual Server Service Instance to an on-premises network through a VPN tunnel. For more information, see [Connecting to your on-premises network](/docs/vpc?topic=vpc-vpn-onprem-example&interface=ui){: new_window}.

A maximum of four VPN connections are supported for one user account. A maximum of four policies (IKE and IPsec) for a VPN connection is supported.
{: important}

To learn more about using the command-line interface (CLI) for VPN connections, see [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

## Power Systems Virtual Servers service instances support with VPN
{: #powervs-support-vpn}

Power Systems Virtual Server supports multiple service instances from the same account. However, only a single service instance can use a VPN connection. If you want to configure a setup with multiple service instances for the same account, open a [Service Ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Connecting to your on-premises network
{: #vpn-connecting-onpremise}

You can configure your VPN gateway to connect to your on-premises network.

Create a VPN gateway in your Power Virtual Server Service Instance and create a VPN connection between the Power Virtual Server Service Instance and the peer gateway of the on-premises network by specifying the following information:

- Connection name - Enter a name for the connection, such as onprem-connection.
- Peer gateway address - Specify the IP address of the VPN gateway for the on-premises network.
- Preshared key - Specify the authentication key of the VPN gateway for the on-premises network.
- Local subnets - Specify one or more subnets in the Power Virtual Server Service Instance you want to connect through the VPN tunnel.
- Peer subnets - Specify one or more subnets in the on-premises network you want to connect through the VPN tunnel.

For the Internet Key Exchange (IKE) and IPsec security parameters, select Auto so the cloud gateway uses auto-negotiation to automatically establish the connection with the on-premises gateway.

The gateway status appears as Pending while the VPN gateway is being created, and the status changes to Available after the gateway is created.
{: tip}

### Configuring the on-premises VPN gateway

The next step is to configure your on-premises VPN gateway peer to connect to your IBM Cloud VPN Gateway for Power Virtual Server Service Instance. The configuration depends on the type of VPN gateway. See the following topics for details.

- [Connecting to a Juniper vSRX peer](/docs/vpc?topic=vpc-juniper-vsrx-config)
- [Connecting to a strongSwan peer](/docs/vpc?topic=vpc-strongswan-config)

### Checking the status of the secure connection

You can test the connection by doing a ping from a virtual server instance to a server in the on-premises network.

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

For achieving redundancy between colocated VM and VPC, you must have two subnets that are attached to different VPNs. Both these subnets must be a part of the colocated VM.
{: note}

You must route Power Systems Virtual Server private network subnets over VPN connections to allow access to your Power Systems Virtual Server over private network.
When you create a subnet or edit details of a subnet, you can attach an existing VPN connection to the subnet.

For more information about attaching or detaching subnets by using CLI, see [VPN subnets](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connection-local-subnets).
