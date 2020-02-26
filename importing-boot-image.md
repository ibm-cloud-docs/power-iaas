---

copyright:
  years: 2019, 2020

lastupdated: "2020-02-11"

keywords: boot image, import boot image, upload boot image, storage types, regions, Tier 1, Tier 3, SSD, NVMe

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Importing a boot image
{: #importing-boot-image}

You can import an AIX or IBM i boot image by using the IBM Cloud CLI or the console. The storage types vary by region. The **us-east (WDC)** and **us-south (DAL)** regions have **Standard** or **SSD** storage types. The **eu-de (FRA04 and FRA05)** region uses **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** storage types. Large boot images take time to successfully import. You might experience a delay before receiving a confirmation message.
{: shortdesc}

You must first generate [Secret and Access keys](/docs/power-iaas?topic=power-iaas-deploy-custom-image#access-keys) to import a boot image.
{: note}

## Using the IBM Cloud CLI to import a boot image
{: #cli-import-image}

Complete the following steps to import a boot image by using the IBM Cloud CLI. For more information, see the [IBM Power Systems Virtual Servers CLI Reference](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#ibmcloud-pi-image-import).

1. To import an AIX or IBM i image from IBM Cloud Storage, use the `ibmcloud pi image-import` command.

    ```shell
    ibmcloud pi image-import IMAGE_NAME --image-path PATH --os-type OSTYPE --access-key KEY --secret-key KEY [--json]
    ```
    {: codeblock}

2. Find your newly imported image by using the `ibmcloud pi images` command.

    ```shell
    ibmcloud pi images [--long] [--json]
    ```
    {: codeblock}

## Using the IBM Cloud console to import a boot image
{: #console-import-image}
{: help}
{: support}

Complete the following steps to import a boot image by using the IBM Cloud console.

  The **Image file name** field supports the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.
  {: important}

1. Click the **Boot images** tab, then **Import**.

2. After you click **Import**, enter all of the required information. Refer to the table at the bottom of the page to complete the necessary fields to import a boot image.

    ![Completing the boot image fields](./images/console-boot-image-fields.png "Completing the boot image fields"){: caption="Figure 1. Completing the boot image fields" caption-side="bottom"}

3. Find your newly uploaded boot image in your **Boot images** tab.

| Field | Description |
| ------| ------------|
| Catalog image name | Enter the name that you want displayed in your catalog.|
| Storage type | **us-east (WDC)** or **us-south (DAL)**: Select whether you want **Standard** or **SSD** for the storage type. <br> **eu-de (FRA04 and FRA05):** Select whether you want **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** for the storage type. A VM cannot have disks from both **Tier 1** and **Tier 3** storage types.|
| Region | Select either **us-east**, **us-south**, or **eu-de** for the region.|
| Image file name | Enter the fully qualified path for the image file. The fully qualified path must be in this format, `endpoint/bucket_name/file_name`. You must use the private endpoint domain. For example, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`. You can identify the endpoint domain, bucket name, and file name by selecting **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object**.
| Cloud Object Storage bucket name | To identity your bucket name, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object name > Buckets**. |
| Cloud Object Storage access key | To identify your access key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object name > Service credentials > View credentials**. Copy the `access_key_id` value and past it into this field.|
| Cloud Object Storage secret key | To identify your secret key, select **Menu icon ![Menu icon](../icons/icon_hamburger.svg "Menu icon") > Resource list > Storage > Cloud Storage Object name > Service credentials > View credentials**. Copy the `secret_access_key` value and paste it into this field.|
