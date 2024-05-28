---

copyright:
  years: 2024

lastupdated: "2024-03-01"

keywords: deploying a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Deploying a Linux for SAP (HANA or NetWeaver) custom image
{: #deploying-SAP-image}

[Off-Premises]{: tag-blue}

[Q2-2024 update start]{: tag-teal}

The Linux&reg; for SAP (HANA or NetWeaver) operating system (OS) image can be deployed within an {{site.data.keyword.powerSysFull}} by using the following methods:

* [SAP provided central image repository](#SAP-pcir).
* [Bring your own customized image](#byoc-SAP).

## SAP provided central image repository
{: #SAP-pcir}

SAP provides a central image repository within a {{site.data.keyword.powerSys_notm}}. SAP manages the repository and the physical size of the image in the repository can be 4 GB.

If SAP manages your subscription, the SAP performs the following operations on {{site.data.keyword.powerSys_notm}}:

* Creating a Cloud Object Storage (COS) bucket to store the images in {{site.data.keyword.powerSys_notm}}.
* Importing the images from the COS bucket to a new workspace that is created by SAP.
* Importing the images from the COS bucket to an existing workspace.
    The central image repository provided by SAP cannot be used to refresh stock images.
    {: note}


If you want to import the images for your workspace, contact SAP to get the details such as access key, secret key, bucket name, COS region, and image name. You can import the images by using the {{site.data.keyword.powerSys_notm}} interface, CLI, API, or Terraform.

The imported images can be deployed only in the single storage pool where the images are stored. To deploy the images to a different storage pool, the images must be stored in the storage pool. If you are using the APIs to import the images, you can specify the details of the storage pools where the image must be stored.

Complete the planning and pricing before you deploy the Linux for SAP (HANA or NetWeaver) image on the {{site.data.keyword.powerSys_notm}} workspace. Also, the pricing must be completed before the end of subscription for managed services with SAP. <!--For more information, see Linux for SAP (HANA or NetWeaver) pricing optimization.-->
{: note}

## Bring your own customized Linux for SAP (HANA or NetWeaver) image
{: #byoc-SAP}

You can bring your own customized Linux for SAP (HANA or NetWeaver) operating system (OS) image to deploy within a {{site.data.keyword.powerSys_notm}}.
Self-certify that the image is an SAP image by selecting the checkbox to distinguish between the {{site.data.keyword.powerSys_notm}} stock image and a customer provided SAP image. For more information about importing an image, see [Using the Power Virtual Server user interface to import a boot image](https://test.cloud.ibm.com/docs-draft/power-iaas?topic=power-iaas-importing-boot-image#console-import-image).

[Q2-2024 update end]{: tag-teal}
