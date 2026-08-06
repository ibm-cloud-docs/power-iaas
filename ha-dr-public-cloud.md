---

copyright:
  years: 2023, 2026

lastupdated: "2026-08-05"


keywords: ha-dr, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, high availability, disaster recovery, power systems, virtual servers, hardware failure

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# High Availability and Disaster Recovery options in {{site.data.keyword.off-prem}}
{: #ha-dr-on-cloud}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---



{{site.data.keyword.powerSysFull}} supports various high availability and disaster recovery solutions that you can deploy in your environment. Host failure recovery is the default high availability solution in {{site.data.keyword.powerSys_notm}}. You can also deploy advanced solutions, such as PowerHA SystemMirror for cluster management and PowerHA geographic mirroring for replication-based disaster recovery.
{: shortdesc}


## Host failure recovery
{: #host-failure-recovery}

{{site.data.keyword.powerSys_notm}} is built on the IBM Power enterprise infrastructure with redundant networking and storage area network (SAN) fabric capabilities. IBM {{site.data.keyword.powerSys_notm}} monitors your infrastructure to ensure that hosts are responsive and operating correctly.

When a host fails unexpectedly, the virtual server instances (VSIs) on the failed host are automatically restarted on another available host. In some cases, you must manually recover the failed host.

The host failure recovery process restarts VSIs on a different available host. This process completely reboots the operating system. After the operating system restarts, you must restart your applications according to your standard boot procedures.



The automated remote restart feature enables host failure recovery by default for all VSIs in the {{site.data.keyword.powerSys_notm}} environment. To disable this feature, you can set **Automated remote restart** to off during VSI creation. Alternatively, you can modify the settings on the Virtual server instance details page. For more information, see [Disabling automated remote restart for a VSI](/docs/power-iaas?topic=power-iaas-modifying-instance#disable-arr).

Host failure recovery:

- Does not restart a pinned VSI. Pinning VSIs to specific hosts results in extended downtime because recovery depends on the time required to repair the failed host. To minimize downtime, ensure that VSIs are not pinned to a host. For more information, see [Virtual server pinning and its impacts on VSI availability](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#vmpinning).

- Does not restart a VSI in a server placement group that uses an affinity policy and includes other VSIs that are hard-pinned to the host. Affinity policies require all VSIs in the group to remain on the same host. A hard-pinned VSI prevents VSIs in the group from moving to another host.



- Restarts the VSI on another host with a different physical serial number. If your software depends on serial numbers, consider using virtual serial numbers (VSNs) for IBM i. Check your independent software vendor (ISV) licensing policy to determine whether VSNs are appropriate.



## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

PowerHA SystemMirror for AIX Standard Edition is available with a monthly subscription model. For more information, see [Standard Edition monthly pricing options](https://www.ibm.com/docs/en/announcements/archive/ENUS219-288){: external}.

After you purchase the software, you can download it from [Entitled Systems Support (ESS)](https://www.ibm.com/servers/eserver/ess/index.wss){: external}. You can install PowerHA SystemMirror for AIX on the virtual server that is running in your {{site.data.keyword.powerSys_notm}} environment. For installation instructions, see [Installing PowerHA SystemMirror](https://www.ibm.com/docs/en/powerha-aix/7.2.x?topic=installing){: external}.

Review the following information for implementing PowerHA SystemMirror for AIX in your {{site.data.keyword.powerSys_notm}} environment:

- Select **Different Server** from the **Colocation Rules** field when you create the virtual servers that are part of the PowerHA SystemMirror cluster. Selecting **Different Server** ensures that the different logical partitions (LPARs) in the PowerHA SystemMirror cluster are not deployed on the same host.

- Select **On** from the **Shareable** field when you create storage volumes for the virtual servers that are part of the PowerHA SystemMirror cluster.

- You do not have access to the HMC, VIOS, and host system on {{site.data.keyword.powerSys_notm}}. Therefore, PowerHA SystemMirror functions that require access to these capabilities, such as Resource Optimized High Availability (ROHA) and Active Node Halt Policy (ANHP), are not available. However, PowerHA SystemMirror 7.2.6 SP1 or later versions support ROHA functions. For more information about configuring and using ROHA with {{site.data.keyword.powerSys_notm}}, see [Resource Optimized High Availability in Cloud](https://www.ibm.com/docs/en/powerha-aix/7.2.x?topic=administering-resources-optimized-high-availability-in-cloud){: external}.

Licenses that are purchased outside a subscription model are not eligible for use with {{site.data.keyword.powerSys_notm}}.
{: note}






## Disaster recovery mechanisms
{: #dr-aix-ibmi}

You can use Geographic Logical Volume Manager (GLVM) replication to implement disaster recovery between two AIX VSIs that are deployed in separate IBM Cloud data centers. For a complete tutorial, see [AIX Disaster Recovery with {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_DR_Tutorial_v1.pdf){: external}.

You can tune the Transmission Control Protocol (TCP) to improve wide area network (WAN) connection performance between AIX virtual machines. For more information, see [TCP tuning for AIX WAN connections](https://www.ibm.com/support/pages/node/6410510){: external}.

You can implement disaster recovery mechanisms between two IBM i VSIs by using PowerHA geographic mirroring. For a complete tutorial, see [IBM i Disaster Recovery with IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_DR_Tutorial_v1.pdf){: external}.

## Business continuity through backup and restore
{: #ha-dr-ha-business}

[{{site.data.keyword.on-prem}}]{: tag-red} Your application configuration and data are not backed up automatically. To recover from a disaster, IBM backs up the configuration data that is needed to rebuild a pod. The configuration data includes the virtual machine configurations and private cloud image repositories. However, you are responsible for backing up and restoring client data and client OS images.

[{{site.data.keyword.off-prem}}]{: tag-blue} Your {{site.data.keyword.powerSys_notm}} configuration and data are not backed up automatically. You can back up your virtual server to [Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) as explained in [Backup strategies for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-backup-strategies). You can also restore your virtual server in case a critical failure occurs.

Importing and exporting images require significant processing power and network bandwidth. As a result, you can submit only one import or export request at a time. Any additional import or export requests are queued. Typically, you import or export system disks (AIX rootvg disks) that are less than 1 TB to facilitate the transfer to and from Cloud Object Storage. If your image is greater than 1 TB, the transfer might take longer and is more likely to fail or time out. The maximum uncompressed image that you can import or export is 10 TB.
