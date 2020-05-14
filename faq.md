---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-14"

keywords: faq, virtual server, network bandwidth, private network setup, multi-tenant environment, delete service, supported operating systems, hardware specifications, software maps, affinity, processor types, pinning, snapshot, clone, restore

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
{:preview: .preview}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}

# FAQ
{: #power-iaas-faqs}

## Where can I learn how to use a Power Systems Virtual Server?
{: #training}
{: faq}
{: support}

To learn more about how to use a {{site.data.keyword.powerSys_notm}}, see the [AIX & IBM i in IBM (Public) Cloud](https://www.youtube.com/watch?v=y5QaNdGJ6R0&feature=youtu.be){: new_window}{: external} video.

This video does not capture the latest updates to the {{site.data.keyword.powerSys_notm}} service. You might notice differences in functionality between what's shown in the video and the current offering.
{: note}

## What versions of AIX and IBM i operating systems (OS) are supported?
{: #os-versions}
{: faq}
{: support}

The supported AIX and IBM i operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}: S922 (9009-22A), E880 (9119-MHE), or E980 (9080-M9S - Frankfurt only). To view a list of the supported AIX and IBM i operating system technology levels, see the following system software maps:

**AIX**

The {{site.data.keyword.powerSys_notm}} service supports only AIX 7.1, or later. When viewing the system software maps, refer to the AIX 7.1 and AIX 7.2 information. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given.

- [S922 (9009-22A) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-vios-only){: new_window}{: external}
- [E880 (9119-MHE) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9119-MHE-vios-only){: new_window}{: external}
- [E980 (9080-M9S) AIX software map](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: new_window}{: external}

**IBM i**

The {{site.data.keyword.powerSys_notm}} service supports only IBM i 7.2, or later. Clients running IBM i 7.1 with a plan to move to an IBM E880 (9119-MHE) must first upgrade the OS to a current support level before migrating to the Cloud. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: new_window}{: external}.

- [S922 (9009-22A), E880 (9119-MHE), and E980 (9080-M9S) software maps](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: new_window}{: external}
- [IBM i PTF minimum levels](/docs/power-iaas?topic=power-iaas-minimum-levels)
- [IBM i release life cycle](https://www.ibm.com/support/pages/release-life-cycle){: new_window}{: external}

## Can I use my own AIX or IBM i image?
{: #image}
{: faq}
{: support}

Yes. This function is known as **bring your own image**. For more information, see [Deploying a custom image within a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-deploy-custom-image).

## What formats should I use when uploading a custom image?
{: #custom-image}
{: faq}

Currently, you can import a custom image in the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.

## What are the available storage types in the storage area network (SAN)?
{: #storage}
{: faq}
{: support}

All regions use **Tier 1 (NVMe-based flash storage)** or **Tier 3 (SSD flash storage)** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs want to select **Tier 3**. The storage types cannot be changed once the volume is created. A VM cannot have disks from both storage types.

If you previously deployed a VM on an old storage type (**SSD** or **standard**), no action is required. Your VM will continue to run using the old storage type. You can also add new disks from those legacy tiers.

The boot image storage type is predefined and cannot be chosen.
{: note}

## How do I extend my AIX rootvg?
{: #rootvg}
{: faq}

By default, the system deployes 20 GBs for the AIX *rootvg*. You can extend the AIX *rootvg* by using the [extendvg](https://www.ibm.com/support/knowledgecenter/nl/ssw_aix_72/e_commands/extendvg.html){: new_window}{: external} command to add a physical volume.

## What's the difference between capped and uncapped shared processor performance? How do they compare to dedicated processor performance?
{: #processor}
{: faq}

When deploying a VM, customers can choose between **dedicated**, **capped shared**, or **uncapped shared** processors for their virtual CPUs (vCPUs). The following list provides a simplified breakdown of their differences:

- **Dedicated**: resources are allocated for a specific client (used for specific third-party considerations)
- **Uncapped shared**: shared among other clients
- **Capped shared**: shared, but resources do not expand beyond those that are requested (used mostly for licensing)

There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. For more information, see [How does shared processor performance compare to dedicated processors](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors){: new_window}{: external} and [Processor pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-processor).

|Dedicated processors|
|:-----------------|
| The hypervisor makes a 1:1 binding of a partition’s processor to a physical processor core. Once a VM is activated, the 1:1 binding is static in that a given operating system (OS) logical thread will always run on that same physical hardware. With a dedicated processor partition, you need to size the wanted number of cores to meet the **peak** demand of the partition. For example, if during a typical workday the CPU consumption is around four cores, but it peaks around eight cores, you need to configure the partition with eight cores. Otherwise, you might encounter queuing delays in dispatching applications because there are not enough cores to handle the peak demand.|
{: class="simple-tab-table"}
{: tab-group="processor"}
{: caption="Table 1. Dedicated processors" caption-side="top"}
{: #proc-table-1}
{: tab-title="Dedicated processors"}

|Shared processors|
|:-----------------|
| For shared processors, there are two sharing modes: capped or uncapped. For a capped partition, the amount of CPU time is capped to the value specified for the entitlement. For example, the partition might consume at most 30 seconds of CPU time every minute for a capped partition with processing units set to 0.5. For an uncapped partition, the number of virtual processors defines the upper limit of CPU consumption and not the value that is specified for processing units. For example, if virtual processors are set to 3, the partition might consume 180 seconds of CPU time every minute (three virtual processors each running at 100% utilization would be three physical cores worth of CPU time). There must be unused capacity available on the server for a partition to consume more than its configured processing units.|
{: class="simple-tab-table"}
{: tab-group="processor"}
{: caption="Table 2. Shared processors" caption-side="top"}
{: #proc-table-2}
{: tab-title="Shared processors"}

## How does my current environment compare to what's available through the Power Systems Virtual Server service?
{: #performance}
{: faq}

If you'd like to compare your current environment's performance to what's available through the {{site.data.keyword.powerSys_notm}} offering, see the [IBM Power Systems Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: new_window}{: external}. For a more condensed comparison, see [IBM Power Systems CPW performance data comparison](https://www.itechsol.com/wp-content/uploads/2018/07/IBM-Power-Systems-CPW-Performance-Data-Comparison-P7-vs-P8-vs-P9-rev3-July-2018.pdf){: new_window}{: external}.

## How do I migrate my VM from one data center to another (WDC04 to DAL13)?
{: #vm-migration}
{: faq}

To migrate your VM from one data center to another, you must capture and export your VM to Cloud Object Storage (COS). After you successfully capture and export your VM, copy it to the COS in the destination region, then perform an import followed by a deploy.

## What does VM pinning do?
{: #pinning}
{: faq}

You can choose to *soft pin* or *hard pin* a VM to the host where it is running. When you *soft pin* a VM for high availability, PowerVC automatically migrates the VM back to the original host once the host is back to its operating state. If the VM has a licensing restriction with the host, the *hard pin* option restricts the movement of the VM during remote restart, automated remote restart, DRO, and live partition migration. The default pinning policy is *none*.

VM pinning is currently available in all data centers except for *WDC04* or *FRA04*.
{: preview}

## What does it mean to set an affinity or anti-affinity rule?
{: #affinity}
{: faq}

You can apply affinity and anti-affinity policies to both VMs and volumes. VM affinity and anti-affinity rules allow you to spread a group of VMs across different hosts or keep them on a specific host.

You can control the placement of a new volume in a particular storage provider based on an existing volume by using volume affinity. When you set an affinity policy for a new storage volume, the volume is created within the same storage provider as an existing volume. With an anti-affinity policy, the new volume is created in a different storage provider as an existing volume.

## Does IBM provide maintenance for the AIX or IBM i operating systems?
{: #licensing-os}
{: faq}

No. It is the customer's responsibility to maintain, update, and manage the AIX or IBM i operating system.

## How does licensing work for the AIX and IBM i operating systems?
{: #os-support}
{: faq}

The license for the operating system is part of the overall cost for the service. You cannot use an existing license that you already purchased.

## How does third-party licensing work?
{: #third-party}
{: faq}

Clients are responsible for third-party licensing.

## What are the hardware specifications?
{: #hardware-specs}
{: faq}
{: support}

For more information, see [Hardware specifications](/docs/power-iaas?topic=power-iaas-about-virtual-server#hardware-specifications).

## Do Power Systems Virtual Servers run in a multi-tenant environment?
{: #multi}
{: faq}

Yes, {{site.data.keyword.powerSys_notm}} run in a multi-tenant environment.

## Are there bare-metal options?
{: #bare}
{: faq}

There are no bare-metal options. The {{site.data.keyword.powerSys_notm}} offering focuses on virtual instances.

## Can you tell me more about your service's snapshotting, cloning, and restoring capabilities?
{: #snapshot}
{: faq}

The {{site.data.keyword.powerSys_notm}} service provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, the [Power Systems Virtual Server API](https://cloud.ibm.com/apidocs/power-cloud#introduction) lets you create delta snapshots, volume clones, and restore your disks. To learn more, see [Snapshotting, cloning, and restoring](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone).

## How do you set up private networks between Intel&reg; Virtual Servers (x86) and Power System Virtual Servers?
{: #connecting}
{: faq}
{: support}

For more information, see [Ordering IBM Cloud Direct Link Connect for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect).

## How do you set up customer site access to a private network by using VPN?
{: #configuring}
{: faq}
{: support}

For more information, see [Configuring IBM Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-configuring-power).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

You must set your own firewall in your IBM Cloud account.

## How do you connect a server instance between two data centers (DAL13 to WDC04)?
{: #gts-cloud-connect}
{: faq}
{: support}

You can use IBM Cloud Connect to connect two data centers. IBM Cloud Connect is a software-defined network interconnect service that brings secure public cloud and SaaS solution connectivity to client locations around the world. For more information, see [Connecting Power Systems Virtual Server instances and networks](/docs/power-iaas?topic=power-iaas-connecting-networks).

IBM Cloud Connect is only available to IBM clients within the US.
{: important}

## How is network bandwidth billed?
{: #billing}
{: faq}
{: support}

**IBM Cloud Classic environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 20 TB is included with each monthly bare metal server. Extra bandwidth can also be purchased per packages. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: new_window}{: external}.

**IBM Cloud Power environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per gigabyte (GB) when you use a public network. If you are using a private network with DirectLink Connect, you are charged **IBM Cloud Classic environment** rates.

## What monitoring services are available?
{: #monitoring}
{: faq}

IBM does not provide status and performance monitoring for the IBM Cloud. Clients must use their own on-premises tools.

## What performance and capacity planning services do you provide for IBM i on IBM Cloud?
{: #ibmi-performance}
{: faq}

IBM uses the same tools that are on an on-premises system.

## IBM i and solution certification
{: #ibmi-certification}
{: faq}

You can find self-certification and listing information on the [IBM Global Solutions Directory](https://www.ibm.com/partnerworld/public/find-partner-solution){: new_window}{: external}.

## How do I delete (cancel) the service or a specific instance?
{: #delete-service}
{: faq}

You can delete the service by clicking the overflow menu in the **Virtual server instances** page and selecting **Delete service**. To delete an instance, click the trash icon after you select the wanted instance.

## How do I open a support ticket for the Power Systems Virtual Server service?
{: #support-ticket}
{: faq}

To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
