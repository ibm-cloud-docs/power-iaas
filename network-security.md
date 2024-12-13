---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-03"

keywords: firewall, ports, network security, vSRX, ICMP

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network security
{: #network-security}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

The infrastructure provides virtual LAN (VLAN) isolation between different tenants, which are enforced at Virtual I/O Server (VIOS) and physical switches and routers.
{: shortdesc}

## Default firewall ports
{: #firewall-ports}

The {{site.data.keyword.powerSysFull}} network security architecture relies on a set of fixed firewall ports open on the *Juniper vSRX* firewalls:
{: shortdesc}

* 22 (SSH)
* 443 (HTTPS)
* 992 (IBM i5250 emulation SSL)
* ICMP traffic

There are plans to add the ability to dynamically configure the firewall rules in the future.
{: note}


The following firewall ports are also open, typically used for IBM i logical partitions (LPARs):

* 2005
* 2007
* 2010
* 2012
* 9470
* 9475
* 9476

The port 6443 is also open for miscellaneous purposes. However, the port 6443 is not open for the WDC04 and DAL13 data centers.

If you need extra ports to be opened, use a customer-specific firewall option. The option is available by using an IBM Cloud firewall, such as Vyatta, Juniper vSRX, or FortiGate, and by connecting to {{site.data.keyword.powerSys_notm}} by using [Direct Link Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). To understand the {{site.data.keyword.powerSys_notm}} connection methods, see [Network architecture diagrams](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#networking-environment).
