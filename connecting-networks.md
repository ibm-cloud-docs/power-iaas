---

copyright:
  years: 2019, 2020

lastupdated: "2020-02-04"

keywords: configuring virtual machine, direct link connectivity, classic infrastructure, power infrastructure, network, Megaport, VxC, POP

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

# Connecting Power Systems Virtual Server instances and networks
{: #connecting-networks}

Learn more about connecting {{site.data.keyword.powerSysShort}} instances and networks. You can connect {{site.data.keyword.powerSysShort}} instance between us-south (*DAL13*) and us-east (*WDC04*).
{: shortdesc}

## Connecting a Power Systems Virtual Server instance between colocations (DAL13 to WDC04)
{: #connecting-instance-colos}

You can use IBM Cloud Connect to connect {{site.data.keyword.cloud_notm}} instances across colocations (colos). IBM Cloud Connect is a software-defined network interconnect service that brings secure public cloud and software as a service (SaaS) solution connectivity to client locations around the world. Currently, you must open a [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support) to order IBM Cloud Connect.

IBM Cloud Connect is only available to IBM clients within the US.
{: important}

IBM Cloud Connect provides network interconnect from 230+ global Point of Presence (POP) locations for:

- Data Center to the Cloud
- Data Center to data center
- Cloud to Cloud (or Multi-Cloud)
- Global Network Peering Platform (GNPP) access

With IBM Cloud Connect, IBM clients have access to:

- Public cloud providers (IBM Cloud, Azure, AWS, Oracle, Alibaba, Salesforce, etc.)
- IBM services like **Watson** and **zCloud.**
- **IBM GNPP Accessible Services & Transports** like ATT, Verizon, Orange, and Equinix.

### Network connectivity between Dallas and Ashburn
{: #connecting-powerio-connectivity}

Learn more about how the IBM Cloud Connect team helps establish a **Direct Connection** between Cloud Connect (Megaport) and Power IaaS infrastructure.

**Dallas, TX (DAL13)**

1. The Power IaaS Direct Connection (DC) is located in **CyrusOne** and uses the standard **Megaport Port**.
2. The Power IaaS team creates a **Service Key** and provides it to the IBM Cloud Connect delivery team to establish the VxC (one **Service Key** per VxC).
3. The IBM Cloud Connect team enters the **Service Key** into the Megaport portal to establish the VxC.
4. The IBM Cloud Connect team creates the VxC.

**Ashburn, VA (WDC04)**

1. The Power IaaS DC is in **Digital Realty** and uses the **ServiceExchange Port**.
2. The Power IaaS team creates a **Service Key** and provides it to the IBM Delivery team to establish the VxC (one **Service Key** per VxC).
3. The IBM Cloud Connect team enters the **Service Key** into the Megaport portal to establish the VxC.
4. The IBM Cloud Connect team creates the VxC.

## Linking private subnets and networks in a Power System Virtual Server on the IBM Cloud
{: #connecting-private-subnets}

 You can link private subnets within a colo that are on the same virtual LAN (VLAN). You must open a support ticket to link private subnets within a colo.
