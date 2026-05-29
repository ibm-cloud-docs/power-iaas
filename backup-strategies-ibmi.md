---

copyright:
  years: 2019, 2026 

lastupdated: "2026-05-27"

keywords: backup strategies, cos, brms, icc, veeam for aix, ibm spectrum support, cloud setup, direct link, reverse proxy

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Backup strategies for IBM i
{: #backup-ibmi}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}



---

## Secure automated backup with Compass for IBM i
{: #secure-backup-IBMi}

Cobalt Iron, which is an IBM Cloud Partner, provides an automated Backup Offering for IBM i instances of IBM {{site.data.keyword.powerSys_notm}}. The Backup Offering is called **Secure Automated Backup with Compass for PowerVS**. It is powered by the Cobalt Iron Compass Tape Gateway (CTG) Virtual Tape Library (VTL) and is accessible from the IBM Cloud catalog.

Cobalt Iron CTG delivers the following capabilities that IBM i users need:
* Airtight security (including the unique Compass Zero Access® architecture)
* Intelligent automation
* Seamless integration with IBM i
* Flexible deployment
* Modern SaaS-native approach to IBM i data protection.

Compass is designed to simplify operations, strengthen security, and support hybrid deployments. Compass helps organizations to modernize their IBM i backup strategies by reducing complexity and risk.

The Compass VTL feature can be used with IBM® Backup, Recovery, and Media Services (BRMS) or with IBM i Save Object (SAV) commands to protect IBM i data.

## Deploying the Compass backup offering for IBM i
{: #deploy-compass-backup}

Complete the following steps to deploy Compass for IBM i in an IBM data center:

1. Set up secure automated backup with Compass for your account for a region from the IBM Cloud catalog.

For Compass to create or manage VPCs, Transit Gateways, and other cloud networking resources, provide an IBM Cloud API key with the following cloud resource permissions for your IBM Cloud account:

   * Transit Gateway (Resource Group specific) : `transit.gateway.edit`
   * VPC Infrastructure (All Resources): `is.vpc.vpc.list` and `is.vpc.vpc.read`
   * VPC Infrastructure (Resource Group specific): `is.vpc.vpc.create`

2. Ensure that your {{site.data.keyword.powerSys_notm}} workspace is connected to the Compass Vault IP addresses that are provided as a part of the Compass service provisioning.
   Complete the following steps to view the Compass Vault IP addresses:

   Complete the following steps to find the specific IP address that is assigned for your Compass Vault in your IBM Cloud Data Center:
   1. Go to the Cloud Resource List in your IBM Cloud account and go to the Storage category.
   2. Double-click the Secure Automated Backup Compass cloud service.
   3. Click **Get Started**.
   4. Click **Step 2 – Setup Compass Name Resolution**.

   The connectivity between your {{site.data.keyword.powerSys_notm}} workspace and the Compass Vault IP addresses is provided through your IBM Cloud Transit Gateway.

4.	Complete the following steps to protect IBM i instance:
   1. Access the Cobalt Iron Commander graphical interface to configure a Compass Virtual Tape Library (VTL).
   2. In the **Admin** tab, select the **Virtual Tape Libraries** tile to open the **Create Virtual Tape Library** wizard.
   3. Create a new Compass VTL as an iSCSI target. The **Create Virtual Tape Library** wizard creates the library, drives, and virtual tape volumes for use by IBM i backup utilities. When Compass creates the VTL, it also creates Challenge Handshake Authentication Protocol (CHAP) authentication for the Compass VTL.
   4. Configure the Compass VTL on your IBM i instance as an iSCSI target device. Use IBM Navigator for IBM i, as it is the preferred way to configure iSCSI targets.
   5. Use the Compass iSCSI VTL as the target for your Backup, Recovery, and Media Services (BRMS) or Save Object (SAV) backups and restores.

   For more information about protecting IBM i with Compass, see [Compass Quick Start Guide for IBM i Data Protection](https://www.cobaltiron.com/wp-content/uploads/2026/02/CobaltIron-Compass-IBMi-QuickStartGuide-20260107.pdf){: external}.

## BRMS and ICC
{: #brms-icc}

Another IBM i backup strategy is to use IBM® Backup, Recovery, and Media Services (BRMS) and IBM Cloud Storage Solutions (ICC). Together, these products automatically back up your LPARs to {{site.data.keyword.cos_full_notm}}. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including Cloud Object Storage. In most cases, this process involves backing up to virtual tapes and image catalogs.

You need extra storage for the LPAR to host the image catalogs until they are moved to Cloud Object Storage.
{: note}

The typical IBM i customer uses the following flow to back up LPARs and objects:

1. Use the 5733-ICC product to connect to Cloud Object Storage (~2 times the disk capacity to hold the backup images).
2. Connect to IBM Cloud Object Storage by following the steps that are mentioned in [Using Cloud Object Storage](/docs/power-iaas?topic=power-iaas-additional-backup-strategies#cos-over-directlink).
3. Complete the back up to Cloud Object Storage by choosing the speed and resiliency that is required.

   - [Working with ICC](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/icc/topics/iccucon_commands_cloud_overview.htm){: external}
   - [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm){: external}
   - [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm){: external}

For a complete tutorial on backing up and restoring IBM i VM data, see [Backing up and restoring data in an IBM i VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Backups_Tutorial_v1.pdf){: external}.

## FalconStor StorSafe VTL
{: #fstor-vtl-2}

For more information, see [FalconStor StorSafe VTL](/docs/power-iaas?topic=power-iaas-manage-vtl).
