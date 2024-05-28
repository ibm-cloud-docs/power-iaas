---

copyright:
  years: 2023, 2024

lastupdated: "2024-04-22"

keywords: faq, {{site.data.keyword.powerSys_notm}} as a service, ppcaas, terminology, video, how-to

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# FAQs
{: #powervs-faqs}

## What is {{site.data.keyword.powerSysFull}} Private Cloud?
{: #what-is-ppc}
{: faq}
{: support}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud is an as-a-service offering that includes a prescriptive set of physical infrastructure (compute, network, and storage). The infrastructure is deployed in your own data center. IBM site reliability engineers (SREs) fully maintain and operate your private cloud infrastructure and manage it through the IBM Cloud. Also, pay-as-you-use billing allows you to easily adjust your workloads. For more information, see [What is IBM {{site.data.keyword.powerSys_notm}} Private cloud](/docs-draft/power-iaas?topic=power-iaas-about-power-iaas).

## What is the difference between {{site.data.keyword.powerSys_notm}} on cloud and private cloud?
{: #private-cloud-on-cloud-diff}

The primary difference between the two is where the physical infrastructure resides. The IBM {{site.data.keyword.powerSys_notm}} Private Cloud infrastructure resides in your data center, while {{site.data.keyword.powerSys_notm}} on cloud infrastructure resides in the IBM data centers.

## Which Power servers are supported?
{: #servers-supported}

[Off-Premises]{: tag-blue} IBM Power S922, IBM Power E980, IBM Power S1022, and IBM Power E1080.

[On-Premises]{: tag-red} IBM Power S1022, IBM Power E1050, IBM Power E1080.

For complete specifications, see [Hardware and software specifications](/docs-draft/power-iaas?topic=power-iaas-about-power-iaas#hardware-software-specs-private-cloud).

<!--The following FAQ is migrated from PowerVS and needs technical review-->
## What versions of AIX, IBM i, and Linux&reg; are supported?
{: #os-versions}
{: faq}
{: support}

The supported AIX, IBM i, and Linux&reg; operating system versions depend on the IBM Power hardware.


### AIX
{: #aix-os-version}

[Off-Premises]{: tag-blue}

The {{site.data.keyword.powerSys_notm}} on cloud offering supports the following operating systems:
* S922  -  7.1 or later
* E980  -  7.1 or later
* S1022 -  7.1 TL 5 or later

Stock images available when you create a virtual machine are:
* AIX 7.3 TL2
* AIX 7.3 TL1 SP2
* AIX 7.2 TL5 SP7
* AIX 7.2 TL5 SP6
* AIX 7.1 TL5 SP9

[On-Premises]{: tag-red}

The IBM {{site.data.keyword.powerSys_notm}} Private Cloud offering supports the following operating systems:
* S1022 - 7.2 or later
* E1080 - 7.2 or later

Stock images available when you create a virtual machine are:
* AIX 7.3 TL1 SP2
* AIX 7.3 TL1 SP1
* AIX 7.2 TL5 SP6
* AIX 7.2 TL5 SP5

<!--**AIX** - The following versions of AIX are supported on {{site.data.keyword.powerSys_notm}} on cloud and private cloud offerings.-->
<!--[Off-Premises]{: tag-blue}-->
<!--The {{site.data.keyword.powerSys_notm}} on cloud offering supports AIX 7.1, or later on the S922 (9009-22A) and E980 (9080-M9S).-->
<!--Power server S1022 (9105-22A) supports AIX 7.1 TL 5 and later.-->

When you view the system software maps, refer to the AIX 7.1, AIX 7.2, and AIX 7.3 information. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given.

- [S922 (9009-22A) AIX software map](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9009-22A-vios-only){: external}
- [E980 (9080-M9S) AIX software map](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}
- [S1022 (9105-22A) AIX software map](https://www.ibm.com/support/pages/node/6604269){: external}

<!-- - [E1080 (9080-HEX) AIX software map](https://www.ibm.com/support/pages/system-software-map-power-systems-e1080-9080-hex-and-aix-all-io-configurations){: external} -->

For more information about end of service pack support (EoSPS) dates, see [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}.

<!--AIX stock images currently available when you create a VM are:-->
<!--* AIX 7.3 TL1 SP2-->
<!--* AIX 7.2 TL5 SP6-->
<!--* AIX 7.1 TL5 SP9-->
<!--[On-Premises]{: tag-red}-->
<!--The {{site.data.keyword.powerSys_notm}} private cloud offering supports AIX 7.2, or later on the S1022 (9105-22A) and E1080 (9080-HEX).-->
<!--AIX stock images currently available for private cloud when you create a VM are:-->
<!--* AIX 7.3 TL1 SP2-->
<!--* AIX 7.3 TL1 SP1-->
<!--* AIX 7.2 TL5 SP6-->
<!--* AIX 7.2 TL5 SP5-->

### IBM i
{: #ibm-os-versions}

{{site.data.keyword.powerSys_notm}} on cloud supports IBM i 7.1, or later.
{{site.data.keyword.powerSys_notm}} private cloud supports IBM i 7.3, or later.

If you are using IBM i 6.1, you must first upgrade the OS to a current support level before migrating to the {{site.data.keyword.powerSys_notm}} on cloud. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

- [S922 (9009-22A), E980 (9080-M9S) and S1022 (9105-22A) software maps](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: external}
- [IBM i PTF minimum levels](/docs-draft/power-iaas?topic=power-iaas-minimum-levels)
- [IBM i release life cycle](https://www.ibm.com/support/pages/release-life-cycle){: external}

IBM i stock images currently available when you create a VM are:

* IBM i COR [^1]
* IBM i 7.5 TR3
* IBM i 7.4 TR9
* IBM i 7.3 TR13
* IBM i 7.2 TR9
* IBM i 7.1 TR11 [^2]

[^1]: IBM i Cloud Optical Repository (COR) is a virtual image that can be deployed and used as a Network File Server (NFS) to perform various IBM i tasks that require media. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.

[^2]: Starting May 1, 2024, IBM i 7.1 is End of Life and no support will be made available. IBM i 7.1 stock images will also become unavailable from {{site.data.keyword.powerSys_notm}} data centers.

### Linux
{: #linux-os-versions}

<!--The following versions of Linux are supported on {{site.data.keyword.powerSys_notm}} on cloud and private cloud offerings.-->

[Off-Premises]{: tag-blue}

{{site.data.keyword.powerSys_notm}} supports Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise (SLES) distributions. The following Linux stock images are available when you select Full Linux Subscription (learn more about [Full Linux® subscription for {{site.data.keyword.powerSys_notm}} on cloud](/docs-draft/power-iaas?topic=power-iaas-set-full-Linux)):

Red Hat

* RHEL 9.2 general purpose (RHEL9-SP2) [new]{: tag-new}
* RHEL 9.2 for Sap HANA (RHEL9-SP2-SAP) [new]{: tag-new}
* RHEL 9.2 for SAP NetWeaver (RHEL9-SP2-SAP-NETWEAVER) [new]{: tag-new}
* RHEL 8.8 general purpose (RHEL8-SP8) [new]{: tag-new}
* RHEL 8.8 for SAP HANA (RHEL8-SP8-SAP) [new]{: tag-new}
* RHEL 8.8 for SAP NetWeaver (RHEL8-SP8-SAP-NETWEAVER) [new]{: tag-new}
* RHEL 8.6 general purpose (RHEL8-SP6)
* RHEL 8.6 for SAP HANA (RHEL8-SP6-SAP)
* RHEL 8.6 for SAP NetWeaver (RHEL8-SP6-SAP-NETWEAVER)
* RHEL 8.4 for SAP HANA (RHEL8-SP4-SAP)
* RHEL 8.4 for SAP NetWeaver (RHEL8-SP4-SAP-NETWEAVER)


SUSE
* SLES 15 SP5 general purpose (SLES15-SP5)
* SLES 15 SP5 for SAP HANA (SLES15-SP5-SAP) [^footnote1]
* SLES 15 SP5 for SAP NetWeaver (SLES15-SP5-SAP-NETWEAVER) [^footnote2]
* SLES 15 SP4 general purpose (SLES15-SP4)
* SLES 15 SP4 for SAP HANA (SLES15-SP4-SAP)
* SLES 15 SP4 for SAP NetWeaver (SLES15-SP4-SAP-NETWEAVER)
* SLES 15 SP3 for SAP HANA (SLES15-SP3-SAP)
* SLES 15 SP3 for SAP NetWeaver (SLES15-SP3-SAP-NETWEAVER)
* SLES 15 SP2 for SAP HANA (SLES15-SP2-SAP)
* SLES 15 SP2 for SAP NetWeaver (SLES15-SP2-SAP-NETWEAVER)

[^footnote1]: Install [insserv package](/docs/sap?topic=sap-power-vs-set-up-power-instances#power-vs-addtl-sw-sles-sap) as a prerequisite.
[^footnote2]: Install [insserv package](/docs/sap?topic=sap-power-vs-set-up-power-instances#power-vs-addtl-sw-sles-sap) as a prerequisite.


The S1022 systems support RHEL 8.4 (and later) and SLES 15 SP3 (and later) versions. [JIRA-PPC-4873 update start]{: tag-teal} The RHEL 9.2 stock images can be deployed on the systems that has core-to-vCPU ratio set to 1:10 or greater. [JIRA-PPC-4873 update end]{: tag-teal}
{: note}

If you opt for a Linux subscription directly from Red Hat or SUSE, you will need to bring your own image. {{site.data.keyword.powerSys_notm}} on cloud supports custom images for the following Linux distributions:

General purpose:
* SLES 12 SP4 or later and SLES 15 SP1 or later
* RHEL 8.4 or later

For SAP workloads:
* SLES 12 SP4 or later and SLES 15 SP1 or later
* RHEL 8.1 or later

To view the certification details in the Red Hat catalog, see [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/hardware/servers/detail/17035){: external} and [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/hardware/servers/detail/9225){: external}. For additional support, refer to the distribution (distro). For instructions, see [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: external}.


[On-Premises]{: tag-red}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud supports Red Hat Enterprise Linux (RHEL) with RHEL stock images that includes support from IBM and access to RHEL bug fixes from Satellite servers hosted on IBM Cloud. This capability is referred to as Full Linux Subscription (FLS) model, which is different from the Bring Your Own License (BYOL) or custom Linux image model. For more information, see [Full Linux subscription for IBM {{site.data.keyword.powerSys_notm}} Private Cloud](/docs-draft/power-iaas?topic=power-iaas-full-linux-sub).

FLS provides access to RHEL OS interim fixes and updates by using activation keys for Power servers that are hosted on an IBM satellite server within the IBM Cloud environment. To register for FLS, select one of the stock (RHEL OS) images that are provided by IBM {{site.data.keyword.powerSys_notm}} Private Cloud.

The following list is an example of FLS offerings:

* Stock images: RHEL 8.4 (General and SAP), RHEL 8.6 (General and SAP), RHEL 9.0 (General)
* Support:	You pay IBM for support
* Patches: You receive keys for satellite servers to obtain Linux patches from Linux distribution (Linux distros)

## Where can I find cost estimates for {{site.data.keyword.powerSys_notm}} infrastructure?
{: #estimate}

To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate pricing](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs-draft/power-iaas?topic=power-iaas-generating-an-estimate). For other pricing-related questions for private cloud, see [Pricing FAQs](/docs-draft/power-iaas?topic=power-iaas-pricing-private-cloud#faq).


## Can private cloud pods be expanded with additional compute nodes?
{: #expand-pods}

Yes, up to the maximum number of compute nodes for the specific configuration size. For example, you can initially start with 5 nodes and then add 3 more nodes.

## Can private cloud pods be expanded with additional storage?
{: #expand-pods-storage}

Yes, you can expand the pod with additional storage capacity. But you cannot add more storage controllers.

## Are the private cloud pods equipped with spare compute nodes for maintenance?
{: #spare-compute-node}

In each pod, one spare node is available that is exclusively usable for IBM operational purposes, such as to perform system maintenance. The system type of the spare node matches the largest client-usable node. For example, if you have a pod with 4X S1022 and 1X E1080 client-usable hosts, then the spare node will be E1080.

## Where can I find the logs for the pod software or operator access logs?
{: #pod-logs}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.atracker_short}} service to track how users and applications interact with the {{site.data.keyword.powerSys_notm}} in IBM Cloud. {{site.data.keyword.atracker_short}} records user-initiated activities that change the state of a service in IBM Cloud. You can use these events to identify the following information:
* The users who made API calls to cloud services.
* The time-stamp when the API calls were made.
* The status of the API call.
* The criticality of the action.

For more information, see [Activity tracker events](/docs-draft/power-iaas?topic=power-iaas-at-events).

<!--The FAQs from here are migrated from PowerVS guide-->

## Can I use my own AIX, IBM i, Linux, or [Linux for SAP (HANA or NetWeaver)]{: tag-teal} image?
{: #image}
{: faq}
{: support}

Yes. This function is known as **bring your own image**. For more information, see [Deploying a custom image within a {{site.data.keyword.powerSys_notm}}](/docs-draft/power-iaas?topic=power-iaas-deploy-custom-image).

[Q2-2024 update start]{: tag-teal}
You can also use customized Linux for SAP (HANA or NetWeaver) images. This function is known as **bring your own image with your own subscription**. See [Deploying a Linux for SAP (HANA or NetWeaver) custom image](https://test.cloud.ibm.com/docs-draft/power-iaas?topic=power-iaas-powervs-faqs#image).
[Q2-2024 update end]{: tag-teal}


## What versions of stock images are available?
{: #stock-images}
{: faq}
{: support}

For each major version (example: Technology Level) of the operating system (OS) that is enabled through the offering, {{site.data.keyword.powerSys_notm}} provides a single stock image. {{site.data.keyword.powerSys_notm}} typically provides stock images for the last three major versions of the supported OS. Any update to the OS stock image is planned only when the image level is certified for {{site.data.keyword.powerSys_notm}} environment.

## When are stock images removed from the catalog?
{: #remove-stock-images}
{: faq}
{: support}

Any unsupported and older stock images are periodically removed from the offering. You will be notified three weeks before the images are removed.

## What happens to virtual machines deployed by using stock images that are removed?
{: #vm-stock-images}
{: faq}
{: support}

If the stock images that are used to depoy the virtual machines are removed, the virtual machines can continue to operate without any issue. You are recommended to update the operating system by following the vendor’s guidelines specific to your operating system.

## What formats should I use when uploading a custom image?
{: #custom-image}
{: faq}

Currently, you can import a custom image in the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.

## What are the available storage types in the storage area network (SAN)?
{: #storage}
{: faq}
{: support}

Each volume has a storage tier, which defines how many I/O operations per second (IOPS) can be started against that volume. These tiers can scale according to the size of the volume.

The following tiers are supported:
* Tier 0 (25 IOPS/GB)
* Tier 1 (10 IOPS per GB)
* Tier 3 (3 IOPS per GB)
* Fixed 5000 IOPS

If you find the storage tiers are over or under-provisioned, you can change the storage tier of an existing volume. For more information, see [Storage tiers](/docs-draft/power-iaas?topic=power-iaas-about-power-iaas#storage-tiers-spec-private-cloud).

## How do I extend my AIX rootvg?
{: #rootvg}
{: faq}

By default, the system deploys 20 GBs for the AIX *rootvg*. You can extend the AIX *rootvg* by using the [extendvg](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/e_commands/extendvg.html){: external} command to add a physical volume.

## What's the difference between capped and uncapped shared processor performance? How do they compare to dedicated processor performance?
{: #processor}
{: faq}

When you deploy a VM, you can choose between **dedicated**, **capped shared**, or **uncapped shared** processors for your virtual CPUs (vCPUs). The following list provides a simplified breakdown of their differences:

- **Dedicated**: resources are allocated for a specific client (used for specific third-party considerations)
- **Uncapped shared**: shared among other clients
- **Capped shared**: shared, but resources do not expand beyond those that are requested (used mostly for licensing)

The core-to-vCPU ratio is 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. For more information, see [How does shared processor performance compare to dedicated processors](https://community.ibm.com/community/user/power/blogs/pete-heyrman1/2020/06/16/how-does-shared-processor-performance-compare-to-d?CommunityKey=71e6bb8a-5b34-44da-be8b-277834a183b0&tab=recentcommunityblogsdashboard){: external}, [Pricing for IBM {{site.data.keyword.powerSys_notm}} Private Cloud](/docs-draft/power-iaas?topic=power-iaas-pricing-private-cloud)), and [Pricing for {{site.data.keyword.powerSys_notm}} on cloud](/docs-draft/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).

|Dedicated processors|
|:-----------------|
| The hypervisor makes a 1:1 binding of a partition’s processor to a physical processor core. After a VM is activated, the 1:1 binding is static in that a given operating system (OS) logical thread will always run on that same physical hardware. With a dedicated processor partition, you need to size the wanted number of cores to meet the **peak** demand of the partition. For example, if during a typical workday the CPU consumption is around four cores, but it peaks around eight cores, you need to configure the partition with eight cores. Otherwise, you might encounter queuing delays in dispatching applications because there are not enough cores to handle the peak demand.|
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


<!--**Example 1**
Maximum Pool Capacity: 8
AIX VM1 VP: 4
AIX VM2 VP: 2

In this example, the maximum pool capacity (8) is greater than the total number of VPs associated with the partitions in a SPP (4+2=6). Therefore, the pricing for OS licensing is calculated as follows:
* The partition VM1 contains four VPs of AIX OS license. So, the price is four times the cost of AIX OS license.
* The partition VM2 contains two VPs of AIX OS license. So, the price is two times the cost of AIX OS license.

Therefore, the total cost for this SPP is six times the cost of AIX.

**Example 2**
Maximum Pool Capacity: 8
AIX VM1 VP: 4
AIX VM2 VP: 2
AIX VM3 VP: 4

In this example, the maximum pool capacity (8) is less than the total number of of VPs associated with the partitions in a SPP (4+2+4=10). Therefore, the pricing for OS licensing is distributed proportionately for all the VPs.
* VM1 is charged with 3.2 times the AIX OS license cost.
* VM2 is charged with 1.6 times the AIX OS license cost.
* VM3 is charged with 3.2 times the AIX OS license cost.-->


## How does my current environment compare to what's available through the {{site.data.keyword.powerSys_notm}}?
{: #performance}
{: faq}

If you like to compare your current environment's performance to what's available through the {{site.data.keyword.powerSys_notm}} offering, see the [IBM Power Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}.

## How do I migrate my VM from one data center to another (WDC04 to DAL13)?
{: #vm-migration}
{: faq}

To migrate your VM from one data center to another, you must capture and export your VM to Cloud Object Storage (COS). After you successfully capture and export your VM, copy it to the COS in the destination region, then perform an import followed by a deployment.

## What does VM pinning do?
{: #pinning}
{: faq}

You can choose to *soft pin* or *hard pin* a VM to the host where it is running. When you *soft pin* a VM for high availability, PowerVC automatically migrates the VM back to the original host once the host is back to its operating state. If the VM has a licensing restriction with the host, the *hard pin* option restricts the movement of the VM during remote restart, automated remote restart, DRO, and live partition migration. The default pinning policy is *none*.

## What does it mean to set an affinity or anti-affinity rule?
{: #affinity}
{: faq}

You can apply affinity and anti-affinity policies to both VMs and volumes.

**VM affinity and anti-affinity policy** allows you to spread a group of VMs across different hosts or keep them on a specific host.

Volume affinity and anti-affinity policy allow you to control the placement of a new volume based on an existing PVM instance (VM) or volume. When you set an affinity policy for a new storage volume, the volume is created within the same storage provider as an existing PVM instance or volume. With an anti-affinity policy, the new volume is created in a different storage provider other than the storage provider the existing PVM instance or volume is located in.

The use of volume affinity policy (affinity or anti-affinity) requires the availability of multiple storage providers. You might experience the following errors when you use a volume affinity policy:

- If an additional storage provider is not available to fulfill the requested policy, you might receive an error. The error indicates the inability to locate a storage provider to create a volume by using the requested volume affinity policy.

- If additional storage providers exist but the storage providers do not have sufficient space to fulfill the requested policy, you might receive an error. The error indicates the inability to locate a storage provider with enough free capacity to satisfy the requested volume size.

## How to set a PVM instance to allow attaching mixed storage?
{: #mixed_storage}
{: faq}

You can now attach storage volumes to a PVM instance from different storage tiers and pools, other than the storage pool the PVM instance's root (boot) volume is deployed in. To accomplish this, you must modify the PVM instance and set the new PVM instance *storagePoolAffinity* property to false. The PVM instance *storagePoolAffinity* property is set to true by default when the PVM instance is deployed and can be changed only by using the modify PVM instance API. Attaching mixed storage to a PVM instance has implications on the PVM instance capture, clone, and snapshot features. For more information about modifying a PVM instance API, see [Modify PVM Instance](/apidocs/power-cloud#pcloud-pvminstances-put).

## Does IBM provide maintenance for the AIX, IBM i, or Linux operating systems?
{: #licensing-os}
{: faq}

No. It is the customer's responsibility to maintain, update, and manage the AIX, IBM i, or Linux operating system.

## How does licensing work for the AIX, IBM i, or Linux operating systems?
{: #os-support}
{: faq}

The license for the AIX and IBM i operating systems is part of the overall cost for the workspace. You cannot use an existing license that you already purchased. Refer to the AIX section to learn how to [create an AIX VM](/docs-draft/power-iaas?topic=power-iaas-create-vm).

You can use the movable IBM i (IBM i MOL) to move your existing on premises entitlements to {{site.data.keyword.powerSys_notm}}. Contact support to know more about the IBM i MOL, see [Getting help and support](/docs-draft/power-iaas?topic=power-iaas-getting-help-and-support).

{{site.data.keyword.powerSys_notm}} supports multiple levels of RHEL and SLES. You can either use IBM provided stock Linux images with IBM Full Linux Subscription or bring your own custom Linux image with vendor-provided subscription.

For more information about supported versions of OS, see [What versions of AIX, IBM i, and Linux&reg; are supported?](/docs-draft/power-iaas?topic=power-iaas-powervs-faqs#os-versions).

## How does third-party licensing work?
{: #third-party}
{: faq}

Clients are responsible for third-party licensing.

## What are the hardware specifications?
{: #hardware-specs}
{: faq}
{: support}

For more information, see [Hardware specifications](/docs-draft/power-iaas?topic=power-iaas-about-virtual-server#hardware-specifications).

## Do {{site.data.keyword.powerSys_notm}} run in a multi-tenant environment?
{: #multi}
{: faq}

[Off-Premises]{: tag-blue}

The {{site.data.keyword.powerSys_notm}} on cloud run in a multi-tenant environment. If you have signed up for a dedicated host you can get single-tenant capabilities.

## Are there bare-metal options?
{: #bare}
{: faq}

There are no bare-metal options. The {{site.data.keyword.powerSys_notm}} offering focuses on virtual instances.

## Can you tell me more about the snapshotting, cloning, and restoring capabilities?
{: #snapshot}
{: faq}

{{site.data.keyword.powerSys_notm}} provides the capability to capture full, point-in-time copies of entire logical volumes or data sets. Using IBM's *FlashCopy* feature, the [{{site.data.keyword.powerSys_notm}} API](https://cloud.ibm.com/apidocs/power-cloud#introduction) lets you create delta snapshots, volume clones, and restore your disks. To learn more, see [Snapshotting, cloning, and restoring](/docs-draft/power-iaas?topic=power-iaas-snapshots-cloning).

## What are the key differences between a snapshot and a clone?
{: #snap-vs-clone}
{: faq}

The key differences are as follows:

| Context | Snapshot | Clone |
|-|-|-|
| Definion | A snapshot is a thin-provisioned group of volumes that cannot be attached to a host or accessed/manipulated. | A clone is created from a snapshot and results in independent volumes which surface in the GUI and can be attached to hosts.|
| Primary function | Revert or restore the source disks to a desired state|Create a complete volume clone|
| Ease of creation | Easy and quick process| Three-step process and takes a long time|
| Pricing | Charged 30% of the regular storage rate| target volume storage plus the GRS costs|
{: caption="Table 5. Differences between a snapshot and clone" caption-side="bottom"}


See [Snapshots, cloning, and restoring](/docs-draft/power-iaas?topic=power-iaas-snapshots-cloning) for more detailed information.

## Is there any UI to perform snapshot or clone operations?
{: #snap-clone-ui}
{: faq}

None. Use the API and CLI to perform snapshot or clone operations. Using the {{site.data.keyword.powerSys_notm}} API and command line interface (CLI) you can create, restore, delete, and attach the snap-shots and volume-clones.

**APIs to create snapshot and clone**
- [Create a new volumes clone request and initiates the Prepare action](/apidocs/power-cloud#pcloud-v2-volumesclone-post)
- [Create a PVM Instance snapshot](/apidocs/power-cloud#pcloud-pvminstances-snapshots-post)

**CLIs to create snapshot and clone**
- [Create a snapshot](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-snapshot)
- [Create a volume clone for specific volumes](/docs/power-iaas-cli-plugin?topic=power-iaas-cli-plugin-power-iaas-cli-reference#create-volume-clone)

## Are there any initial snapshot requirement in terms of storage?
{: #snap-storage-req}
{: faq}

None. The storage is allocated on demand.

## Does the snapshot and volume clone supports any safeguard policy?
{: #snap-clone-safeguard}
{: faq}

None. {{site.data.keyword.powerSys_notm}} does not (currently) provide any options to safeguarded copy (such as cyber protection).

## Can you tell me more about the backup process using the PowerHA Toolkit for IBM i?
{: #poweha-toolkit}
{: faq}

The PowerHA Toolkit for IBM i provides the 5250 user interfaces and automation to use them for backups. In a nutshell, it does the following tasks:
- Automates the memory flush
- Create the volumes-clone
- Attach the clones to a host
- Start the host
- kicki-off the backups
- Move the BRMS data back to the production VM before shutting down the backup VM
- Remove the cloned volumes.

It also allows you to quickly create an intermediate snap-shot then a volumes-clone before entering the long-running volume detach or attach phase. You can pause the process immediately before attaching volumes.

## How do you set up private networks between Intel&reg; Virtual Servers (x86) and {{site.data.keyword.powerSys_notm}}?
{: #connecting}
{: faq}
{: support}

[Off-Premises]{: tag-blue}

See the tutorial on [IBM {{site.data.keyword.powerSys_notm}} integration with x86-based workloads](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_and_x86_Integration_Tutorial_v1.pdf).

## How do you set up customer site access to a private network by using VPN?
{: #configuring}
{: faq}
{: support}

[Off-Premises]{: tag-blue}
For a complete tutorial on site-to-site Virtual Private Network (VPN) connectivity from a private cloud environment to {{site.data.keyword.powerSys_notm}}, see [IBM {{site.data.keyword.powerSys_notm}} Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.
For more information on VPN, see [Managing VPN connections](/docs-draft/power-iaas?topic=power-iaas-VPN-connections).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

[Off-Premises]{: tag-blue}
You must set your own firewall in your IBM Cloud account.

## How do you connect a server instance between two data centers (DAL13 to WDC04)?
{: #gts-cloud-connect}
{: faq}
{: support}

You can use IBM Cloud Connect to connect two data centers. IBM Cloud Connect is a software-defined network interconnect service that brings secure connectivity to client locations around the world.

IBM Cloud Connect is only available to IBM clients within the US.
{: important}

## How is network bandwidth billed?
{: #billing}
{: faq}
{: support}

[Off-Premises]{: tag-blue}
**IBM Cloud Classic environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 20 TB is included with each monthly bare metal server. Extra bandwidth can also be purchased per package. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: external}.

**IBM {{site.data.keyword.powerSys_notm}} environment:** Inbound bandwidth is unlimited and not charged. Bandwidth is not charged when you use a public network. If you are using a private network with DirectLink Connect, you are charged **IBM Cloud Classic environment** rates.

## What monitoring services are available?
{: #monitoring}
{: faq}

IBM does not provide status and performance monitoring for the {{site.data.keyword.powerSys_notm}}. Clients must use their own private cloud tools.

## What performance and capacity planning services do you provide for IBM i?
{: #ibmi-performance}
{: faq}

IBM uses the same tools that are on a private cloud system.

## IBM i and solution certification
{: #ibmi-certification}
{: faq}

You can find self-certification and listing information on the [IBM Global Solutions Directory](https://www.ibm.com/partnerworld/public/find-partner-solution){: external}.

## How do I delete a workspace?
{: #delete-service}
{: faq}

To delete a workspace (and all its resources), use the left navigation to navigate the workspace page. Find the workspace to be deleted and click the overflow menu on the upper right corner of the tile. Click **Delete** and confirm the request from the pull-down menu by typing *Delete* in the text field. Finally, click the red **Delete** button to initiate the request.

## How do I delete a single virtual server instance?
{: #delete-service-instance}
{: faq}

There are two methods to delete a virtual server instance. Both deletion methods are manual processes. To delete all VSIs, delete the workspace or delete a subset of the virtual server instance.

- Delete a single virtual server instance from the Virtual server instances page.
Click the overflow menu (icon with 3 vertical dots) on the far right of each virtual server instance entry on the table. From the pull-down menu, click **Delete** to open the deleted confirmation modal. Click **Delete instance** to initiate the deletion request. This action cannot be undone.

- Delete a single virtual server instance from the details page.
Navigate to the virtual server instance's details page by clicking the virtual server instance name present on the table, on the Virtual server instances page. Find and click the trash icon on the upper right of the screen. Confirm the request by clicking **Delete instance**. This action cannot be undone.

## How do I open a support ticket for the {{site.data.keyword.powerSys_notm}} workspace?
{: #support-ticket}
{: faq}

To open a support ticket, see [Getting help and support](/docs-draft/power-iaas?topic=power-iaas-getting-help-and-support).

## What are the supported databases that I can run for SAP on {{site.data.keyword.powerSys_notm}}?
{: #support-databases}
{: faq}

On an AIX VM, the following databases are supported:
- IBM Db2 for LUW (Linux, UNIX, and Windows) version 10.5, or later
- Oracle Database version 12.1.0.2, or later
- SAP Adaptive Server Enterprise version 16.0 SP03, or later

On a Linux VM, the following database is supported:
- SAP HANA Platform 2.0 SPS 04, or later

You can find an up-to-date list at [SAP Apps on IBM {{site.data.keyword.powerSys_notm}}](https://launchpad.support.sap.com/#/notes/2855850){: external}.

## How can I get the WebSphere Application Server that are delivered through the **Web Enablement for i** packages, and are available at no additional charge with IBM i?
{: #web-enablement-for-ibmi}
{: faq}

If you have an IBM i VM instance with the licensed program bundle in the {{site.data.keyword.powerSys_notm}} offering, you can download the WebSphere Application Server. This is available in the Web Enablement for i software at the Entitled System Support (ESS) website by completing the following steps:

1. Go to the [ESS website](https://www.ibm.com/servers/eserver/ess/index.wss){: external}.

2. Sign in. If this is the first time you are using ESS, refer to the **Help** section on the left menu. Download and read the **ESS_Registration_IBM_Customers_Guidelines** PDF.

3. Go to **My Entitled Software > IBM i evaluation and NLV download**.

4. Find the required software that you can download, install, and use. For example:

    **Web Enablement for i (5722-WE2)** - WebSphere Express V8.5.5
    **Web Enablement for i (5733-WE3)** - WebSphere V9

## How do I run Red Hat OpenShift Container Platform (OCP) on {{site.data.keyword.powerSys_notm}}?
{: #ocp_on_powervs}
{: faq}

You can find a complete tutorial at the IBM Developer site: [Deploying Red Hat OpenShift Container Platform 4.x on IBM {{site.data.keyword.powerSys_notm}}](https://developer.ibm.com/series/deploy-ocp-cloud-paks-power-virtual-server/){: external}.


## What is the network latency over Direct Link?
{: #network_latency}
{: faq}

[Off-Premises]{: tag-blue}
Network latency over Direct link is less than 1 millisecond in every location. To know more about network latency, see [Understanding latency](https://cloud.ibm.com/docs/dl?topic=dl-understanding-latency).

## What must be the network latency between the data center and the corresponding IBM Cloud region?
{: #network_latency-private-cloud}

[On-Premises]{: tag-red} The network latency between your data center and the corresponding IBM Cloud region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Network latency](/docs-draft/power-iaas?topic=power-iaas-network_latency_main).


<!--## How many DHCP pools can be created on the {{site.data.keyword.powerSys_notm}} private cloud?-->
<!--{: #dhcp-pool}-->
<!--{: faq}-->

<!--[On-Premises]{: tag-red}-->
<!--No of DHCP pools that can be created TBD-->
<!--Sridhar to provide input-->


## Are we notified about any planned maintenance activities?
{: #planned_maintenance_activity}
{: faq}

For planned maintenance and disruptive changes, the {{site.data.keyword.powerSys_notm}} operations team sends you notifications at least 7 days in advance. Watch the Notifications space in the IBM Cloud dashboard for these alerts. You can receive a copy of these notifications directly in your inbox if your email is subscribed for notifications.

## How do I convert existing volumes to replication enabled volumes?
{: #convert-to-replication-vol}
{: faq}

[Off-Premises]{: tag-blue}

You can retype the volume to toggle the `replicationEnable` flag of the volume by using [Perform an action on a Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-action-post) request. This is possible only when the volume pool of existing volume supports replication.

## How can I check whether volume is already replication enabled?
{: #check-for-replication-vol}
{: faq}

[Off-Premises]{: tag-blue}

You need to check the `replicationEnabled` attribute of the volume. A volume is replicationEnabled when it is true.

## How can I check whether a volume is a primary or an auxiliary volume?
{: #check-for-primary-vol}
{: faq}


[Off-Premises]{: tag-blue}

Volume is an auxiliary when `isAuxiliary` field of volume is true. When `replicationEnabled` is true and `isAuxiliary` is false then the volume is a primary volume.

## How can I check the serial number of my virtual server instance?
{: #check-serial-no}
{: faq}

The serial number is available after you deploy your virtual server instance and you can choose to display the serial number system value.

Pin the IBM i virtual server instances that use the IBM i licenses. If you do not pin the virtual server instances and request a migration to a different host, the serial numbers changes, and the IBM i license will not work.

## What should I do If I do not see the latest information in the UI?
{: #ui-not-updated}
{: faq}

Consider the following if you do not see an update in the User Interface(UI):

1. {{site.data.keyword.powerSys_notm}} utilizes a new caching mechanism for some resources to ensure that UI refresh operations complete in a timely manner.
2. In some scenarios out-dated information may be shown while the cache is updated, for approximately four minutes.
3. You can refresh the page to trigger an update to the cached data, eventually leading to the updated information's display.
4. When the DC has a heavy amount of traffic, and the cache is not refreshed within the last four minutes, {{site.data.keyword.powerSys_notm}} UI may display an error message. A subsequent page refresh retrieves and displays the updated information.

## Why can’t I see the storage pool and tier of my boot images?
{: #stock-image-copy-improve}
{: faq}

IBM improved the performance of copying a stock image into customers' accounts. As a result of this new feature, the newly copied stock image acts like an image reference, where volumes are not accessible to the user. The improved process now offers:
1.  Faster copy of stock image to your private project.
2.  The stock image cannot be exported. One can do VM capture and export on a deployed VM that uses the stock image.
3.  Storage pool and tier of a stock image shows "Empty" (API) or "Any" (UI) as VM can be deployed to any tier or pool by using the stock image.

## Can I select a specific resource group when I create a cloud connection?
{: #cc-res-group}
{: faq}

[Off-Premises]{: tag-blue}
No. When you create a cloud connection by using {{site.data.keyword.powerSys_notm}}, the cloud connection is always created in the default resource group even if you choose a specific resource group.

## What is the Maximum Transmission Unit (MTU) size that is supported in {{site.data.keyword.powerSys_notm}} networks?
{: #mtu-max}
{: faq}

The {{site.data.keyword.powerSys_notm}} supports a smaller MTU size of 1476 bytes for the public network interfaces and for the private network interfaces that are attached to a {{site.data.keyword.powerSys_notm}} VPN.

## Can I automate the Maximum Transmission Unit (MTU) configuration?
{: #mtu-config}
{: faq}

Yes, you can automate the network configurations such as the Maximum Transmission Unit (MTU).

To automate the MTU configuration, you need to customize your cloud-init network configuration. For more information, see the [Cloud-init docs on network configuration](https://cloudinit.readthedocs.io/en/latest/reference/network-config-format-v1.html){: external}.

Both AIX and IBM i support custom cloud-init configurations at the time of {{site.data.keyword.powerSys_notm}} instance (VM) deployment.

You can customize the cloud-init configurations only through the {{site.data.keyword.powerSys_notm}} API. The custom cloud-init is specified by the `userData` request parameter. For more information, see [Create a new Power VM Instance](https://cloud.ibm.com/apidocs/power-cloud#pcloud-pvminstances-post).

[On-Premises]{: tag-red} The automation of MTU is not supported. The admin must update the MTU value on the virtual machine manually.

## Can I add user interface to an existing virtual machine?
{: #ui-vm}
{: faq}

Yes, you can add a user interface to an existing virtual machine by performing Operation System administration steps to configure the desired adapter settings.
