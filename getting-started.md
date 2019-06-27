---

copyright:
  years: 2019

lastupdated: "2019-06-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{hide-in-docs: .hide-in-docs}
{hide-dashboard: .hide-dashboard}

# Getting started with Power Systems Virtual Servers
{: #getting-started}


{{site.data.keyword.powerSysFull}} is an infrastructure as a service offering that you can use to deploy a virtual server, also known as a logical partition (LPAR), in a matter of minutes.
{:shortdesc}

You can quickly deploy {{site.data.keyword.powerSys_notm}}s to meet your specific business needs. With {{site.data.keyword.powerSys_notm}} you can create a hybrid cloud environment that allows you to easily control workload demands.
{: hide-dashboard}

{{site.data.keyword.powerSys_notm}}s can run AIX or IBM i workloads in different geographic locations.

## Terminology
{: #gs-terminology}

Before you create a virtual server, you must understand the difference in terminology between a {{site.data.keyword.powerSys_notm}} **service** and a {{site.data.keyword.powerSys_notm}} **instance**. Think of the {{site.data.keyword.powerSys_notm}} **service** as a container for all {{site.data.keyword.powerSys_notm}} **instances** at a specific geographic location. The {{site.data.keyword.powerSys_notm}} **service** is available from the **Resource list** in the {{site.data.keyword.cloud}} UI. The service can contain multiple {{site.data.keyword.powerSys_notm}} **instance**.

For example, you can have two {{site.data.keyword.powerSys_notm}} **services**, one in Dallas and another in Washington DC. Each service can contain multiple {{site.data.keyword.powerSys_notm}} **instances**.

## Before you begin
{: #gs-before-you-begin}

Before you create your first Power Systems Virtual Server instance, review the following prerequisites:

1. {: hide-dashboard} Create an IBM Cloud account. To create an IBM Cloud account, see [Sign up for IBM Cloud ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/registration){: new_window}.

1. Create a public and private SSH key that you can use to securely connect to your {{site.data.keyword.powerSys_notm}}.

1. (Optional) If you want to use a custom image for the AIX or IBM i operating systems, you must create an IBM Cloud Object Storage and upload the image. For more information, see [Configuring a custom image](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

1. (Optional) If you want to use a private network to connect to a {{site.data.keyword.powerSys_notm}} instance, you must order the Direct Link Connect service. For more information, see [Ordering IBM Cloud Direct Link Connect from the UI Console](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## Next steps
{: #gs-next-steps}

With an IBM Cloud account and a private and public SSH key, you are now ready to [Create the {{site.data.keyword.powerSys_notm}} service](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
