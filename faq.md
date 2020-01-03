---

copyright:
  years: 2019

lastupdated: "2020-1-03"

keywords: faq, virtual server, network bandwidth, private network setup, multi-tenant environment, delete service, supported operating systems, hardware specifications, software maps

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
{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}

# FAQ
{: #power-iaas-faqs}

## Where can I learn how to use a Power Systems Virtual Server?
{: #training}
{: faq}
{: support}

To learn more about how to use a {{site.data.keyword.powerSys_notm}}, see the [AIX & IBM i in IBM (Public) Cloud](https://youtu.be/y5QaNdGJ6R0){: new_window}{: external} video.

This video does not capture the latest updates to the {{site.data.keyword.powerSys_notm}} offering. You might notice differences in functionality between what's shown in the video and the current offering.
{: note}

## What versions of AIX and IBM i operating systems are supported?
{: #os_versions}
{: faq}
{: support}

The supported AIX and IBM i operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}: S922 (9009-22A) or E880 (9119-MHE). To view a list of the supported AIX and IBM i operating system technology levels, see the following system software maps:

Because AIX 6.1 does not support `cloud-init`, you must perform a `mksysb-based` installation of the operating system over an existing LPAR that was provisioned.
{: important}

**AIX**

* [S922 (9009-22A) AIX software map ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-vios-only)
* [E880 (9119-MHE) AIX software map ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9119-MHE-vios-only)

**IBM i**

* [S922 (9009-22A) and E880 (9119-MHE) software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: new_window}{: external}

## Can I use my own AIX or IBM i image?
{: #image}
{: faq}
{: support}

Yes. This function is known as **bring your own image**. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/infrastructure/power-iaas?topic=power-iaas-deploy-custom-image).

## What formats should I use when uploading a custom image?
{: #custom-image}
{: faq}

Currently, you can import a custom image in the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.

## What are the available boot image storage types?
{: #storage}
{: faq}
{: support}

The storage types vary by region. The storage type cannot be changed once the volume is created.

The **us-east (WDC)** and **us-south (DAL)** regions use **Standard** or **SSD** storage types.

The **eu-de (FRA04)** region uses **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs should select **Tier 3**. For more information, see [Importing a boot image](/docs/infrastructure/power-iaas?topic=power-iaas-importing-boot-image#console-import-image).

## Does IBM provide maintenance for the AIX or IBM i operating systems?
{: #licensing_os}
{: faq}

No. It is the customer's responsibility to maintain, update, and manage the AIX or IBM i operating system.

## How does licensing work for the AIX and IBM i operating systems?
{: #os_support}
{: faq}

The license for the operating system is part of the overall cost for the service. You cannot use an existing license that you already purchased.

## How does third-party licensing work?
{: #thridparty}
{: faq}

Clients are responsible for third-party licensing.

## What are the hardware specifications?
{: #hardwarespecs}
{: faq}
{: support}

For more information, see [Hardware specifications](/docs/infrastructure/power-iaas?topic=power-iaas-about-virtual-server#hardware-specifications).

## Do Power Systems Virtual Servers run in a multi-tenant environment?
{: #multi}
{: faq}

Yes, {{site.data.keyword.powerSys_notm}} run in a multi-tenant environment.

## Are there bare-metal options?
{: #bare}
{: faq}

There are no bare-metal options. The {{site.data.keyword.powerSys_notm}} offering focuses on virtual instances.

## How do you set up private networks between Intel&reg; Virtual Servers (x86) and Power System Virtual Servers?
{: #connecting}
{: faq}
{: support}

For more information, see [Ordering IBM Cloud Direct Link Connect for Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## How do you set up customer site access to a private network by using VPN?
{: #configuring}
{: faq}
{: support}

For more information, see [Configuring IBM Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-power).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

You must set your own firewall in your IBM Cloud account.

## How do you connect a server instance between two colocations (DAL to WDC)?
{: #gts-cloud-connect}
{: faq}
{: support}

You can use IBM Cloud Connect to connect two colocations. IBM Cloud Connect is a software-defined network interconnect service that brings secure public cloud and SaaS solution connectivity to client locations around the world. For more information, see [Connecting Power Systems Virtual Server instances and networks](/docs/infrastructure/power-iaas?topic=power-iaas-connecting-networks).

## How is network bandwidth billed?
{: #billing}
{: faq}
{: support}

**IBM Cloud Classic environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 20 TB is included with each monthly bare metal server. Extra bandwidth can also be purchased per packages. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: new_window}{: external}.

**IBM Cloud Power environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per gigabyte (GB) when using a public network. If you are using a private network with DirectLink Connect, you are charged **IBM Cloud Classic environment** rates.

## What monitoring services are available?
{: #monitoring}
{: faq}

IBM does not provide status and performance monitoring for the IBM Cloud. Clients must use their own on-premises tools.

## What performance and capacity planning services do you provide for IBM i on IBM Cloud?
{: #ibmi-performance}
{: faq}

IBM uses the same tools that are on an on-premises system.

## IBM i and solution certification
{: #ibmi-certification}
{: faq}

You can find self-certification and listing information on the [IBM Global Solutions Directory](https://www-356.ibm.com/partnerworld/gsd/homepage.do){: new_window}{: external}.

## How do I delete the service or a specific instance?
{: #delete-service}
{: faq}

You can delete the service by clicking the overflow menu in the **Virtual server instances** page and selecting **Delete service**. To delete an instance, click the trash icon after you select the wanted instance.
