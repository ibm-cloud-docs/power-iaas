---

copyright:
  years: 2019, 2020

lastupdated: "2020-04-29"

keywords: linux, sles, compute, profiles, sap, hana, compute profile, balanced profile

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

# SUSE Linux compute profiles
{: #linux profiles}

Learn about popular Linux profiles when you provision a {{site.data.keyword.powerSys_notm}} and choose SUSE Linux Enterprise Server (SLES) for SAP (HANA) as your operating system.

A profile is a combination of instance attributes, such as cores and Random Access Memory (RAM), that can be instantiated quickly to start a virtual server instance (VSI). In the IBM Cloud console, you can choose from popular profile configurations or select from a list of profiles that best fit your needs. To view all of the profiles available, click **View all profiles** on the provisioning page.

The following popular profiles are available for SLES for SAP (HANA) virtual machines (VMs):

*cp* stands for **Compute profile**, while *bp* indicates a **Balanced profile**.
{: tip}

| Profile      | CPUs | RAM  |
| ------------ | ---- | ---- |
| cp1-4x280    | 4    | 280  |
| bp1-16x2250  | 16   | 16   |
| bp1-16x7000  | 50   | 7000 |
| bp1-16x14000 | 16   | 64   |
| bx2-32x128   | 32   | 128  |
| bx2-48x192   | 48   | 192  |
{: caption="Table 1. Popular SLES for SAP profiles" caption-side="top"}
