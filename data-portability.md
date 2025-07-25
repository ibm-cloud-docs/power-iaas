---

copyright:
  years: 2025
lastupdated: "2025-07-25"

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



By using data portability for {{site.data.keyword.powerSysFull}}, you can perform tasks such as transferring data and processing the data, either in your data center location or on a service provider location. You can port the data by using a set of tools and procedures.
{: shortdesc}


You can accomplish the following tasks by using data portability:

* Export the digital artifacts that are needed to implement similar workloads.

* Process the data on the {{site.data.keyword.powerSys_notm}} or on a service provider location that supports the Power architecture.


{{site.data.keyword.powerSys_notm}} is an Infrastructure as a Service (IaaS) offering. As a {{site.data.keyword.powerSys_notm}} user, you own the data, operating system images, and configuration parameters. {{site.data.keyword.powerSys_notm}} architecture follows a typical on-premises Power deployments to facilitate data portability. The infrastructure design enables {{site.data.keyword.powerSys_notm}} to maintain key enterprise software certification and support as the {{site.data.keyword.powerSys_notm}} architecture replicates a certified private cloud infrastructure.






## Responsibilities
{: #data-port-respon}

{{site.data.keyword.powerSys_notm}} provides interfaces and instructions to guide you to copy and store your content on your selected location. The content can include data that is stored on logical volumes, operating system images, and configuration parameters.

You are responsible for the use of the exported data and configuration to enable data portability to other infrastructures. You are responsible for creating and executing the plan to set up the infrastructure on a different service provider that has capabilities similar to the {{site.data.keyword.powerSys_notm}} services.

For more information about the responsibility assignment matrix for {{site.data.keyword.powerSys_notm}}, see [High-level architecture](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#high-level-architecture-on-cloud).





## Migrating the data
{: #data-port-export-proc}

Migrating the data from one infrastructure to another requires planning and strategies to achieve the expected performance. Perform the steps defined in the following topics to migrate Power workloads to a {{site.data.keyword.powerSys_notm}}:

* [Planning a workload migration to IBM&reg; Power&reg; Virtual Server](/docs/power-iaas?topic=power-iaas-system-migration)
* [Migration strategies for AIX](/docs/power-iaas?topic=power-iaas-migration-aix)
* [Migration strategies for IBM i](/docs/power-iaas?topic=power-iaas-migration-strategies-power)
* [Additional migration strategies](/docs/power-iaas?topic=power-iaas-additional-migration-strategies-power)
* [Using third-party tools for migration](/docs/power-iaas?topic=power-iaas-migration-strategies-managed-thirdparty)
* [Back up and restore](/docs/power-iaas?topic=power-iaas-backup-restore)


{{site.data.keyword.powerSys_notm}} provides the capability to capture full or selected copies of the logical volumes or data sets. By using IBM FlashCopy&reg; feature and {{site.data.keyword.powerSys_notm}} APIs, you can create delta snapshots, volume clones, and restore your disks. For more information, see [Snapshots, cloning, and restoring](/docs/power-iaas?topic=power-iaas-snapshots-cloning).







## Capturing and exporting a virtual machine
{: #data-port-export-data}

{{site.data.keyword.powerSys_notm}} provides mechanisms to capture and export a virtual machine (VM). For more information, see [Capturing and exporting a virtual machine (VM)](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm).

## Data ownership
{: #data-port-data-owner}

The data that is exported to on-premises or on service providers is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/terms/?id=Z126-6304_WS){: external}.
