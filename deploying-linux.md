---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-11"

keywords: linux deployment, ova, powervc capture, vm capture from vios

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Deploying a Linux Virtual Server
{: #linux-deployment}

You can use the {{site.data.keyword.powerSys_notm}}) service to deploy a generic Linux&trade; virtual machine (VM). When you are provisioning a VM, select **Linux** for your operating system. The {{site.data.keyword.powerSys_notm}} service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. Only Red Hat and SUSE Linux OVA images are currently supported.
{: shortdesc}

After you deploy your Linux VM, you must log in to obtain the wanted subscription from a Linux vendor. To reach the Linux vendor satellite servers (where you can register and obtain packages and fixes), you must attach a public network to your VM. To learn more about the registration process, see [Registering and subscribing to SLES](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#registering-sles).

## How to create an OVA format Linux image
{: #ova-format}

Learn how to create an OVA image of a Red Hat Linux or SUSE Linux operating system and import it into the {{site.data.keyword.powerSys_notm}} environment.

### Using PowerVC to capture and import an OVA image
{: #powervc-capture}

If you've deployed PowerVC in your on-premises environment, you can use it to [capture any supported LPAR](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.0/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window}{: external} and create an OVA image. After you create the OVA image, upload it to your Cloud Object Storage (COS) account and import it into the {{site.data.keyword.powerSys_notm}} environment.

### Capturing an image from VIOS
{: #vios-capture}

Download and use the **insert name of tool** to capture an image from VIOS of any client LPAR that is running on a host.

You must shut down your LPAR for this method to work. Otherwise, you might encounter disk errors.
{: important}

**Paul inserts text**
