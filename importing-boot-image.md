---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-31"

keywords: boot image, import, upload boot image, storage types, regions, tier 1, tier 3, ssd, nvme

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

# Importing a boot image
{: #importing-boot-image}

You can import an AIX or IBM i boot image by using the {{site.data.keyword.powerSysFull}} CLI or the console. All data centers use **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs want to select **Tier 3**. The storage types cannot be changed once the volume is created. A VM cannot have disks from both storage types. Large boot images take time to successfully import. You might experience a delay before receiving a confirmation message.
{: shortdesc}

Image import requires HMAC keys (access, secret) in order to access your IBM Cloud Object Storage bucket. If you have not already generated your HMAC keys you can follow the instructions in [Using IBM COS HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
{: important}

A new {{site.data.keyword.powerSysFull}} Job feature is introduced to track long running asynchronous operations like VM Capture, Image Export, and Image Import. As part of this feature, new version of Power Cloud API and CLI enhancements have been introduced for these operations. To view the new Power Cloud API for Image Import, see [Create a new image from available images you have stored in IBM COS](/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-post). CLI enhancements include changes to the existing [`ibmcloud pi image-import`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import) command and a new [`ibmcloud pi jobs`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-jobs) command.

The new IBM® Power Systems™ Virtual Server VM Capture, Image Export, and Image Import features are restricted to one operation at a time per IBM® Power Systems™ Virtual Server Service. If one of these operations is submitted successfully, then another new operation for VM Capture, Image Export, and Image Import cannot be submitted until the previous operation is complete.

You can use the IBM® Power Systems™ Virtual Server legacy REST APIs for VM Capture, Image Export, and Image Import until 1 October 2022. You must plan to transition to the new IBM® Power Systems™ Virtual Server REST APIs or CLI commands within the sunset period.
{: note}

## Using the {{site.data.keyword.powerSys_notm}} CLI to import a boot image
{: #cli-import-image}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} CLI. For more information, see the [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import).

1. To import an AIX or IBM i image from IBM Cloud Object Storage, use the [`ibmcloud pi image-import`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import) command.

2. Find your newly imported image by using the `ibmcloud pi images` command.

    ```shell
    ibmcloud pi images [--long] [--json]
    ```
    {: codeblock}

## Using the Power Systems Virtual Server user interface to import a boot image
{: #console-import-image}
{: help}
{: support}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} user interface.

The **Image file name** field supports the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.
{: note}

1. Click **Boot images**, then **Import image**.

2. After you click **Import**, enter all of the required information. Refer to the table at the bottom of the page to complete the necessary fields to import a boot image.

3. Find your newly uploaded boot image in **Boot images**.

| Field | Description |
| ------| ------------|
| Catalog image name | Enter the name that you want your imported image to display in your image name catalog.|
| Storage type | Select whether you want **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** for the storage type. A VM cannot have disks from both **Tier 1** and **Tier 3** storage types.|
| Storage pool | The custom image storage volume(s) will be placed in the storage pool based on your selection of one of the available storage pool placement options (auto-select, affinity, or anti-affinity). The boot volume of any VM deployed by using this image will be deployed in the same storage pool. For more information about storage volumes, see [Adding and managing storage volumes](/docs/power-iaas?topic=power-iaas-modifying-server#adding-managing-volume).| 
| Auto-select pool | Select **Auto-select pool** to automatically create the storage volume in a pool that has sufficient capacity. |
| Affinity | Use Affinity to identify the storage pool to use based on an existing PVM instance (VM) or volume from your account. The custom image storage volumes will be placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object the storage pool that is selected is based on the PVM instance’s root (boot) volume. |
| Anti-affinity | Use Anti-affinity to identify one or more storage pools that you want excluded from getting selected based on one or more existing PVM instances (VMs) or volumes from your account. The storage pools where the list of anti-affinity object(s) reside will not be selected when choosing a storage pool to create the custom image storage volume(s) in. . If you are using PVM instances as the anti-affinity objects the storage pool that will get excluded are based on each PVM instance’s root (boot) volume provided. |
| Source details (Cloud storage) | Use the following fields to set the Cloud storage details.|
| Region | Select either **us-east**, **us-south**, **ca-tor**, **eu-de**, or **eu-gb**, **au-syd**, **jp-tok**, **jp-osa** for the region.|
| Image file name | Enter the file name of the image. The image file name must not contain spaces. Supported file formats are *tar* and *ova*. You can compress image files by using *gzip*. The supported file name extensions are *.ova*, *.ova.gz*, *.tar*, *.tar.gz* and *.tgz*. You must use the private endpoint domain. For example, `Aix_7200-03-02-1846_cldrdy_112018.gz`. 
| Bucket name | Sub folders can be used and specified as *bucketName/optional/folders*. Optional folders are created automatically if they don’t exist. To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Buckets**. |
| Cloud Object Storage access key | To identify your access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field.|
| Cloud Object Storage secret key | To identify your secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field.|
{: caption="Table 1. Boot images options" caption-side="bottom"}
