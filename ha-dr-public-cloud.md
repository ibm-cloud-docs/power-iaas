---

copyright:
  years: 2023, 2024

lastupdated: "2025-05-16"

keywords: ha-dr, {{site.data.keyword.powerSys_notm}} as a service, private cloud, before you begin, terminology, high availability, disaster recovery, power systems, virtual servers, hardware failure

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# High Availability and Disaster Recovery options in {{site.data.keyword.off-prem}}
{: #ha-dr-on-cloud}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---






This topic describes various high availability and disaster recovery solutions that you can deploy in the {{site.data.keyword.powerSysFull}} environment. The host failure recovery is the default high availability solution supported by {{site.data.keyword.powerSys_notm}}. This topic also covers some of the advanced high availability and disaster recovery solutions that you can deploy.
{: shortdesc}


## Host failure recovery
{: #host-failure-recovery}

{{site.data.keyword.powerSys_notm}} is built on the IBM Power enterprise infrastructure, including redundant networking and storage area network (SAN) fabrics capabilities. IBM Power Virtual Server continuously monitors your infrastructure to ensure that all the hosts are working correctly and responsive.

When a host fails unexpectedly, the virtual server instances on the failed host are automatically restarted on a working host. In some cases, manual recovery of the failed host is attempted.

The host failure recovery process involves restarting the virtual server instances on alternate hosts and results in a complete reboot of the operating system. After the operating system is rebooted, the applications must be restarted to recover and resume as per your standard boot procedures.
{: note}

The host failure recovery:

- Is enabled by default for all the virtual server instances in the Power Virtual Server environment.

- Does not restart any pinned virtual server instances. [Pinning virtual server instances](/docs/power-iaas?topic=power-iaas-powervs-faqs#pinning) to specific hosts results in extended downtime, as the recovery depends on the time taken to repair the failed host. To prevent or minimize downtime, ensure that the virtual server instances are not pinned to the host.

- Restarts the virtual server instance on another host with a different physical serial number. If your software depends on serial numbers, consider using capabilities such as virtual serial numbers (VSN) for IBM i, depending on your independent software vendor (ISV) licensing policies.



## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

You can use a monthly subscription model when you purchase PowerHA SystemMirror for AIX Standard Edition. For more information, see [Standard Edition monthly pricing options](https://www.ibm.com/docs/en/announcements/archive/ENUS219-288){: external}.

After you purchase the software, you can download it from [Entitled Systems Support (ESS)](https://www.ibm.com/servers/eserver/ess/index.wss){: external}. You can install PowerHA SystemMirror for AIX on the virtual server that is running in your {{site.data.keyword.powerSys_notm}} environment. For installation instructions, see [Installing PowerHA SystemMirror](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html){: external}.

Review the following information for implementing PowerHA SystemMirror for AIX in your {{site.data.keyword.powerSys_notm}} environment.

- Select **Different Server** from the **Colocation Rules** field when you are creating the virtual servers that are part of the PowerHA SystemMirror cluster. Selecting **Different Server** ensures that the different logical partitions (LPARs) that might be a part of the PowerHA SystemMirror cluster are not deployed on the same host.

- Select **On** from the **Shareable** field when you create storage volumes for the virtual severs that are part of the PowerHA SystemMirror cluster.

- You do not have access to the HMC, VIOS, and the host system on {{site.data.keyword.powerSys_notm}}. Therefore, any PowerHA SystemMirror functions that require access to these capabilities, such as Resource Optimized High Availability (ROHA) and Active Node Halt Policy (ANHP), are not available. However, PowerHA SystemMirror 7.2.6 SP1 or later versions support Resource Optimized High Availability (ROHA) functions. For more information about configuring and by using ROHA with {{site.data.keyword.powerSys_notm}}, see [Resource Optimized High Availability in Cloud](https://www.ibm.com/docs/en/powerha-aix/7.2?topic=administering-resources-optimized-high-availability-in-cloud){: external}

Licenses that are purchased outside a subscription model license are not eligible to be used in the {{site.data.keyword.powerSys_notm}}.
{: note}

## Disaster recovery mechanisms
{: #dr-aix-ibmi}

You can implement a disaster recovery mechanism between two AIX virtual server instances that are installed on separate IBM Cloud data centers by using GLVM replication. For a complete tutorial, see [AIX Disaster Recovery with IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_DR_Tutorial_v1.pdf){: external}. The Transmission Control Protocol (TCP) helps in tuning to improve wide area network (WAN) connection performance between AIX virtual machines. For more information, see [IBM support](https://www.ibm.com/support/pages/node/6410510).

You can implement disaster recovery mechanisms between two IBM i virtual server instances by using PowerHA geographic mirroring. For a complete tutorial, see [IBM i Disaster Recovery with IBM {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_DR_Tutorial_v1.pdf){: external}.

## Business Continuity through backup and restore
{: #ha-dr-ha-business}

[{{site.data.keyword.on-prem}}]{: tag-red} Your application configuration and data are not backed up automatically. To recover from a disaster, IBM backs up your configuration data that is required to rebuild a pod. The configuration data includes the virtual machine configurations and private cloud image repositories. However, backup and restoration of client data and client OS images is your responsibility.

[{{site.data.keyword.off-prem}}]{: tag-blue} Your {{site.data.keyword.powerSys_notm}} configuration and data are not backed up automatically. You can back up your virtual server to [Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) as explained in [Backup strategies for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-backup-strategies). You can also restore your virtual server in case a critical failure occurs.

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from Cloud Object Storage. If your image size is greater than 1 TB, your transfer might take a long time and be prone to failure. The maximum uncompressed image size that you can import or export is **10 TB**.
