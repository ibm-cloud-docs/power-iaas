---

copyright:
  years: 2019, 2024

lastupdated: "2024-04-05"

keywords: ssh key, AIX virtual machine, configure ssh key, new virtual server, public ssh key, connecting private subnets, gateway, CIDR, reserve IP, DNS

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Configuring a private network subnet
{: #configuring-subnet}
{: help}
{: support}

You can configure a private network subnet when you create a {{site.data.keyword.powerSysFull}}, providing your subnet a name and specifying a Classless Inter-Domain Routing (CIDR).
{: shortdesc}

How the private network subnet is configured, depends on the {{site.data.keyword.powerSys_notm}} Workspace networking configuration, which can use one of the following four approaches:
1. {{site.data.keyword.powerSys_notm}} Workspace enabled with the [Power Edge Router (PER)](/docs/power-iaas?topic=power-iaas-per). This is default for most locations if created after mid-2023, and can use [VPN Connections](/docs/power-iaas?topic=power-iaas-VPN-connections).
2. {{site.data.keyword.powerSys_notm}} Workspace enabled with [Power Cloud Connections](/docs/power-iaas?topic=power-iaas-cloud-connections). Former default, and can use [VPN Connections](/docs/power-iaas?topic=power-iaas-VPN-connections).
3. [{{site.data.keyword.dl_short}} Connect for {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect).
4. [{{site.data.keyword.powerSys_notm}} VPN service (Power VPNaaS) to {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-VPN-connections-deprecated).

When you specify a CIDR, the following are automatically populated:
- A gateway
- An IP range 
- DNS server.

You must use CIDR notation when you choose the IP ranges for your private network subnet. CIDR notation is defined in [RFC 1518](https://tools.ietf.org/html/rfc1518){: external} and [RFC 1519](https://tools.ietf.org/html/rfc1519){: external}.

Here is the format of a CIDR:
```shell
<IPv4 address>/<number>
```
{: screen}

For example, consider a CIDR - `192.168.100.14/24` that explains the following:
- IPv4 address - `192.168.100.14`
- Associated routing prefix - `192.168.100.0` 
- Subnet mask - `255.255.255.0` that has 24 leading 1 bits.

To create a new subnet, complete the following steps:

1. Sign in to the [IBM Cloud Portal](https://cloud.ibm.com){: external}.

2. Select the menu icon and select **Resource List**.

3. Click the arrow next to **Services**.

4. Select the {{site.data.keyword.powerSys_notm}} workspace you would like to assign a subnet.

5. Click **Subnets** in the left navigation pane, then **Add subnet**.

6. Enter a name for the subnet, CIDR value (for example: 192.168.100.14/24), gateway number (for example: 192.168.100.15), and the IP range values for the subnet.

7. You must provide the **DNS server** value.
    A **DNS server** value of `9.9.9.9` might not be reachable if you do not have a public IP. This can cause the LPAR to hang during startup. Go with the default DNS server value of `127.0.0.1` to avoid this issue. You can add up to 20 DNS servers. The DNS IP addresses must be separated by commas.

8. You can also attach a primary and redundant cloud connection to the subnet to set up high availability. For more information on high availability, see [Setting up high availability over cloud connections](/docs/power-iaas?topic=power-iaas-cloud-connections#ha-availability-cloud-connections).

9. Click **Create subnet**.

You can also edit an existing subnet by clicking the subnet in the table. You can attach or detach cloud connections to each of the subnets in the **Attached cloud connections** section.

You can also create and configure a private network subnet by using the IBM CLI. Use the following command to create a private network subnet:

```shell
ibmcloud pi network-create-private NETWORK_NAME --cidr-block CIDR --ip-range "startIP-endIP[,startIP-endIP]" [--dns-servers "DNS1 DNS2"] [--gateway GATEWAY] [--json]
```
{: codeblock}

## Reserving IP addresses
{: #reserv-ip}

Use the reserved IPs to block {{site.data.keyword.powerSys_notm}} from assigning a specific IP address to a virtual server instance.

You get the option to:
- Add an IP address
- See the list of the reserved IP address
- Delete the reserved IP address.

An IP address present in the reserved list, is not auto assigned to a virtual server instance.

You must delete the reserved IP address manually to remove the IP reservation. Deleting the virtual machine instance does not delete the reserved IP address that is associated with it.
{: note}

### Adding an IP address in the reserved list
{: #add-resrv-ip}

To add an IP address to the reserved IP address list, perform the following steps:
1. Open the [Subnets](https://cloud.ibm.com/power/subnets){: external} page in the IBM Cloud.
2. From the list of subnets that you have created, click the subnet for which you want to reserve the IP address.
3. Click **Reserve IP**.
4. Enter your IP address in the **IP address** field.

   Make sure the IP address that you want to reserve falls in the IP range that you have defined while provisioning the subnet.
   {: note}

5. Provide a description of your reserved IP in the **Reserved IP description (optional)** field.

## Networking considerations
{: #networking-considerations}

You can establish a private network communication between two {{site.data.keyword.powerSys_notm}} instances by using any one of the following four approaches:
1.	Use a PER enabled workspace. See, [Getting started with PER](/docs/power-iaas?topic=power-iaas-per).
2.	Create and attach the subnet to a cloud connection and transit gateway.
3.	Setup routing over Direct Links. See, [Ordering Direct Link 2.0 Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#order-direct-link-connect-2.0)
4.	Configure VPNaaS and set up routing with VPNaaS. See, [Managing VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections).

In case you are not using any of the four approaches, open a [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support) if you need to establish a private network communication between the two {{site.data.keyword.powerSys_notm}} instances.


For example, if you add a subnet `172.10.10.0/24` from user interface, and if this use case requires communication between the virtual server instances that are attached to the subnet without the use of the other approaches listed previously, you must open a support ticket and provide the following subnet information that is displayed in the {{site.data.keyword.powerSys_notm}} user interface.

| Name          |  Gateway     | VLAN ID | CIDR       |
| ------------- |  ----------- | ------- | ---------- |
| powerns-net02 |  172.10.10.1 | 3001    | 172.10.10.0/26 |
{: caption="Table 1. Example subnet information displayed in UI" caption-side="bottom"}

## Using CIDR notation
{: #cidr-notation}

You must not use an IP range outside of the ranges that are defined by [RFC 1918](https://tools.ietf.org/html/rfc1918){: external} (`10.0.0.0/8`, `172.16.0.0/12`, or `192.168.0.0/16`) for a subnet. The instances that are attached to that subnet might not be able to reach parts of the public internet.

If you are using an IP range outside of the ranges that are defined by [RFC 1918](https://tools.ietf.org/html/rfc1918){: external} (`10.0.0.0/8`, `172.16.0.0/12`, or `192.168.0.0/16`) for a subnet you must use IANA assigned IPs and GRE tunneling. For more information see [Generic Routing Encapsulation (GRE) tunneling](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-configuring-power#gre-tunneling). PowerVS assigns IPs as Internal IP from the prefix 192.168.0.0/16 to your accounts for Public Network access. Once a public subnet is assigned, you cannot use those IPs for private networks.

The following networks are filtered out and are not accepted: 10.0.0.0/14, 10.200.0.0/14, 10.198.0.0/15, and 10.254.0.0/16.
{: note}

The number after the slash represents the bit length of the subnet mask. As a result, the smaller the number after the slash, the **more** IP addresses you are allocating. The following table lists the number of available addresses in a subnet (based on its specified CIDR block size):

| CIDR block size | Available IP addresses (WDC04,WDC06) | Available IP addresses (non-WDC) |
| --------------- | ------------------------------ | ---------------------------------- |
|      /22        |        1019                    |          1021                      |
|      /23        |         507                    |           509                      |
|      /25        |         123                    |           125                      |
|      /26        |          59                    |            61                      |
|      /27        |          27                    |            29                      |
|      /28        |          11                    |            13                      |
{: caption="Table 2. Understanding CIDR notation caption" caption-side="bottom"}
