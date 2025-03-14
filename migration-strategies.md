﻿---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-05"

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

Learn about the various strategies to migrate your data and workloads to an {{site.data.keyword.powerSysFull}}.
{: shortdesc}

## IBM i migration strategies
{: #migration-ibmi}

Learn about migration strategies that are specific to IBM i systems.

Recent IBM i migration enhancements:
1.	BRMS enhanced to [support software data compression](https://helpsystemswiki.atlassian.net/wiki/spaces/IWT/pages/165642446/Enhancements+to+BRMS){: external} for tape and virtual tape
2.	[90-day software license for BRMS and ICC](https://www.ibm.com/docs/en/announcements/offers-subscription-term-pricing-backup-recovery-media-services-i-cloud-storage-solutions-i){: external}.

## Backup Recovery and Media Services (BRMS) and Cloud Storage (ICC)
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

For more information, see [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: external} and [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm){: external}.



## Logical Replication with Geographic Mirroring and PowerHA SystemMirror for i
{: #logical-rep-glvm}

GeoMirroring enables IBM i disk mirroring technology on multiple system environments and supports host-based and logical replication across geographically distant sites. Geo mirroring supports synchronous and asynchronous modes. You can integrate PowerHA SystemMirror (Enterprise Edition) for network monitoring and automated failover support.

- [Geographic mirroring](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_73/rzaue/rzalygeographicmirror.htm){: external}
- [IBM PowerHA SystemMirror for i: Using Geographic Mirroring](https://www.redbooks.ibm.com/redbooks/pdfs/sg248401.pdf){: external}
