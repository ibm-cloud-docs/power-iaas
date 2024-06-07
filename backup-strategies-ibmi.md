---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-06"

keywords: backup strategies, cos, brms, icc, veeam for aix, ibm spectrum support, cloud setup, direct link, reverse proxy

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Backup strategies for IBM i
{: #backup-ibmi}

A common IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including Cloud Object Storage. In most cases, this process involves backing up to virtual tapes and image catalogs.

You need extra storage for the LPAR to host the image catalogs until they are moved to Cloud Object Storage.
{: note}

The typical IBM i customer uses the following flow to back up LPARs and objects:

1. Use the 5733-ICC product to connect to Cloud Object Storage (COS) (~2 times the disk capacity to hold the backup images).
2. Connect to IBM COS by following the steps that are mentioned in [Using Cloud Object Storage](/docs/power-iaas?topic=power-iaas-backup-strategies#cos-over-directlink).
4. Complete the back up to COS by choosing the speed and resiliency that is required.

   - [Working with ICC](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/icc/topics/iccucon_commands_cloud_overview.htm){: external}
   - [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm){: external}
   - [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: external}

For a complete tutorial on backing up and restoring IBM i VM data, see [Backing up and restoring data in an IBM i VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Backups_Tutorial_v1.pdf){: external}.
