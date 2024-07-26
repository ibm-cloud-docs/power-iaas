---

copyright:
  years: 2023, 2024

lastupdated: "2024-07-26"

keywords: ha-dr, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, high availability, disaster recovery, power systems, virtual servers, hardware failure

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery options (On-premises)
{: #ha-dr-private-cloud}

---

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

For the pod software, {{site.data.keyword.powerSysFull}} removes all single points of failure by implementing redundancy as follows:

- Redundancy in power supplies to the servers that are connected to different power sources.
- Redundancy in network adapters that are connected to redundant network switches.
- Redundancy in Fibre Channel adapters that are connected to redundant storage area network (SAN) fabrics.
- A dual-VIOS setup with redundant subcomponents for each Virtual I/O Server (VIOS).
- A dual-HMC setup is provided with medium size pod. However, a small pod configuration has only a single HMC. For small pods, the standby system is shared between the managing and managed nodes.
- Dual storage systems that allow host-based mirroring of customer data.

By using the remote restart function, the {{site.data.keyword.powerSys_notm}} restarts the virtual server instances on a different host system if a hardware failure occurs. This process provides basic High Availability (HA) capabilities against power failure. However, the remote restart function might not be helpful if a storage hardware fails. For advanced high-availability functions, you can implement HA clusters and HA services such as PowerHA SystemMirror, on the virtual server instances. For HA clusters, you must use server placement groups with anti-affinity policy to enable the functions of the following items:
* All virtual machines run on different systems.
* You have disks from different controllers.
* You can create mirror volume groups.

For client-managed applications, you must implement a high-availability strategy. For example, you can use solutions such as Red Hat Enterprise Linux High Availability or SUSE Linux Enterprise High Availability.


## Disaster recovery mechanisms IBM {{site.data.keyword.powerSys_notm}} (On-premises)
{: #disaster-recovery-mech-private-cloud}

Disaster recovery addresses the catastrophic events during which the IBM Cloud region might become unavailable.

For the IBM-managed software, the disaster recovery strategy remains the same as the high-availability strategy. For client-managed applications and software, you are responsible for the disaster recovery strategy. For example, you can use solutions such as Red Hat Enterprise Linux High Availability and SUSE Linux Enterprise Clustered Disaster Recovery.
