---

copyright:
  years: 2023, 2024

lastupdated: "2024-02-07"

keywords: ha-dr, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #ha-dr}

Both High Availability (HA) and Disaster Recovery (DR) are essential for business continuity. HA addresses local planned and unplanned outages for hardware or software. Disaster recovery addresses the catastrophic events during which the IBM Cloud region might become unavailable. Review the topic to understand the HA and DR for private cloud and on cloud offerings.

## High availability and disaster recovery options in private cloud
{: #ha-dr-private-cloud}

[Private Cloud]{: tag-red}

For the pod software, {{site.data.keyword.powerSysFull}} removes all single points of failure by implementing redundancy as follows:

- Redundancy in power supplies to the server that are connected to different power sources.
- Redundancy in network adapters that are connected to redundant network switches.
- Redundancy in Fibre Channel adapters that are connected to redundant storage area network (SAN) fabrics.
- A dual-VIOS setup with redundant subcomponents for each Virtual I/O Server (VIOS).
- A dual-HMC setup is provided with medium size pod. However, a small pod configuration has only a single HMC. For small pods, the standby system is shared between the managing and managed nodes.
- Dual storage systems that allow host-based mirroring of customer data.

By using the remote restart function, the {{site.data.keyword.powerSys_notm}} restarts the virtual server instances on a different host system if a hardware failure occurs. This process provides basic High Availability (HA) capabilities against power failure. However, the remote restart function might not be helpful if a storage hardware fails. For advanced high-availability function, you can implement HA clusters and HA services such as PowerHA SystemMirror, on the virtual server instances. For HA clusters, you must use server placement groups with anti-affinity policy to enable the functionality of the following items:
* All virtual machines run on different systems.
* You have disks from different controllers.
* You can create mirror volume groups.

For client-managed applications, you must implement high-availability strategy. For example, you can leverage solutions such as Red Hat Enterprise Linux High Availability or SUSE Linux Enterprise High Availability.

### Disaster recovery mechanisms for private cloud
{: #disaster-recovery-mech-private-cloud}

Disaster recovery addresses the catastrophic events during which the IBM Cloud region might become unavailable.

For the IBM-managed software, the disaster recovery strategy remains the same as the high-availability strategy. For client-managed applications and software, you are responsible for the disaster recovery strategy. For example, you can leverage solutions such as Red Hat Enterprise Linux High Availability and SUSE Linux Enterprise Clustered Disaster Recovery.


## High Availability and Disaster Recovery options on cloud
{: #ha-dr-on-cloud}

[On Cloud]{: tag-blue}

The {{site.data.keyword.powerSys_notm}} instance restarts the virtual servers on a different host system if a hardware failure occurs. This process provides basic High Availability (HA) capabilities for {{site.data.keyword.powerSys_notm}}. If you want more advanced HA or Disaster Recover (DR) solutions, you can deploy the following applications in your {{site.data.keyword.powerSys_notm}} environment.
{: shortdesc}

### PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

You can use a monthly subscription model when you purchase PowerHA SystemMirror for AIX Standard Edition. For more information, see [Standard Edition monthly pricing options](https://www.ibm.com/docs/en/announcements/archive/ENUS219-288){: external}.

After you purchase the software, you can download it from [Entitled Systems Support (ESS)](https://www.ibm.com/servers/eserver/ess/index.wss){: external}. You can install PowerHA SystemMirror for AIX on the virtual server that is running in your {{site.data.keyword.powerSys_notm}} environment. For installation instructions, see [Installing PowerHA SystemMirror](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html){: external}.

Review the following information for implementing PowerHA SystemMirror for AIX in your {{site.data.keyword.powerSys_notm}} environment.

- Select **Different Server** from the **Colocation Rules** field when you are creating the virtual servers that are part of the PowerHA SystemMirror cluster. Selecting **Different Server** ensures that the different logical partitions (LPARs) that might be a part of the PowerHA SystemMirror cluster are not deployed on the same host.

- Select **On** from the **Shareable** field when you create storage volumes for the virtual severs that are part of the PowerHA SystemMirror cluster.

- You do not have access to the HMC, VIOS, and the host system on {{site.data.keyword.powerSys_notm}}. Therefore, any PowerHA SystemMirror functions that require access to these capabilities, such as Resource Optimized High Availability (ROHA) and Active Node Halt Policy (ANHP), are not available. However, PowerHA SystemMirror 7.2.6 SP1 or later versions support Resource Optimized High Availability (ROHA) functions. For more information about configuring and by using ROHA with {{site.data.keyword.powerSys_notm}}, see [Resource Optimized High Availability in Cloud](https://www.ibm.com/docs/en/powerha-aix/7.2?topic=administering-resources-optimized-high-availability-in-cloud){: external}

Licenses that are purchased outside a subscription model license are not eligible to be used in the {{site.data.keyword.powerSys_notm}}.
{: note}

### Disaster recovery mechanisms
{: #dr-aix-ibmi}

You can implement a disaster recovery mechanism between two AIX virtual server instances that are installed on separate IBM Cloud data centers by using GLVM replication. For a complete tutorial, see [AIX Disaster Recovery with IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_DR_Tutorial_v1.pdf){: external}. The Transmission Control Protocol (TCP) helps in tuning to improve wide area network (WAN) connection performance between AIX virtual machines. For more information, see [IBM support](https://www.ibm.com/support/pages/node/6410510).

You can implement disaster recovery mechanisms between two IBM i virtual server instances by using PowerHA geographic mirroring. For a complete tutorial, see [IBM i Disaster Recovery with IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_DR_Tutorial_v1.pdf){: external}.

### Business Continuity through backup and restore
{: #ha-dr-ha-business}

[Private Cloud]{: tag-red} Your application configuration and data are not backed up automatically. To recover from a disaster, IBM backs up your configuration data that is required to rebuild a pod. The configuration data includes the virtual machine configurations and private cloud image repositories. However, backup and restoration of client data and client OS images is your responsibility.

[On Cloud]{: tag-blue} Your {{site.data.keyword.powerSys_notm}} configuration and data are not backed up automatically. You can back up your virtual server to [Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) as explained in [Backup strategies for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-backup-strategies). You can also restore your virtual server in case a critical failure occurs.

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from Cloud Object Storage. If your image size is greater than 1 TB, your transfer might take a long time and is prone to failure. The maximum [uncompressed ]{: tag-teal}image size that you can import or export is **10 TB**.
