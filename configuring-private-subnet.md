---

copyright:
  years: 2019

lastupdated: "2019-11-18"

keywords: ssh key, AIX virtual machine, configure ssh key, new virtual server, public ssh key, connecting private subnets, gateway, CIDR, DAL, WDC

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Configuring a private network subnet
{: #configuring-subnet}

You can configure a private network subnet when you create a {{site.data.keyword.powerSysFull}}. You must give your subnet a **Name** and specify a **Classless inter-domain routing (CIDR)**. When you specify a CIDR, the **Gateway**, **IP range**, and **DNS server** are automatically populated.
{: shortdesc}

You must use CIDR notation when you choose the IP ranges for your private network subnet. CIDR notation is defined in [RFC 1518](https://tools.ietf.org/html/rfc1518){: external} and [RFC 1519](https://tools.ietf.org/html/rfc1519){: new_window}{: external}.

```shell
<IPv4 address>/number>
```
{: screen}

For example, `192.168.100.14/24` represents the IPv4 address, `192.168.100.14`, and its associated routing prefix `192.168.100.0`, or equivalently, its subnet mask `255.255.255.0` (which has 24 leading 1-bits).

The first IP address is always reserved for the gateway in the Washington, D.C. (WDC) and Dallas (DAL) colocations (colo). The second and third IP addresses are reserved for gateway high-availability (HA) in only the WDC colo. The subnet address and subnet broadcast address are reserved in both colos.
{: important}

  ![Configuring a new private network](./images/console-configure-private-network.png "Configuring a new private network"){: caption="Figure 5. Configuring a new private network" caption-side="bottom"}

You can also create a private network subnet by using the IBM CLI. Use the following command to create a private network subnet:

```shell
ibmcloud pi network-create-private NETWORK_NAME --cidr-block CIDR --ip-range "startIP-endIP[,startIP-endIP]" [--dns-servers "DNS1 DNS2"] [--gateway GATEWAY] [--json]
```
{: codeblock}

## Using CIDR notation
{: #cidr-notation}

If you use an IP range outside of those that are defined by [RFC 1918](https://tools.ietf.org/html/rfc1918){: new_window}{: external} (`10.0.0.0/8`, `172.16.0.0/12`, or `192.168.0.0/16`) for a subnet, the instances that are attached to that subnet might not be able to reach parts of the public internet.

The number after the slash represents the bit length of the subnet mask. As a result, the smaller the number after the slash, the **more** IP addresses you are allocating. The following table lists the number of available addresses in a subnet, based on its specified CIDR block size:

| CIDR block size | Available IP Addresses (WDC) | Available IP Addresses (DAL)
| --------------- | ---------------------------- |---------------------------
|      /22        |        1019                  |          1021
|      /23        |         507                  |          509
|      /24        |         251                  |          253
|      /25        |         123                  |          125
|      /26        |          59                  |           61
|      /27        |          27                  |           29
|      /28        |          11                  |           13
