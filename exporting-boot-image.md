---

copyright:
  years: 2024, 2026

lastupdated: "2026-09-03"

keywords: exporting a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, boot image, export, hmac keys, checksum

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Exporting a boot image
{: #exporting-boot-image}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}

---

You can export a custom boot image from your image catalog to IBM Cloud Object Storage by using the {{site.data.keyword.powerSysFull}} user interface, CLI, or API. Use the **Export boot image** feature to back up or archive a custom boot image, or to copy it to a different workspace or account.
{: shortdesc}

You cannot export IBM-provided stock images. Only custom boot images are available for export. Custom boot images include images that you imported by using the **Import image** function and images that you captured by using the **Capture and export** function.
{: note}

Boot image import and export are long-running, asynchronous operations. {{site.data.keyword.powerSys_notm}} monitors these operations across all workspaces in your account. You can run only one import or export operation at a time in a workspace. You cannot start another operation in that workspace until the current operation is complete.
{: important}

## Before you begin
{: #before-you-begin-export}

Before you export a boot image, verify that you have the following prerequisites:

- A {{site.data.keyword.powerSys_notm}} workspace with at least one custom boot image in your image catalog.
- An IBM Cloud Object Storage bucket to export the custom boot image to. For more information, see [Create some buckets to store your data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets){: external}.
- Hash-based Message Authentication Code (HMAC) credentials that are generated for your COS instance. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} user interface
{: #console-export-image}
{: help}
{: support}

To export a boot image from your image catalog by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}** and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. Select the workspace that contains the boot image that you want to export. The "Virtual server instances" page of the selected workspace is displayed.

5. Click **Boot images** in the navigation panel.

6. Click the overflow menu for the boot image that you want to export and select **Export**. The "Export boot image" panel is displayed.

7. In the "Export boot image" panel, complete the following steps:

   1. From the **Region** drop-down list, select the region that contains your COS bucket.

   2. In the **Bucket name** field, enter the name of the bucket to which you want to export the image. If you want to export the image to a subfolder in the bucket, specify the full path by using the `bucketName/optional/folders` format.

      To identify your bucket name, go to **Navigation menu** > **Resource list** > **Storage** and click your Cloud Object Storage instance name. Your buckets are listed on the **Buckets** tab.

   3. Copy the `access_key_id` value from your COS service credentials and paste it into the **HMAC access key** field.

      To find your service credentials, go to **Navigation menu** > **Resource list** > **Storage**, click your Cloud Object Storage instance name, and then go to **Service credentials** > **View credentials**.

   4. Copy the `secret_access_key` value from your COS service credentials and paste it into the **HMAC secret access key** field.

   5. Set **Generate checksum file** to **On** to generate a checksum file.

      The checksum file is created and placed in the IBM Cloud Object Storage bucket with the exported boot image. The checksum file name is based on the name of the boot image file and uses the `.sha256` file extension. After the export completes, run the `shasum -a 256` command to verify the integrity of the exported boot image file.

   The maximum image size that you can export is 10 TB.
   {: note}

8. Click **Export**. The "Export boot image" dialog is displayed with the export operation details.

9. Review the information and click **Export** to confirm.

The boot image export job is submitted. You can monitor the progress in the **Status** column on the **Boot images** page. For more details, see [Viewing boot image export results](#view-export-results).

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-export-image}

To export a boot image, run the [`ibmcloud pi image export`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export) command. To verify that the boot image is exported, run the [`ibmcloud pi image export-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export-show) command.

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} API
{: #api-export-image}

To export a boot image to IBM Cloud Object Storage by using the API, use the [Add image export job to the jobs queue](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v2-images-export-post){: external} method with the required properties in the request body: `accessKey` and `bucketName`. You can also include the optional properties `region` and `secretKey`. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).

```sh
curl -X POST \
  https://us-east.power-iaas.cloud.ibm.com/pcloud/v2/cloud-instances/$CLOUD_INSTANCE_ID/images/$IMAGE_ID/export \
  -H "Authorization: Bearer $TOKEN" \
  -H "CRN: $CRN" \
  -H "Content-Type: application/json" \
  -d '{
    "bucketName": "my-cos-bucket-name",
    "accessKey": "my-cos-access-key",
    "region": "us-east",
    "secretKey": "my-cos-secret-key"
  }'
```
{: pre}

## Viewing boot image export results
{: #view-export-results}

After you start a boot image export, the **Status** column on the **Boot images** page shows the export progress. To view details, click **View details** to open the "Ongoing job status" dialog. The dialog shows the following information:

- Job ID
- Operation type
- Input resource
- Creation time
- Steps completed

To view the boot image export job details by using the CLI, use the [`ibmcloud pi image export-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export-show) command.

To view the boot image export job details by using the API, use the [Get detail of last image export job](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v2-images-export-get){: external} method.

## Related information
{: #related-info-export}

For information about importing custom boot images, see [Importing a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image).

For information about capturing and exporting virtual server instances, see [Capturing and exporting a virtual server instance](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm).
