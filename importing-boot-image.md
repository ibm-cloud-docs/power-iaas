---

copyright:
  years: 2024

lastupdated: "2025-03-28"

keywords: importing a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to, boot image, import, upload boot image, storage types, regions, tier 1, tier 3, ssd, nvme

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Importing a boot image
{: #importing-boot-image}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

You can import a custom boot image by using the {{site.data.keyword.powerSysFull}} CLI or the console. All data centers use **Tier 0**, **Tier 1**, **Tier 3**, and **Fixed IOPs** storage types. After the volume is created, you cannot change the storage types. A virtual machine (VM) can have disks from multiple storage types. Large boot images take time to successfully import. You might experience a delay in receiving a confirmation message.
{: shortdesc}

Image import requires Hash-Based Message Authentication Code (HMAC) keys (access, secret) to access your IBM Cloud Object Storage bucket. To generate your HMAC keys, see [Using IBM COS HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
{: important}

The {{site.data.keyword.powerSysFull}} Job feature tracks long-running asynchronous operations like VM capture, image export, and image import across multiple workspaces in your cloud account.

As part of this Job feature, the following API and CLIs are available:
- API for image import - [Create a new image from available images you have stored in IBM COS](/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-post){: external}.
- CLI command - [`ibmcloud pi image import`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import){: external}.
- CLI command [`ibmcloud pi jobs`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-job){: external}.

The {{site.data.keyword.powerSys_notm}} VM capture, image export, and image import features are restricted to one operation at a time per {{site.data.keyword.powerSys_notm}} workspace. If one of these operations is submitted successfully, then another new operation (VM capture, image export, and image import) cannot be submitted until the previous operation is complete.
{: important}


## Using the {{site.data.keyword.powerSys_notm}} API to import a boot image
{: #api-import-image}

To import a boot image, you can use the APIs listed in the [Create a new image from available images you have stored in IBM COS](/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-post){: external} topic.


   To import a customized SAP HANA or SAP NetWeaver image, specify the following image details:

```text
      "importDetails":{
         "licenseType":"byol",
   "product":"Hana",
         "vendor":"SAP"
      }
```
{: codeblock}



## Using the {{site.data.keyword.powerSys_notm}} CLI to import a boot image
{: #cli-import-image}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} CLI. For more information, see the [{{site.data.keyword.powerSys_notm}} CLI Reference](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference){: external}.

1. To import a custom image from IBM Cloud Object Storage, use the [`ibmcloud pi image-import`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-image-import){: external} command.

2. Find your newly imported image by using the `ibmcloud pi images` command.

    ```text
    shell
    ibmcloud pi images [--long] [--json]
    ```
    {: codeblock}



3. To import a customized SAP HANA or SAP NetWeaver image, use the [`-d, --import-details strings`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command.


## Using the {{site.data.keyword.powerSys_notm}} user interface to import a boot image
{: #console-import-image}
{: help}
{: support}

Complete the following steps to import a boot image by using the {{site.data.keyword.powerSys_notm}} user interface.

The **Image file name** field supports the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.
{: note}

1. Click **Boot images**, then **Import image**.



   If you are importing a customized SAP HANA or SAP NetWeaver image, you must select the self-certification checkbox.
   {: note}

2. After you click **Import image**, enter all of the required information. Refer to the table at the end of the page to complete the necessary fields to import a boot image.


   Select the **Validate import with checksum file** toggle button to validate the import file against the checksum file. You can generate the checksum file while exporting the image files to the IBM Cloud Object Storage bucket. The checksum file and the import images must be placed in the same bucket. The checksum file name is based on the name of the imported image file and has the file extension `.sha256`. For more information about generating a checksum file, see [Using the Power Virtual Server user interface to capture and export a VM](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export).

   If you are creating your own image, you can create a checksum image and place it with your own image in the same bucket. One of the ways to generate the checksum image is by using the command `shasum -a 256 <filename>` or `sha256sum <filename>`.

   Validating an import file against the checksum file might add extra time to the image import process.
   {: note}


3. Find your newly uploaded boot image in **Boot images**.

4. Return to **Virtual server instances** and provision a new {{site.data.keyword.powerSys_notm}} virtual service instance. Click the arrow in the appropriate boot image tile to see your custom boot image.




| Field | Description |
| ------| ------------|
| Catalog image name | Enter the name that you want your imported image to display in your image name catalog.|
| Storage type | Select whether you want **Tier 1 (NVMe-based Flash Storage)** or **Tier 3 (SSD Flash Storage)** for the storage type. A VM cannot have disks from both **Tier 1** and **Tier 3** storage types.|
| Storage pool | One or more custom image storage volumes are placed in the storage pool based on the storage pool placement options (auto-select, affinity, or anti-affinity) that you choose. The boot volume of any VM that is deployed by using this image deploys in the same storage pool. For more information about storage volumes, see [Adding and managing storage volumes](/docs/power-iaas?topic=power-iaas-modifying-instance#modifying-volume-network).|
| Auto-select pool | Select this option to automatically create the storage volume in a pool that has sufficient capacity. |
| Affinity | Use this option to identify the storage pool that must be used to place the boot volumes, based on an existing PVM instance (VM) or storage volume from your account. The custom image storage volumes are placed in the same storage pool where the affinity object resides. If you are using a PVM instance as the affinity object, the storage pool that is selected to place the boot volumes is based on the PVM instance’s root (boot) volume. |
| Anti-affinity | Use this option to identify one or more storage pools that you want to exclude from getting selected to place the boot volumes based on one or more existing PVM instances (VMs) or storage volumes from your account. While choosing a storage pool to create the custom image storage volumes, the storage pools in which the list of anti-affinity objects reside are selected. If you are using PVM instances as the anti-affinity objects, the storage pools are excluded depending on each PVM instance’s root (boot) volume that you specified. |
| Source details (Cloud storage) | Use the following fields to set the Cloud storage details.|
| Region | Select either **us-east**, **us-south**, **ca-tor**, **eu-de**, **eu-es**, **eu-gb**, **au-syd**, **jp-tok**, **jp-osa** for the region.|
| Image file name | Enter the file name of the image. The image file name must not contain spaces. Supported file formats are `tar` and `ova`. You can compress image files by using `gzip`. The supported file name extensions are `.ova`, `.ova.gz`, `.tar`, `.tar.gz` and `.tgz`. You must use the private endpoint domain. For example, `Aix_7200-03-02-1846_cldrdy_112018.gz`.
| Bucket name | Sub folders can be used and specified as `bucketName/optional/folders`. Optional folders are created automatically if they don’t exist. To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Buckets**. |
| Cloud Object Storage access key | To identify your access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field.|
| Cloud Object Storage secret key | To identify your secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Object Storage name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field.|
{: caption="Boot images options" caption-side="bottom"}


If you' want to download your image at a later point, go to the **Resource List** in the IBM Cloud dashboard user interface, and access your **Cloud Object Storage** workspace. In the bucket where your image is stored, select the image file that you want to download and select **Download objects**. For more information about the Cloud Object Storage CLI command, see [Download an object](https://cloud.ibm.com/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli#ic-download-object){: external}.
