---

copyright:
  years: 2019

lastupdated: "2019-12-17"

keywords: migration strategies, ICOS, mass data migration, MDM, PowerVC, backup and restore, replication, Aspera, mksysb

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

# Migration strategies for IBM Power Systems Virtual Servers
{: #migration-strategies-power}

Learn how to migrate your data and workloads to the {{site.data.keyword.powerSysFull}}.
{: shortdesc}

## IBM Cloud Object Storage (ICOS)
{: #migration-icos}

ICOS can be used as an intermediary location to store files from your on-premises environment. You can retrieve and send your files to the {{site.data.keyword.powerSys_notm}} environment from this location. You must create ICOS buckets to transfer data over the public internet and or privately secured links. For more information, see [IBM Cloud Object Storage: FAQ](https://www.ibm.com/cloud/object-storage/faq).

## Mass Data Migration (MDM)
{: #migration-mdm}

MDM provides a simple and secure way to physically transfer data (terabytes to petabytes) to the IBM Cloud. As part of the MDM process, IBM sends the client an MDM-approved device, who uploads their data to the device on-premises and sends it back. IBM then transfers and stores the content in ICOS for later retrieval from within the {{site.data.keyword.powerSys_notm}} environment. For more information, see [IBM Cloud Object Storage: FAQ](https://www.ibm.com/cloud/mass-data-migration/faq).

## PowerVC images and ICOS
{: #migration-powervc-icos}

If you have an environment with access to PowerVC, you can capture OVA images to easily migrate your data. The {{site.data.keyword.powerSys_notm}} offering allows you to provision a new virtual server based on an OVA image. To accomplish this, regardless of the operating system (OS), you must complete the following steps:

1. Create an OVA image on your local system.
2. Copy the OVA image to the IBM Cloud.
3. Deploy the OVA image and provision a new {{site.data.keyword.powerSys_notm}}.

For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/infrastructure/power-iaas?topic=power-iaas-deploy-custom-image).

## Aspera Technologies
{: #aspera-technologies}

IBM Aspera&reg; on Cloud is a hosted service that quickly and reliably moves and shares your data sets across a hybrid cloud environment. IBM Aspera can help transfer data to the IBM Cloud for later retrieval from the {{site.data.keyword.powerSys_notm}} environment. For more information, see [IBM Aspera on Cloud](https://www.ibm.com/cloud/high-speed-data-transfer).

## Replication
{: #replication}

You can use various replication mechanisms to migrate and sync environments between on-premises and the {{site.data.keyword.powerSys_notm}}.

Storage area network (SAN) and hardware-based replication is not currently a migration option.
{: note}

### Host and OS-based logical replication
{: #replication-host}

IBM recommends that you use PowerHA SystemMirror (Enterprise Edition) with Geomirroring and Geographic Logical Volume Manager (GLVM). The following host and os-based logical replication options exist depending on your OS:

- AIX - GLVM
- IBM i - Geomirroring

### Application-specific replication
{: #replication-app}

Applications might have replication mechanisms that can sync multiple mechanisms. These are some of the application-specific replication options:

- *Db2 HADR*
- *Oracle Data Guard*
- *Oracle Goldengate*
- *iCluster*
- *MIMIX from Syncsort*

## Backup and restore
{: #backup-restore}

You can back up your environment on-premises and restore it to the IBM Cloud. In most cases, ICOS, and NFS servers serve as an intermediary to store (back up) and retrieve (restore) data. For more information on OS-specific, see

## Third-party vendors and tools
{: #third-party}

Customers can use third-party tools to perform data migration. Some commonly used third-party tools for data migration are:

- *iCluster*
- *MIMIX from Syncsort*

## IBM teams and managed services
{: #teams-managed-services}

You can engage IBM teams and services to assist you throughout the migration lifecycle. For more information, contact your IBM representatives:

- [Power Lab Services](https://www.ibm.com/it-infrastructure/services/lab-services)
- [IBM Services for Cloud Migration](https://www.ibm.com/services/cloud/migration)

## AIX
{: #migration-aix}

Learn about migration strategies that are specific to AIX systems.

### Migration by using MKSYSB
{: #migration-mksysb}

You can migrate your data by using the `mksysb` command:

1. Back up the on-premises OS with the `alt_disk_mksysb` command and transfer it to ICOS.
2. Create a new {{site.data.keyword.powerSys_notm}} and import the image.
3. Restore the on-premises image.

For more information see [Restoring an AIX mksysb image onto an IBM Cloud virtual machine (VM)]()

### Logical replication with GLVM and PowerHA SystemMirror for AIX Enterprise Edition
{: #logical-replication}

GLVM is an OS-based IP replication approach. It is based on the AIX LVM and enables data and logical volume mirroring across geographically distant locations. GLVM supports both synchronous and asynchronous modes. You can integrate PowerHA System Mirror (Enterprise Edition) to network monitoring and automated failover support. For more information, see the following links.

- [Geographic Logical Volume Manager (GLVM)](https://www.ibm.com/support/knowledgecenter/en/SSPHQG_7.2/glvm/ha_glvm_glvm.html)
- [Configuring geographically mirrored volume groups](https://www.ibm.com/support/knowledgecenter/en/SSPHQG_7.2/glvm/ha_glvm_config_glvm.html)
- [Exploiting IBM PowerHA SystemMirror V6.1 for AIX Enterprise Edition](http://www.redbooks.ibm.com/redbooks/pdfs/sg247841.pdf)
- [PowerHA SystemMirror for AIX 7.2](https://www.ibm.com/support/knowledgecenter/en/SSPHQG_7.2/navigation/welcome.html)
- [IBM PowerHA SystemMirror for AIX Cookbook](http://www.redbooks.ibm.com/abstracts/sg247739.html)
- [PowerHA SystemMirror for AIX on Fix Central](https://www-945.ibm.com/support/fixcentral/options?selectionBean.selectedTab=find&selection=Cluster+software%3bibm%2fOther+software%2fPowerHAClusterManager)

## IBM i
{: #migration-ibmi}

Learn about migration strategies that are specific to IBM i systems.

### Backup Recovery and Media Services (BRMS) and Cloud Storage (ICC)
{: #ibmi-brms-icc}

Image catalogs are created out of objects that are backed up by using optical devices. These catalogs must be transferred to the IBM Cloud by using some of the migration strategies described earlier (MDM, ICOS, Aspera, NFS server, etc.) and then restored on the IBM Cloud instance. BRMS is an IBM i product that can be used to automate activities that help define and process your backup, recovery, and media management operations. The ICC product can be integrated with BRMS to move and retrieve objects from remote locations, including ICOS.

The following steps detail how to migrate your OS and data from an on-premises system to the {{site.data.keyword.powerSys_notm}} environment. Keep in mind that most of these steps can be automated by using BRMS and ICC.

1. Create your IBM i VM in the IBM Cloud.
1. Create a virtual tape and *IMGCLG* on that deployed VM.
1. Create a virtual tape and *IMGCLG* on the on-premises system.
   1. Perform an operating system save by performing the following operation, `GO LICPGM Option 40`.
1. Transfer or FTP the images to the IBM Cloud. You can accomplish this by using some of the previously mentioned migration strategies (MDM,ICOS, Aspera, etc).
1. Restore or slip the installation of the OS to get the base OS to the same level as it was on your on-premises system.
1. Migrate your remaining data.

For more information, see [Data backup and recovery by using BRMS and IBM Cloud Storage Solutions for i](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8backupandrecoveryusingBRMSandICC.htm) and [BRMS with Cloud Storage Solutions for i considerations and requirements](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_74/rzai8/rzai8brmscloudrequireandconsider.htm).

### Logical Replication with Geographic Mirroring and PowerHA SystemMirror for AIX Enterprise Edition
{: #logical-rep-glvm}

Geographic Mirroring (GeoMirroring) enables IBM i disk mirroring technology to multiple systems environments and supports host-based and logical replication across geographically distant sites. Geomirroring supports synchronous and asynchronous modes. You can integrate PowerHA SystemMirror (Enterprise Edition) to network monitoring and automated failover support. For more information, see the following links:

- [Geographic mirroring](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_73/rzaue/rzalygeographicmirror.htm)
- [IBM PowerHA SystemMirror for i: Using Geographic Mirroring](https://www.redbooks.ibm.com/redbooks/pdfs/sg248401.pdf)
