---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-23"

keywords: Linux, compute, profiles, SLES, SAP

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

# SUSE Linux compute profiles
{: #registering-linux}

When you provision a {{site.data.keyword.powerSys_notm}} and choose SUSE Linux Enterprise Server (SLES) for SAP, you can choose from a variety of profiles.: Balanced, Compute, and Memory.

A profile is a combination of instance attributes, such as the number of vCPUs, amount of RAM, number of GPUs, and more that can be instantiated quickly to start a virtual server instance. In the IBM Cloud console, you can choose from popular profile configurations or select from a list of profiles that best fit your needs.
{: note}

The following balanced profiles are available for x86_64 processors:

| Profile | vCPU | GB RAM | Network Performance Cap (Gbps) |
|---------|---------|---------|---------|
| bx2-2x8 | 2 | 8 | 4 |
| bx2-4x16 | 4 | 16 | 8 |
| bx2-8x32 | 8 | 32 | 16 |
| bx2-16x64 | 16 | 64 | 32 |
| bx2-32x128 | 32  | 128 | 64 |
| bx2-48x192 | 48 | 192 | 80 |
{: caption="Table 2. x86-64 balanced profile options" caption-side="top"}


Choose your machine type, processor, memory, and cores. There is a 1:1 ratio of CPUs to vCPUs for shared cores, which rounds up. For example, 1.25 CPUs equals 2 vCPUs.