---

copyright:
  years: 2019, 2026 

lastupdated: "2026-07-16"

keywords: firewall, ports, network security, vSRX, ICMP

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network security for {{site.data.keyword.powerSys_notm}}
{: #network-security}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---




The {{site.data.keyword.powerSysFull}} infrastructure provides virtual LAN (VLAN) isolation between tenants by using the Virtual I/O Server (VIOS), physical switches, and routers.
{: shortdesc}

To understand the {{site.data.keyword.powerSys_notm}} connection methods, see [Network architecture diagrams](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#networking-environment).

You can use network security groups to secure private subnets. Public subnets rely on a default set of firewall ports rather than network security groups. For more information, see [Network security groups in IBM Power Virtual Server](/docs/power-iaas?topic=power-iaas-network-security-groups).

## Default firewall ports for public subnets
{: #firewall-ports-public}

{{site.data.keyword.powerSys_notm}} uses a fixed set of firewall ports on the Juniper vSRX firewalls:

* 22 (SSH)
* 443 (HTTPS)
* 992 (IBM i5250 emulation SSL)
* ICMP (Internet Control Message Protocol)

The following firewall ports on the Juniper vSRX firewalls are also open, and are typically used for IBM i logical partitions (LPARs):

* 2005
* 2007
* 2010
* 2012
* 9470
* 9475
* 9476

Port 6443 is also open for general use, except in the `WDC04` and `DAL13` data centers.
