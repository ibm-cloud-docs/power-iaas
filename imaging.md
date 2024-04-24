---

copyright:
  years: 2023

lastupdated: "2023-03-28"

keywords: planning, site-readiness, {{site.data.keyword.powerSys_notm}} as a service, private cloud

subcollection: power-iaas


#  this topic needs more information...
---

{{site.data.keyword.attribute-definition-list}}

# Connectivity to IBM COS buckets to import custom images
{: #conn-COS-custom-image}

[Private Cloud]{: tag-red}

You can maintain a set of operating system images in your IBM Cloud Object Storage (COS) buckets. These images are referred to as custom images. You can import these custom images into the boot volumes of the logical partitions (LPARs).

To import the stored custom images from the **Boot images** page, click **Import image** option. Enter the following information in the **Import boot image** panel to complete the following steps:
* A custom image name that must be used during virtual machine provisioning
* Storage tier number
* Storage pool preferences
* Region of your COS instance
* File name of the custom image to be imported as specified in the COS instance
* Your COS bucket name
* Hash-based Message Authentication Code (HMAC) secret key and access key

IBM {{site.data.keyword.powerSys_notm}} Private Cloud processes the custom image file as follows:
* Downloads the image file from the COS instance.
* Imports the image file into the attached storage.
* Converts the image file into an image volume.
* Copies the image volume as a boot volume to deploy the LPAR.

The following diagram describes the architecture to import custom images stored in the IBM COS buckets:
![Control plane connectivity with IBM COS bucket.](./figures/COS-VPE-direct-link-control-plane.jpg "Control plane connectivity with IBM COS bucket."){: caption="Figure 1. Control plane connectivity with IBM COS bucket." caption-side="bottom"}
