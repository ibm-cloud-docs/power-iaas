---

copyright:
  years: 2019, 2022

lastupdated: "2022-09-15"

keywords: linux, sles, compute, profiles, sap, hana, compute profile, balanced profile, e980

subcollection: power-iaas

---

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

# System Applications and Products in Data Processing (SAP) and Power Systems Virtual Servers
{: #power-iaas-sap}

Learn more about SAP within {{site.data.keyword.powerSysShort}}.
{. shortdesc}

## Implementing SAP NetWeaver in the Power Systems Virtual Server environment
{: #sap-netweaver}

You can deploy SAP NetWeaver on an AIX or Linux&reg; operating system within the Power Systems Virtual Server environment. Select **AIX** or **SLES for SAP (NetWeaver) - Client supplied subscription** under **Operating system** in the {{site.data.keyword.powerSys_notm}} user interface, and deploy the virtual machine (VM). After you deploy the VM, you can deploy NetWeaver inside of it.

When you select the **SLES for SAP (NetWeaver) - Client supplied subscription** option, the **SLES for SAP** operating system is deployed inside the provisioned VM. You need to purchase the subscription for the **SLES for SAP** operating system and register it inside the VM by using the **SLES registration server**. For more information on purchasing and registering Linux subscriptions, see [Using Linux within the Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-using-linux).

You can choose any sized resources (CPU, memory, etc.) when you deploy the VM for NetWeaver purposes.
{: note}

## SLES for SAP (HANA) compute profiles
{: #linux-profiles}

Learn about popular Linux profiles when you provision a {{site.data.keyword.powerSys_notm}} and choose SLES for SAP (HANA) as your operating system.

A profile is a combination of instance attributes, such as cores and Random Access Memory (RAM), that can be instantiated quickly to start a virtual server instance (VSI). Inside the {{site.data.keyword.powerSys_notm}} user interface, you can choose from popular profile configurations or select from a list of profiles that best fit your needs. To view all of the profiles available, click **View all profiles** on the provisioning page.

## Popular profiles
{: #popular-profiles}

The following popular profiles are available for SLES for SAP (HANA) VMs. All of the profiles are dedicated cores that are running on an [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: external} with **Tier 1** storage.

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

To see a list of all of the available profiles for SLES for SAP (HANA) VMs, click **View all profiles**. All of the profiles are dedicated cores that are running on an [IBM Power System E980 (9080-M9S)](https://www.ibm.com/downloads/cas/VX0AM0EP){: external} with **Tier 1** storage.

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
