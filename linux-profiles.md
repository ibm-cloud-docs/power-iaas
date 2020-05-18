---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-15"

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

# SLES for SAP (HANA) compute profiles
{: #linux-profiles}

Learn about popular Linux profiles when you provision a {{site.data.keyword.powerSys_notm}} and choose SUSE Linux Enterprise Server (SLES) for SAP (HANA) as your operating system.
{: shortdesc}

A profile is a combination of instance attributes, such as cores and Random Access Memory (RAM), that can be instantiated quickly to start a virtual server instance (VSI). In the IBM Cloud console, you can choose from popular profile configurations or select from a list of profiles that best fit your needs. To view all of the profiles available, click **View all profiles** on the provisioning page.

## Popular profiles
{: #popular-profiles}

The following popular profiles are available for SLES for SAP (HANA) virtual machines (VMs). All of the profiles are dedicated cores that are running on an [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: new_window}{: external} with **Tier 1** storage.

*cp* stands for **Compute profile**, while *bp* indicates a **Balanced profile**.
{: tip}

| Profile       | Cores    | RAM      |
| ------------- | -------- | -------- |
| cp1-4x280     | 4 CPUs   | 280 GB   |
| bp1-16x2250   | 16 CPUs  | 2250 GB  |
| bp1-50x7000   | 50 CPUs  | 7000 GB  |
| bp1-100x14000 | 100 CPUs | 14000 GB |
{: caption="Table 1. Popular SLES for SAP profiles" caption-side="top"}

## All profiles
{: #all-profiles}

To see a list of all of the available profiles for SLES for SAP (HANA) virtual machines, click **View all profiles**. All of the profiles are dedicated cores that are running on an [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: new_window}{: external} with **Tier 1** storage.

| Profile       | Cores    | RAM      | Production certified? |
| ------------- | -------- | -------- | --------------------- |
| cp1-4x280     | 4 CPUs   | 280 GB   | Under certification   |
| bp1-16x2250   | 16 CPUs  | 2250 GB  | Under certification   |
| bp1-50x7000   | 50 CPUs  | 7000 GB  | Under certification   |
| bp1-100x14000 | 100 CPUs | 14000 GB | Under certification   |
| bp1-4x512     | 4 CPUs   | 512 GB   | Not yet certified     |
| bp1-8x1024    | 8 CPUs   | 1024 GB  | Not yet certified     |
| bp1-30x4500   | 30 CPUs  | 4500 GB  | Not yet certified     |
| bp1-80x11200  | 80 CPUs  | 11200 GB | Not yet certified     |
| bp1-20x2800   | 20 CPUs  | 2800 GB  | Not yet certified     |
| bp1-25x3500   | 25 CPUs  | 3500 GB  | Not yet certified     |
| bp1-70x10000  | 70 CPUs  | 10000 GB | Not yet certified     |
{: caption="Table 2. All SLES for SAP profiles" caption-side="top"}