---

copyright:
  years: 2023, 2026 

lastupdated: "2026-06-24"

keywords: ha-dr, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, high availability, disaster recovery, power systems, virtual servers, hardware failure

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery options in {{site.data.keyword.on-prem}}
{: #ha-dr-private-cloud}

---



{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

For the pod software, {{site.data.keyword.powerSysFull}} removes all single points of failure by implementing redundancy as follows:

- Redundancy in power supplies to the servers that are connected to different power sources.
- Redundancy in network adapters that are connected to redundant network switches.
- Redundancy in Fibre Channel adapters that are connected to redundant storage area network (SAN) fabrics.
- A dual-VIOS setup with redundant subcomponents for each Virtual I/O Server (VIOS).
- A dual-HMC setup is provided with medium size pod. However, a small pod configuration has only a single HMC. For small pods, the standby system is shared between the managing and managed nodes.
- Dual storage systems that allow host-based mirroring of customer data.

## Host failure recovery
{: #host-failure-recovery-private}

{{site.data.keyword.powerSys_notm}} is built on the IBM Power enterprise infrastructure with including redundant networking and storage area network (SAN) fabrics capabilities. IBM Power Virtual Server continuously monitors your infrastructure to ensure that hosts are responsive and operating correctly.

When a host fails unexpectedly, the virtual server instances (VSIs) on the failed host are automatically restarted on another available host. In some cases, manual recovery of the failed host is required.

The host failure recovery process involves restarting the VSIs on alternate hosts and results in a complete reboot of the operating system. After the operating system is rebooted, the applications must be restarted to recover and resume as per your standard boot procedures.
{: note}

Host failure recovery is enabled by default for all VSIs in the {{site.data.keyword.powerSys_notm}} environment through the automated remote restart feature. You can disable automated remote restart for a VSI by modifying the related settings on the Virtual server instance details page. For more information, see [Disabling automated remote restart for a VSI](/docs/power-iaas?topic=power-iaas-modifying-instance#disable-arr).

Host failure recovery:

- Does not restart a pinned VSI. When you pin virtual server instances to specific hosts, the recovery depends on the time taken to repair the failed host, which results in extended downtime. To minimize downtime, ensure that VSIs are not pinned to a host. For more information, see [What does VSI pinning do?](/docs/power-iaas?topic=power-iaas-powervs-faqs#pinning).



- Restarts the VSI on another host with a different physical serial number. If your software depends on serial numbers, consider using virtual serial numbers (VSN) for IBM i, depending on your independent software vendor (ISV) licensing policies.

For advanced high-availability functions, you can implement HA clusters and HA services such as PowerHA SystemMirror, on the virtual server instances. For HA clusters, you must use server placement groups with anti-affinity policy to enable the functions of the following items:

* All virtual server instances run on different systems.
* You have disks from different controllers.
* You can create mirror volume groups.

For client-managed applications, you must implement a high-availability strategy. For example, you can use solutions such as Red Hat Enterprise Linux High Availability or SUSE Linux Enterprise High Availability.


## Disaster recovery mechanisms in {{site.data.keyword.on-prem-fname}}
{: #disaster-recovery-mech-private-cloud}

Disaster recovery addresses the catastrophic events during which the IBM Cloud region might become unavailable.

For the IBM-managed software, the disaster recovery strategy remains the same as the high-availability strategy. For client-managed applications and software, you are responsible for the disaster recovery strategy. For example, you can use solutions such as Red Hat Enterprise Linux High Availability and SUSE Linux Enterprise Clustered Disaster Recovery.
