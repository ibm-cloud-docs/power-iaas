---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-07"

keywords: firewall, ports, network security, vSRX, ICMP

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network security
{: #network-security}

[Off-premises]{: tag-blue}

The infrastructure provides virtual LAN (VLAN) isolation between different tenants, which are enforced at Virtual I/O Server (VIOS) and physical switches and routers.
{: shortdesc}

## Default firewall ports
{: #firewall-ports}

The {{site.data.keyword.powerSysFull}} network security architecture relies on a set of fixed firewall ports open on the *Juniper vSRX* firewalls:
{: shortdesc}

There are plans to add the ability to dynamically configure the firewall rules in the future.
{: note}

* 22 (SSH)
* 443 (HTTPS)
* 992 (IBM i5250 emulation SSL)
* ICMP traffic

The following firewall ports are also open, typically used for IBM i logical partitions (LPARs):

* 2005
* 2007
* 2010
* 2012
* 9470
* 9475
* 9476

The port 6443 is also open for miscellaneous purposes. This port will not be open for the WDC04 and DAL13 data centers.

If you need extra ports to be opened, you can consider a customer-specific firewall option that is available by using an IBM Cloud firewall, such as Vyatta, Juniper vSRX, or FortiGate, and by connecting to {{site.data.keyword.powerSys_notm}} by using [Direct Link Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). To understand the {{site.data.keyword.powerSys_notm}} connection methods, see [Network architecture diagrams](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#networking-environment).
