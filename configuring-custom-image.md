---

copyright:
  years: 2019, 2023

lastupdated: "2023-09-19"

keywords: custom image, boot image, upload image, deploy, boot volume

subcollection: power-iaas

---

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

# Deploying a custom image within a Power Systems Virtual Server
{: #deploy-custom-image}

You can bring your own customized AIX or IBM i operating system (OS) image to deploy within a IBM&reg; Power Systems&trade; Virtual Server.
{: shortdesc}

You cannot transfer an OS license from an on-premises system to a {{site.data.keyword.powerSys_notm}}. The license cost is factored into the overall hourly billing rate.
{: note}

The basic steps that are involved in deploying an instance by using a custom image are:

1. Create the custom image.
2. Store the image in your **Cloud Object Storage** account.
3. Point the {{site.data.keyword.powerSys_notm}} console to the image in the **Cloud Object Storage** and deploy the Virtual Server instance.

## Before you begin
{: #before-you-begin-deploy}

Before you can use a custom image as the boot volume, review the following information:

- You must have a basic understanding of [IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-cloud-object-storage) concepts.
- If you do not have an existing AIX or IBM i image, you can use IBM® PowerVC™ from your on-premise environment to capture and export an image for use with a {{site.data.keyword.powerSys_notm}}. For more information, see [Capturing a virtual machine](https://www.ibm.com/docs/en/powervc/2.0.1?topic=images-capturing-virtual-machine){: external} and [Exporting images](https://www.ibm.com/docs/en/powervc/2.0.2?topic=init-installing-configuring-cloud-linux){: external}. To capture and export an image by using IBM PowerVC, the PowerVC private environment must contain N_Port ID Virtualization (NPIV) data volumes. The Power Systems Virtual Servers does not support captured images from environment with shared Storage Pools (SSP) vSCSI data volumes. 
- Alternatively, if you have already deployed a virtual server instance, you can capture it and redeploy a new virtual server instance. To accomplish this, you can use the [{{site.data.keyword.cloud}} CLI](/docs/cli?topic=cli-getting-started){: external} to capture a virtual server instance.
- You must verify that your AIX, IBM i, or Linux OS technology level is supported on the Power Systems hardware that you selected in the **Machine Type** field.

For complete tutorials on migrating your AIX and IBM i workloads to Power Systems Virtual Servers, see [Migrating AIX to IBM Power Systems Virtual Servers](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Migration_Tutorial_v1.pdf){: external} and [Migrating IBM i to IBM Power Systems Virtual Servers](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Migration_Tutorial_v1.pdf){: external}.

The supported AIX and IBM i operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}. 

If you are running AIX 6.1 or IBM i 6.1, or earlier, you must first upgrade the OS to current support level before migrating to the {{site.data.keyword.powerSys_notm}}.
{: important}

To view a list of the supported AIX, IBM i, and Linux operating system technology levels, see the following system software maps:

### AIX
{: #aix-details}

The {{site.data.keyword.powerSys_notm}} offering supports AIX 7.1, or later on the S922 (9009-22A) and E980 (9080-M9S). 

Power Systems <!-- E1080 (9080-HEX) and --> S1022 (9105-22A) supports AIX 7.1 TL 5 and later.

When you view the system software maps, refer to the AIX 7.1, AIX 7.2, and AIX 7.3 information. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given. 


- [S922 (9009-22A) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-vios-only){: external}
- [E980 (9080-M9S) AIX software map](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}
- [S1022 (9105-22A) AIX software map](https://www.ibm.com/support/pages/node/6604269){: external}

<!-- - [E1080 (9080-HEX) AIX software map](https://www.ibm.com/support/pages/system-software-map-power-systems-e1080-9080-hex-and-aix-all-io-configurations){: external} -->

For more information on end of service pack support (EoSPS) dates, see [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}.
{: note}

### IBM i
{: #ibmi-details}

The {{site.data.keyword.powerSys_notm}} offering supports IBM i 7.1, or later. Clients running IBM i 6.1, or earlier, must first upgrade the OS to current support level before migrating to the Power Systems Virtual Server. IBM i 7.4 supports direct upgrades from IBM i 5.4, 6.1 or 7.1. For more information, see [Migrating to IBM i 7.2 from 5.4, 6.1 or 7.1](https://www.ibm.com/docs/en/i/7.4?topic=considerations-migrating-i-72-from-54-61-71){: external}. 

Power Systems <!-- E1080 (9080-HEX) and  -->S1022 (9105-22A) supports IBM i 7.3 and later versions. See [S922 (9009-22A), E980 (9080-M9S), and S1022 (9105-22A) software maps](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: external} for more information.
  
Learn more about the [IBM i PTF minimum levels](/docs/power-iaas?topic=power-iaas-minimum-levels) and [IBM i release lifecycle](https://www.ibm.com/support/pages/release-life-cycle){: external}

IBM i 7.1 virtual machines (VMs) supports only 64 storage volumes per VM. IBM i 7.2, and later, supports up to 127 storage volumes per VM. IBM i 7.1, IBM i 7.2, and IBM i 7.3 VMs are at end of support and are in service extension. Therefore, additional Service Extension fees apply.
{: note}

### Linux
{: #linux-details}

SUSE Linux Enterprise (SLES) and Red Hat Enterprise Linux (RHEL) are supported with the appropriate IBM Cloud environment cloud-init packages. Download the appropriate cloud-init package and configure it as per the steps documented as follows:
- [Installing and configuring cloud-init on SLES](https://www.ibm.com/docs/en/powervc/2.1.0?topic=linux-installing-configuring-cloud-init-sles){: external}.
- [Installing and configuring cloud-init on RHEL](https://www.ibm.com/docs/en/powervc/2.1.0?topic=linux-installing-configuring-cloud-init-rhel){: external}.


Power Systems <!-- E1080 (9080-HEX) and  -->S1022 (9105-22A) supports: RHEL 8.4 (and later) and SLES 15 SP3 (and later) versions.

For SAP applications, ensure that you use an IBM stock OS image for SAP. These images are certified for SAP application use; bring your own images are not supported. To learn more about SAP applications with PowerVS, please see these [Must-Reads](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-planning-items){: external} before you start deployment. 
{: note}

## Creating an IBM Cloud Object Storage bucket
{: #cloud-storage-bucket}

1. Type **object storage** into the catalog's search box and select **Cloud Object Storage**.

2. Give the service a name, add tags (if wanted), select your pricing plan and click **Create**.

3. After you click **Create**, you are taken to the **Cloud Object Storage** landing page. Select **Create Bucket**.

4. From here, you are automatically redirected to the workspace where you can start creating buckets. Your {{site.data.keyword.cos_short}} instances are listed under **Storage** in the **Resource List**. The terms *resource instance* and *workspace* refer to the same concept, and can be used interchangeably.

5. Choose a unique name. All buckets in all regions across the globe share a single namespace. Ensure that you have the correct permissions to create a bucket.

    When you create buckets or add objects, be sure to avoid the use of Personally Identifiable Information (PII). PII is information that can identify any user (natural person) by name, location, or any other means.
    {: note}

6. First, choose a wanted level of *resiliency*, and then a *location* where you would like your data to be physically stored. Resiliency refers to the scope and scale of the geographic area across which your data is distributed. *Cross Region* resiliency spreads your data across several metropolitan areas, while *Regional* resiliency spreads data across a single metropolitan area. A single data center distributes data across devices within a single site only.

7. Choose the bucket's *storage class*, which is a reflection of how often you expect to read the stored data and determines billing details. Follow the **Create** link to create and access your new bucket.

    Buckets are a way to organize your data, but they are not the only way. Object names (often referred to as object keys) can use one or more forward slashes for a directory-like organizational system. You then use the portion of the object name before a delimiter to form an object prefix, which is used to list related objects in a single bucket through the API.
    {: tip}

Objects are limited to 200 MB when uploaded through the console unless you use the Aspera High-Speed Transfer plug-in. Larger objects (up to 10 TB) can also be split into parts and uploaded in parallel using the API. Object keys can be up to 1024 characters in length, and it's best to avoid any characters that might be problematic in a web address. These special characters (*?*, *=*, *<*, etc.) might cause unwanted behavior if not URL-encoded. For more information, see the [Cloud Object Storage tutorial](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).

## Generating secret and access keys with Hash-based Message Authentication Code (HMAC)
{: #access-keys}

1. You can generate secret and access keys when you create the service credentials for the IBM Cloud Object Storage. To create the service credentials, you must have `Writer` access for the **Object Storage** bucket.

2. Select **New credential** under **Service credentials** in the **Cloud Object Storage** pane.

3. Complete all of the wanted fields for adding a credential. Remember to check **Include HMAC Credential** for obtaining a **Hash-based Message Authentication Code (HMAC)** credential.

4. Find your new service credential in the service credentials table.

    To view your credential information, such as your secret and access keys, click the arrow to the right of **View credentials**. For more information, see [Service credentials](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) and [Bucket permissions](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).

## Using a custom boot image to provision a new instance
{: #upload-custom-boot}
{: help}
{: support}

Complete the following steps to provision a new instance by using a custom boot image. For more information about importing a custom boot image by using the {{site.data.keyword.powerSys_notm}} CLI, see [Importing a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image#cli-import-image). Large boot images take time to successfully import. You might experience a delay before you receive a confirmation message.

1. Before you create a new {{site.data.keyword.powerSys_notm}} instance, go to **Boot images** and click **Import**.

2. After you click **Import**, refer to the following table to complete the **Import boot image** fields:
    The **Image file name** field supports the following formats: *.ova*, *.ova.gz*, *.tar*, *.tar.gz* and *.tgz*.
    {: important}

| Field | Description |
| ------| ------------|
| Catalog image name | Enter the name that you want displayed in your catalog.|
| Storage type | Select whether you want **Tier 1** or **Tier 3** for the storage type. A VM cannot have disks from both **Tier 1** and **Tier 3** storage types. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).
| Region | Select either **us-east**, **us-south**, **br-sao**, **ca-tor**, **ca-mon**, **eu-de**, or **eu-gb**, **au-syd**, **jp-tok**, **jp-osa** for the region. |
| Image file name | Enter the file name of the image. The image file name must not contain spaces. Supported file formats are *tar* and *ova*. You can compress image files by using *gzip*. The supported file name extensions are *.ova*, *.ova.gz*, *.tar*, *.tar.gz* and *.tgz*. You must use the private endpoint domain. For example, `Aix_7200-03-02-1846_cldrdy_112018.gz`.
| Bucket name | Sub folders can be used and specified as *bucketName/optional/folders*. Optional folders are created automatically if they don’t exist. Optional folders can be added during an [export image](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export) operation to Cloud Object Storage. To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Buckets**. |
| Cloud Object Storage access key | To identify your access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field. |
| Cloud Object Storage secret key | To identify your secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field. |
{: caption="Table 1. Importing a boot image" caption-side="bottom"} 

1. Return to **Virtual server instances** and provision a new {{site.data.keyword.powerSys_notm}} instance. Click the arrow in the appropriate boot image tile to see your custom boot image.

    If you'd like to download your image at a later point, go to the **Resource List** in the {{site.data.keyword.powerSys_notm}} user interface. Once there, access your **Cloud Object Storage** workspace. In the bucket where your image is stored, select the image file that you want to download and select **Download objects**. See [Download an object](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-download-object) for the Cloud Object Storage CLI command.
    {: tip}
