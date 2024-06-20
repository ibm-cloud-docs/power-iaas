---

copyright:
  years: 2024

lastupdated: "2024-06-20"

keywords: deploying a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Deploying a Linux for SAP (HANA or NetWeaver) custom image
{: #deploying-SAP-image}


[Off-premises]{: tag-blue}

The Linux&reg; for SAP (HANA or NetWeaver) operating system (OS) image can be deployed within an {{site.data.keyword.powerSysFull}} by using the following methods:

* [SAP provided central image repository](#SAP-pcir).
* [Bring your own customized image](#byoc-SAP).

## SAP provided central image repository
{: #SAP-pcir}

SAP provides a central image repository within a {{site.data.keyword.powerSys_notm}}. SAP manages the repository and the physical size of the image in the repository can be 4 GB.

If SAP manages your subscription, the SAP performs the following operations on {{site.data.keyword.powerSys_notm}}:

* Creating a Cloud Object Storage bucket to store the images in {{site.data.keyword.powerSys_notm}}.
* Importing the images from the Cloud Object Storage bucket to a new workspace that is created by SAP.
* Importing the images from the Cloud Object Storage bucket to an existing workspace.
    The central image repository that is provided by SAP cannot be used to refresh stock images.
    {: note}


If you want to import the images for your workspace, contact SAP to get the details such as access key, secret key, bucket name, Cloud Object Storage region, and image name. You can import the images by using the {{site.data.keyword.powerSys_notm}} interface, CLI, API, or Terraform.

To deploy imported images to a storage pool, they can only be used within the same storage pool where they are initially stored. If you wish to deploy the images to a different storage pool, you must first store the images in that specific storage pool. When utilizing APIs for image import, you have the option to define the storage pool where the images should be stored.

Before deploying the Linux for SAP (HANA or NetWeaver) image on the {{site.data.keyword.powerSys_notm}} workspace, ensure that the planning and pricing are finalized. Additionally, make sure to complete the pricing before the managed services subscription with SAP expires. 
