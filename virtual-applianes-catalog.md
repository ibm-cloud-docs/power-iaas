---

copyright:
  years: 2022

lastupdated: "2022-06-06"

keywords: virtual appliance, VTL, virtual tape, onboarding, ISV

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:preview: .preview}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Virtual appliances
{: #virtual-appliances}

Virtual appliances enable you to use additional services within Power Systems Virtual Servers like virtual tape libraries. Enable independent software vendors (ISVs) to participate in the Power as a service ecosystem with bundled capacity and revenue sharing. 

## Onboarding your virtual server images for Power Systems Virtual Servers
{: #onboard-vsi}

Independent software vendors can sell software on the IBM Cloud platform by enrolling in the Partner Center and completing the onboarding process from the IBM Cloud catalog. For more information, see [Selling on IBM Cloud](/docs/sell?topic=sell-selling-clouds){: external}.

As part of the onboarding process for selling Power Virtual Server software, sellers are required to provide a public (shareable) virtual server image asset. To provide a public virtual server image for Power Systems Virtual Server, complete the following steps:

1.	Create your [Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).
2.	Create an instance of [IBM Cloud Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) and upload your image to a bucket.
3.	Create your [HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main).
4.	[Open a support case](/docs/power-iaas?topic=power-iaas-getting-help-and-support) so that the Power Systems Virtual Server product management team can convert your image into a stock image. Include your HMAC credentials and bucket details in the support case.

## Virtual tape libraries
{: #virtual-tape-libraries}

Virtual tape libraries are devices that are commonly used to backup IBM i data. The Power Systems Virtual Servers replicates the on-premises solution by providing a software virtual tape library (VTL) appliance that can be dynamically provisioned in the IBM Cloud. FalconStor Restore provides a deduplicated, scalable backup solution and is the only IBM certified on-premises and PowerVS VTL solution for IBM i. For more information, see [Power Virtual Server VTL Overview](https://cloud.ibm.com/media/docs/downloads/power-iaas/PowerVS_VTL_Overview.pdf){: external}.