---

copyright:
  years: 2024, 2026 

lastupdated: "2026-07-10"

keywords: importing a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to, boot image, import, upload boot image, storage types, regions, tier 1, tier 3

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Importing a boot image
{: #importing-boot-image}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

You can import a boot image when you want to use a custom operating system (OS) image instead of an IBM-provided stock image. After importing, you can use the boot image to create a {{site.data.keyword.powerSys_notm}} virtual server instance. You can import a boot image from an IBM Cloud Object Storage (COS) bucket by using the {{site.data.keyword.powerSysFull}} user interface, CLI, or API.
{: shortdesc}

When you import a boot image, you select a storage tier and storage pool for the image. {{site.data.keyword.powerSys_notm}} places the boot volumes that are created from this imported boot image in the storage pool that you specify during the import. The storage tier and storage pool cannot be changed after import. A virtual server instance (VSI) can have disks from multiple storage types. All data centers use Tier 0, Tier 1, Tier 3, and Fixed IOPs storage types.

Large boot images take time to import successfully. You might experience a delay in receiving a confirmation message.
{: note}

VSI capture, image export, and image import are long-running asynchronous operations that {{site.data.keyword.powerSys_notm}} monitors across all workspaces in your account. Only one of these operations can run at a time per workspace. You cannot start a new operation until the ongoing operation completes.
{: important}

## Before you begin
{: #before-you-begin-import}

Before you import a boot image, ensure the following prerequisites are in place:

- You have uploaded your boot image file to an IBM Cloud Object Storage bucket. Supported file formats are `.ova`, `.ova.gz`, `.tar`, `.tar.gz`, and `.tgz`. For more information, see [Create some buckets to store your data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets){: external}.
- You have generated HMAC credentials for your COS instance. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main){: external}.
- You have a {{site.data.keyword.powerSys_notm}} workspace.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} user interface
{: #console-import-image}
{: help}
{: support}

To import a boot image by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}** and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. Select the workspace to which you want to import the boot image. The **Virtual server instances** page of the selected workspace is displayed.

5. Click **Boot images** in the navigation panel, then click **Import image**. The Import boot image panel is displayed.

6. In the Import boot image panel, complete the following steps in the **Source** section:

   1. Select the image OS from the **Image OS** drop-down list.

      If you select a customized SAP HANA or SAP NetWeaver image, select the self-certification checkbox.

   2. From the **Region** drop-down list, select the region where your COS bucket is located.

   3. Enter the file name of the image in the **Image filename** field. The image file name must not contain spaces.

      Supported file formats include `tar` and `ova`. You can compress image files by using `gzip`. The supported file name extensions are `.ova`, `.ova.gz`, `.tar`, `.tar.gz`, and `.tgz`. For example, `Aix_7200-03-02-1846_cldrdy_112018.ova.gz`.

   4. Enter the name of your bucket in the **Bucket name** field. If your image file is stored in a subfolder within the bucket, specify the full path by using the `bucketName/optional/folders` format.

      To identify your bucket name, go to **Navigation menu > Resource list > Storage**, and click your Cloud Object Storage instance name. Your buckets are listed in the left navigation.

   5. Copy the `access_key_id` value from your COS service credentials and paste it into the **HMAC access key** field.

      To find your service credentials, go to **Navigation menu > Resource list > Storage**, click your Cloud Object Storage instance name, and then go to **Service credentials > View credentials**.

   6. Copy the `secret_access_key` value from your COS service credentials and paste it into the **HMAC secret access key** field.

   7. Set **Validate import with checksum file** to **On** to validate the import file against the checksum file. You must store the checksum file and the imported boot image in the same bucket.

      You can generate the checksum file while you export the image files to the IBM Cloud Object Storage bucket.

      The checksum file name is based on the name of the imported boot image file and uses the `.sha256` file extension. For more information about generating a checksum file, see [Using the Power Virtual Server user interface to capture and export a VM](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export).

      If you create your own boot image, you can create a checksum file and store the checksum file with your boot image in the same bucket. You can generate the checksum file by using the `shasum -a 256 <filename>` or `sha256sum <filename>` command.

      Validating an import file against the checksum file might increase the import time.
      {: note}

