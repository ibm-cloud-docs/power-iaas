---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-10"

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

Learn more about different AIX and IBM i backup strategies for the {{site.data.keyword.powerSysFull}} service.
{: shortdesc}

## Image capture
{: #backup-image-capture}

Image capture produces a storage FlashCopy of the logical partition (LPAR) and works on both IBM i or AIX virtual machines (VMs). You can use image capture to store backup images within your account (locally), directly to [IBM Cloud Object Storage (COS)](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-capturing-exporting-vm), or both.

Importing and exporting images requires a considerable amount of processing power and network bandwidth. As a result, you can submit only one import or export request before it is queued. Typically, users import or export system disks (AIX rootvg disks) that are smaller in size (**less than 1 TB**) to facilitate the transfer to and from COS. If your image size is greater than 1 TB, your transfer might take a long time and is prone to failure. The maximum image size that you can import or export is **10 TB**.

## AIX backup strategies
{: #backup-aix}

{{site.data.keyword.powerSys_notm}} users can implement any compatible agent-based backup for AIX virtual machines (VM). *Veeam for AIX* and *IBM Spectrum Protect* are two commonly used backup strategies.

- *Veeam for AIX* provides simple physical server backup solutions for machines that are running in respective UNIX&reg; operating systems. With them, IT organizations can provide industry-leading file-based backup and disaster recovery for their environments.
- *IBM Spectrum Protect* provides scalable data protection for physical file servers, applications, and virtual environments. Organizations can scale up to manage billions of objects per backup server. They can reduce backup infrastructure costs with built-in data efficiency capabilities and the ability to migrate data to tape, public cloud services, and on-premises object storage. *IBM Spectrum Protect* can also be a data offload target for *IBM Spectrum Protect Plus,* providing the ability to use your existing investment for long-term data retention and disaster recovery.

It's the user's responsibility to set up and maintain these environments. Remember to check for any connectivity and bandwidth restrictions to the LPAR server. Your LPAR servers can also use {{site.data.keyword.cos_full_notm}} as a repository.

- [Veeam Agents for IBM AIX](https://www.veeam.com/ibm-aix-oracle-solaris-backup.html){: new_window}{: external}
- [What can IBM Spectrum Protect do for your business?](https://www.ibm.com/us-en/marketplace/data-protection-and-recovery){: new_window}{: external}

## IBM i backup strategies
{: #backup-ibmi}

A common IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including ICOS. In most cases, this process involves backing up to virtual tapes and image catalogs. Note, you might need extra storage for the LPAR to host the image catalogs until they are moved to ICOS.

- [Working with ICC](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/icc/topics/iccucon_commands_cloud_overview.htm){: new_window}{: external}
- [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm){: new_window}{: external}
- [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: new_window}{: external}

The typical IBM i customer uses the following flow to perform a backup:

1. Use the 5770-ICC product to connect to COS (~2 times the disk capacity to hold the backup images).
2. Connect to IBM's classic infrastructure by using Direct Link Connect.
3. Create a Nginx reverse proxy. You can provision the reverse proxy from a virtual server instance (x86) for bandwidth up to 1 Gbps. If more bandwidth is needed, you must use a bare metal server.
4. Complete the back up to COS by choosing the speed and resiliency that is required.

## Managed services and IBM Resiliency Services
{: #managed-services}

Contact an IBM representative if you need help with understanding the different backup lifecycle processes.
