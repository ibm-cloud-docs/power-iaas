---

copyright:
  years: 2019

lastupdated: "2019-09-27"

keywords: faq, virtual server, network bandwidth billing, multi-tenant environment, ibm cloud

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

# FAQ
{: #power-iaas-faqs}

## Where can I learn how to use a Power Systems Virtual Server?
{: #training}
{: faq}

To learn more about how to use a {{site.data.keyword.powerSys_notm}}, see the [AIX & IBM i in IBM (Public) Cloud](https://youtu.be/y5QaNdGJ6R0){: new_window}{: external}c video.

This video does not capture the latest updates to the {{site.data.keyword.powerSys_notm}} offering. You might notice differences in functionality between what's shown in the video and the current offering.
{: note}

## What versions of AIX and IBM i operating systems are supported?
{: #os_versions}
{: faq}

The supported AIX and IBM i operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}: S922 (9009-22A) or E880 (9119-MHE). To view a list of the supported AIX and IBM i operating system technology levels, see the following system software maps:

Because AIX 6.1 does not support `cloud-init`, you must perform a `mksysb-based` installation of the operating system over an existing LPAR that was provisioned.
{: important}

**AIX**

* [S922 (9009-22A) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-all-io){: new_window}{: external}
* [E880 (9119-MHE) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9119-MHE-all-io){: new_window}{: external}

**IBM i**

* [S922 (9009-22A) and E880 (9119-MHE) software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: new_window}{: external}

## Can I use my own AIX or IBM i image?
{: #image}
{: faq}

Yes. This function is known as **bring your own image**. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/infrastructure/power-iaas?topic=power-iaas-deploy-custom-image).

## What formats should I use when uploading a custom image?
{: #custom-image}
{: faq}

Currently, you can import a custom image in the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.

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

For more information, see [Hardware specifications](/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-hardware-specifications).

## Do Power Systemes Virtual Servers run in a multi-tenant environment?
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

For more information, see [Ordering IBM Cloud Direct Link Connect for Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## How do you set up customer site access to a private network by using VPN?
{: #configuring}
{: faq}

For more information, see [Configuring IBM Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-power).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

You must set your own firewall in your IBM Cloud account.

## How is network bandwidth billed?
{: #billing}
{: faq}

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
