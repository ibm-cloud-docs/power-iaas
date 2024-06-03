---

copyright:
  years: 2024

lastupdated: "2024-05-22"

keywords: importing a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to, boot image, import, upload boot image, storage types, regions, tier 1, tier 3, ssd, nvme

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Importing a boot image
{: #importing-boot-image}

You can import a custom boot image by using the {{site.data.keyword.powerSysFull}} CLI or the console. All data centers use **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs can select **Tier 3**. The storage types cannot be changed once the volume is created. A VM cannot have disks from both storage types. Large boot images take time to successfully import. You might experience a delay before receiving a confirmation message.
{: shortdesc}

Image import requires HMAC keys (access, secret) to access your IBM Cloud Object Storage bucket. If you have not already generated your HMAC keys you can follow the instructions in [Using IBM COS HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
{: important}

The {{site.data.keyword.powerSysFull}} Job feature tracks long-running asynchronous operations like VM capture, image export, and image import across multiple workspaces in your cloud account.

As part of this Job feature, the following API and CLIs are available:
- API for image import - [Create a new image from available images you have stored in IBM COS](/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-post).
- CLI command - [`ibmcloud pi image import`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-image-import).
- CLI command [`ibmcloud pi jobs`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference-v1#ibmcloud-pi-job).

The {{site.data.keyword.powerSys_notm}} VM capture, image export, and image import features are restricted to one operation at a time per {{site.data.keyword.powerSys_notm}} workspace. If one of these operations is submitted successfully, then another new operation (VM capture, image export, and image import) cannot be submitted until the previous operation is complete.
{: important}

## Using the {{site.data.keyword.powerSys_notm}} CLI to import a boot image
{: #cli-import-image}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} CLI. For more information, see the [{{site.data.keyword.powerSys_notm}} CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference).

1. To import a custom image from IBM Cloud Object Storage, use the [`ibmcloud pi image-import`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import) command.

2. Find your newly imported image by using the `ibmcloud pi images` command.

    ```shell
    ibmcloud pi images [--long] [--json]
    ```
    {: codeblock}

## Using the {{site.data.keyword.powerSys_notm}} user interface to import a boot image
{: #console-import-image}
{: help}
{: support}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} user interface.

The **Image file name** field supports the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.
{: note}

1. Click **Boot images**, then **Import image**.

  <!--Q2
   [Q2-2024 update start]{: tag-teal} If you are importing customized SAP HANA or SAP NetWeaver image, you must select the self-certification checkbox.[Q2-2024 update end]{: tag-teal}
   {: note}
  -->
  <!-- Q2 -->

2. After you click **Import image**, enter all of the required information. Refer to the table at the bottom of the page to complete the necessary fields to import a boot image.

3. Find your newly uploaded boot image in **Boot images**.

<!--4. Return to **Virtual server instances** and provision a new {{site.data.keyword.powerSys_notm}} virtual service instance. Click the arrow in the appropriate boot image tile to see your custom boot image.-->
<!-- Q2 -->


| Field | Description |
| ------| ------------|
| Catalog image name | Enter the name that you want your imported image to display in your image name catalog.|
| Storage type | Select whether you want **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** for the storage type. A VM cannot have disks from both **Tier 1** and **Tier 3** storage types.|
| Storage pool | The custom image storage volume(s) will be placed in the storage pool based on the storage pool placement options (auto-select, affinity, or anti-affinity) that you choose. The boot volume of any VM that is deployed by using this image will be deployed in the same storage pool. For more information about storage volumes, see [Adding and managing storage volumes](/docs-draft/power-iaas?topic=power-iaas-modifying-instance#modifying-volume-network).|
| Auto-select pool | Select this option to automatically create the storage volume in a pool that has sufficient capacity. |
| Affinity | Use this option to identify the storage pool that must be used to place the boot volumes, based on an existing PVM instance (VM) or storage volume from your account. The custom image storage volumes will be placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object, the storage pool that is selected to place the boot volumes is based on the PVM instance’s root (boot) volume. |
| Anti-affinity | Use this option to identify one or more storage pools that you want to exclude from getting selected to place the boot voulmes based on one or more existing PVM instances (VMs) or storage volumes from your account. While choosing a storage pool to create the custom image storage volume(s), the storage pools in which the list of anti-affinity object(s) reside will not be selected. If you are using PVM instances as the anti-affinity objects, the storage pools are excluded depending on each PVM instance’s root (boot) volume that you specified. |
| Source details (Cloud storage) | Use the following fields to set the Cloud storage details.|
| Region | Select either **us-east**, **us-south**, **ca-tor**, **eu-de**, **eu-es**, **eu-gb**, **au-syd**, **jp-tok**, **jp-osa** for the region.|
| Image file name | Enter the file name of the image. The image file name must not contain spaces. Supported file formats are *tar* and *ova*. You can compress image files by using *gzip*. The supported file name extensions are *.ova*, *.ova.gz*, *.tar*, *.tar.gz* and *.tgz*. You must use the private endpoint domain. For example, `Aix_7200-03-02-1846_cldrdy_112018.gz`.
| Bucket name | Sub folders can be used and specified as *bucketName/optional/folders*. Optional folders are created automatically if they don’t exist. To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Buckets**. |
| Cloud Object Storage access key | To identify your access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field.|
| Cloud Object Storage secret key | To identify your secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field.|
{: caption="Table 1. Boot images options" caption-side="bottom"}

<!--The following content is not in PowerVS but retaining it to get comments from TR-->
If you'd like to download your image at a later point, go to the **Resource List** in the IBM Cloud dashboard user interface, and access your **Cloud Object Storage** workspace. In the bucket where your image is stored, select the image file that you want to download and select **Download objects**. See [Download an object](https://cloud.ibm.com/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-download-object){: external} for the Cloud Object Storage CLI command.
