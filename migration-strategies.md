---

copyright:
  years: 2019, 2026 

lastupdated: "2026-11-02"

keywords: migration strategies, cos, mass data migration, pwoervc, backup and restore, replication, aspera, mksysb, aws cli, pip, yum

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Migration strategies for IBM i
{: #migration-strategies-power}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Learn about the various strategies that are specific to IBM i systems to migrate your data and workloads to an {{site.data.keyword.powerSysFull}}.
{: shortdesc}

Recent IBM i migration enhancements include the following items:
* [Software data compression in BRMS](https://helpsystemswiki.atlassian.net/wiki/spaces/IWT/pages/165642446/Enhancements+to+BRMS){: external} to support tape and virtual tape compression.
* [IBM offers subscription term pricing for IBM Backup, Recovery and Media Services for i and IBM Cloud Storage Solutions for i](https://www.ibm.com/docs/en/announcements/offers-subscription-term-pricing-backup-recovery-media-services-i-cloud-storage-solutions-i){: external} to facilitate migration to new servers.
* [IBM i migrate while active](https://www.ibm.com/support/pages/ibm-i-migrate-while-active){: external} to migrate data without shutting down the system.

## BRMS and Cloud Storage (ICC)
{: #ibmi-brms-icc}

BRMS is an IBM i product that can be used to automate activities that help define and process your backup, recovery, and media management operations. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including Cloud Object Storage.

The following high-level steps detail how to migrate your OS and data from an {{site.data.keyword.on-prem}} system to the {{site.data.keyword.powerSys_notm}} environment. Keep in mind that most of these steps can be automated by using BRMS and ICC.

1.	Create your IBM i VM in the {{site.data.keyword.powerSys_notm}}.
2.	Create a virtual media and _IMGCLG_ on the deployed VM.
3.	Create a virtual optical and _IMGCLG_ on the {{site.data.keyword.on-prem}} system and perform an operating system save.
4.	FTP the images to the {{site.data.keyword.powerSys_notm}}.
5.	Restore or slip the installation of the OS to get the base OS to the same level as it was on your {{site.data.keyword.on-prem}} system.
6.	Migrate your remaining data.

Refer to this documentation on migrating [IBM i to the Cloud by using BRMS and Cloud Storage Solutions with FTP](https://cloud.ibm.com/media/docs/downloads/power-iaas/IBMi_BRMS_ICC.pdf){: external}.

For more information, see [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: external} and [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/docs/en/i/7.6.0?topic=ssw_ibm_i_76/rzai8/rzai8brmscloudrequireandconsider.html){: external}.



## Migrating IBM i partitions by using PowerHA SystemMirror for IBM i geographic mirroring
{: #migration-gm-sm}

You can migrate an IBM i partition to a {{site.data.keyword.powerSys_notm}} instance by using geographic mirroring with PowerHA SystemMirror (Enterprise Edition). The {{site.data.keyword.powerSys_notm}} instance serves as the replication target.

Before you configure geographic mirroring, establish a private network connection between your on-premises system and your {{site.data.keyword.powerSys_notm}} workspace. For more information, see [Connecting a client-managed data center](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-on-orem) and [VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections). After you establish the connection, data replicates continuously from the on-premises source system to the {{site.data.keyword.powerSys_notm}} instance. After you verify that the data is synchronized, perform a switchover to complete the migration. For instructions on performing a planned switchover, see the "Switching a geographic mirroring environment" chapter in [IBM PowerHA SystemMirror for i: Using Geographic Mirroring](https://www.redbooks.ibm.com/redbooks/pdfs/sg248401.pdf){: external}.

You can use geographic mirroring in synchronous or asynchronous mode. For more information, see the "Modes of operation" section in [IBM PowerHA SystemMirror for i: Using Geographic Mirroring](https://www.redbooks.ibm.com/redbooks/pdfs/sg248401.pdf){: external}.

To use network monitoring and automated failover, you need a license for IBM PowerHA SystemMirror for i or IBM PowerHA Full System Manager for i. You can add these licenses when you create a virtual server instance (VSI). For more information, see [Creating a Power Virtual Server workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service).


For more information about geographic mirroring, see the following resources:

- [Geographic mirroring](https://www.ibm.com/docs/en/i/7.6.0?topic=ssw_ibm_i_76/rzaue/rzalygeographicmirror.html){: external}
- [IBM PowerHA SystemMirror for i: Using Geographic Mirroring](https://www.redbooks.ibm.com/redbooks/pdfs/sg248401.pdf){: external}
