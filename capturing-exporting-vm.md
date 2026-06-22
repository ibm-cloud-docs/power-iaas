---

copyright:
  years: 2023, 2026 

lastupdated: "2026-06-18"

keywords: image catalog, virtual server instance capture, cos bucket, export virtual server instance, ova

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Capturing and exporting a VSI
{: #capturing-exporting-vm}





{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---



You can capture and export a virtual server instance (VSI) by using the {{site.data.keyword.powerSysFull}} user interface, CLI, or API. When you capture a VSI, the boot volume and any attached data volumes are saved as a volume-backed image. The image is stored in new volumes on the storage providers. You can export the captured image to the image catalog, an IBM Cloud Object Storage bucket, or both. When an image is exported, the volumes of the image are copied and packaged in an Open Virtualization Appliance (OVA) file. The OVA file is compressed by using *gzip* before it is uploaded to your selected destination.
{: shortdesc}

When you capture and export a VSI, you can choose the image catalog, Cloud Object Storage, or both as destinations. The image catalog is stored on the IBM Power storage area network (SAN). IBM Cloud Object Storage is encrypted and dispersed across multiple geographic locations, and accessed over HTTP by using a REST API. IBM Cloud Object Storage uses the distributed storage technologies that are provided by the IBM Cloud Object Storage System (formerly Cleversafe). After capturing an image to the image catalog, you can export it to Cloud Object Storage as a separate operation. You can also deploy the captured image to create a clone of the VSI by using a different network configuration.

The maximum image size that you can export to Cloud Object Storage is 10 TB.
{: note}

The {{site.data.keyword.powerSysFull}} Job feature tracks long-running asynchronous operations like VSI capture, image export, and image import across multiple workspaces in your cloud account.

The VSI capture, image export, and image import features are restricted to one operation at a time per {{site.data.keyword.powerSys_notm}} workspace. Wait until one operation is complete before you submit a new operation (VSI Capture, Image Export, and Image Import).
{: important}

You are charged different rates based on whether you export to the image catalog or Cloud Object Storage.
{: note}

Before you capture an IBM i VSI, ensure that any buffer I/O memory is flushed (written) to the disk by using the following command:

```text
CHGASPACT ASPDEV(*SYSBAS) OPTION(*FRCWRT)
```
{: codeblock}

## Capturing and exporting a VSI by using the {{site.data.keyword.powerSys_notm}} user interface
{: #console-capture-export}

Complete the following steps to capture and export a VSI:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. In the search box, type {{site.data.keyword.powerSys_notm}} and click the **{{site.data.keyword.powerSys_notm}}** tile.

3. Click **Workspaces** in the navigation panel. The Workspaces page with a list of existing workspaces is displayed.

4. Select your workspace from the displayed list of workspaces.

5. Click **Virtual server instances** in the navigation panel.

6. Select the VSI that you want to capture. Ensure that the VSI is in an active state. The **Virtual server instance details** page is displayed.

7. On the **Virtual server instance details** page, click options menu (3 vertical dots) and select **Capture and export**. The Capture and export virtual server pane is displayed.

8. In the **Capture contents** section, the boot volume of the selected VSI is automatically selected. You can optionally select any additional data volumes that are attached to the VSI.

   Any volumes that are not shown are not on the same storage pool as the boot volume and cannot be included in the capture.
   {: note}

9. Click **Next**.

10. In the **Destination** section, select the export destination for the captured image:

    - **Image catalog**: Stores the image in your workspace image catalog for future deployments
    - **IBM Cloud Object Storage**: Exports to IBM Cloud Object Storage

    **Image catalog**

    If you selected **Image catalog** as the export destination, complete the following steps:

    1. Enter an image name in the **Image name** field.

    2. Optional: enter tags in the **User tags** field.

    **IBM Cloud Object Storage**

    If you selected **IBM Cloud Object Storage** as the export destination, complete the following steps:

    1. Select the **Region** where your IBM Cloud Object Storage bucket is located.

    2. In the **Bucket name** field, enter the name of the bucket where you want to export the image. Optionally, you can specify folder paths within the bucket.

    3. In the **HMAC access key** field, provide your HMAC access key. For more information, see [Generating HMAC credentials](/docs/power-iaas?topic=power-iaas-deploy-custom-image#access-keys).

    4. In the **HMAC secret access key** field, provide your HMAC secret access key.

    5. Set **Generate checksum file** to **On** to generate a checksum file.

       The checksum file is created and placed in the IBM Cloud Object Storage bucket along with the exported image. The checksum file name is based on the name of the image file and has the file extension `.sha256`. Use the command `shasum -a 256` to verify that the copied file is correct.

       If you are creating your own image, you can create a checksum image and place it with your own image in the same bucket. One of the ways to generate the checksum image is by using the command `shasum -a 256 <filename>` or `sha256sum <filename>`.

       Generating a checksum file might increase the image capture and export time.
       {: note}

11. Click the terms and conditions link to read the IBM Cloud Terms of Use. To continue, select the **I agree to the Terms and conditions** checkbox.

12. Click **Capture and export**. The **Capture & export virtual server** dialog is displayed with information about the capture operation. Review the information and click **Capture and export**.

When the capture and export operation is complete, a notification is displayed indicating the status of the operation.

To view your exported image:

- If you exported your volume-backed image to IBM Cloud Object Storage, navigate to your Cloud Object Storage bucket to view the image.

- If you exported your volume-backed image to the image catalog, navigate to the **Boot images** page to view the image.

## Capturing and exporting a VSI by using the {{site.data.keyword.powerSys_notm}} CLI
{: #cli-capture-export}

To capture and export a VSI, use the [`ibmcloud pi instance-capture`](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-capture) command. You can export it to the image catalog, Cloud Object Storage, or both.

```text
ibmcloud pi instance-capture INSTANCE_ID --destination DEST --name NAME [--volumes "VOLUME1 VOLUME2"] [--access-key KEY] [--secret-key KEY] [--region REGION] [--image-path TYPE]
```
{: codeblock}

To see your newly exported image in the image catalog by using the CLI, use the `ibmcloud pi image-list-catalog` command:

```text
ibmcloud pi image-list-catalog [--long] [--json]
```
{: codeblock}

To see your newly exported image in Cloud Object Storage by using the CLI, use the `ibmcloud cos list-objects` command:

```text
ibmcloud cos list-objects --bucket BUCKET_NAME [--delimiter DELIMITER] [--encoding-type METHOD] [--prefix PREFIX] [--starting-token TOKEN] [--page-size SIZE] [--max-items NUMBER] [--region REGION] [--json]
```
{: codeblock}

## Capturing and exporting a VSI by using the {{site.data.keyword.powerSys_notm}} API
{: #api-capture-export}

To capture and export a VSI to the image catalog or IBM Cloud Object Storage by using the API, use the [Add a capture pvm-instance to the jobs queue](https://cloud.ibm.com/apidocs/power-cloud#pcloud-v2-pvminstances-capture-post){: external} method.

## Related information
{: #related-info-capture-exp}

For information about exporting boot images from your image catalog to IBM Cloud Object Storage, see [Exporting a boot image](/docs/power-iaas?topic=power-iaas-exporting-boot-image).

For information about importing boot images from IBM Cloud Object Storage, see [Importing a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image).
