---

copyright:
  years: 2019

lastupdated: "2019-l1-07"

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

## Default firewall ports
{: #firewall-ports}

The {{site.data.keyword.powerSysShort}} network security architecture relies on a set of fixed firewall ports open on the *Juniper vSRX* firewalls:
{: shortdesc}

* 22 (SSH)
* 443 (HTTPS)
* 992 (IBM i5250 emulation SSL)
* ICMP traffic

If you need additional ports to be opened, you must submit a [service ticket](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support). Support representatives can *manually* open the port for you. There are plans to add the dynamic configuration of the firewall rules in the future.
