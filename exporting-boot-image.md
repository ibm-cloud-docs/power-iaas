---

copyright:
  years: 2026

lastupdated: "2026-06-23"

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

You can export a custom boot image from your image catalog to IBM Cloud Object Storage.
{: shortdesc}

Image export requires Hash-Based Message Authentication Code (HMAC) access and secret keys to access your IBM Cloud Object Storage bucket. To generate HMAC keys for your storage bucket, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
{: important}

The maximum image size that you can export is 10 TB.
{: note}

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} user interface
{: #console-export-image}

To export a boot image from your image catalog by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type {{site.data.keyword.powerSys_notm}} and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. Select the workspace which contains the boot image that you want to export. The **Virtual server instances** page of the selected workspace is displayed.

5. Click **Boot images** in the navigation panel.

6. Click the options menu (3 vertical dots) for the boot image you want to export and select **Export**. The Export boot image panel is displayed.

7. In the Export boot image panel, complete the following steps:

   1. Select the **Region** where your IBM Cloud Object Storage bucket is located.

   1. In the **Bucket name** field, enter the name of the bucket where you want to export the image. Optionally, you can specify folder paths within the bucket using the format `<bucketName>/optional/folders`.

   1. In the **HMAC access key** field, provide your HMAC access key.

      To identify your access key, click the **menu icon** ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > **Resource list** > **Storage** > *Cloud Object Storage name* > **Service credentials** > **View credentials**. Copy the `access_key_id` value and paste it into the **HMAC access key** field.

   1. In the **HMAC secret access key** field, provide your HMAC secret access key.

      To identify your secret key, click the **menu icon** ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > **Resource list** > **Storage** > *Cloud Object Storage name* > **Service credentials** > **View credentials**. Copy the `secret_access_key` value and paste it into the **HMAC secret access key** field.

   1. Set **Generate checksum file** to **On** to generate a checksum file.

      The checksum file is created and placed in the IBM Cloud Object Storage bucket along with the exported image. The checksum file name is based on the name of the image file and uses the `.sha256` file extension. Use the `shasum -a 256` command to verify the integrity of the exported image file.

8. Click **Export**. The **Export boot image** dialog is displayed with information about the export operation. Review the information and click **Export** to begin exporting the image.

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-export-image}

You can use the [`ibmcloud pi image export`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export) command to export an image to IBM Cloud Object Storage.

Example command syntax:

```sh
ibmcloud pi image export IMAGE_ID --bucket BUCKET_NAME --region REGION_NAME --access-key KEY --secret-key KEY [--json]
```
{: pre}

Where:

`IMAGE_ID`
:   The ID of the image to export.

`BUCKET_NAME`
:   The Cloud Object Storage bucket name.

`REGION_NAME`
:   The region where your bucket resides.

`KEY`
:   Your HMAC access and secret keys.

To view details of an image export job, use the [`ibmcloud pi image export-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export-show) command.

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} API
{: #api-export-image}

To export a boot image to IBM Cloud Object Storage by using the API, use the [Add image export job to the jobs queue](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-images-export-post){: external} method.

## Viewing boot image export results
{: #view-export-results}

After you start a boot image export operation, the **Status** column on the **Boot images** page shows the export progress. To view more details, click **View details** to open the **Ongoing job status** dialog. The following information is displayed:

- Job ID
- Operation type
- Input resource
- Creation time
- Steps completed

To view details of an image export job by using the CLI, use the [`ibmcloud pi image-export-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference#ibmcloud-pi-image-export-show) command.

To view the image export status by using the API, use the [Get detail of last image export job](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-images-export-get){: external} method.

## Related information
{: #related-info-export}

For information about importing custom boot images, see [Importing a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image).

For information about capturing and exporting virtual server instances, see [Capturing and exporting a virtual server instance](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm).
