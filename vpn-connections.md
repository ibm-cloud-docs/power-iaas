---

copyright:
  years: 2021

lastupdated: "2021-08-05"

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
{: VPN-connections}

Virtual Private Networking (VPN) access enables you to manage your Power Systems Virtual Servers remotely and securely over the IBM Cloud® private network. You can use VPN to log in to the private network, complete your work, and log out.

With VPN access, you can:
•Establish a VPN connection to the private network via SSL, or IPsec.
•Access your Virtual Servers through its primary private IP address by SSH or RDP.
•Connect to your Virtual Server’s IPMI IP address for low-level server management or rescue needs.

Each of your account can be given VPN access and can be limited regarding the subnets to which it needs access. You must have VPN access enabled and a VPN password specified before attempting to log in to VPN services.

A maximum of four VPN coonections are supported for one account. Maximum number of policies (IKE and IPSEC) is limited to four.
{: important}

To learn more about using the command-line interface to for VPN connections, see [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#vpn-connections).

## Creating VPN connections

- To create a new VPN connection, use the following command.

    ```
    ibmcloud pi vpn-connection-create VPN_CONNECTION_NAME --mode Policy|Route --peer-gateway-address PEER_GATEWAY  --peer-subnet-cidrs "CIDR1 [CIDRn]" --connection-state=True|False --ike-policy-id IKE_POLICY_ID --ipsec-policy-id IPSEC_POLICY_ID --local-subnet-ids "ID1 [IDn]" [--json]
    ```
    {: codeblock}

- To view details of a VPN connection, use the following command.

    ```
    ibmcloud pi vpn-connection VPN_CONNECTION_ID [--json]
    ```
    {: codeblock}

- To update a VPN connection, use the following command.

    ```
    ibmcloud pi vpn-connection-update VPN_CONNECTION_ID [--name VPN_CONNECTION_NAME] [--peer-gateway-address PEER_GATEWAY] [--connection-state=True|False] [--ike-policy-id IKE_POLICY_ID] [--ipsec-policy-id IPSEC_POLICY_ID] [--json]
    ```
    {: codeblock}

- To delete a VPN connection, use the following command.

    ```
    ibmcloud pi vpn-connection-delete VPN_CONNECTION_ID
    ```
    {: codeblock}

- To view allowable and default values for attributes when creating IKE and IPSec policies for a VPN connection, use the following command.

    ```
    ibmcloud pi vpn-connection-options [--json]
    ```
    {: codeblock}

## Creating IKE and IPsec Policies

When you create your VPN connection, you must select IKE policy and IPsec policy. IBM will provide default IKE policy and IPSEC policy. You can also create your policies based on your requirements.

### Adding a VPN IKE policies

- To add an IKE policy, use the following command:

    ```
    ibmcloud pi vpn-ike-policy-add IKE_POLICY_NAME --version VERSION --authentication AUTHENTICATION --encryption ENCRYPTION --dhgroup DH_GROUP --presharedkey KEY [--json]
    ```

- To View an IKE policy, use the following command:

    ```
    ibmcloud pi vpn-ike-policy IKE_POLICY_ID [--json]
    ```

- To list all IKE policies associated to the VPN connection, use the following command:

    ```
    ibmcloud pi vpn-ike-policies [--json]
    ```

- To update an IKE policy, use the following command:

    ```
    ibmcloud pi vpn-ike-policy-update IKE_POLICY_ID  [--name NEW_NAME] [--version VERSION] [--authentication AUTHENTICATION] [--encryption ENCRYPTION] [--dhgroup DH_GROUP] [--presharedkey KEY] [--json]
    ```

- To delete an IKE policy, use the following command:

    ```
    ibmcloud pi vpn-ike-policy-delete IKE_POLICY_ID
    ```

### Adding and configuring IPSec policy

- To add an IPSec policy, use the following command:

    ```
    ibmcloud pi vpn-ipsec-policy-add IPSEC_POLICY_NAME --authentication AUTHENTICATION --encryption ENCRYPTION --dhgroup DH_GROUP --pfs [--json]
    ```

- To view an IPSec policy, use the following command:

    ```
    ibmcloud pi vpn-ipsec-policy IPSEC_POLICY_ID [--json]
    ```

- To list all IPSec policies, use the following command:

    ```
    ibmcloud pi vpn-ipsec-policies [--json]
    ```

- To update an IPSec policies, use the following command:

    ```
    ibmcloud pi vpn-ipsec-policy-update IPSEC_POLICY_ID  [--name NEW_NAME] [--authentication AUTHENTICATION] [--encryption ENCRYPTION] [--dhgroup DH_GROUP] [--presharedkey KEY] [--pfs=True|False] [--json]
    ```

- To delete an IPSec policies, use the following command:

    ```
    ibmcloud pi vpn-ipsec-policy-delete IPSEC_POLICY_ID
    ```

## Attaching subnets to VPN connections

If you created a Power Systems Virtual Servers service that contains VPN connections, you also have Local subnets and Peer subnets that are connected to the VPN connection.

- To attach a local subnet a sepcific VPN connection, use the following command:

    ```
    ibmcloud pi vpn-connection-local-subnet-attach VPN_CONNECTION_ID --local-subnet-id ID [--json]
    ```

- To detach a local subnet from a VPN connection, use the following command:

    ```
    ibmcloud pi vpn-connection-local-subnet-detach VPN_CONNECTION_ID --local-subnet-id ID
    ```

You must route Power Systems Virtual Server private network subnets over VPN connections to allow access to your Power Systems Virtual Server over private network.
When you create subnet or edit details of subnet, you can attach an existing VPN connection to the subnet.

- To attach a peer subnet to a specific VPN connection, use the following command:

    ```
    ibmcloud pi vpn-connection-peer-subnet-attach VPN_CONNECTION_ID --peer-subnet-cidr CIDR [--json]
    ```

- To detach a peer subnet from a VPN connections, use the following command:

    ```

    ibmcloud pi vpn-connection-peer-subnet-detach VPN_CONNECTION_ID --peer-subnet-cidr CIDR
    ```

- To view the list of peer subnets attached to a specific VPN connection, use the following command:

    ```
    ibmcloud pi vpn-connection-peer-subnets VPN_CONNECTION_ID [--json]
    ```