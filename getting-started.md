---

copyright:
  years: 2019, 2021

lastupdated: "2022-09-13"

keywords: getting started, infrastructure as a service, iaas, before you begin, terminology, video, how-to

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
{:external: target="_blank" .external}

# Getting started with IBM Power Systems Virtual Servers
{: #getting-started}

{{site.data.keyword.powerSysFull}} is a Power Systems offering. Power Systems Virtual Servers are located in the IBM data centers, distinct from the IBM Cloud servers with separate networks and direct-attached storage. You can use the Power Systems Virtual Servers to deploy a virtual server, also known as a logical partition (LPAR), in a matter of minutes. IBM Power Systems clients who have typically relied upon on-premises-only infrastructure can now quickly and economically extend their Power IT resources off-premises. Avoid the large capital expense or added risk when migrating your essential workloads and get started with Power Systems Virtual Servers today!
{: shortdesc}

In the data centers, the Power Systems Virtual Servers are separated from the rest of the IBM Cloud servers with separate networks and direct-attached storage. The internal networks are fenced but offer connectivity options to IBM Cloud infrastructure or on-premises environments. This infrastructure design enables Power Systems Virtual Servers to maintain key enterprise software certification and support as the Power Systems Virtual Server architecture is identical to certified on-premises infrastructure.

Power Systems Virtual Servers integrates your AIX, IBM i, or Linux&reg; capabilities in an off-premises environment distinct from the IBM Cloud. You get fast, self-service provisioning, flexible management both on-premises and off-premises, and similar to on-premises it can be connected to access a stack of enterprise services from IBM – all with pay-as-you-use billing that lets you easily scale up and out. You can quickly deploy a {{site.data.keyword.powerSys_notm}} to meet your specific business needs and easily control workload demands. For frequently asked questions about the {{site.data.keyword.powerSys_notm}}, see [FAQs](/docs/power-iaas?topic=power-iaas-power-iaas-faqs).

If you are creating or configuring a {{site.data.keyword.powerSys_notm}} instance to support an SAP NetWeaver or SAP HANA workload, see [Planning your deployment](/docs/sap?topic=sap-power-vs-planning-items) and [Deploying your infrastructure](https://cloud.ibm.com/docs/sap?topic=sap-power-vs-set-up-infrastructure).

If you are creating or configuring a Red Hat OpenShift Cluster on Power Systems Virtual Server, see [Deploying Red Hat OpenShift Container Platform 4.x on IBM Power Systems Virtual Servers](https://developer.ibm.com/components/ibm-power/series/deploy-ocp-cloud-paks-power-virtual-server/){: external}.

## Terminology
{: #terminology}

Before you create a virtual server, you must understand the difference in terminology between a {{site.data.keyword.powerSys_notm}} **workspace** and a {{site.data.keyword.powerSys_notm}} **instance**. Think of the {{site.data.keyword.powerSys_notm}} **workspace** as a container for all {{site.data.keyword.powerSys_notm}} **instances** at a specific geographic region. The {{site.data.keyword.powerSys_notm}} **workspace** is available from the **Resource list** in the {{site.data.keyword.powerSys_notm}} user interface. The workspace can contain multiple {{site.data.keyword.powerSys_notm}} **instances**. For example, you can have two {{site.data.keyword.powerSys_notm}} **workspaces**, one in Dallas, Texas, and another in Washington, D.C. Each workspace can contain multiple {{site.data.keyword.powerSys_notm}} **instances**.

## Before you begin
{: #before-you-begin}

Before you create your first Power Systems Virtual Server instance, review the following prerequisites:

1. Create an IBM Cloud account. To create an IBM Cloud account, see [Signing up for the IBM Cloud](https://cloud.ibm.com/registration){: external}.

2. Review the Identity and Access Management (IAM) information at [Managing Power Systems Virtual Servers (IAM)](/docs/power-iaas?topic=power-iaas-managing-resources-and-users).

3. Create a public and private SSH key that you can use to securely connect to your {{site.data.keyword.powerSys_notm}}. To create a public and private SSH key, see [Adding an SSH key](/docs/ssh-keys?topic=ssh-keys-adding-an-ssh-key).

4. *(Optional)* If you want to use a custom AIX or IBM i image, you must create an IBM Cloud Object Storage (COS) and upload it there. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

5. *(Optional)* If you want to use a private network to connect to a {{site.data.keyword.powerSys_notm}} instance, you must order the [Direct Link Connect](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#steps-to-order-direct-link-connect) service. You cannot create a private network during the VM provisioning process. You must first use the {{site.data.keyword.powerSys_notm}} user interface, command line interface (CLI), or application programming interfaced (API) to [create one](/docs/power-iaas?topic=power-iaas-configuring-subnet).

## Next steps
{: #next-steps}

With a new IBM Cloud account and a private and public SSH key, you're ready to [Create a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)!
