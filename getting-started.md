---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-19"

keywords: getting started, infrastructure as a service, before you begin, terminology, video, how-to

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

# Getting started tutorial
{: #getting-started}

{{site.data.keyword.powerSysFull}} is an infrastructure as a service offering that you can use to deploy a virtual server, also known as a logical partition (LPAR), in a matter of minutes. IBM Power Systems clients who have typically relied upon on-premises-only infrastructure can now quickly and economically extend their Power IT resources into the cloud. Avoid the large capital expense or added risk when migrating your essential workloads and get started with a {{site.data.keyword.cloud_notm}} today.
{: shortdesc}

A {{site.data.keyword.cloud_notm}} integrates your IBM AIX and IBM i capabilities into the IBM Cloud experience. That means you get fast, self-service provisioning, flexible management both on-premises and off, and access to a stack of enterprise IBM Cloud services – all with pay-as-you-use billing that lets you easily scale up and out.

You can quickly deploy a {{site.data.keyword.powerSys_notm}} to meet your specific business needs. With a {{site.data.keyword.powerSys_notm}}, you can create a hybrid cloud environment that allows you to easily control workload demands. For frequently asked questions about the {{site.data.keyword.powerSys_notm}} service, see [FAQs](/docs/power-iaas?topic=power-iaas-power-iaas-faqs).

## Terminology
{: #terminology}

Before you create a virtual server, you must understand the difference in terminology between a {{site.data.keyword.powerSys_notm}} **service** and a {{site.data.keyword.powerSys_notm}} **instance**. Think of the {{site.data.keyword.powerSys_notm}} **service** as a container for all {{site.data.keyword.powerSys_notm}} **instances** at a specific geographic region. The {{site.data.keyword.powerSys_notm}} **service** is available from the **Resource list** in the {{site.data.keyword.cloud}} UI. The service can contain multiple {{site.data.keyword.powerSys_notm}} **instances**.

For example, you can have two {{site.data.keyword.powerSys_notm}} **services**, one in Dallas and another in Washington, D.C. Each service can contain multiple {{site.data.keyword.powerSys_notm}} **instances**.

## Before you begin
{: #before-you-begin}

Before you create your first Power Systems Virtual Server instance, review the following prerequisites:

1. Create an IBM Cloud account. To create an IBM Cloud account, see [Sign up for IBM Cloud](https://cloud.ibm.com/registration){: new_window}{: external}.

2. Create a public and private SSH key that you can use to securely connect to your {{site.data.keyword.powerSys_notm}}. To create a public and private SSH key, see [Adding an SSH key](/docs/ssh-keys?topic=ssh-keys-adding-an-ssh-key).

3. _(Optional)_ If you want to use a custom image for the AIX or IBM i operating systems, you must create an IBM Cloud Object Storage and upload the image. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

4. _(Optional)_ If you want to use a private network to connect to a {{site.data.keyword.powerSys_notm}} instance, you must order the Direct Link Connect service. For more information, see [Ordering Direct Link connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#steps-to-order-direct-link-connect).

    You cannot create a private network during the VM provisioning process. You must first go to the **Networks** tab.
    {: important}

5. *(Optional)* Watch the **AIX & IBM i in IBM (Public) Cloud** video to learn more about the {{site.data.keyword.powerSys_notm}} offering.

The **AIX & IBM i in IBM (Public) Cloud** video does not capture the latest updates to the {{site.data.keyword.powerSys_notm}} offering. You might notice differences in functionality between what's shown in the video and the current offering.
{: note}

<iframe id= youtube-power-iaas title= "AIX & IBM i in the IBM (Public) Cloud" type="text/html" width="560" height="315" src="https://www.youtube.com/embed/y5QaNdGJ6R0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Next steps
{: #next-steps}

With an IBM Cloud account and a private and public SSH key, you are now ready to [Create a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server).
