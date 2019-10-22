---

copyright:
  years: 2019

lastupdated: "2019-l0-22"

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

# Default firewall ports
{: #firewall}

Th {{site.data.keyword.powerSysShort}} network security architecture relies on a set of fixed firewall ports open on the *Juniper vSRX* firewalls:
{: shortdesc}

* 22 (SSH)
* 443 (HTTPS)
* 992 (IBM i5250 emulation SSL)
* ICMP traffic

If you need additional ports to be opened, you must submit a service ticket to request to vSRX appliance administrators to *manually* open the port. Dynamic configuration of the firewall rules will be added as an option through REST APIs, GUI, etc, at a later time.
