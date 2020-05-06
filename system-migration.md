---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-05"

keywords: workload migration, power systems, hardware, migration checklist

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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Planning a workload migration to an IBM POWER8 or POWER9 system
{: #system-migration}

When workloads are deployed on a new system, you must pay attention to its configuration and tuning to achieve the expected performance. The {{site.data.keyword.powerSys_notm}} service uses three different IBM Power Systems: E880 (9119-MHE), E980 (9080-M9S), and S922 (9009-22A). For more information, see [Hardware specifications](/docs/power-iaas?topic=power-iaas-about-virtual-server#hardware-specifications).
{: shortdesc}

The {{site.data.keyword.powerSys_notm}} service supports only AIX 7.1, or later. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given. Your current AIX level and POWER processor family can help determine which migration path to follow.

IBM i customers must use IBM i 7.2, or later. Clients running IBM i 7.1 with a plan to move to an E880 (9119-MHE) must first upgrade the operating system (OS) to a current support level before migrating to the Cloud. IBM i 7.2 supports direct upgrades from IBM i 5.4, 6.1 or 7.1. To learn more, see [Migrating to i 7.2 from 5.4, 6.1 or 7.1](https://www.ibm.com/support/knowledgecenter/en/ssw_ibm_i_72/rzahy/rzahymig-po.htm){: new_window}{: external}.

## Migration checklist
{: #migration-checklist}

Before you migrate to a newer IBM Power System, review the following checklist:

- Plan the system migration.
- Install the latest required software and apply the available fixes.
- Set the appropriate processor compatibility mode for logical partitions (LPARs) before and after migration.
- Plan the virtual processor (VP) and entitlement for each LPAR to best fit your operation and performance requirements.
- Follow the I/O consideration guide.
- Consider contacting [IBM Systems Lab Services](#lab-services) to ease the migration process.

## Migrating to an IBM POWER8 system
{: power8-migration}

**AIX 5.3 and earlier**

You need to migrate to a POWER8-supported level. To accomplish this migration, you have three options:

1. Network Installation Manager (NIM) `alt disk` migration
2. Migrate in-place, then either `mksysb`, `alt_disk_copy`, or Logical Partiion Mobility (LPM) (when going from a
POWER6 or POWER7 system).
3. Create a `mksysb` of an AIX 5.2 or 5.3 system, install the supported 7.1 version on the POWER8 system, and create an AIX 5.2 or 5.3 versioned WPAR from the `mksysb`.

**AIX 6.1 or 7.1**

You have the option of doing an AIX update to a supported level instead of a migration. If you are on AIX 6.1, you must migrate to 7.1 to get POWER8 capabilities. To accomplish this migration, there are three options:

1. If you are at a level that supports POWER8 and if the system is LPM-capable, use LPM to move to the POWER8 system.
2. If you are at a level that supports POWER8, use `mksysb` or `alt_disk_copy` to move to the POWER8 system. Perform an AIX update on the POWER8 system only if needed.
3. Update in-place and either `mksysb`, `alt_disk_copy`, or LPM (when going from POWER6 or POWER7 system). If `alt_disk_copy` is chosen, the update can be to the alternative disk rather than in-place.

Learn more about transitioning to an IBM POWER8 system by downloading [Transitioning to POWER8: Migration Paths for AIX systems to POWER8](http://www14.software.ibm.com/webapp/set2/sas/f/best/Transitioning_to_POWER8.pdf){: new_window}{: external}.

**IBM i V6R1, or later**

For an IBM i Power System, see [Data migrations](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzamc/rzamc1.htm){: new_window}{: external} to learn how to safely migrate data to an IBM POWER8 system.

## Migrating to an IBM POWER9 system
{: power9-migration}

Learn more about migrating workloads from an existing IBM POWER7 or POWER8 system to a POWER9 system. Before you begin your migration, review the information in this section.

- The support website [Fix Central](https://www.ibm.com/support/fixcentral/){: new_window}{: external} provides updates for IBM i and AIX. Where possible, update your LPAR operating system to the recommended levels before you migrate to a newer system.

    Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates.
    {: note}

- POWER9 makes more efficient use of the 8 hardware SMT threads that are available per CPU (when running in *SMT8* mode). When you migrate from a POWER7 or POWER8 system, consider the use of SMT8. Also, consider reducing the allocation of CPUs (in dedicated CPU LPARs), or reducing VPs and CPU entitlement on shared CPU LPARs.

- Capacity planning is important when you are considering processor migration. When you are setting performance improvement goals and expectations, take note of the application behavior (for example, highly multi-threaded workloads vs single-threaded workload).

To learn more about IBM POWER9 system performance and migration strategies, see the following articles:

- [Hints and tips for migrating workloads to IBM POWER9 processor-based systems](https://www.ibm.com/downloads/cas/39XWR7YM){: new_window}{: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: new_window}{: external}
- [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: new_window}{: external}

## Lab services
{: #lab-services}

[IBM Systems Lab Services](https://www.ibm.com/itinfrastructure/services/lab-services){: new_window}{: external} has service offerings available to assist you with resolving system, application, and database performance problems. Formal and informal training opportunities are also available where you can learn how to use performance tools and resolve issues on your own. If you need help with assessing the potential impact of a migration, benchmarking a system environment, or identifying ways to improve performance, contact [IBM Lab Services](mailto:ibmsls@us.ibm.com){: new_window}{: external}.
