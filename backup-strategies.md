---

copyright:
  years: 2019, 2020

lastupdated: "2020-02-03"

keywords: backup strategies, ICOS, BRMS, ICC, Veeam for AIX, IBM Spectrum Protect

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Backup strategies for IBM Power Systems Virtual Servers
{: #backup-strategies}

Learn more about different AIX and IBM i backup strategies for the {{site.data.keyword.powerSysFull}} offering.
{: shortdesc}

## Image capture
{: #migration-icos}

Image capture produces a storage FlashCopy of the logical partition (LPAR) and works on both IBM i or AIX virtual machines (VMs). You can use image capture to store backup images within your account (locally), directly to [IBM Cloud Object Storage](https://cloud.ibm.com/docs/infrastructure/power-iaas?topic=power-iaas-capturing-exporting-vm), or both.

## AIX backup strategies
{: #backup-aix}

{{site.data.keyword.powerSysShort}} users can implement any compatible agent-based backup for AIX virtual machines (VM). *Veeam for AIX* and *IBM Spectrum Protect* are two commonly used backup strategies.

- *Veeam for AIX* provides simple physical server backup solutions for machines that are running in respective UNIX operating systems. With them, IT organizations can provide industry-leading file-based backup and disaster recovery for their environments.
- *IBM Spectrum Protect* provides scalable data protection for physical file servers, applications, and virtual environments. Organizations can scale up to manage billions of objects per backup server. They can reduce backup infrastructure costs with built-in data efficiency capabilities and the ability to migrate data to tape, public cloud services, and on-premises object storage. *IBM Spectrum Protect* can also be a data offload target for *IBM Spectrum Protect Plus,* providing an ability to use your existing investment for long-term data retention and disaster recovery.

It's the user's responsibility to set up and maintain these environments. Remember to check for any connectivity and bandwidth restrictions to the LPAR server. Your LPAR servers can also use {{site.data.keyword.cos_full_notm}} as a repository. For more information on *Veeam for AIX* and *IBM Spectrum Protect,* see the following articles:

- [Veeam Agents for IBM AIX](https://www.veeam.com/ibm-aix-oracle-solaris-backup.html)
- [What can IBM Spectrum Protect do for your business?](https://www.ibm.com/us-en/marketplace/data-protection-and-recovery)

## IBM i backup strategies
{: #backup-ibmi}

A common IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including ICOS. In most cases, this process involves backing up to virtual tapes and image catalogs. Note, you might need extra storage for the LPAR to host the image catalogs until they are moved to ICOS. For more information on working with BRMS and ICC, see the following articles:

- [Working with ICC](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/icc/topics/iccucon_commands_cloud_overview.htm)
- [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm)
- [Data backup and recovery using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm)

## Managed services and IBM Resiliency Services
{: #managed-services}

Contact an IBM representative if you need help with understanding the different backup lifecycle processes.
