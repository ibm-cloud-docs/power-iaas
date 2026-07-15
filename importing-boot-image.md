---

copyright:
  years: 2024, 2026 

lastupdated: "2026-07-15"

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

You can import a boot image when you want to use a custom operating system (OS) image instead of an IBM-provided stock image. After you import the boot image, you can use it to create a {{site.data.keyword.powerSys_notm}} virtual server instance (VSI). You can import a boot image from an IBM Cloud Object Storage (COS) bucket by using the {{site.data.keyword.powerSysFull}} user interface, CLI, or API.
{: shortdesc}

When you import a boot image, you select a storage tier and storage pool for the image. {{site.data.keyword.powerSys_notm}} places the boot volumes that are created from this imported boot image in the storage pool that you specify during the import. You cannot change the storage tier or storage pool after you import the image. A VSI can have disks from multiple storage types. All {{site.data.keyword.powerSys_notm}} data centers support Tier 0, Tier 1, Tier 3, and Fixed IOPs storage types.

Boot image import and export are long-running asynchronous operations that {{site.data.keyword.powerSys_notm}} monitors across all workspaces in your account. You can run only one import or export operation at a time in a workspace. You cannot start a new operation until the ongoing operation completes.
{: important}

## Before you begin
{: #before-you-begin-import}

Before you import a boot image, complete the following prerequisites:

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

4. Select the workspace to which you want to import the boot image. The "Virtual server instances" page of the selected workspace is displayed.

5. Click **Boot images** in the navigation panel, then click **Import image**. The "Import boot image" panel is displayed.

6. In the **Import boot image** panel, complete the following steps in the **Source** section:

   1. Select the image OS from the **Image OS** dropdown list.

      If you select a customized SAP HANA or SAP NetWeaver image, select the self-certification checkbox.

   2. From the **Region** dropdown list, select the region that contains your COS bucket.

   3. Enter the file name of the image in the **Image filename** field. The image file name must not contain spaces.

      The supported file name extensions are `.ova`, `.ova.gz`, `.tar`, `.tar.gz`, and `.tgz`. You can compress image files by using `gzip`. For example: `Aix_7200-03-02-1846_cldrdy_112018.ova.gz`.

   4. Enter the name of your bucket in the **Bucket name** field. If your image file is stored in a subfolder within the bucket, specify the full path by using the `bucketName/optional/folders` format.

      To identify your bucket name, go to **Navigation menu > Resource list > Storage** and click your Cloud Object Storage instance name. Your buckets are listed in the navigation panel.

   5. Copy the `access_key_id` value from your COS service credentials and paste it into the **HMAC access key** field.

      To find your service credentials, go to **Navigation menu > Resource list > Storage**, click your Cloud Object Storage instance name, and then go to **Service credentials > View credentials**.

   6. Copy the `secret_access_key` value from your COS service credentials and paste it into the **HMAC secret access key** field.

   7. Set **Validate import with checksum file** to **On** to verify the imported file against the checksum file. You must store the checksum file and the boot image file in the same COS bucket.

      You can generate the checksum file when you export the image files to the IBM Cloud Object Storage bucket.

      The checksum file name is based on the name of the boot image file and uses the `.sha256` file extension. For more information about generating a checksum file, see [Using the Power Virtual Server user interface to capture and export a VM](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm#console-capture-export).

      If you create your own boot image, you can create a checksum file and store it with your boot image in the same bucket. You can generate the checksum file by running the `shasum -a 256 <filename>` or `sha256sum <filename>` command.

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

      A VSI cannot use Tier 1 and Tier 3 storage types simultaneously. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#storage-tiers).
      {: note}

   4. In the **Storage pool** field, select a storage pool placement option.

      {{site.data.keyword.powerSys_notm}} places one or more custom image storage volumes in the storage pool based on the option that you select: **Auto-select**, **Affinity**, or **Anti-affinity**. The boot volume of any VSI that you deploy by using this image is created in the same storage pool. For more information about storage volumes, see [Adding and managing storage volumes](/docs/power-iaas?topic=power-iaas-modifying-instance#modifying-volume-network).

      The following storage pool placement options are available:

      - **Auto-select**: Automatically creates the storage volume in a storage pool with sufficient capacity.

      - **Affinity**: Identifies the storage pool to use for placing the boot volumes, based on an existing VSI or storage volume from your account. {{site.data.keyword.powerSys_notm}} stores the custom image storage volumes in the same storage pool where the affinity object exists. If you use a VSI as the affinity object, {{site.data.keyword.powerSys_notm}} determines the storage pool based on the boot volume of that VSI.

      - **Anti-affinity**: Identifies one or more storage pools that you want to exclude. {{site.data.keyword.powerSys_notm}} does not consider the excluded storage pools when placing boot volumes. The pools to exclude are identified based on existing VSIs or storage volumes in your account. When you select this option, {{site.data.keyword.powerSys_notm}} excludes the storage pools where the anti-affinity objects exist when it creates the custom image storage volumes. If you use VSIs as the anti-affinity objects, {{site.data.keyword.powerSys_notm}} excludes the storage pools based on the boot volume of each VSI.

9. Click **Import image**.

   Large boot images might take longer to import. You might experience a delay before you receive a confirmation message.
   {: note}

The new boot image is listed on the **Boot images** page.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-import-image}

To import a boot image, use the [`ibmcloud pi image import`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) command. To verify that the import completed successfully, use the [`ibmcloud pi image list`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image) command.

If you are using a bring-your-own-license (BYOL) SAP HANA or SAP NetWeaver image, add the [`--import-details`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import) flag to the `ibmcloud pi image import` command to identify the image as SAP-certified.

## Importing a boot image by using the {{site.data.keyword.powerSys_notm}} API
{: #api-import-image}

To import a boot image from IBM Cloud Object Storage by using the API, use the [Create an cos-image import job](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v1-cloudinstances-cosimages-post){: external} method with the following required properties in the request body: `imageName`, `imageFilename`, and `bucketName`. For private buckets, also include `accessKey` and `secretKey`, which are the HMAC access key and secret key for your COS instance. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main){: external}.

```sh
curl -X POST \
  https://us-east.power-iaas.cloud.ibm.com/pcloud/v1/cloud-instances/$CLOUD_INSTANCE_ID/cos-images \
  -H "Authorization: Bearer $TOKEN" \
  -H "CRN: $CRN" \
  -H "Content-Type: application/json" \
  -d '{
    "imageName": "my-image-name",
    "imageFilename": "my-os-image-file.ova.gz",
    "bucketName": "my-cos-bucket-name",
    "region": "us-east",
    "accessKey": "my-cos-access-key",
    "secretKey": "my-cos-secret-key",
    "storageType": "tier3"
  }'
```
{: pre}

If you are using a bring-your-own-license (BYOL) SAP HANA or SAP NetWeaver image, include the `importDetails` object in the request body to identify the image as SAP-certified:

```json
"importDetails": {
   "licenseType": "byol",
   "product": "Hana",
   "vendor": "SAP"
}
```
{: codeblock}

## Viewing boot image import results
{: #view-import-results}

After you start a boot image import operation, the **Status** column on the **Boot images** page shows the import progress. To view more details, click **View details** to open the **Ongoing job status** dialog. The dialog shows the following information:

- Job ID
- Operation type
- Input resource
- Creation time
- Steps completed

To view the boot image import job details by using the CLI, use the [`ibmcloud pi image import-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-import-show) command.

To view the boot image import job details by using the API, use the [Get detail of last cos-image import job](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v1-cloudinstances-cosimages-get){: external} method.

## Downloading a boot image from Cloud Object Storage
{: #download-boot-image-cos}

To download the boot image after you import it, navigate to **Resource list** in the IBM Cloud dashboard and access your **Cloud Object Storage** instance. In the bucket where your boot image is stored, click the boot image file, and then click **Download objects**. For more information about the Cloud Object Storage CLI command, see [Download an object](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#ic-download-object){: external}.
