---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-31"

keywords: boot image, import, upload boot image, storage types, regions, tier 1, tier 3, ssd, nvme

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

# Importing a boot image
{: #importing-boot-image}

You can import an AIX or IBM i boot image by using the {{site.data.keyword.powerSysFull}} CLI or the console. All data centers use **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs want to select **Tier 3**. The storage types cannot be changed once the volume is created. A VM cannot have disks from both storage types. Large boot images take time to successfully import. You might experience a delay before receiving a confirmation message.
{: shortdesc}

If you previously deployed a VM on an old storage type (**SSD** or **standard**), no action is required. Your VM continues to run by using the old storage type. You can also add new disks from those legacy tiers.

You must first generate [Secret and Access keys](/docs/power-iaas?topic=power-iaas-deploy-custom-image#access-keys) to import a boot image.
{: important}

A new {{site.data.keyword.powerSysFull}} Job feature is introduced that you can use to track long running asynchronous operations like VMCapture, Image Export, and Image Import. As part of this feature, new version of API and CLI enhancements are introduced for the Image Import operation. To view the new API for Image Import, see [Create a new image from available images in COS](/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-post). CLI enhancements include changes to the existing [`ibmcloud pi image-import`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import) command and a new [`ibmcloud pi jobs`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-jobs) command.

You can import only a single VM image at a time per {{site.data.keyword.powerSysFull}} instance. If you attempt another operation when one operation is still in progress, an error is displayed. You can use the {{site.data.keyword.powerSysFull}} legacy REST APIs for Image Import until 1st October 2022. You must plan to transition to the new {{site.data.keyword.powerSysFull}} REST APIs or CLI commands within the sunset period.
{: note}

## Using the {{site.data.keyword.powerSys_notm}} CLI to import a boot image
{: #cli-import-image}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} CLI. For more information, see the [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import).

1. To import an AIX or IBM i image from IBM Cloud Object Storage, use the `ibmcloud pi image-import` command.

    ```shell
    ibmcloud pi image-import IMAGE_NAME --image-path PATH --os-type OSTYPE --access-key KEY --secret-key KEY [--json]
    ```
    {: codeblock}

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

    ![Completing the boot image fields](./images/console-boot-image-fields.png "Completing the boot image fields"){: caption="Figure 1. Completing the boot image fields" caption-side="bottom"}

3. Find your newly uploaded boot image in **Boot images**.

| Field | Description |
| ------| ------------|
| Catalog image name | Enter the name that you want displayed in your catalog.|
| Storage type | Select whether you want **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** for the storage type. A VM cannot have disks from both **Tier 1** and **Tier 3** storage types.|
| Region | Select either **us-east**, **us-south**, **br-sao**, **ca-tor**, **ca-mon**, **eu-de**, or **eu-gb**, **au-syd**, **jp-tok**, **jp-osa** for the region.|
| Image file name | Enter the file name of the image. The image file name must not contain spaces. Supported file formats are *tar* and *ova*. You can compress image files by using *gzip*. The supported file name extensions are *.ova*, *.ova.gz*, *.tar*, *.tar.gz* and *.tgz*. You must use the private endpoint domain. For example, `Aix_7200-03-02-1846_cldrdy_112018.gz`. <!-- You can identify the endpoint domain, bucket name, and file name by selecting **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage**. -->
| Bucket name | Sub folders can be used and specified as *bucketName/optional/folders*. Optional folders are created automatically if they don’t exist. Optional folders can be added during an [export image](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export) operation to Cloud Object Storage. To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Buckets**. |
| Cloud Object Storage access key | To identify your access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field.|
| Cloud Object Storage secret key | To identify your secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field.|
