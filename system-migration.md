---

copyright:
  years: 2019, 2023

lastupdated: "2023-07-06"

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

# Planning a workload migration to an IBM® Power® Systems
{: #system-migration}

When workloads are deployed on a new system, you must pay attention to its configuration and tuning to achieve the expected performance. {{site.data.keyword.powerSys_notm}} uses different IBM Power Systems: <!-- E880 (9119-MHE),  -->E980 (9080-M9S), S922 (9009-22A), and E1080 (9080-HEX). For more information, see [Hardware specifications](/docs/power-iaas?topic=power-iaas-about-virtual-server#hardware-specifications).
{: shortdesc}

For AIX, {{site.data.keyword.powerSys_notm}} supports only AIX 7.1, or later. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given. Your current AIX level and Power processor family can help determine which migration path to follow.

IBM i customers must use IBM i 7.1, or later. Clients running IBM i 6.1 must first upgrade the operating system (OS) to a current support level before migrating to the Power Systems Virtual Server. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

## Migration checklist
{: #migration-checklist}

Before you migrate to a newer IBM Power System, review the following checklist:

- Plan the system migration.
- Install the latest required software and apply the available fixes.
- Set the appropriate processor compatibility mode for logical partitions (LPARs) before and after migration.
- Plan the virtual processor (VP) and entitlement for each LPAR to best fit your operation and performance requirements.
- Follow the I/O consideration guide.
- Consider contacting [IBM Systems Lab Services](#lab-services) to ease the migration process.

<!-- ## Migrating to an IBM POWER8 system
{: #power8-migration}

**AIX 5.3 and earlier** - You need to migrate to a POWER8-supported level. To accomplish this migration, you have three options:

1. Network Installation Manager (NIM) `alt disk` migration.
2. Migrate in-place, then either `mksysb`, `alt_disk_copy`, or Logical Partition Mobility (LPM) (when migrating from a POWER6 or POWER7 system).
3. Create a `mksysb` image of an AIX 5.2 or 5.3 system, install the supported 7.1 version on the POWER8 system, and create an AIX 5.2 or 5.3 versioned WPAR from the `mksysb` image.

**AIX 6.1 or 7.1** - You have the option of doing an AIX update to a supported level instead of a migration. If you are on AIX 6.1, you must migrate to 7.1 to get POWER8 capabilities. To accomplish this migration, there are three options:

1. If you are at a level that supports POWER8 and if the system is LPM-capable, use LPM to move to the POWER8 system.
2. If you are at a level that supports POWER8, use `mksysb` or `alt_disk_copy` to move to the POWER8 system. Perform an AIX update on the POWER8 system only if needed.
3. Update in-place and either `mksysb`, `alt_disk_copy`, or LPM (when going from POWER6 or POWER7 system). If `alt_disk_copy` is chosen, the update can be to the alternative disk rather than in-place.

**IBM i V6R1, or later** - For an IBM i Power System, see [Data migrations](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzamc/rzamc1.htm){: external} to learn how to safely migrate data to an IBM POWER8 system. -->

<!-- Obsolete Power 8 content -->

## Migrating to an IBM POWER9 system
{: #power9-migration}

Learn more about migrating workloads from your older IBM POWER System to a POWER9 System. Before you begin your migration, review the information in this section.

- The support website [Fix Central](https://www.ibm.com/support/fixcentral/){: external} provides updates for IBM i and AIX. Where possible, update your LPAR operating system to the recommended levels before you migrate to a newer system.
    Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates.
    {: tip}

- POWER9 makes more efficient use of the 8 hardware SMT threads that are available per CPU (when running in *SMT8* mode). When you migrate from a older system, consider the use of SMT8. Also, consider reducing the allocation of CPUs (in dedicated CPU LPARs), or reducing VPs and CPU entitlement on shared CPU LPARs.
- Capacity planning is important when you are considering processor migration. When you are setting performance improvement goals and expectations, take note of the application behavior (for example, highly multi-threaded workloads vs single-threaded workload).

To learn more about IBM POWER9 system performance and migration strategies, see the following articles:

- [Hints and tips for migrating workloads to IBM POWER9 processor-based systems](https://www.ibm.com/downloads/cas/39XWR7YM){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}

<!-- ## Migrating to an IBM POWER10 system
{: #power10-migration}

Learn more about migrating workloads from an existing IBM POWER system to a POWER10 system. Before you begin your migration, review the information in this section.

**AIX and IBM i** - The support website [Fix Central](https://www.ibm.com/support/fixcentral/){: external} provides updates for IBM i and AIX. Where possible, update your LPAR operating system to the recommended levels before you migrate to a newer system. Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates. Hence it is recommended to install the required and latest updates from Fix Central before you start your migration. For IBM i the supported levels are IBM i 7.3 TR 11 and IBM i 7.4 TR 5, or later.

**Linux** - You must migrate your Linux operating system level to a Power10-supported level. To accomplish this migration, the following Linux distributions are supported:

|  IBM® Power10 processor-based systems    |  Supported Linux distributions  |
|-------------------|--------------|
| 9080-HEX (IBM Power® E1080)   |  Little Endian: \n * Red Hat Enterprise Linux 8.4, any subsequent RHEL 8.x releases \n * Red Hat Enterprise Linux 8.2 (POWER9 compatibility mode only). \n * SUSE Linux Enterprise Server 15 SP3, any subsequent SLES 15 updates \n * SUSE Linux Enterprise Server 12 SP5 (POWER9 compatibility mode only) |

{: caption="Table 1. Supported Linux distributions for Power10 processor-based systems" caption-side="bottom"}

To learn more about IBM POWER10 system performance and migration strategies, see the following articles:

- [System to IBM i mapping](https://www.ibm.com/support/pages/system-ibm-i-mapping){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}
- [Supported Linux distributions and virtualization options for Power10 Linux on Power servers](https://www.ibm.com/docs/en/linux-on-systems?topic=lpo-supported-linux-distributions-virtualization-options-power10-linux-power-servers){: external} -->

<!-- new power 10 content. p10 systems not enabled in DCs yet as of July 06, 23 -->
## Lab services
{: #lab-services}

[IBM Systems Lab Services](https://www.ibm.com/it-infrastructure/services/lab-services){: external} has service offerings available to assist you with resolving system, application, and database performance problems. Formal and informal training opportunities are also available where you can learn how to use performance tools and resolve issues on your own. If you need help with assessing the potential impact of a migration, benchmarking a system environment, or identifying ways to improve performance, contact [IBM Lab Services](mailto:ibmsls@us.ibm.com){: external}.
