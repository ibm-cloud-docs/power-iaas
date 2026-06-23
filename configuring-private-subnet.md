---

copyright:
  years: 2019, 2026 

lastupdated: "2026-06-23"

keywords: ssh key, AIX virtual machine, configure ssh key, new virtual server, public ssh key, connecting private subnets, gateway, CIDR, reserve IP, DNS

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring a private network subnet
{: #configuring-subnet}
{: help}
{: support}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}



---

You can configure a private network subnet when you create an {{site.data.keyword.powerSysFull}} by providing your subnet a name and specifying a Classless Inter-Domain Routing (CIDR).
{: shortdesc}

In a {{site.data.keyword.off-prem}}, the private network subnet configuration depends on the networking configuration of the {{site.data.keyword.powerSys_notm}} workspace. The networking configuration of the workspace can use one of the following approaches:

* {{site.data.keyword.powerSys_notm}} workspace that is enabled with the [Power Edge Router (PER)](/docs/power-iaas?topic=power-iaas-per). This configuration is the default for most locations if the workspace is created after mid-2023 and the workspace can use VPN Connections.
* {{site.data.keyword.powerSys_notm}} workspace that is enabled with [Power Cloud Connections](/docs/power-iaas?topic=power-iaas-cloud-connections). In this configuration, PER is the default connection, and the workspace can use VPN Connections.

For more information about VPN connections, see [VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections).




When you specify a CIDR, the following values are automatically populated:
- A gateway
- An IP range
- DNS server

