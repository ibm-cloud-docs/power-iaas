---

copyright:
  years: 2021, 2024

lastupdated: "2024-06-08"

keywords: VPN connections, IKE policies, IPsec policies, vpnaas, VPC VPN, VPN as a service

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.powerSys_notm}} VPN
{: #VPN-connections-deprecated}

The {{site.data.keyword.powerSys_notm}} VPN is deprecated and IBM won't provide standard support after 18 January 2025. Create your new VPN connection by using the [IBM Cloud VPC VPN](/docs/power-iaas?topic=power-iaas-VPN-connections#vpc-vpn). For existing {{site.data.keyword.powerSys_notm}} VPN connections, upgrading to VPC VPN is encouraged before March 2024 with the end of service on 14 July 2025. If you need any assistance on upgrading or migration, open a [support ticket](https://www.ibm.com/cloud/support){: external} or engage with your Customer Support Manager (CSM).
{: deprecated}

## Creating a {{site.data.keyword.powerSys_notm}} VPN
{: #pvs-vpn}

You can connect a virtual private network (VPN) gateway in your client-managed environment<!--Q2 client-managed to be confirmed by Joe--> to an IBM Cloud™ VPN gateway that is created within a {{site.data.keyword.powerSys_notm}} VPN service. You can use the VPN to connect to the Power Virtual Server private network, complete your work securely, and log out. This capability offers you site-to-site IP security (IPsec) VPN between your client-managed<!--Q2 client-managed to be confirmed by Joe--> location and {{site.data.keyword.powerSys_notm}}s to enable low-cost secure connectivity.

With VPN access, you can:

- Ensure private and low-cost connectivity to IBM Cloud services.
- Access your Virtual Servers through the private IP address by using Secure Shell (SSH) and your other client-managed<!--Q2 client-managed to be confirmed by Joe--> applications that are running on your client-managed<!--Q2 client-managed to be confirmed by Joe--> host.

The {{site.data.keyword.powerSys_notm}} infrastructure consists of subnets and virtual server instances (VSIs). You can use VPN as a service with your existing VSIs and private networks. To create a VSI on a private network, see [Creating a {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet). You can use VPN to securely connect your Power Virtual Server workspace to a network in the client-managed environment<!--Q2 client-managed to be confirmed by Joe--> through a VPN tunnel. For more information, see [Connecting to your client-managed environment network](/docs/vpc?topic=vpc-vpn-onprem-example&interface=ui).

A maximum of four VPN connections are supported for one user account. A maximum of four policies (IKE and IPsec) for a VPN connection are supported on each data center. Currently, VPN for {{site.data.keyword.powerSys_notm}}s is supported in DAL12, DAL13, FRA04, FRA05, LON04, LON06, MON01, OSA21, SAO01, SYD04, SYD05, TOR01, and TOK04 data centers. When you use the Power Virtual Server network automation service for the first time, it might result in a temporary timeout failure. You must retry the operation as the same error might not occur again.
{: important}

Due to your bandwidth variation when connecting via a shared VPN gateway, performance varies. For workloads that require the transfer of large data volumes, you should consider by using a site-to-site VPN configuration with your own dedicated gateway devices. For more information, see [Configuring the client-managed environment VPN gateway](/docs/power-iaas?topic=power-iaas-VPN-connections#configure-onpremise-vpngateway).
{: important}

To learn more about using the command-line interface (CLI) for VPN connections, see [IBM {{site.data.keyword.powerSys_notm}}s CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

### {{site.data.keyword.powerSys_notm}} workspace support with VPN
{: #powervs-support-vpn}

{{site.data.keyword.powerSys_notm}} supports multiple workspaces from the same account. However, only a single workspace can use a VPN connection. If you want to configure a VPN connection for multiple workspaces for the same account, open a [Service Ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

### Connecting to a network in the client-managed environment<!--Q2 client-managed to be confirmed by Joe-->
{: #vpn-connecting-onpremise}

You can configure your VPN to connect to your network in the client-managed environment<!--Q2 client-managed to be confirmed by Joe--> by following these steps in the {{site.data.keyword.powerSys_notm}} CLI or API.

1. [Create an IKE policy](/docs/power-iaas?topic=power-iaas-VPN-connections#creating-IKE-policies).
2. [Create an IPsec policy](/docs/power-iaas?topic=power-iaas-VPN-connections#creating-IKE-policies).
3. [Create a VPN connection](/docs/power-iaas?topic=power-iaas-VPN-connections#creating-VPN-connections).
4. Configure your IPsec gateway enduring IKE policy, IPsec policy, and VPN connection parameters in your client-managed environment<!--Q2 client-managed to be confirmed by Joe--> that are compatible.

#### Configuring the VPN gateway in the client-managed environment<!--Q2 client-managed to be confirmed by Joe-->
{: #configure-onpremise-vpngateway}

The next step is to configure your VPN gateway peer to connect in the client-managed environment<!--Q2 client-managed to be confirmed by Joe--> to your IBM Cloud VPN Gateway for Power Virtual Server workspace. The configuration depends on the type of VPN gateway. See the following topics for details.

Any configurations that are not listed in this section are not supported by {{site.data.keyword.powerSys_notm}}. If you need a different configuration or predictable performance, you must opt for the configuration that is described in [Site-to-site VPN connectivity](/docs/power-iaas?topic=power-iaas-vpn-connectivity) with redundant VPN connections.

- [Connecting to a Juniper vSRX peer](/docs/vpc?topic=vpc-juniper-vsrx-config)
- [Connecting to a strongSwan peer](/docs/vpc?topic=vpc-strongswan-config)
- [Connecting to a IBM Cloud VPC VPN Gateway peer](/docs/vpc?topic=vpc-vpn-overview)

#### Checking the status of the secure connection
{: #check-secure-connection}

You can test the connection by doing a ping from a virtual server instance to a server in the network in your client-managed environment<!--Q2 client-managed to be confirmed by Joe-->.

### Creating IKE and IPsec policies
{: #creating-IKE-policies}

Before you create a VPN connection, you must set the IKE and IPsec policies. IBM provides default IKE and IPsec policies. You can also create custom policies based on your requirements.

#### Adding a VPN IKE policy to a VPN connection
{: #adding-IKE-policies}

You can use the default or custom IKE policies to define security parameters that will be used during Phase 1 of IKE negotiation. In this phase, credentials and security policies are exchanged between the VPN and peer device to authenticate with each other and to establish a secure communication channel that will be used for Phase 2 of IKE negotiation.

To create an IKE policy, complete the following steps:

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **VPN connections**.
2. In the **VPN connections** page, click **IKE policies** to open the **IKE policies** tab.
3. Click **Create policy**.
4. In the **New IKE policy** page, enter the following details:
     - **Name**: Specify a name for the IKE policy, such as 'powervs-vpn-ike1'. The maximum number of characters for the name is 47 characters.
     - **IKE version**: Select the IKE version. Valid values are 1, 2. IKE policy version 2 is not compatible with policy-based VPN connections.
     - **Authentication**: Select the authentication algorithm of the IKE Policy. Valid values are 'none', 'sha1', 'sha-256', 'sha-384'.
     - **Encryption**: Select the encryption algorithm of the IKE policy. Valid values are '3des-cbc', 'aes-128-cbc', 'aes-128-gcm', 'aes-192-cbc', 'aes-256-cbc', 'aes-256-gcm', and 'des-cbc'. When you use 'aes-128-gcm' or 'aes-256-gcm', the **Authentication** option must be set to 'none'.
     - **Diffie-Hellman (DH) group**: Select the DH group number of the IKE policy. Valid values are 1, 2, 5, 14, 19, 20, 24.
     - **Key lifetime**: Specify the key lifetime of the IKE policy in seconds. The valid value is in the range 180 - 86400 seconds.
     - **Preshared key**: Specify the authentication key of the VPN gateway for the network in the client-managed environment<!--Q2 client-managed to be confirmed by Joe-->.

5. Click **Create**.

To create, view, update, or delete an IKE policy by using CLI, see CLI reference for [VPN IKE policy](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-ike-policy).

The display of an example IKE Policy is as follows. Pre-shared key is not displayed for an IKE policy.

```text
Ibmcloud pi vpn-ike-policy a757fb8d0a324e4abe0589bc17fbad7c
ID               a757fb8d0a324e4abe0589bc17fbad7c
Name             rs-ike-1
Version          2
Authentication   sha-256
Encryption       aes-256-cbc
Dh Group         2
Key Lifetime     28800
```
{: screen}

#### Adding and configuring IPsec policy to a VPN connection
{: #adding-IPsec-policies}

You can use the default or custom IPsec policies to define the security parameters that will be used during Phase 2 of IKE negotiation. In this phase, the VPN and peer devices use the security association that is established during Phase 1 of IKE negotiation to negotiate what traffic to send and how to authenticate and encrypt that traffic.

To create an IPsec policy, complete the following steps:

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **VPN connections**.
2. In the **VPN connections** page, click **IPsec policies** to open the **IPsec policies** tab.
3. Click **Create policy**.
4. In the **New IPsec policy** page, enter the following details:
     - **Name**: Specify a name for the IPsec policy, such as 'powervs-vpn-ipsec1'. The maximum number of characters in the name is 47.
     - **PFS**: Enable Perfect Forward Secrecy that changes the keys that are used to encrypt and decrypt information frequently and automatically.
     - **Authentication**: Select the authentication encryption type of the IPsec policy. Valid values are 'none', 'hmac-md5-96', 'hmac-sha-256-128', 'hmac-sha1-96'.
     - **Encryption**: Select the connection encryption policy of the IPsec Policy. Valid values are '3des-cbc', 'aes-128-cbc', 'aes-128-gcm', 'aes-192-cbc', 'aes-192-gcm', 'aes-256-cbc', 'aes-256-gcm', 'des-cbc'. When you use the 'aes-128-gcm', 'aes-192-gcm', or 'aes-256-gcm' value, the **Authentication** option must be set to 'none'.
     - **Diffie-Hellman (DH) group**: Select the DH group number of the IPsec policy. Valid values are 1, 2, 5, 14, 19, 20, 24.
     - **Key lifetime**: Specify the key lifetime of the IPsec policy in seconds. The valid value is in the range 180 - 86400 seconds.
5. Click **Create**.

To create, view, update, or delete an IPsec policy by using CLI, see the CLI reference for [VPN IPsec policy](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-ike-policy).

The display of an example IPsec policy is as follows:

```text
Ibmcloud pi vpn-ips-policy befd77bd25a04c388c43ccb3973966be
ID                        befd77bd25a04c388c43ccb3973966be
Name                      rs-ipsec-1
Authentication            hmac-sha-256-128
Encryption                aes-256-cbc
Dh Group                  2
Perfect Forward Secrecy   true
Key Lifetime              28800
```
{: screen}

### Creating the {{site.data.keyword.powerSys_notm}} VPN connection
{: #creating-VPN-connections}

**Prerequisite**: You must create at least one local subnet in the {{site.data.keyword.powerSys_notm}} interface and a peer subnet in your client-managed<!--Q2 client-managed to be confirmed by Joe--> environment. You can connect your client-managed<!--Q2 client-managed to be confirmed by Joe--> environment and the {{site.data.keyword.powerSys_notm}} network through the VPN tunnel. For instructions about creating a subnet, see [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet).

To create a VPN connection, complete the following steps:
1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **VPN connections**.
2. In the **VPN connections** page, click **Create connection**.
3. In the **Create a new VPN connection** page, enter the following details:
    - **Connection name**: Enter a name for the connection, such as 'powervs-vpn-dallas'.
    - **Peer gateway address**: Specify the IP address of the VPN gateway for the network in your client-managed environment<!--Q2 client-managed to be confirmed by Joe-->.
    - **Preshared key**: Specify the authentication key of the VPN gateway for the network in your client-managed environment<!--Q2 client-managed to be confirmed by Joe-->.
    - **IKE policy**: Use the default IKE policy or specify a custom IKE policy to define security parameters that will be used during Phase 1 of IKE negotiation.
    - **IPsec policy**: Use the default IPsec policy or specify a custom IPsec policy to define the security parameters that will be used during Phase 2 of IKE negotiation.
    - **Mode**: Select either **Route-based mode** or **Policy-based mode** to determine how the traffic is sent through the VPN tunnel. You cannot edit the mode of the VPN connection after you create the VPN connection.
    - **Local subnets**: Specify one or more subnets in the Power Virtual Server workspace that you want to connect through the VPN tunnel.
    - **Peer subnets**: Specify one or more subnets in the network in your client-managed environment<!--Q2 client-managed to be confirmed by Joe--> that you want to connect through the VPN tunnel.
    - **Dead peer detection**: Shows the dead peer detection settings for the VPN connection. You can use the settings information to detect a dead IKE peer. These settings are displayed for informational purposes only; you cannot modify these settings.
4. Review the estimated cost and click **Create**.

You can edit the VPN connection options after creating a VPN connection. Click the existing VPN connection that you want to edit, click **Edit details**, and modify the options.

To create, view, update, or delete a VPN connection by using CLI, see the CLI reference for [VPN connections](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

When you delete a virtual server instance, it deletes the private networks (subnets) and other resources. It would help if you considered the following:
-  You must delete VPN connections before deleting the virtual server instance.
-  When there are more than one virtual server instances that use the Cloud Connection, and you delete one, you can delete the Cloud Connection from the existing server instances.
{: note}

IKE policy version 2 is not compatible with policy-based VPN connections. If you attempt to add an IKE policy version 2 to a policy-based VPN connection, an error is displayed.
{: important}

The display of an example VPN connection is as follows:

```text
ID                      1471c65163dd44daa969cf3edddd20a8
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
{: screen}

### Attaching subnets to VPN connections
{: #attach_subnets_VPN}

If you create a {{site.data.keyword.powerSys_notm}}s workspace that contains VPN connections, you must also have Local subnets and Peer subnets that are connected to the VPN connection. When you create a VPN connection, ensure that a local subnet and a peer subnet are attached to the VPN connection.

For achieving redundancy between colocated VM and VPC, you must have two subnets that are attached to different VPNs. Both these subnets must be a part of the colocated VM.
{: note}

You must route {{site.data.keyword.powerSys_notm}} private network subnets over VPN connections to allow access to your {{site.data.keyword.powerSys_notm}} over private network.
When you create a subnet or edit details of a subnet, you can attach an existing VPN connection to the subnet.

To create, attach, or detach a local subnet or a peer subnet to a VPN connection, complete the following steps:
1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **VPN connections**.
2. In the **VPN connections** page, click an existing VPN connection that you want to edit.
3. In the **VPN connection details** page, click **Attach another +** option to attach other local and peer subnets. Click **Detach** to detach the existing local and peer subnets from the VPN connection.

For more information about attaching or detaching subnets by using CLI, see the CLI reference for [VPN subnets](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connection-local-subnets).

In addition to the subnet restrictions specified in [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet), VPNaaS has the following restrictions:

a. Subnets with `10.xx.xx.xx/8` address are not supported.

b. These additional subnets are restricted:
     `10.8.0.0/14`
     `10.45.0.0/16`
     `10.63.0.0/16`
     `10.65.0.0/16`
     `10.72.0.0/16`
     `10.74.0.0/15`
     `10.95.96.0/20`
     `10.114.0.0/15`
     `10.123.0.0/16`
     `10.128.0.0/13`
     `10.136.0.0/13`
     `10.150.0.0/15`
     `10.184.0.0/13`
     `10.192.0.0/13`
     `10.208.0.0/12`
     `10.240.0.0/14`
     `10.21.1.0/26`
     `10.182.28.192/26`

c. You might get a "subnet not available" message while creating subnets in certain locations. Choose a different subnet to resolve this issue.
