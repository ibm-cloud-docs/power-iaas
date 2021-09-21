---

copyright:
  years: 2019, 2021

lastupdated: "2021-05-07"

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

<!-- ## Where can I learn how to use a Power Systems Virtual Server?
{: #training}
{: faq}
{: support}

To learn more about how to use a {{site.data.keyword.powerSys_notm}}, see the [AIX & IBM i in IBM (Public) Cloud](https://www.youtube.com/watch?v=y5QaNdGJ6R0&feature=youtu.be){: new_window}{: external} video.

This video does not capture the latest updates to the {{site.data.keyword.powerSys_notm}} service. You might notice differences in functionality between what's shown in the video and the current offering.
{: note}

## Is IBM Power Systems Virtual Servers located on IBM Cloud?
{: #on-cloud}
{: faq}
{: support}

No, {{site.data.keyword.powerSys_notm}} is a colocated infrastructure as a service (IaaS) offering with low-latency connectivity to the full catalog of IBM Cloud offerings.-->

## What is IBM Power Systems Virtual Server?
{: #what-is-powervs}
{: faq}
{: support}

IBM Power Systems Virtual Server is a hosted infrastructure offering that allows you to quickly integrate with the Internet for on-demand provisioning. This offering provides a secure and scalable server virtualization environment that is built upon the advanced RAS features and leading performance of the Power Systems™ platform. The IBM Power Systems Virtual Servers are located in IBM data centers and distinct from the IBM Cloud servers with separate networks and direct-attached storage.

## What versions of AIX, IBM i, and Linux are supported?
{: #os-versions}
{: faq}
{: support}

The supported AIX, IBM i, and Linux&reg; operating system versions depend on the IBM Power Systems hardware that you select for the {{site.data.keyword.powerSys_notm}}: S922 (9009-22A), E880 (9119-MHE), or E980 (9080-M9S). To view a list of the supported AIX, IBM i, and Linux operating system technology levels, see the following system software maps:

**AIX**

The {{site.data.keyword.powerSys_notm}} service supports only AIX 7.1, or later. When viewing the system software maps, refer to the AIX 7.1 and AIX 7.2 information. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given.

- [S922 (9009-22A) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-vios-only){: new_window}{: external}
- [E880 (9119-MHE) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9119-MHE-vios-only){: new_window}{: external}
- [E980 (9080-M9S) AIX software map](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: new_window}{: external}

  For information on end of service pack support (EoSPS) dates, see [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: new_window}{: external}.

**IBM i**

The {{site.data.keyword.powerSys_notm}} service supports IBM i 7.1, or later. Clients running IBM i 6.1 must first upgrade the OS to a current support level before migrating to the Power Systems Virtual Server. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: new_window}{: external}.

- [S922 (9009-22A), E880 (9119-MHE), and E980 (9080-M9S) software maps](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: new_window}{: external}
- [IBM i PTF minimum levels](/docs/power-iaas?topic=power-iaas-minimum-levels)
- [IBM i release life cycle](https://www.ibm.com/support/pages/release-life-cycle){: new_window}{: external}

**Linux**

The {{site.data.keyword.powerSys_notm}} service supports the following Linux distributions:

- SUSE Linux Enterprise (SLES) 12 and SLES 15
- Red Hat Enterprise Linux (RHEL) 8.1, 8.2, 8.3

To view the certification details in the Red Hat catalog, see [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/cloud/instance-types/detail/5636281){: new_window}{: external} and [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/cloud/instance-types/detail/5636201){: new_window}{: external}. For additional support, refer to the distribution (distro). For instructions, see [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: new_window}{: external}.

## Can I use my own AIX, IBM i, or Linux image?
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

All regions use **Tier 1** or **Tier 3** storage types. The **Tier 1** storage type is best for customers who require higher throughput. Customers who do not require exceptionally high throughput and are looking to minimize costs want to select **Tier 3**. The storage types cannot be changed once the volume is created. A VM cannot have disks from both storage types. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-about-virtual-server#storage-tiers).

If you previously deployed a VM on an old storage type (**SSD** or **standard**), no action is required. Your VM continues to run by using the old storage type. You can also add new disks from those legacy tiers.

The boot image storage type is predefined and cannot be chosen.
{: note}

## How do I extend my AIX rootvg?
{: #rootvg}
{: faq}

By default, the system deploys 20 GBs for the AIX *rootvg*. You can extend the AIX *rootvg* by using the [extendvg](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/e_commands/extendvg.html){: new_window}{: external} command to add a physical volume.

## What's the difference between capped and uncapped shared processor performance? How do they compare to dedicated processor performance?
{: #processor}
{: faq}

When deploying a VM, customers can choose between **dedicated**, **capped shared**, or **uncapped shared** processors for their virtual CPUs (vCPUs). The following list provides a simplified breakdown of their differences:

- **Dedicated**: resources are allocated for a specific client (used for specific third-party considerations)
- **Uncapped shared**: shared among other clients
- **Capped shared**: shared, but resources do not expand beyond those that are requested (used mostly for licensing)

There is a core-to-vCPU ratio of 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. For more information, see [How does shared processor performance compare to dedicated processors](https://community.ibm.com/community/user/power/blogs/pete-heyrman1/2020/06/16/how-does-shared-processor-performance-compare-to-d?CommunityKey=71e6bb8a-5b34-44da-be8b-277834a183b0&tab=recentcommunityblogsdashboard){: new_window}{: external} and [Processor pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-processor).

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

## What does it mean to set an affinity or anti-affinity rule?
{: #affinity}
{: faq}

You can apply affinity and anti-affinity policies to both VMs and volumes.

**VM affinity and anti-affinity policy** allows you to spread a group of VMs across different hosts or keep them on a specific host.

Volume affinity and anti-affinity policy allow you to control the placement of a new volume based on an existing PVM instance (VM) or volume. When you set an affinity policy for a new storage volume, the volume is created within the same storage provider as an existing PVM instance or volume. With an anti-affinity policy, the new volume is created in a different storage provider other than the storage provider the existing PVM instance or volume is located in. You can now attach storage volumes to a PVM instance from different storage tiers and pools, other than the storage pool the PVM instance's root (boot) volume is deployed in. To accomplish this you must modify the PVM instance and set the new PVM instance *storagePoolAffinity* property to false. The PVM instance *storagePoolAffinity* property is set to true by default when the PVM instance is deployed and can be changed only by using the modify PVM instance API. For more information about modifying a PVM instance API, see [Modify PVM Instance](/apidocs/power-cloud#pcloud-pvminstances-put). Attaching mixed storage to a PVM instance has implications on the PVM instance capture, clone, and snapshot features. See [Modify PVM Instance](/apidocs/power-cloud#pcloud-pvminstances-put) API for more details.

The use of volume affinity policy (affinity or anti-affinity) requires the availability of multiple storage providers. You might experience the following errors when you use a volume affinity policy:

- If an additional storage provider is not available to fulfill the requested policy, you might receive an error that indicates the inability to locate a storage provider to create a volume by using the requested volume affinity policy.

- If additional storage providers exist but the storage providers do not have sufficient space to fulfill the requested policy, you might receive an error that indicates the inability to locate a storage provider with enough free capacity to satisfy the requested volume size.

## Does IBM provide maintenance for the AIX, IBM i or Linux operating systems?
{: #licensing-os}
{: faq}

No. It is the customer's responsibility to maintain, update, and manage the AIX, IBM i or Linux operating system.

## How does licensing work for the AIX, IBM i, or Linux operating systems?
{: #os-support}
{: faq}

The license for the AIX and IBM i operating systems is part of the overall cost for the service. You cannot use an existing license that you already purchased. The {{site.data.keyword.powerSys_notm}} service does not provide Linux stock images. You must bring your own Linux image (OVA format) and subscription. RHEL and SLES OVA images are currently supported.

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

## How do you set up private networks between Intel&reg; Virtual Servers (x86) and Power Systems Virtual Servers?
{: #connecting}
{: faq}
{: support}

See the tutorial on [IBM Power Systems Virtual Server integration with x86-based workloads](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_and_x86_Integration_Tutorial_v1.pdf).

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

You can use IBM Cloud Connect to connect two data centers. IBM Cloud Connect is a software-defined network interconnect service that brings secure connectivity to client locations around the world. For more information, see [Connecting Power Systems Virtual Server instances and networks](/docs/power-iaas?topic=power-iaas-connecting-networks).

IBM Cloud Connect is only available to IBM clients within the US.
{: important}

## How is network bandwidth billed?
{: #billing}
{: faq}
{: support}

**IBM Cloud Classic environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 20 TB is included with each monthly bare metal server. Extra bandwidth can also be purchased per packages. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: new_window}{: external}.

**IBM Power Systems Virtual Server environment:** Inbound bandwidth is unlimited and not charged. Bandwidth is not charged when you use a public network. If you are using a private network with DirectLink Connect, you are charged **IBM Cloud Classic environment** rates.

## What monitoring services are available?
{: #monitoring}
{: faq}

IBM does not provide status and performance monitoring for the Power Systems Virtual Server. Clients must use their own on-premises tools.

## What performance and capacity planning services do you provide for IBM i?
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

## What are the supported databases that I can run for SAP on Power Systems Virtual Server?
{: #support-databases}
{: faq}

On an AIX VM, the following databases are supported:

  - IBM&reg; Db2 for LUW (Linux, UNIX, and Windows) version 10.5, or later
  - Oracle Database version 12.1.0.2, or later
  - SAP Adaptive Server Enterprise version 16.0 SP03, or later

On a Linux VM, the following database is supported:

  - SAP HANA Platform 2.0 SPS 04, or later

You can find an up-to-date list at [SAP Apps on IBM Power Systems Virtual Server](https://launchpad.support.sap.com/#/notes/2855850){: new_window}{: external}.

## How can I get the WebSphere Application Server that are delivered through the **Web Enablement for i** packages, and are available at no additional charge with IBM i?
{: web-enablement-for-ibmi}
{: faq}

If you have an IBM i VM instance with the licensed program bundle in the Power Systems Virtual Server offering, you can download the WebSphere Application Server that is available  in the Web Enablement for i software at the Entitled System Support (ESS) website by completing the following steps:

1. Go to the [ESS website](https://www.ibm.com/servers/eserver/ess/index.wss){: new_window}{: external}.

2. Sign in. If this is the first time you are using ESS, refer to the **Help** section on the left menu. Download and read the **ESS_Registration_IBM_Customers_Guidelines** PDF.

3. Go to **My Entitled Software > IBM i evaluation and NLV download**.

4. Find the required software that you can download, install, and use. For example:

    **Web Enablement for i (5722-WE2)** - WebSphere Express V8.5.5
    **Web Enablement for i (5733-WE3)** - WebSphere V9

<!--## Can Power VC provide support for more than 1 language to VM Console for a single Novalink host?

PowerVC does not provide capacity to support multiple language support for Client VM console feature.-->

## How do I run Red Hat OpenShift Container Platform (OCP) on Power Systems Virtual Servers?
{: ocp_on_powervs}
{: faq}

You can find a complete tutorial at the IBM Developer site: [Deploying Red Hat OpenShift Container Platform 4.x on IBM Power Systems Virtual Servers](https://developer.ibm.com/series/deploy-ocp-cloud-paks-power-virtual-server/){: new_window}{: external}.

## What is the network latency over Direct Link?
{: network_latency}
{: faq}

Network latency over Direct link is less than 1 millisecond in every location. To know more about network latency, see [Understanding latency](https://cloud.ibm.com/docs/dl?topic=dl-understanding-latency). 

## Are we notified about any planned maintenance activities?
{: planned_maintenance_activity}
{: faq}

For planned maintenance and disruptive changes, the Power Systems Virtual Server operations team sends you notifications at least 7 days in advance. Watch the Notifications space in the IBM Cloud dashboard for these alerts. You can receive a copy of these notifications directly in your inbox if your email is subscribed for notifications.