---

copyright:
  years: 2019

lastupdated: "2019-7-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Configuring a custom image with a Power Systems Virtual Server
{: #configuring-custom-image}

You can bring your own customized AIX or IBM i operating system image to deploy a {{site.data.keyword.powerSysFull}}.
{:shortdesc}

You cannot transfer an operating system license from an on-premises system to a {{site.data.keyword.powerSys_notm}} that is running in the cloud environment. The license cost is factored into the overall hourly billing rate.
{: note}

## Before you begin
{: #cci-before-you-begin}

Before you can use a custom image as the boot volume, review the following information:

* You must verify that the AIX or IBM i operating system technology level is supported on the Power Systems hardware that you selected in the **Machine Type** field. To view a list of the supported AIX and IBM i operating system technology levels and Power System hardware, see [System software maps ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).
* You must have a basic understanding of **IBM Cloud Object Storage** concepts. For more information, see [About IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage).
* If you do not have an existing AIX or IBM i image, you can use IBM® PowerVC™ to capture and export an image for use with a {{site.data.keyword.powerSys_notm}}. For more information, see [Capturing a virtual machine ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} and [Exporting images ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}.

## Uploading a custom image as an object
{: #cci-uploading}

1. Create an IBM Cloud Storage object and upload your image. For more information, see [Upload data](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload).
2. Generate secret and access keys with Hash-based Message Authentication Code (HMAC). You can generate these keys when you create the service credentials for the IBM Cloud Storage object. To create the service credentials, you must have `Writer` access for the **Object Storage** bucket. For more information, see [Service credentials](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) and [Bucket permissions](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions).
3. From the [IBM Cloud catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog){: new_window}, click the Power Virtual Server tile to add the image. If you already created the virtual server instance, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Devices** and select your existing virtual server.

 Complete the following fields to create your {{site.data.keyword.powerSys_notm}} and click **Custom AIX image** or **Custom IBM i Image**.

| Field | Description |
| ------| ------------|
| Cloud Object Storage bucket name | To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object name > Buckets**. |
| Cloud Object Storage access key | To identify you access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field. |
| Cloud Object Storage secret key | To identify you secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field. |
| Image Path | Enter the fully qualified path for the image file. The fully qualified path must be in this format, `endpoint/bucket_name/file_name`. You must use the private endpoint domain. For example, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. You can identify the endpoint domain, bucket name, and file name by selecting **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object**.
