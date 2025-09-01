---

copyright:
  years: 2019, 2025

lastupdated: "2025-08-25"

keywords: workload migration, power systems, hardware, migration checklist

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Planning a workload migration to {{site.data.keyword.powerSysFull}}
{: #system-migration}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

When workloads are deployed on a new system, you must pay attention to its configuration and tuning to achieve the expected performance. {{site.data.keyword.powerSys_notm}} uses different IBM Power Systems depending on the location type.
{: shortdesc}



[{{site.data.keyword.off-prem}}]{: tag-blue}

- E980 (9080-M9S)
- S922 (9009-22A)
- S1022 (9105-22A)
- E1080 (9080-HEX)
- S1122 (9824-22A)

[{{site.data.keyword.on-prem}}]{: tag-red}

- S1122 (9824-22A)
- E1150 (9043-MRU)
- E1180 (9080-HEU)









For more information on hardware specifications that you might need, see [Hardware specifications for {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}}](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#hardware-specifications-on-cloud) and [Hardware and software specifications for {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}} ](/docs/power-iaas?topic=power-iaas-private-cloud-architecture#hardware-software-specs-private-cloud).



## Supported AIX versions for {{site.data.keyword.powerSys_notm}}
{: migration-aix-sup}

For AIX, {{site.data.keyword.powerSys_notm}} supports only AIX 7.1, or later. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given. Your current AIX level and POWER processor family can help determine which migration path to follow.


## Supported IBM i versions for {{site.data.keyword.powerSys_notm}}
{: migration-IBMi-sup}

IBM i customers must use IBM i 7.2 or later. If you are running IBM i 6.1, you must first upgrade the operating system (OS) to a current support level before migrating to the {{site.data.keyword.powerSys_notm}}. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

## Migration checklist for {{site.data.keyword.powerSys_notm}}
{: #migration-checklist}

Before you migrate to a newer IBM Power, review the following checklist:

- Plan the system migration.
- Install the latest required software and apply the available fixes.
- Set the appropriate processor compatibility mode for logical partitions (LPARs) before and after migration.
- Plan the virtual processor (VP) and entitlement for each LPAR to best fit your operation and performance requirements.
- Perform the steps provided in the I/O consideration guide.
- Consider contacting [IBM Technology Expert Labs](#lab-services) to ease the migration process.




## Migrating to an IBM Power11
{: #power11-migration}

Learn more about migrating workloads from an existing IBM Power system to a Power11 system. Before you begin your migration, review the information in this section.

**AIX and IBM i** - You must update your LPAR operating system to the recommended levels before you migrate to a newer system. Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates. Hence it is recommended to install the required and latest updates from Fix Central before you start your migration.

**Linux** - You must migrate your Linux operating system level to a Power11-supported level.

For more information about the supported operating system levels and available stock images for Power11 systems, see [What versions of AIX, IBM i, and Linux® are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).




For more information about IBM Power11 performance and migration strategies, see the following articles:

- [System to IBM i mapping](https://www.ibm.com/support/pages/system-ibm-i-mapping){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}
- [System software maps for SUSE Linux Enterprise Server](https://www.ibm.com/support/pages/node/6023374){: external}
- [System software maps for Red Hat Enterprise Linux](https://www.ibm.com/support/pages/node/6024466){: external}



## Migrating to an IBM Power10 in IBM data center
{: #power10-migration}

[{{site.data.keyword.off-prem}}]{: tag-blue}


Learn more about migrating workloads from an existing IBM Power system to a Power10 system. Before you begin your migration, review the information in this section.

**AIX and IBM i** - You must update your LPAR operating system to the recommended levels before you migrate to a newer system. Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates. Hence it is recommended to install the required and latest updates from Fix Central before you start your migration. For IBM i the supported levels are IBM i 7.3 TR 11 and IBM i 7.4 TR 5, or later.

**Linux** - You must migrate your Linux operating system level to a Power10-supported level.

For more information about the supported operating system levels and available stock images for Power11 systems, see [What versions of AIX, IBM i, and Linux® are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).




To learn more about IBM Power10 performance and migration strategies, see the following articles:

- [System to IBM i mapping](https://www.ibm.com/support/pages/system-ibm-i-mapping){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power performance resource center](https://www.ibm.com/it-infrastructure/resources/power-performance/){: external}
- [Supported Linux distributions and virtualization options for Power10 Linux on Power servers](https://www.ibm.com/docs/en/linux-on-systems?topic=lpo-supported-linux-distributions-virtualization-options-power10-linux-power-servers){: external}


## Migrating to an IBM Power9 in IBM data center
{: #power9-migration}

[{{site.data.keyword.off-prem}}]{: tag-blue}

Learn more about migrating workloads from your older IBM POWER to a Power9 system. Before you begin your migration, review the information in this section.

Installing only the minimum levels can leave your partitions or workloads vulnerable to issues that have been resolved in some of the latest updates.
{: tip}

- Power9 makes more efficient use of the 8 hardware SMT threads that are available per CPU (when running in *SMT8* mode). When you migrate from an older system, consider the use of SMT8. Also, consider reducing the allocation of CPUs (in dedicated CPU LPARs), or reducing VPs and CPU entitlement on shared CPU LPARs.
- Capacity planning is important when you are considering processor migration. When you are setting performance improvement goals and expectations, take note of the application behavior (for example, highly multi-threaded workloads vs single-threaded workloads).

To learn more about IBM Power9 performance and migration strategies, see the following articles:

- [Hints and tips for migrating workloads to IBM Power9](https://www.ibm.com/downloads/cas/39XWR7YM){: external}
- [IBM i on Power - Performance FAQ](https://www.ibm.com/downloads/cas/QWXA9XKN){: external}
- [IBM Power Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}


## Lab services for {{site.data.keyword.powerSys_notm}}
{: #lab-services}

[IBM Technology Expert Labs](https://www.ibm.com/products/expertlabs){: external} has service offerings available to assist you with resolving system, application, and database performance problems. Formal and informal training opportunities are also available where you can learn how to use performance tools and resolve issues on your own.
