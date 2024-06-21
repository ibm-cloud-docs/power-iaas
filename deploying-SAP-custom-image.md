---

copyright:
  years: 2024

lastupdated: "2024-06-21"

keywords: deploying a boot image, {{site.data.keyword.powerSys_notm}} as a service, private cloud, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Deploying a Linux for SAP (HANA or NetWeaver) custom image
{: #deploying-SAP-image}


[Off-premises]{: tag-blue}

The Linux&reg; for SAP (HANA or NetWeaver) operating system (OS) image can be deployed within an {{site.data.keyword.powerSysFull}} by using IBM&reg; provided central image repository for SAP offerings. You can bring your own SAP (HANA or NetWeaver) image with your own subscription, import the image to your workspace, and create a virtual machine by using the image.


You can import an image by using the {{site.data.keyword.powerSys_notm}} interface, CLI, API, or Terraform.

When you import a Linux for SAP (HANA or NetWeaver) custom image through the interface, select the self-certification checkbox to confirm that the image is an SAP image. For more information about importing an image, see [Using the Power Virtual Server user interface to import a boot image](/docs/power-iaas?topic=power-iaas-importing-boot-image#console-import-image).



The IBM provided central image repository for SAP offerings cannot be used to refresh the stock images.
{: note}

An imported SAP image is stored into a single storage pool and can be deployed only in that single storage pool. To deploy the SAP image into other storage pools, you must import the image into those storage pools. If you use APIs for image import, you can define the storage pool where the images can be stored.