7. Click **Next**.

8. Enter the following information in the **Destination** section:

   1. In the **Custom image name** field, enter a name for the imported boot image.

   2. Optional: In the **User tags** field, enter tags to organize or identify this boot image.

      User tags are visible account-wide. Do not include sensitive data in tag names.
      {: note}

   3. In the **Tier** field, select one of the following storage type options:
      - **Tier 0 (25 IOPs / GB)**
      - **Tier 1 (10 IOPs / GB)**
      - **Tier 3 (3 IOPs / GB)**
      - **Fixed IOPs (5000 IOPs)**

      A VSI cannot use **Tier 1** and **Tier 3** storage types at the same time. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).
      {: note}

   4. In the **Storage pool** field, select a storage pool placement option.

      {{site.data.keyword.powerSys_notm}} places one or more custom image storage volumes in the storage pool based on the option that you select: auto-select, affinity, or anti-affinity. The boot volume of any VSI that you deploy by using this image is created in the same storage pool. For more information about storage volumes, see [Adding and managing storage volumes](/docs/power-iaas?topic=power-iaas-modifying-instance#modifying-volume-network).

      The following storage pool placement options are available:

      - **Auto-select**: Automatically creates the storage volume in a storage pool with sufficient capacity.

      - **Affinity**: Identifies the storage pool to use for placing the boot volumes, based on an existing VSI or storage volume from your account. The custom image storage volumes are stored in the same storage pool in which the affinity object exists. If you use a VSI as the affinity object, the storage pool is determined based on the boot volume of that VSI.

      - **Anti-affinity**: Identifies one or more storage pools that you want to exclude. {{site.data.keyword.powerSys_notm}} does not consider the excluded storage pools when placing boot volumes, based on existing VSIs or storage volumes in your account. When you select this option, {{site.data.keyword.powerSys_notm}} excludes the storage pools in which the anti-affinity objects exist when creating the custom image storage volumes. If you use VSIs as the anti-affinity objects, {{site.data.keyword.powerSys_notm}} excludes the storage pools based on the boot volume of each VSI.

9. Click **Import image**.

The new boot image is listed on the **Boot images** page.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-import-image}

You can use the [`ibmcloud pi image import`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command to import a boot image from IBM Cloud Object Storage.

Example command syntax:

```sh
ibmcloud pi image import IMAGE_NAME --image-path IMAGE_PATH --os-type OS_TYPE --access-key KEY --secret-key KEY [--bucket BUCKET_NAME] [--region REGION_NAME] [--json]
```
{: pre}

Where:

`IMAGE_NAME`
:   The name for the imported boot image.

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

To view the newly imported boot image, use the [`ibmcloud pi image`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image) command.

Example command syntax:

```sh
ibmcloud pi images [--long] [--json]
```
{: pre}

To import a customized SAP HANA or SAP NetWeaver image, use the [`-d, --import-details strings`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} API
{: #api-import-image}

To import a boot image from IBM Cloud Object Storage by using the API, use the [Create an cos-image import job](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v1-cloudinstances-cosimages-post){: external} method.

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

To view details of a boot image import job by using the CLI, use the [`ibmcloud pi image import-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import-show) command.

To view the image import status by using the API, use the [Get detail of last cos-image import job](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v1-cloudinstances-cosimages-get){: external} method.

## Downloading a boot image from Cloud Object Storage
{: #download-boot-image-cos}

To download your boot image after importing it, navigate to the **Resource List** in the IBM Cloud dashboard, and access your **Cloud Object Storage** workspace. In the bucket where your boot image is stored, select the boot image file that you want to download and select **Download objects**. For more information about the Cloud Object Storage CLI command, see [Download an object](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#ic-download-object){: external}.
