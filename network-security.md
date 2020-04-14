---

copyright:
  years: 2019, 2020

lastupdated: "2020-01-23"

keywords: firewall, ports, network security, vSRX, ICMP

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

# Network security
{: #network-security}

Infrastructure provides virtual LAN (VLAN) isolation between different tenants, which are enforced at Virtual I/O Server (VIOS) and physical CISCO switches and routers.
{: shortdesc}

## Default firewall ports
{: #firewall-ports}

The public {{site.data.keyword.powerSysShort}} network security architecture relies on a set of fixed firewall ports open on the *Juniper vSRX* firewalls:
{: shortdesc}

There are plans to add the ability to dynamically configure the firewall rules in the future.
{: note}

* 22 (SSH)
* 443 (HTTPS)
* 992 (IBM i5250 emulation SSL)
* ICMP traffic

The following firewall ports are also available for IBM i virtual machines (VM):

* 2005
* 2007
* 2010
* 2012
* 9470
* 9475
* 9476

If you need extra ports to be opened, you must submit a [support ticket](/docs/power-iaas?topic=power-iaas-getting-help-and-support). Support representatives can **manually** open ports for you.
