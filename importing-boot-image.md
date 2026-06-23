---

copyright:
  years: 2024, 2026 

lastupdated: "2026-06-23"

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

You can import a custom boot image by using the {{site.data.keyword.powerSysFull}} user interface, CLI, or API. All data centers use **Tier 0**, **Tier 1**, **Tier 3**, and **Fixed IOPs** storage types. After you create a storage volume, you cannot change its storage type. A virtual server instance (VSI) can have disks from multiple storage types. Large boot images take time to import successfully. You might experience a delay in receiving a confirmation message.
{: shortdesc}

Image import requires Hash-Based Message Authentication Code (HMAC) access and secret keys to access your IBM Cloud Object Storage bucket. To generate HMAC keys for your IBM Cloud Object Storage bucket, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
{: important}

The {{site.data.keyword.powerSys_notm}} Job feature tracks long-running asynchronous operations like VSI capture, image export, and image import across multiple workspaces in your cloud account.

The {{site.data.keyword.powerSys_notm}} VSI capture, image export, and image import features are restricted to one operation at a time per {{site.data.keyword.powerSys_notm}} workspace. If you submit one of these operations successfully, you cannot submit another operation (VSI capture, image export, or image import) until the previous operation completes.
{: important}

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} user interface
{: #console-import-image}
{: help}
{: support}

To import a boot image by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type {{site.data.keyword.powerSys_notm}} and click the {{site.data.keyword.powerSys_notm}} tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. Select the workspace where you want to import the boot image. The **Virtual server instances** page of the selected workspace is displayed.

5. Click **Boot images** in the navigation panel, then click **Import image**. The Import boot image panel is displayed.

6. In the Import boot image panel, complete the following steps in the **Source** section:

   1. Select the image OS from the **Image OS** drop-down list.

      If you select a customized SAP HANA or SAP NetWeaver image, select the self-certification checkbox.

   2. Select the region where your image is stored from the **Region** drop-down list.

   3. Enter the file name of the image in the **Image filename** field. The image file name must not contain spaces. Supported file formats are `tar` and `ova`. You can compress image files by using `gzip`. The supported file name extensions are `.ova`, `.ova.gz`, `.tar`, `.tar.gz`, and `.tgz`. You must use the private endpoint domain. For example, `Aix_7200-03-02-1846_cldrdy_112018.ova.gz`.

   4. Enter the name of your bucket in the **Bucket name** field. Optionally, you can specify folder paths within the bucket by using the format `<bucketName>/optional/folders`. Optional folders are created automatically if they do not exist.

      To identify your bucket name, click the **menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > *Cloud Object Storage name* > Buckets**.

   5. Enter your HMAC access key in the **HMAC access key** field.

      To identify your access key, select the **menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > *Cloud Object Storage name* > Service credentials > View credentials**. Copy the `access_key_id` value and paste it into the **HMAC access key** field.

   6. Enter your HMAC secret access key in the **HMAC secret access key** field.

      To identify your secret key, click the **menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > *Cloud Object Storage name* > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into the **HMAC secret access key** field.

   7. Set **Validate import with checksum file** to **On** to validate the import file against the checksum file. You can generate the checksum file while you export the image files to the IBM Cloud Object Storage bucket. Place the checksum file and import images in the same bucket.

      The checksum file name is based on the name of the imported image file and uses the `.sha256` file extension. For more information about generating a checksum file, see [Using the Power Virtual Server user interface to capture and export a VM](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export).

      If you are creating your own image, you can create a checksum file and place the checksum file with your own image in the same bucket. You can generate the checksum file by using the `shasum -a 256 <filename>` or `sha256sum <filename>` command.

      Validating an import file against the checksum file might increase the import time.
      {: note}

7. Click **Next**.

8. Enter the following information in the **Destination** section:

   1. In the **Custom image name** field, enter a name for the imported image.

   2. Optional: In the **User tags** field, enter tags. If you use user tags for billing, consider using **key:value** pairs, such as `costctr:124`.

      User tags are visible account-wide. Do not include sensitive data in tag names.
      {: note}

   3. In the **Tier** field, select one of the following storage type options:
      - **Tier 0 (25 IOPs / GB)**
      - **Tier 1 (10 IOPs / GB)**
      - **Tier 3 (3 IOPs / GB)**
      - **Fixed IOPs (5000 IOPs)**

      **Tier 1** uses NVMe-based flash storage and **Tier 3** uses SSD flash storage.

      A VSI cannot have disks from both **Tier 1** and **Tier 3** storage types.
      {: note}

   4. In the **Storage pool** field, select a storage pool placement option. One or more custom image storage volumes are placed in the storage pool based on the storage pool placement options (auto-select, affinity, or anti-affinity) that you choose. The boot volume of any VSI that is deployed by using this image is created in the same storage pool. For more information about storage volumes, see [Adding and managing storage volumes](/docs/power-iaas?topic=power-iaas-modifying-instance#modifying-volume-network).

      The following storage pool placement options are available:

      - **Auto-select**: Automatically creates the storage volume in a storage pool with sufficient capacity.

      - **Affinity**: Identifies the storage pool that must be used to place the boot volumes, based on an existing PVM instance (VSI) or storage volume from your account. The custom image storage volumes are placed in the same storage pool where the affinity object resides. If you use a PVM instance as the affinity object, the storage pool that is selected to place the boot volumes is based on the root (boot) volume of the PVM instance.

      - **Anti-affinity**: Identifies one or more storage pools that you want to exclude from selection. The excluded storage pools are not considered when boot volumes are placed based on the existing PVM instances (VSIs) or storage volumes in your account. While you choose a storage pool to create the custom image storage volumes, the storage pools in which the list of anti-affinity objects reside are selected. If you use PVM instances as the anti-affinity objects, the storage pools are excluded depending on the root (boot) volume of each PVM instance.

9. Click **Import image**.

The new boot image is listed on the **Boot images** page.

You can use the imported boot image to create a {{site.data.keyword.powerSys_notm}} virtual server instance.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-import-image}

You can use the [`ibmcloud pi image import`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command to import an image from IBM Cloud Object Storage.

Example command syntax:

```sh
ibmcloud pi image import IMAGE_NAME --image-path IMAGE_PATH --os-type OS_TYPE --access-key KEY --secret-key KEY [--bucket BUCKET_NAME] [--region REGION_NAME] [--json]
```
{: pre}

Where:

`IMAGE_NAME`
:   The name for the imported image.

`IMAGE_PATH`
:   The path to the image file in the bucket.

`OS_TYPE`
:   The operating system type.

`KEY`
:   Your HMAC access and secret keys.

`BUCKET_NAME`
:   The Cloud Object Storage bucket name.

`REGION_NAME`
:   The region where your bucket resides.

To view the newly imported image, use the [`ibmcloud pi image`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image) command.

Example command syntax:

```sh
ibmcloud pi images [--long] [--json]
```
{: pre}

To import a customized SAP HANA or SAP NetWeaver image, use the [`-d, --import-details strings`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} API
{: #api-import-image}

To import a boot image from IBM Cloud Object Storage by using the API, use the [Create an cos-image import job](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-post){: external} method.

To import a customized SAP HANA or SAP NetWeaver image, specify the following image details:

```text
"importDetails":{
   "licenseType":"byol",
   "product":"Hana",
   "vendor":"SAP"
}
```
{: codeblock}

## Viewing boot image import results
{: #view-import-results}

After you start a boot image import operation, the **Status** column on the **Boot images** page shows the import progress. To view more details, click **View details** to open the **Ongoing job status** dialog. The following information is displayed:

- Job ID
- Operation type
- Input resource
- Creation time
- Steps completed

To view details of an image import job by using the CLI, use the [`ibmcloud pi image import-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import-show) command.

To view the image import status by using the API, use the [Get detail of last cos-image import job](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v1-cloudinstances-cosimages-get){: external} method.

## Downloading a boot image from Cloud Object Storage
{: #download-boot-image-cos}

To download your image after importing it, navigate to the **Resource List** in the IBM Cloud dashboard, and access your **Cloud Object Storage** workspace. In the bucket where your image is stored, select the image file that you want to download and select **Download objects**. For more information about the Cloud Object Storage CLI command, see [Download an object](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#ic-download-object){: external}.
