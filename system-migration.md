---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-20"

keywords: workload migration, power systems, hardware, migration checklist

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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Planning a workload migration to {{site.data.keyword.powerSysFull}}
{: #system-migration}

When workloads are deployed on a new system, you must pay attention to its configuration and tuning to achieve the expected performance. {{site.data.keyword.powerSys_notm}} uses different IBM Power Systems: E980 (9080-M9S), S922 (9009-22A), and S1022 (9105-22A) .
{: shortdesc}

For more information on hardware specifications that you might need, see [Hardware specifications for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-about-power-iaas#hardware-specifications-on-cloud) and [Hardware and software specifications for {{site.data.keyword.powerSys_notm}} Private Cloud](/docs/power-iaas?topic=power-iaas-about-power-iaas#hardware-software-specs-private-cloud).

For AIX, {{site.data.keyword.powerSys_notm}} supports only AIX 7.1, or later. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given. Your current AIX level and POWER processor family can help determine which migration path to follow.

IBM i customers must use IBM i 7.2 or later. If you are running IBM i 6.1, you must first upgrade the operating system (OS) to a current support level before migrating to the {{site.data.keyword.powerSys_notm}}. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

## Migration checklist
{: #migration-checklist}

Before you migrate to a newer IBM Power, review the following checklist:

- Plan the system migration.
- Install the latest required software and apply the available fixes.
- Set the appropriate processor compatibility mode for logical partitions (LPARs) before and after migration.
- Plan the virtual processor (VP) and entitlement for each LPAR to best fit your operation and performance requirements.
- Follow the I/O consideration guide.
- Consider contacting [IBM Technology Expert Labs](#lab-services) to ease the migration process.

## Migrating to an IBM Power9
{: #power9-migration}

Learn more about migrating workloads from your older IBM POWER to a Power9. Before you begin your migration, review the information in this section.

Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates.
{: tip}

- Power9 makes more efficient use of the 8 hardware SMT threads that are available per CPU (when running in *SMT8* mode). When you migrate from an older system, consider the use of SMT8. Also, consider reducing the allocation of CPUs (in dedicated CPU LPARs), or reducing VPs and CPU entitlement on shared CPU LPARs.
- Capacity planning is important when you are considering processor migration. When you are setting performance improvement goals and expectations, take note of the application behavior (for example, highly multi-threaded workloads vs single-threaded workloads).

To learn more about IBM Power9 performance and migration strategies, see the following articles:

- [Hints and tips for migrating workloads to IBM Power9](https://www.ibm.com/downloads/cas/39XWR7YM){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}

## Migrating to an IBM Power10
{: #power10-migration}

Learn more about migrating workloads from an existing IBM Power to a Power10. Before you begin your migration, review the information in this section.

**AIX and IBM i** - You must update your LPAR operating system to the recommended levels before you migrate to a newer system. Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates. Hence it is recommended to install the required and latest updates from Fix Central before you start your migration. For IBM i the supported levels are IBM i 7.3 TR 11 and IBM i 7.4 TR 5, or later.

**Linux** - You must migrate your Linux operating system level to a Power10-supported level. To accomplish this migration, the following Linux distributions are supported:

|  IBM® Power10 processor-based systems    |  Supported Linux distributions  |
|-------------------|--------------|
| S1022 (9105-22A)   |  * Red Hat Enterprise Linux 8.4, any subsequent RHEL 8.x releases \n * Red Hat Enterprise Linux 8.2 (Power9 compatibility mode only). \n * SUSE Linux Enterprise Server 15 SP3, any subsequent SLES 15 updates \n * SUSE Linux Enterprise Server 12 SP5 (Power9 compatibility mode only) |
{: caption="Table 1. Supported Linux distributions for Power10 processor-based systems" caption-side="bottom"}



To learn more about IBM Power10 performance and migration strategies, see the following articles:

- [System to IBM i mapping](https://www.ibm.com/support/pages/system-ibm-i-mapping){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}
- [Supported Linux distributions and virtualization options for Power10 Linux on Power servers](https://www.ibm.com/docs/en/linux-on-systems?topic=lpo-supported-linux-distributions-virtualization-options-power10-linux-power-servers){: external} 


## Lab services
{: #lab-services}

[IBM Technology Expert Labs](https://www.ibm.com/products/expertlabs){: external} has service offerings available to assist you with resolving system, application, and database performance problems. Formal and informal training opportunities are also available where you can learn how to use performance tools and resolve issues on your own.
