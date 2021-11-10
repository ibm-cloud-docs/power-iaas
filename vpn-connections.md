---

copyright:
  years: 2021

lastupdated: "2021-10-29"

keywords: VPN connections, IKE policies, IPsec policies

subcollection: power-iaas

---

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

You can connect an on-premises virtual private network (VPN) gateway to an IBM Cloud™ VPN gateway that is created within a Power Systems Virtual Server VPN service. You can use the VPN to connect to the Power Virtual Server private networks, complete your work securely, and log out. This capability offers you site-to-site IP security (IPsec) VPN between your on-premises location and Power Systems Virtual Servers to enable low-cost secure connectivity.

With VPN access, you can:

- Ensure private and low-cost connectivity to IBM Cloud services.
- Access your Virtual Servers through the private IP address by using Secure Shell (SSH) and your other on-premises applications that are running on your on-premises host.

The Power Systems Virtual Server infrastructure consists of subnets and virtual server instances (VSIs). You can use VPN as a service with your existing VSIs and private networks. To create a VSI on a private network, see [Creating a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet). You can use VPN to securely connect your Power Virtual Server Service Instance to an on-premises network through a VPN tunnel. For more information, see [Connecting to your on-premises network](/docs/vpc?topic=vpc-vpn-onprem-example&interface=ui).

A maximum of four VPN connections are supported for one user account. A maximum of four policies (IKE and IPsec) for a VPN connection is supported. Currently, VPN for Power Systems Virtual Servers is supported in DAL12, FRA04, LON04, LON06, SYD04, SYD05, and TOK04 data centers. When you use the Power Virtual Server network automation service for the first time, it might result in a temporary timeout failure. You must retry the operation as the same error might not occur again.
{: important}

