---

copyright:
  years: 2023, 2024

lastupdated: "2024-06-06"

keywords: image catalog, virtual machine capture, cos bucket, export virtual machine, ova

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Capturing and exporting a virtual machine (VM)
{: #capturing-exporting-vm}

You can capture and export an AIX or IBM i VM instance by using the {{site.data.keyword.powerSysFull}} user interface or CLI. A VM is captured as a volume-backed image. The image is stored in new volumes on the storage providers. An image can be exported to an IBM Cloud Object Storage (Cloud Object Storage) bucket. When an image is exported, the volumes of the image are copied and packaged in an Open Virtualization Appliance (OVA) file. The OVA file is compressed by using *gzip* before it gets uploaded to the IBM Cloud Object Storage bucket.
{: shortdesc}

When you capture and export a VM, you can choose the image catalog, Cloud Object Storage, or both as destinations. The image catalog is on the IBM Power storage area network (SAN). IBM Cloud Object Storage is encrypted and dispersed across multiple geographic locations, and accessed over HTTP by using a REST API. This service uses the distributed storage technologies that are provided by the IBM Cloud Object Storage System (formerly Cleversafe). You can always export your image in your image catalog to Cloud Object Storage at a later point. You can also deploy the captured image to create a clone of the VM by using a different network configuration.

The {{site.data.keyword.powerSysFull}} Job feature tracks long-running asynchronous operations like VM capture, image export, and image import across multiple workspaces in your cloud account. See the following APIs and CLIs that are associated to these tasks:
- API for VM capture - [Capture a PVM instance and create a deployable image (version 2)](/apidocs/power-cloud#pcloud-v2-pvminstances-capture-post).
- API for image export - [Add an image export job to the jobs queue (version 2)](/apidocs/power-cloud#pcloud-v2-images-export-post).
- CLI for instance capture - [`ibmcloud pi instance-capture`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-instance-capture) command.
- CLI for jobs - [`ibmcloud pi jobs`](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-jobs) command.

The VM capture, image export, and image import features are restricted to one operation at a time per {{site.data.keyword.powerSys_notm}} workspace. If one of these operations is submitted successfully, then another new operation (VM Capture, Image Export, and Image Import) cannot be submitted until the previous operation is complete.
{: important}

You are charged different rates based on whether you export to the image catalog or COS.
{: note}

Before you capture an IBM i VM, ensure that any buffer I/O memory is flushed (written) to the disk by running the following command:

```text
CHGASPACT OPTION(*FRCWRT)
```
{: codeblock}


## Using the {{site.data.keyword.powerSys_notm}} user interface to capture and export a VM
{: #console-capture-export}

Complete the following steps to capture and export a virtual server instance:

1. Click the **Capture and export** icon in your **Boot images** view.

2. Choose the volumes that you want to capture and export.

3. Select whether you want to export the volume-backed image to the image catalog, COS, or both.

4. Give your captured image a **Name**.

5. *(Optional)* If you decide to export to COS, you are presented with more options:
   1. Select the **Region**.
   2. Select your **Bucket name** and **optional folders**.
   3. Provide your [HMAC access and HMAC secret keys](/docs/power-iaas?topic=power-iaas-deploy-custom-image#access-keys).

6. Click **Export**.

7. If the capture and export operation is successful, you are presented with a confirmation message.

    If you select large volumes, the export process can take a significantly long time.
    {: important}

8. Find your newly exported image by completing either one of the following tasks:

   - If you chose to capture and export your volume-backed image to COS, go to your COS bucket.

   - If you chose to capture and export your volume-backed image to the image catalog, go to **Boot images**.

9. *(Optional)* If you'd like to export your volume-backed image from your image catalog to COS, select it, and click the **Capture and export** icon.

## Using the CLI to capture and export a VM
{: #cli-capture-export}

To learn more about using the command-line interface to capture and export a VM, see [{{site.data.keyword.powerSysFull}} Private Cloud CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference) and [IBM COS CLI](/docs/cloud-object-storage-cli-plugin?topic=cloud-object-storage-cli-plugin-ic-cos-cli).

1. To capture an AIX or IBM i VM, use the `ibmcloud pi instance-capture` command. You can export it to your image catalog, COS, or both.

    ```text
    ibmcloud pi instance-capture INSTANCE_ID --destination DEST --name NAME [--volumes "VOLUME1 VOLUME2"] [--access-key KEY] [--secret-key KEY] [--region REGION] [--image-path TYPE]
    ```
    {: codeblock}

2. Find your newly exported image by completing either one of the following tasks:

    - To see your newly exported image in the image catalog, use the `ibmcloud pi image-list-catalog` command:

        ```text
        ibmcloud pi image-list-catalog [--long] [--json]
        ```
        {: codeblock}

    - To see your newly exported image in COS, use the `ibmcloud cos list-objects` command:

        ```text
        ibmcloud cos list-objects --bucket BUCKET_NAME [--delimiter DELIMITER] [--encoding-type METHOD] [--prefix PREFIX] [--starting-token TOKEN] [--page-size SIZE] [--max-items NUMBER] [--region REGION] [--json]
        ```
        {: codeblock}
