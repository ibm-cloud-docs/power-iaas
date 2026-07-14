---

copyright:
  years: 2026

lastupdated: "2026-07-14"

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

You can export a custom boot image from your image catalog to IBM Cloud Object Storage by using the {{site.data.keyword.powerSysFull}} user interface, CLI, or API.
{: shortdesc}

VSI capture, image export, and image import are long-running asynchronous operations that {{site.data.keyword.powerSys_notm}} monitors across all workspaces in your account. Only one of these operations can run at a time per workspace. You cannot start a new operation until the ongoing operation completes.
{: important}

The maximum image size that you can export is 10 TB.
{: note}

## Before you begin
{: #before-you-begin-export}

Before you export a boot image, complete the following prerequisites:

- You have a {{site.data.keyword.powerSys_notm}} workspace with at least one custom boot image in your image catalog.
- You have an IBM Cloud Object Storage bucket to export the image to. For more information, see [Create some buckets to store your data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets){: external}.
- You have generated HMAC credentials for your COS instance. For more information, see [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main){: external}.

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} user interface
{: #console-export-image}
{: help}
{: support}

To export a boot image from your image catalog by using the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type **{{site.data.keyword.powerSys_notm}}** and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. Select the workspace that contains the boot image that you want to export. The **Virtual server instances** page of the selected workspace is displayed.

5. Click **Boot images** in the navigation panel.

6. Click the options menu for the boot image that you want to export and select **Export**. The **Export boot image** panel is displayed.

7. In the **Export boot image** panel, complete the following steps:

   1. From the **Region** dropdown list, select the region that contains your COS bucket.

   2. In the **Bucket name** field, enter the name of the bucket where you want to export the image. If your image file must be stored in a subfolder within the bucket, specify the full path by using the `bucketName/optional/folders` format.

   3. Copy the `access_key_id` value from your COS service credentials and paste it into the **HMAC access key** field.

      To find your service credentials, go to **Navigation menu > Resource list > Storage** and click your Cloud Object Storage instance name. Then go to **Service credentials > View credentials**.

   4. Copy the `secret_access_key` value from your COS service credentials and paste it into the **HMAC secret access key** field.

   5. Set **Generate checksum file** to **On** to generate a checksum file.

      The checksum file is created and placed in the IBM Cloud Object Storage bucket along with the exported image. The checksum file name is based on the name of the image file and uses the `.sha256` file extension. Run the `shasum -a 256` command to verify the integrity of the exported image file.

8. Click **Export**. The **Export boot image** dialog opens with information about the export operation. Review the information and click **Export** to confirm.

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-export-image}

To export a boot image, use the [`ibmcloud pi image export`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export) command. To verify that the export completed successfully, use the [`ibmcloud pi image export-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export-show) command.

## Exporting a boot image by using the {{site.data.keyword.powerSys_notm}} API
{: #api-export-image}

To export a boot image to IBM Cloud Object Storage by using the API, use the [Add image export job to the jobs queue](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v2-images-export-post){: external} method.

## Viewing boot image export results
{: #view-export-results}

After you start a boot image export operation, the **Status** column on the **Boot images** page shows the export progress. To view more details, click **View details** to open the **Ongoing job status** dialog. The dialog shows the following information:

- Job ID
- Operation type
- Input resource
- Creation time
- Steps completed

To view the boot image export job details by using the CLI, use the [`ibmcloud pi image export-show`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image-export-show) command.

To view the image export status by using the API, use the [Get detail of last image export job](https://cloud.ibm.com/docs/apis/power-cloud#pcloud-v2-images-export-get){: external} method.

## Related information
{: #related-info-export}

For information about importing custom boot images, see [Importing a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image).

For information about capturing and exporting virtual server instances, see [Capturing and exporting a virtual server instance](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm).
