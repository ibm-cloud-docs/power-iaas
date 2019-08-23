---

copyright:
  years: 2019n

lastupdated: "2019-03-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}

# FAQ
{: #power-iaas-faqs}

## What versions of AIX and IBM i operating systems are supported?
{: #os_versions}
{: faq}

The supported AIX and IBM i operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}: S922 (9009-22A) or E880 (9119-MHE). To view a list of the supported AIX and IBM i operating system technology levels and IBM Power System hardware, see [System software maps ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps).

## Can I use my own AIX or IBM i image?
{: #image}
{: faq}

Yes. This function is known as **bring your own image**. For more information, see [Configuring a custom image](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image).

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

You are responsible for third-party licensing.

## What are the hardware specifications?
{: #hardwarespecs}
{: faq}

For hardware specifications, see [Hardware specifications](/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-hardware-specifications).

## Does {{site.data.keyword.powerSys_notm}} run in a multi-tenant environment?
{: #multi}
{: faq}

Yes, {{site.data.keyword.powerSys_notm}} runs in a multi-tenant environment.

## Are there bare-metal options?
{: #bare}
{: faq}

No, there are no bare-metal options. The {{site.data.keyword.powerSys_notm}} offering focuses on virtual instances.

## What training is available using IBM Cloud?
{: #training}
{: faq}

To learn more about how to use IBM Power Systems Virtual Servers, see the [AIX & IBM i in IBM (Public) Cloud ![External link icon](../icons/launch-glyph.svg "External link icon")](https://youtu.be/y5QaNdGJ6R0) video.

## How do you set up private networks between Intel&trade; Virtual Servers (x86) and Power System Virtual Servers?
{: #connecting}
{: faq}

For more information, see [Ordering IBM Cloud Direct Link Connect for Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## How do you set up customer site access to that private network by using VPN?
{: #configuring}
{: faq}

For more information, see [Configuring IBM Power Systems Virtual Servers](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

You must set your own firewall in your IBM Cloud account.

## How is network bandwidth billed?
{: #billing}
{: faq}

IBM does not currenty charge for public network traffic (this is subject to change). If you are using a private network with DirectLink Connect, you are charged IBM's standard rates. Public bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 500 GB is included with each monthly bare metal server. Extra bandwidth can also be purchased per packages.For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth).

<!-- ## WBackup and DR options for Virtual Servers?
{: #wbackup}
{: faq}

Backup and DR for cloud to cloud – BRMS with Cloud Storage Solutions or use manual with Savsys.  PowerHA Enterprise edition for Geo.  Licensing TBD for this bundle (can not bring their own license) – Bob to determine date/terms. -->

## What monitoring services are available?
{: #monitoring}
{: faq}

IBM does not provide status and performance monitoring for the IBM Cloud. The client must use their own on-premises tools.

## What performance and capacity planning services do you provide for IBM i on IBM Cloud?
{: #ibmi-performance}
{: faq}

IBM uses the same tools that are on an on-premises system.

## IBM i and solution certification
{: #ibmi-certification}
{: faq}

You can find self-certification and listing information on the [IBM Global Solutions Directory ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www-356.ibm.com/partnerworld/gsd/homepage.do).

<!--
## Is there a price difference between shared or dedicated cores?
{: #shared}
{: faq}

No. Performance of shared cores is almost identical to dedicated cores. However, as server utilization spikes, there might be a cache or memory latency impacts. -->
