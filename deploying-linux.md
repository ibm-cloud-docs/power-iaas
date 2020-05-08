---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-07"

keywords: linux, sles, compute, profiles, sap, hana, compute profile, balanced profile, e980

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

# Linux Virtual Server deployment
{: #linux-deployment}

Learn about popular Linux profiles when you provision a {{site.data.keyword.powerSys_notm}} and choose SUSE Linux Enterprise Server (SLES) for SAP (HANA) as your operating system.
{: shortdesc}

A profile is a combination of instance attributes, such as cores and Random Access Memory (RAM), that can be instantiated quickly to start a virtual server instance (VSI). In the IBM Cloud console, you can choose from popular profile configurations or select from a list of profiles that best fit your needs. To view all of the profiles available, click **View all profiles** on the provisioning page.

The following popular profiles are available for SLES for SAP (HANA) virtual machines (VMs). All of the profiles are dedicated cores that are running on an [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: new_window}{: external} with **Tier 1** storage.

*cp* stands for **Compute profile**, while *bp* indicates a **Balanced profile**.
{: tip}

| Profile       | CPUs | RAM (GB) |
| ------------- | ---- | -------- |
| cp1-4x280     | 4    | 280      |
| bp1-16x2250   | 16   | 2250     |
| bp1-50x7000   | 50   | 7000     |
| bp1-100x14000 | 100  | 14000    |
{: caption="Table 1. Popular SLES for SAP profiles" caption-side="top"}
