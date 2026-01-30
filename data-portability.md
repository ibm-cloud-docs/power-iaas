---

copyright:
  years: 2025
lastupdated: "2026-01-30"

keywords: data portability, power virtual server

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}



# Understanding data portability for {{site.data.keyword.powerSys_notm}}
{: #data-portability}



---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}

---

On IBM Cloud, data portability refers to a set of tools and procedures. You can use data to transfer data from {{site.data.keyword.powerSysFull}} to on-premises or on a different service provider that supports the Power architecture to implement a similar workload or to process data.
{: shortdesc}

{{site.data.keyword.powerSys_notm}} is an Infrastructure as a Service (IaaS) offering. As a {{site.data.keyword.powerSys_notm}} user, you own the data, operating system images, and configuration parameters. The {{site.data.keyword.powerSys_notm}} architecture follows Power deployments within infrastructure to facilitate data portability. The {{site.data.keyword.powerSys_notm}} architecture is identical to a certified private cloud infrastructure. The infrastructure is designed such that the {{site.data.keyword.powerSys_notm}} can maintain key enterprise software certification and support.

## Responsibilities
{: #data-port-respon}

{{site.data.keyword.powerSys_notm}} provides interfaces and instructions to guide you to copy and store your content on your selected location. The content can include data that is stored on logical volumes, operating system images, and configuration parameters.

You are responsible for the following actions:
- Use of the exported data
- Use of the configuration to enable data portability to other infrastructures
- Create and execute the plan to set up the infrastructure on a different service provider that has capabilities similar to the {{site.data.keyword.powerSys_notm}} services

For more information about the responsibility assignment matrix for {{site.data.keyword.powerSys_notm}}, see [High-level architecture](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#high-level-architecture-on-cloud).

## Migrating data
{: #data-port-export-proc}

To migrate data from one infrastructure to another, you must create a plan and have a strategy to achieve the expected performance. Complete the steps that are defined in the following topics to migrate Power workloads to a {{site.data.keyword.powerSys_notm}}:

* [Planning a workload migration to IBM&reg; Power&reg; Virtual Server](/docs/power-iaas?topic=power-iaas-system-migration)
* [Migration strategies for AIX](/docs/power-iaas?topic=power-iaas-migration-aix)
* [Migration strategies for IBM i](/docs/power-iaas?topic=power-iaas-migration-strategies-power)
* [Additional migration strategies](/docs/power-iaas?topic=power-iaas-additional-migration-strategies-power)
* [Using third-party tools for migration](/docs/power-iaas?topic=power-iaas-migration-strategies-managed-thirdparty)
* [Back up and restore](/docs/power-iaas?topic=power-iaas-backup-restore)

You can use {{site.data.keyword.powerSys_notm}} to capture full or specific copies of the logical volumes or data sets. By using IBM FlashCopy&reg; feature and {{site.data.keyword.powerSys_notm}} APIs, you can create delta snapshots, volume clones, and restore your disks. For more information, see [Snapshots, cloning, and restoring](/docs/power-iaas?topic=power-iaas-snapshots-cloning).

## Exported data formats
{: #data-port-export-data}

{{site.data.keyword.powerSys_notm}} provides mechanisms to capture and export a virtual machine (VM). For more information about the available options to capture and export a VM, see [Capturing and exporting a virtual machine (VM)](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm).


## Data ownership
{: #data-port-data-owner}

The data that is exported to your on-premises resources or on service providers resources is classified as customer content. Customer ownership and licensing rights are applicable to the exported content as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/terms/?id=Z126-6304_WS){: external}.
