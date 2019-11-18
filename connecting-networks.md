---

copyright:
  years: 2019

lastupdated: "2019-11-18"

keywords: configuring virtual machine, direct link connectivity, classic infrastructure, power infrastructure, network, Megaport, VxC

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

Learn more about connecting {{site.data.keyword.powerSysShort}} instances and networks.
{: shortdesc}

## Connecting a Power Systems Virtual Server instance between colocations (colo) (DAL to WDC)
{: #connecting-classic}

You can use IBM Cloud Connect to connect {{site.data.keyword.cloud_notm}} instances across colos. IBM Cloud Connect is a software-defined network interconnect service that brings secure public cloud and SaaS solution connectivity to client locations around the world. You must open a [support ticket](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support) to order IBM Cloud Connect.

IBM Cloud Connect provides network interconnect from 230+ global POP locations for:

1. Data Center to the Cloud
1. Data Center to Data Center
1. Cloud to Cloud (or Multi-Cloud)
1. Global Network Peering Platform (GNPP) access

With IBM Cloud Connect, IBM clients have access to:

- Public cloud providers (IBM Cloud, Azure, AWS, Oracle, Alibaba, Salesforce, etc.)
- IBM value-added services like Watson and zCloud.
- **IBM GNPP Accessible Services & Transports** like ATT, Verizon, Orange, Equinix, etc.)

## Linking private subnets and networks in a Power System Virtual Server on the IBM Cloud
{: #connecting-subnet}

 You can link private subnets within a colo that are on the same virtual LAN (VLAN). You must open a suport ticket with IBM to enable this functionality.