You must use a CIDR notation when you choose the IP ranges for your private network subnet. CIDR notation is defined in [RFC 1518](https://tools.ietf.org/html/rfc1518){: external} and [RFC 1519](https://tools.ietf.org/html/rfc1519){: external}.
A CIDR has the following format:
```shell
<IPv4 address>/<number>
```
{: screen}

For example, `192.168.100.14/24` represents the IPv4 address, `192.168.100.14`, and its associated routing prefix `192.168.100.0`, or equivalently, its subnet mask `255.255.255.0` (which has 24 leading 1 bit).

## Configure a private network subnet by using UI

To create a new subnet, complete the following steps:

You cannot assign the subnet that is already assigned to another virtual machine. However, when you edit the configuration of a virtual machine, you can assign the same subnet multiple times.
{: note}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type {{site.data.keyword.powerSys_notm}} and click the {{site.data.keyword.powerSys_notm}} tile.

3. In the navigation panel, click **Workspaces**. The workspaces page with a list of existing workspaces is displayed.

4. Click your workspace from the list to open the virtual server instance page.

5. Click **Subnets** in the left navigation panel, then click **Create subnet**. The new subnet panel is displayed.

6. Enter a name, CIDR value (for example, '192.168.100.14/24'), gateway number (for example, '192.168.100.15'), and the IP range values for the subnet.

7. Enter the **DNS server** value.

    A **DNS server** value of `9.9.9.9` might not be reachable if you don't have a public IP. This issue can cause the LPAR to hang during the startup operation. You can use the default DNS server value of `127.0.0.1` to avoid this issue. You can add up to 20 DNS server IP addresses separated by commas.

8. Set **Advertise** to one of the following options:
    - **Enabled**: The static route is advertised to external connections. **Advertise** is set to **Enabled** by default.
    - **Disabled**: The static route is not advertised to external connections.

9. Set **Subnet ARP Broadcast** to one of the following options:
    - **Enabled**: Distributes the Address Resolution Protocol (ARP) traffic in the {{site.data.keyword.powerSys_notm}} network fabric.

    - **Disabled**: Does not distribute the ARP traffic in the {{site.data.keyword.powerSys_notm}} network fabric. **Subnet ARP Broadcast** is set to **Disabled** by default.

    For more information about subnet ARP broadcast, see [Configuring the ARP broadcast in Power Virtual Server subnets](/docs/power-iaas?topic=power-iaas-subnet-arp-oracle-rac).

10. Set **DHCP** to to one of the following options:
    - **Enabled**: Network interfaces that are configured to use Dynamic Host Configuration Protocol (DHCP) receive their IPv4 configurations automatically. **DHCP** is set to **Enabled** by default.

    - **Disabled**: Network interfaces that are configured to use DHCP do not receive their IPv4 configurations automatically.

    The DHCP service is available only in IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.on-prem}}. For more information about DHCP, see [DHCP network inside the pod](/docs/power-iaas?topic=power-iaas-network_use_cases#dhcp-network-new).

11.  You can also attach a primary and redundant cloud connection to the subnet to set up high availability in an {{site.data.keyword.off-prem}}. For more information about high availability, see [Setting up high availability over cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#ha-availability-cloud-connections).

10. Click **Create subnet**.


## Updating an existing subnet
{: #update-subnet}

Complete the following steps to update an existing subnet:

1.  Click **Subnets** in the left navigation panel.

2. Click the subnet that you want to update from the displayed list.

3. Click **Edit details** to update the subnet.

You can attach or detach cloud connections to each of the subnets in the **Attached cloud connections** section in {{site.data.keyword.off-prem}}.

## Configure a private network subnet by using CLI

You can also create and configure a private network subnet by using the IBM command-line interface (CLI). Use the following command to create a private network subnet:

```shell
ibmcloud pi network-create-private NETWORK_NAME --cidr-block CIDR --ip-range "startIP-endIP[,startIP-endIP]" [--dns-servers "DNS1 DNS2"] [--gateway GATEWAY] [--json]
```
{: codeblock}

## Reserving IP addresses
{: #reserv-ip}

Use the reserved IP addresses to block {{site.data.keyword.powerSys_notm}} from assigning a specific IP address to a virtual server instance.

You can complete the following tasks:
- Add IP address
- See the list of reserved IP addresses
- Delete the reserved IP address

An IP address that is present in the reserved list is not auto assigned to a virtual server instance.

### Adding an IP address in the reserved list
{: #add-resrv-ip}

To add an IP address into the reserved IP address list, complete the following steps:
* Open the [Subnets](https://cloud.ibm.com/power/subnets){: external} page in the IBM Cloud.
* From the list of subnets that are created, click the subnet for which you want to reserve the IP address.
* Click **Reserve IP**.
* Enter your IP address in the **IP address** field.

   Make sure the IP address that you want to reserve falls in the IP range that is defined when the subnet is created.
   {: note}

* Provide a description of your reserved IP in the **Reserved IP description (optional)** field.

## Networking considerations for {{site.data.keyword.off-prem}}
{: #networking-considerations}

You can establish a private network communication between the two {{site.data.keyword.powerSys_notm}} instances with any one of the following approaches:
1.	Use a PER-enabled workspace. See, [Getting started with PER](/docs/power-iaas?topic=power-iaas-per).
2.	Create and attach the subnet to a cloud connection and Transit Gateway.



















## Using CIDR notation
{: #cidr-notation}



You can use CIDR notations if public subnets are enabled and are in use. You can specify CIDR notation for a public subnet with either an [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918){: external} IP address space (`10.0.0.0/8`, `172.16.0.0/12`, or `192.168.0.0/16`) or an IP address space registered with the Internet Assigned Numbers Authority (IANA). You must plan carefully when you use a non-RFC 1918 IP address space. If a subnet contains non-RFC 1918 IP addresses, a virtual server instance (VSI) in that subnet might not reach certain IP addresses when public networks are also attached to the VSI.

The {{site.data.keyword.powerSys_notm}} assigns internal IP addresses from the `192.168.0.0/16` CIDR block to your account to enable connectivity to public networks. The IP addresses from the `192.168.0.0/16` block that are assigned to your account for public network use cannot be used for private networks.










The number after the slash represents the bit length of the subnet mask. As a result, the smaller the number after the slash, the more IP addresses you are allocating. The following table lists the number of available addresses in a subnet (based on its specified CIDR block size):

| CIDR block size | Available IP addresses (WDC04, WDC06) | Available IP addresses (non-WDC) |
| --------------- | ------------------------------------- | -------------------------------- |
| /22             | 1019                                  | 1021                             |
| /23             | 507                                   | 509                              |
| /25             | 123                                   | 125                              |
| /26             | 59                                    | 61                               |
| /27             | 27                                    | 29                               |
| /28             | 11                                    | 13                               |
{: caption="Understanding CIDR notation caption" caption-side="bottom"}
