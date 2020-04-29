---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-27"

keywords: linux, registering, subscription, sles, rhel

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

# Using Linux within a Power Systems Virtual Server
{: #using-linux}

{{site.data.keyword.powerSysShort}} service supports SUSE Linux Enterprise Server (SLES) and Red Hat Enterprise Linux (RHEL).

## Preparing your Power Systems Virtual Server to use SLES
{: #preparing-sles}

The {{site.data.keyword.powerSys_notm}} service does not provide a subscription to SUSE Linux. You must purchase the SUSE Linux subscription from SUSE and then enable it.

You cannot contact the SUSE-based repository and download the appropriate software packages without first enabling your SUSE Linux subscription.
{: note}

1. To buy a SUSE subscription, see [How to Buy](https://www.suse.com/support/?id=SUSE_Linux_Enterprise_Server_for_SAP_Applications#how-to-buy){: new_window}{: external}.
2. To register your system, see [Registering an Installed System](https://documentation.suse.com/sles/12-SP4/single-html/SLES-deployment/#sec-y2-sw-register){: new_window}{: external}.

## Preparing your Power Systems Virtual Server to use RHEL
{: #preparing-rhel}

To use RHEL within the {{site.data.keyword.powerSys_notm}} service, you must use PowerVC to capture your RHEL image, then import it as an Open Virtualization Appliance (OVA) file.
