---

copyright:
  years: 2019, 2020

lastupdated: "2021-02-18"

keywords: release notes, announcements, feature updates, changes, power systems virtual server

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
{:preview: .preview}
{:external: target="_blank" .external}

# Release notes
{: #release-notes}

Use these release notes to learn about the latest changes to the {{site.data.keyword.powerSysShort}} service.
{: shortdesc}

## February 2021
{: #feb-2021}

- You can now choose *MON01* data center to deploy your {{site.data.keyword.powerSys_notm}}.
- The Power Systems Virtual Server offering now supports IBM i 7.1. For more information, see [Minimium PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels).
- You can clone a volume or multiple volumes to create a consistent full copy of the volume. For more information, see [Cloning a volume](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone#cloning-volume).
- You can resize the memory and core counts to a maximum of 8 times of the specified values, and to a minimum of 1/8 times of the specified values when the VM was provisioned. For more information see [Resizing the virtual machine core count and memory](/docs/power-iaas?topic=power-iaas-modifying-server#resize-core-mem).

## December 2020
{: #december-2020}

- You can now use the Power Systems Virtual Server service to deploy a generic Red Hat Enterprise Linux (RHEL) virtual machine (VM). For more information, see [Using RHEL within the Power Systems Virtual Server service](/docs/power-iaas?topic=power-iaas-using-rhel-within-the-power-systems-virtual-server-service).
- You can now choose *SAO01* data center to deploy your {{site.data.keyword.powerSys_notm}}.

## November 2020
{: #november-2020}

- The storage tiers (**Tier 1** and **Tier 3**) in {{site.data.keyword.powerSysShort}} are now based on I/O operations per second (IOPS). For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).
- In DAL12, DAL13, and TOK04 data centers, you can now provision up to 23,070 GB of memory for the E980 systems. For more information, see [Pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server).
- Review the list of [License Program Products (LPP) and IBM i operating system features](/docs/power-iaas?topic=power-iaas-ibmi-lpps) that are included in the Power Systems Virtual Server offering.

## October 2020
{: #october-2020}

- You can now choose *TOK04* data center to deploy your {{site.data.keyword.powerSys_notm}}.
- You can now use the IBM Direct Link Connect (2.0) service to create a seamless connection that allows access to IBM Cloud® resources from your {{site.data.keyword.powerSys_notm}} instance. For more information, see [Ordering Direct Link Connect 2.0](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect#help).
- The following tutorials are now available for your reference:
  - [AIX Disaster Recovery with IBM Power Systems Virtual Servers](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_DR_Tutorial_v1.pdf){: new_window}{: external}
  - [IBM i Disaster Recovery with IBM Power Systems Virtual Servers](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_DR_Tutorial_v1.pdf){: new_window}{: external}
  - [Backing up and restoring data in an AIX VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Backups_Tutorial_v1.pdf){: new_window}{: external}
  - [Backing up and restoring data in an IBM i VM](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Backups_Tutorial_v1.pdf){: new_window}{: external}
  - [Configuring IBM Cloud Mass Data Migration (MDM) on AIX VM](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-configuring-mdm){: new_window}{: external}
  - [Configuring Mass Data Migration (MDM) on IBM i VM](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-configuring-mass-data-migration-mdm-on-ibm-i-vm){: new_window}{: external}
  - [Migrating AIX to IBM Power Systems Virtual Servers](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_AIX_Migration_Tutorial_v1.pdf){: new_window}{: external}
  - [Migrating IBM i to IBM Power Systems Virtual Servers](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_IBMi_Migration_Tutorial_v1.pdf){: new_window}{: external}
  - [Site-to-site VPN connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: new_window}{: external}
  - [Integration with x86-based workloads](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_and_x86_Integration_Tutorial_v1.pdf){: new_window}{: external}

## September 2020
{: #september-2020}

- You can now choose *LON04*, *SYD04*, and *DAL12* data centers to deploy your {{site.data.keyword.powerSys_notm}}.
- For IBM i and AIX VM instances, you can now view a [System Reference Code (SRC)](/docs/power-iaas?topic=power-iaas-modifying-server#detecting-problems-by-using-the-system-reference-code-src-) that describes information about a detected error.
- You can now use the [Operations panel](/docs/power-iaas?topic=power-iaas-configuring-ibmi#managing-the-ibm-i-vm-instance) in the IBM i VM instance to manage advanced VM operations and configuration.
- Added port 6443 in the list of open [firewall ports](/docs/power-iaas?topic=power-iaas-network-security#firewall-ports).

## July 2020
{: #july-2020}

The {{site.data.keyword.powerSys_notm}} instance supports the SAP NetWeaver and SAP HANA workload. For more information, see [Getting started with SAP NetWeaver on IBM Power Systems Virtual Servers](/docs/sap-netweaver-power?topic=sap-netweaver-power-getting-started) and [Getting started with SAP HANA on IBM Power Systems Virtual Servers](/docs/sap-hana-power?topic=sap-hana-power-getting-started).

## June 2020
{: #june-2020}

- You can now deploy Linux on a {{site.data.keyword.powerSys_notm}}. To learn more, see [Using Linux within the Power Systems Virtual Server service](/docs/power-iaas?topic=power-iaas-using-linux).
- The {{site.data.keyword.powerSys_notm}} service now includes [a highly available 5 Gbps connection](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## May 2020
{: #may-2020}

- IBM i software keys were cleared out due to an IBM Cloud update. You must re-apply any IBM i software licenses through the {{site.data.keyword.powerSys_notm}} user interface. The following IBM i builds require updates:
    - 7.4 MF99301 SI70544
    - 7.3 MF99207 SI69686
    - 7.2 SI71091
- Created a new article on [Planning a workload migration to an IBM POWER8 or POWER9 system](/docs/power-iaas?topic=power-iaas-system-migration).
- Added [snapshot, clone and restore capabilities](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone) to the {{site.data.keyword.powerSys_notm}} service. You can use these new capabilities by using the [Power Systems Virtual Server API](https://cloud.ibm.com/apidocs/power-cloud#introduction).

- There is now a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs.

  If you resize your VM, the core-to-vCPU ratio updates to the new value for all operating systems.
  {: important}

## April 2020
{: #april-2020}

- The {{site.data.keyword.powerSys_notm}} service now offers lower latency direct connectivity to customers in all regions except for *Washington 2*. You must select **IBM POWER VIRTUAL SERVER** as the **Network Provider** instead of **MEGAPORT** to take advantage of this offer.
- If you select IBM i as your boot image, the {{site.data.keyword.powerSys_notm}} user interface now generates a list with the following licenses: *IBM i Cloud Storage Solution*, *IBM i Power HA*, and *Rational Dev Studio for IBM i*. Adding a license increases the service's cost.
- You can now provision a {{site.data.keyword.powerSys_notm}} in the *TOR01* data center.
- You can now provision a {{site.data.keyword.powerSys_notm}} in the *LON06* data center.
- Added a virtual machine (VM) pinning policy (*none*, *soft*, or *hard*). You can choose to *soft pin* or *hard pin* a VM to the host where it is currently running. When you *soft pin* a VM for high availability, PowerVC automatically migrates the VM back to the original host once the host is back to its operating state. If the VM has a licensing restriction with the host, the *hard pin* option restricts the movement of the VM during remote restart, automated remote restart, DRO and live partition migration. The default pinninig policy is *none*. You can add the **pinPolicy** parameter when:

    - [Creating a new PVM Instance](https://cloud.ibm.com/apidocs/power-cloud#create-a-new-pvm-instance){: new_window}{: external}
    - [Getting a PVM Instance's current state or information](https://cloud.ibm.com/apidocs/power-cloud#get-a-pvm-instance-s-current-state-or-information){: new_window}{: external}
    - [Updating a PVM Instance](https://cloud.ibm.com/apidocs/power-cloud#update-a-pcloud-pvm-instance){: new_window}{: external}

## March 2020
{: #march-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} with a capped shared processor. For more information, see the [FAQ](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor) and [Processor types](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-processor).

## February 2020
{: #feb-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} in the *FRA05* data center.