To learn more about using the command-line interface (CLI) for VPN connections, see [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

## Power Systems Virtual Servers service instances support with VPN
{: #powervs-support-vpn}

Power Systems Virtual Server supports multiple service instances from the same account. However, only a single service instance can use a VPN connection. If you want to configure a setup with multiple service instances for the same account, open a [Service Ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

## Connecting to your on-premises network
{: #vpn-connecting-onpremise}

You can configure your VPN to connect to your on-premises network by following these steps in the Power Virtual Server CLI or API.

1. Create an IKE Policy, see [Creating IKE and IPsec policies](/docs/power-iaas-cli-plugin?topic=power-iaas-VPN-connections#creating-IKE-policies).
2. Create an IPsec Policy, see [Creating IKE and IPsec policies](/docs/power-iaas-cli-plugin?topic=power-iaas-VPN-connections#creating-IKE-policies).
3. Create a VPN connection, see [Creating VPN connections](/docs/power-iaas-cli-plugin?topic=power-iaas-VPN-connections#creating-VPN-connections).
4. Configure your on-premises IPsec Gateway enduring IKE Policy, IPsec Policy, and VPN Connection parameters that are compatible.

### Configuring the on-premises VPN gateway
{: #configure-onpremise-vpngateway}

The next step is to configure your on-premises VPN gateway peer to connect to your IBM Cloud VPN Gateway for Power Virtual Server Service Instance. The configuration depends on the type of VPN gateway. See the following topics for details.

- [Connecting to a Juniper vSRX peer](/docs/vpc?topic=vpc-juniper-vsrx-config)
- [Connecting to a strongSwan peer](/docs/vpc?topic=vpc-strongswan-config)
- Connecting to a IBM Cloud VPC VPN Gateway peer

Create a VPN gateway in your Power Virtual Server Service Instance and create a VPN connection between the Power Virtual Server Service Instance and the peer gateway of the on-premises network by specifying the following information:

- Connection name - Enter a name for the connection, such as onprem-connection.
- Peer gateway address - Specify the IP address of the VPN gateway for the on-premises network.
- Preshared key - Specify the authentication key of the VPN gateway for the on-premises network.
- Local subnets - Specify one or more subnets in the Power Virtual Server Service Instance you want to connect through the VPN tunnel.
- Peer subnets - Specify one or more subnets in the on-premises network you want to connect through the VPN tunnel.

For the Internet Key Exchange (IKE) and IPsec security parameters, select Auto so the cloud gateway uses auto-negotiation to automatically establish the connection with the on-premises gateway.

The gateway status appears as Pending while the VPN gateway is being created, and the status changes to Available after the gateway is created.
{: tip}

### Checking the status of the secure connection
{: #check-secure-connection}

You can test the connection by doing a ping from a virtual server instance to a server in the on-premises network.

## Creating VPN connections
{: #creating-VPN-connections}

You can create a new VPN connection by using the `ibmcloud pi vpn-connection-create` command. For creating, viewing, updating, or deleting a VPN connection by using CLI, see [VPN connections](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

You can view allowable and default values for attributes when you are creating Internet Key Exchange (IKE) and IPsec policies for a VPN connection. These values are listed under each command in the CLI.

IKE policy version 2 is not compatible with policy-based VPN connections. If you attempt to add an IKE policy version 2 to a policy-based VPN connection, an error is displayed.
{: important}

The display of an example VPN connection is as follows:

```ID                      1471c65163dd44daa969cf3edddd20a8
Name                    rs-vpc-vpn01
Status                  active
Mode                    route
Local Gateway Address   169.48.225.198
Peer Gateway Address    130.198.12.241
VPN Gateway Address     169.48.225.198
IKE Policy              ID: a757fb8d0a324e4abe0589bc17fbad7c, Name: rs-ike-1
IPSec Policy            ID: befd77bd25a04c388c43ccb3973966be, Name: rs-ipsec-1
Peer Subnets            10.245.0.0/27
Networks                cb36a4e8-23d1-4ddc-b6c0-cf640ae0456d
Dead Peer Detection     Action: restart, Interval: 10, Threshold: 5
```

## Creating IKE and IPsec policies
{: #creating-IKE-policies}

When you create a VPN connection, you must set the IKE and IPsec policies. IBM provides default IKE and IPsec policies. You can also create custom policies based on your requirements.

### Adding a VPN IKE policy to a VPN connection
{: #adding-IKE-policies}

You can use the default or custom IKE policies to define security parameters that will be used during Phase 1 of IKE negotiation. In this phase, credentials and security policies are exchanged between the VPN and peer device to authenticate with each other and to establish a secure communication channel that will be used for Phase 2 of IKE negotiation.

You can add an IKE policy by using the `ibmcloud pi vpn-ike-policy-add` command. For more information about adding, viewing, updating, or deleting an IKE policy by using CLI, see [VPN IKE policy](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-ike-policy).

The display of an example IKE Policy is as follows. Pre-shared key is not displayed for an IKE policy.

```Ibmcloud pi vpn-ike-policy a757fb8d0a324e4abe0589bc17fbad7c
ID               a757fb8d0a324e4abe0589bc17fbad7c
Name             rs-ike-1
Version          2
Authentication   sha-256
Encryption       aes-256-cbc
Dh Group         2
Key Lifetime     28800
```

### Adding and configuring IPsec policy to a VPN connection
{: #adding-IPsec-policies}

You can use the default or custom IPsec policies to define security parameters that will be used during Phase 2 of IKE negotiation. In this phase, the VPN and peer device use the security association that is established during Phase 1 of IKE negotiation to negotiate what traffic to send and how to authenticate and encrypt that traffic.

You can add an IPsec policy by using the `ibmcloud pi vpn-ipsec-policy-add` command. For more information on adding, viewing, updating, or deleting an IPsec policy by using CLI, see [VPN IPsec policy](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-ike-policy).

The display of an example IPsec Policy is as follows:

```Ibmcloud pi vpn-ips-policy befd77bd25a04c388c43ccb3973966be
ID                        befd77bd25a04c388c43ccb3973966be
Name                      rs-ipsec-1
Authentication            hmac-sha-256-128
Encryption                aes-256-cbc
Dh Group                  2
Perfect Forward Secrecy   true
Key Lifetime              28800
```

## Attaching subnets to VPN connections
{: #attach_subnets_VPN}

If you create a Power Systems Virtual Servers service that contains VPN connections, you must also have Local subnets and Peer subnets that are connected to the VPN connection.

For achieving redundancy between colocated VM and VPC, you must have two subnets that are attached to different VPNs. Both these subnets must be a part of the colocated VM.
{: note}

You must route Power Systems Virtual Server private network subnets over VPN connections to allow access to your Power Systems Virtual Server over private network.
When you create a subnet or edit details of a subnet, you can attach an existing VPN connection to the subnet.

For more information about attaching or detaching subnets by using CLI, see [VPN subnets](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connection-local-subnets).

