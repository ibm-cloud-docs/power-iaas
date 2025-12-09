---

copyright:
  years: 2023, 2025

lastupdated: "2025-12-08"

keywords: faq, virtual server, network bandwidth, private network setup, multi-tenant environment, delete workspace, supported operating systems, hardware specifications, software maps, affinity, processor types, pinning, snapshot, clone, restore

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# FAQs for {{site.data.keyword.powerSys_notm}}
{: #powervs-faqs}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}





{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---


## What is {{site.data.keyword.powerSysFull}} Private Cloud?
{: #what-is-ppc}
{: faq}
{: support}

IBM {{site.data.keyword.powerSys_notm}} Private Cloud is an as-a-service offering that includes a prescriptive set of physical infrastructure (compute, network, and storage). The infrastructure is deployed in your own data center. IBM site reliability engineers (SREs) fully maintain and operate your {{site.data.keyword.on-prem}} infrastructure and manage it through the IBM Cloud. Also, you can adjust your workloads by using pay-as-you-use billing. For more information, see [What is IBM {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-about-power-iaas).



## What is the difference between the {{site.data.keyword.off-prem}} and {{site.data.keyword.on-prem}} offerings of IBM {{site.data.keyword.powerSys_notm}}?
{: #private-cloud-on-cloud-diff}
{: faq}



The primary difference between the two is where the physical infrastructure resides. The {{site.data.keyword.on-prem}} infrastructure resides in your data center, while {{site.data.keyword.powerSys_notm}} infrastructure resides in the IBM data centers.

## Which Power servers are supported?
{: #servers-supported}
{: faq}

[{{site.data.keyword.off-prem}}]{: tag-blue} IBM Power S922, IBM Power E980, IBM Power S1022, IBM Power S1122.

[{{site.data.keyword.on-prem}}]{: tag-red} IBM Power S1122, IBM Power E1150, IBM Power E1180.

For complete specifications, see [Hardware specifications for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#hardware-specifications-on-cloud) and [Hardware and software specifications for {{site.data.keyword.on-prem-fname}}](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-private-cloud-architecture#hardware-software-specs-private-cloud).



## What versions of AIX, IBM i, and Linux&reg; are supported?
{: #os-versions}
{: faq}
{: support}

The supported versions of AIX, IBM i, and Linux&reg; operating systems depend on the IBM Power hardware.


### AIX
{: #aix-os-version}
{: faq}

[{{site.data.keyword.off-prem}}]{: tag-blue}

The IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}} supports the following versions of the AIX operating system:

* S922 - AIX 7.1 or later
* E980 - AIX 7.1 or later
* S1022 - AIX 7.1 Technology Level (TL) 5 or later
* S1122 - AIX 7.2 TL5 SP10 and 7.3 TL3 SP1 or later

The following stock images are available when you create a virtual machine:





- AIX 7.3 TL4 SP0
- AIX 7.3 TL3 SP1
- AIX 7.2 TL5 SP10
- AIX 7.2 TL5 SP11
- AIX 7.1 TL5 SP9[^1]






[{{site.data.keyword.on-prem}}]{: tag-red}

The {{site.data.keyword.on-prem-fname}} supports the following versions of the AIX operating system:

- S1122 - AIX 7.2 TL5 SP9 or later
- S1150 - AIX 7.2 TL5 SP9 or later
- E1180 - AIX 7.2 TL5 SP9 or later

The following stock images are available when you create a virtual machine:




- AIX 7.3 TL4 SP0
* AIX 7.3 TL3 SP0
- AIX 7.2 TL5 SP11
* AIX 7.2 TL5 SP9
* AIX 7.1 TL5 SP9[^1A]


[^1]: AIX 7.1 on Power Virtual Server ended normal support on 30 April 2023 and is supported via service extension only. Please refer to the [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external} upcoming EoL dates and prepare to upgrade to a later version.

[^1A]: AIX 7.1 on Power Virtual Server ended normal support on 30 April 2023 and is supported via service extension only. Please refer to the [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external} upcoming EoL dates and prepare to upgrade to a later version.




To view the system software maps, refer to the AIX 7.1, AIX 7.2, and AIX 7.3 information. If you use an unsupported version, it is subject to outages during planned maintenance windows with no advanced notification given.

For more information about which versions of AIX are compatible with various Power Systems, see the [System to AIX maps](https://www.ibm.com/support/pages/node/6020074){: external}.


For more information about end of service pack support (EoSPS) dates, see [AIX support lifecycle](https://www.ibm.com/support/pages/aix-support-lifecycle-information){: external}.

### IBM i
{: #ibm-os-versions}
{: faq}

{{site.data.keyword.powerSys_notm}} supports IBM i 7.2, or later.
The {{site.data.keyword.on-prem-fname}} supports IBM i 7.3, or later.

If you are using IBM i 6.1, you must first upgrade the OS to a current support level, then migrate to the {{site.data.keyword.powerSys_notm}}. IBM i 7.2 supports direct [upgrades from IBM i 6.1 or 7.1 (N-2)](https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_72/rzahc/fastpathrzahc.htm){: external}.

- [S922 (9009-22A), E980 (9080-M9S), S1022 (9105-22A), S1122 (9824-22A), and E1180 (9080-HEU) software maps](https://www-01.ibm.com/support/docview.wss?uid=ssm1platformibmi){: external}
- [IBM i PTF minimum levels](/docs/power-iaas?topic=power-iaas-minimum-levels)
- [IBM i release life cycle](https://www.ibm.com/support/pages/release-life-cycle){: external}

IBM i stock images currently available when you create a VM are:







* IBM i COR[^2][^3]
* IBM i 7.6
* IBM i 7.5 TR5
* IBM i 7.4 TR11
* IBM i 7.3 TR13[^5]
* IBM i 7.2 TR9[^5A][^6]




[^2]: IBM i Cloud Optical Repository (COR) is a virtual image. You can deploy the image and use it as a Network File Server (NFS) to perform various IBM i tasks that require media. For more information on COR images, see [Cloud Optical Repository](https://cloud.ibm.com/media/docs/downloads/power-iaas/Cloud_Optical_Repository.pdf){: external}.

[^3]: For more information about performing an upgrade, see [57xxSS1 Option 1 or Option 3 in *ERROR - Tips Before Reinstallation](https://www.ibm.com/support/pages/57xxss1-option-1-or-option-3-error-tips-reinstallation){: external}.

[^5]: IBM i 7.3 and 7.2 on Power Virtual Server ended normal support on 1 October 2023 and are supported via paid service extension only. Please refer to the [IBM i lifecycle](https://www.ibm.com/support/pages/release-life-cycle){: external} page for upcoming EoL dates and prepare to upgrade to a later version.

[^5A]: IBM i 7.3 and 7.2 on Power Virtual Server ended normal support on 1 October 2023 and are supported via paid service extension only. Please refer to the [IBM i lifecycle](https://www.ibm.com/support/pages/release-life-cycle){: external} page for upcoming EoL dates and prepare to upgrade to a later version.


The IBM i 7.4, 7.5, 7.6, and COR OS images in the Image Catalog are supported on Power10 and later systems. However, you can create a custom image or upgrade your IBM i virtual server instance (VSI) by downloading the media from [Entitled Systems Support (ESS)](https://www.ibm.com/servers/eserver/ess/landing/landing-page) and by navigating to **My entitled software** > **IBM i Evaluation and NLV Download** section.
{: note}






[^6]: Not supported on {{site.data.keyword.on-prem}}.




### Linux
{: #linux-os-versions}
{: faq}

[{{site.data.keyword.off-prem}}]{: tag-blue}

{{site.data.keyword.powerSys_notm}} supports Red Hat Enterprise Linux (RHEL) and SUSE Linux Enterprise (SLES) distributions. Linux stock images are available when you select Full Linux Subscription or bring your own license. For more information, see [Full Linux® subscription for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-set-full-Linux).

The following list of Linux stock images are available:

Red Hat

* RHEL 9.6 general purpose (RHEL9-SP6) [^footnote11]
* RHEL 9.6 for SAP HANA (RHEL9-SP6-SAP-HANA)
* RHEL 9.6 for SAP NetWeaver (RHEL9-SP6-SAP-NETWEAVER)
* RHEL 9.4 general purpose (RHEL9-SP4) [^footnote5]
* RHEL 9.4 for SAP HANA (RHEL9-SP4-SAP-HANA)
* RHEL 9.4 for SAP NetWeaver (RHEL9-SP4-SAP-NETWEAVER)
* RHEL 9.2 for SAP HANA (RHEL9-SP2-SAP)
* RHEL 9.2 for SAP NetWeaver (RHEL9-SP2-SAP-NETWEAVER)
* RHEL 8.10 general purpose (RHEL8-SP10)  [^footnote6]
* RHEL 8.10 for SAP HANA (RHEL8-SP10-SAP-HANA)
* RHEL 8.10 for SAP NetWeaver (RHEL8-SP10-SAP-NETWEAVER)
* RHEL 8.8 for SAP HANA (RHEL8-SP8-SAP)
* RHEL 8.8 for SAP NetWeaver (RHEL8-SP8-SAP-NETWEAVER)
* RHEL 8.6 for SAP HANA (RHEL8-SP6-SAP)
* RHEL 8.6 for SAP NetWeaver (RHEL8-SP6-SAP-NETWEAVER)






SUSE [^footnote8]

* SLES 15 SP7 general purpose (SLES15)  [^footnote12]
* SLES 15 SP7 for SAP HANA (SLES15-SP7-SAP)
* SLES 15 SP7 for SAP NetWeaver (SLES15-SP7-SAP-NETWEAVER)
* SLES 15 SP6 general purpose (SLES15)  [^footnote7]
* SLES 15 SP6 for SAP HANA (SLES15-SP6-SAP) [^footnote9]
* SLES 15 SP6 for SAP NetWeaver (SLES15-SP6-SAP-NETWEAVER) [^footnote10]
* SLES 15 SP5 for SAP HANA (SLES15-SP5-SAP)
* SLES 15 SP5 for SAP NetWeaver (SLES15-SP5-SAP-NETWEAVER)
* SLES 15 SP4 for SAP HANA (SLES15-SP4-SAP)
* SLES 15 SP4 for SAP NetWeaver (SLES15-SP4-SAP-NETWEAVER)
* SLES 15 SP3 for SAP HANA (SLES15-SP3-SAP)
* SLES 15 SP3 for SAP NetWeaver (SLES15-SP3-SAP-NETWEAVER)




[^footnote5]: RHEL 9.4 GP is supported on IBM Power9, Power10 and Power11 systems.
[^footnote6]: RHEL 8.10 GP is supported on IBM Power9, Power10 and Power11 systems.
[^footnote11]: RHEL 9.6 GP is supported on IBM Power9, Power10 and Power11 systems.

[^footnote7]: SLES 15 SP6 GP is supported on IBM Power9, Power10 and Power11 systems.
[^footnote12]: SLES 15 SP7 GP is supported on IBM Power9, Power10 and Power11 systems.
[^footnote9]: Install the [insserv package](/docs/sap?topic=sap-power-vs-set-up-power-instances#power-vs-addtl-sw-sles-sap) as a prerequisite.
[^footnote10]: Install the [insserv package](/docs/sap?topic=sap-power-vs-set-up-power-instances#power-vs-addtl-sw-sles-sap) as a prerequisite.
[^footnote8]: SLES images are not currently supported on {{site.data.keyword.on-prem}}.



The S1022 systems support RHEL 8.4 (and later) and SLES 15 SP3 (and later) versions.
{: note}

To use your own license, select the OS image that with `-BYOL` suffix. On the **Create virtual server instance** page, these images are listed under the **Client supplied subscription** section. Alternatively, you can create your own customized Linux image in OVA format by using the Linux stock images that are available when you select Full Linux Subscription. For more information, see [Creating a custom Linux image in OVA format](/docs/power-iaas?topic=power-iaas-linux-deployment).

To view the certification details in the Red Hat catalog, see [IBM Power System E980 (9080-M9S)](https://catalog.redhat.com/hardware/servers/detail/17035){: external} and [IBM Power System S922 (9009-22A)](https://catalog.redhat.com/hardware/servers/detail/9225){: external}. For additional support, refer to the distribution (distro). For instructions, see [Installing and configuring cloud-init on Linux](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.4/com.ibm.powervc.standard.help.doc/powervc_install_cloudinit_hmc.html){: external}.


[{{site.data.keyword.on-prem}}]{: tag-red}

The {{site.data.keyword.on-prem-fname}} supports Red Hat Enterprise Linux (RHEL) with RHEL stock images that includes support from IBM and access to RHEL bug fixes from Satellite servers hosted on IBM Cloud. This capability is referred to as the Full Linux Subscription (FLS) model, which is different from the bring your own license or custom Linux image model. For more information, see [Full Linux subscription for {{site.data.keyword.on-prem-fname}}](/docs/power-iaas?topic=power-iaas-full-linux-sub).
{: #FLS}


FLS provides access to RHEL OS fixes and updates through activation keys for Power servers, which are hosted on an IBM satellite server within the IBM Cloud environment. To register for FLS, select one of the stock (RHEL OS) images that are provided by the IBM {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.on-prem}}.

The following list is an example of the FLS offerings:





* Stock images: RHEL 8.4 (General), RHEL 8.6 (General), RHEL 9.4 (General)
* Support: You pay IBM for support
* Patches: You receive keys for satellite servers to obtain Linux patches from Linux distribution (Linux distros)

## Where can I find cost estimates for {{site.data.keyword.powerSys_notm}} infrastructure?
{: #estimate}
{: faq}

To generate an estimated price, use the [{{site.data.keyword.powerSys_notm}} Estimate cost](https://cloud.ibm.com/power/estimate){: external} tool. For more information, see [Generating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate). For other pricing-related questions for {{site.data.keyword.on-prem-fname}}, see [Pricing FAQs](/docs/power-iaas?topic=power-iaas-pricing-private-cloud#faq).



## Can {{site.data.keyword.on-prem-fname}} in Client location pods be expanded with additional compute nodes?
{: #expand-pods}
{: faq}

Yes, you can add up to the maximum number of compute nodes for a specific configuration size. For example, you can start with 5 nodes and then add 3 more nodes.

## Can {{site.data.keyword.on-prem-fname}} in Client location pods be expanded with additional storage?
{: #expand-pods-storage}
{: faq}

Yes, you can expand the pod with additional storage capacity. But you cannot add more storage controllers.

## Are the {{site.data.keyword.on-prem-fname}} in Client location pods equipped with spare compute nodes for maintenance?
{: #spare-compute-node}
{: faq}

In each pod, one spare node is available that is exclusively usable for IBM operational purposes, such as to perform system maintenance. The system type of the spare node matches the largest client-usable node. For example, if you have a pod with 4X S1022 and 1X E1080 client-usable hosts, then the spare node is E1080.



## Where can I find the logs for the pod software or operator access logs?
{: #pod-logs}
{: faq}




As a security officer, auditor, or manager, you can use the IBM Cloud Logs service to manage general purpose application logs, platform logs, or structured audit events. IBM Cloud Logs can be used with logs from both IBM Cloud services and customer applications. For more information, see [Getting started with IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-getting-started){: external}




## Will the pod disconnect from the IBM Cloud if there is an unplanned network outage?
{: #pod-disconnect-unplanned-nw-mcp}
{: faq}

If an unplanned network outage occurs for the management network that is connecting the IBM Cloud instance to the pod infrastructure, the VMs continue to run within the pod.

See Table 1 for the implications of a pod that is running in a disconnected mode due to an unplanned network outage. Also, the primary and secondary management connections (Direct Link or site-to-site VPN) to the IBM Cloud are lost.

{{_include-segments/network-outage-impact-table.md}}





## Can I use my own AIX, IBM i, or Linux  image?
{: #image}
{: faq}
{: support}

Yes. This feature is known as **bring your own image**. For more information, see [Deploying a custom image within IBM {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-deploy-custom-image).





## What versions of stock images are available?
{: #stock-images}
{: faq}
{: support}

For each major version (example: Technology Level) of the operating system (OS) that is enabled through the offering, {{site.data.keyword.powerSys_notm}} provides a single stock image. {{site.data.keyword.powerSys_notm}} typically provides stock images for the last three major versions of the supported OS. Any update to the OS stock image is planned only when the image level is certified for {{site.data.keyword.powerSys_notm}} environment.

## When are stock images removed from the catalog?
{: #remove-stock-images}
{: faq}
{: support}

Any unsupported and older stock images are periodically removed from the offering. You are notified three weeks before the images are removed.

## What happens to virtual machines deployed by using stock images that are removed?
{: #vm-stock-images}
{: faq}
{: support}

If the stock images that are used to deploy the virtual machines are removed, the virtual machines can continue to operate without any issue. You are recommended to update the operating system by following the vendor’s guidelines specific to your operating system.

## What formats can I use to upload a custom image?
{: #custom-image}
{: faq}

Currently, you can import a custom image in the following formats: _.ova_, _.ova.gz_, _.tar_, _.tar.gz_ and _.tgz_.

## What storage types are available in the storage area network (SAN)?
{: #storage-faq}
{: faq}
{: support}

Each volume has a storage tier, which defines how many I/O operations per second (IOPS) can be started against that volume. These tiers can scale according to the size of the volume.

The following tiers are supported:
* Tier 0 (25 IOPS/GB)
* Tier 1 (10 IOPS per GB)
* Tier 3 (3 IOPS per GB)
* Fixed 5000 IOPS

If you find the storage tiers are over or under-provisioned, you can change the storage tier of an existing volume. For more information, see [Storage tiers](/docs/power-iaas?topic=power-iaas-private-cloud-architecture#storage-tiers-spec-private-cloud).

## How do I extend my AIX rootvg?
{: #rootvg}
{: faq}

By default, the system deploys 20 GBs for the AIX _rootvg_. You can extend the AIX _rootvg_ by using the [extendvg](https://www.ibm.com/support/knowledgecenter/ssw_aix_72/e_commands/extendvg.html){: external} command to add a physical volume.

## What's the difference between shared capped and shared uncapped processor performance? How are they compared with dedicated processor performance?
{: #processor}
{: faq}

When you deploy a VM, you can choose between **Dedicated**, **Shared capped**, or **Shared uncapped** cores. The following list provides a simplified breakdown of their differences:

- **Shared uncapped**: shared among other clients
- **Shared capped**: shared, but resources do not expand beyond the requested capacity (used mostly for licensing)
- **Dedicated**: resources are allocated for a specific client (used for specific third-party considerations)

The core-to-virtual core ratio is 1:1. For shared processors, fractional cores round up to the nearest whole number. For example, 1.25 cores equal 2 virtual cores. For more information, see [How does shared processor performance compare to dedicated processors](https://community.ibm.com/community/user/power/blogs/pete-heyrman1/2020/06/16/how-does-shared-processor-performance-compare-to-d?CommunityKey=71e6bb8a-5b34-44da-be8b-277834a183b0&tab=recentcommunityblogsdashboard){: external}, [Pricing for {{site.data.keyword.on-prem-fname}}](/docs/power-iaas?topic=power-iaas-pricing-private-cloud), and [Pricing for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).

| Dedicated processors                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The hypervisor makes a 1:1 binding between the processor of the partition and a physical processor core. After a VM is activated, the 1:1 binding is static. In the VM, the operating system (OS) logical thread runs on the physical processor core that is bound with the processor. With a dedicated processor partition, you must resize the number of cores to meet the **peak** demand of the partition. For example, on a typical workday, the CPU consumption is around four cores. But, because of the **peak** demand, the processor requires around eight cores. So, configure the partition with eight cores to handle the **peak** demand and avoid any queuing delays in dispatching the applications. |
{: class="simple-tab-table"}
{: tab-group="processor"}
{: caption="Dedicated processors" caption-side="top"}
{: #proc-table-1}
{: tab-title="Dedicated processors"}

| Shared processors                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Shared processors have two sharing modes: capped or uncapped. For a capped partition, the amount of CPU time is capped to the value specified for the entitlement. For example, a capped partition with processing units set to 0.5, can use up to 30 seconds of CPU time every minute. For an uncapped partition, the number of virtual processors defines the upper-limit of CPU consumption and not the value that is specified for processing units. For example, if the number of virtual processors are set to 3, the partition can use up to 180 seconds of CPU time every minute (three virtual processors each running at 100% utilization are equivalent of three physical cores worth of CPU time). The server must have unused capacity available for a partition to use more than its configured processing units. |
{: class="simple-tab-table"}
{: tab-group="processor"}
{: caption="Shared processors" caption-side="top"}
{: #proc-table-2}
{: tab-title="Shared processors"}










## How does my current environment compare to what's available through the {{site.data.keyword.powerSys_notm}}?
{: #performance}
{: faq}

If you like to compare your current environment's performance to what's available through the {{site.data.keyword.powerSys_notm}} offering, see the [IBM Power Performance Report](https://www.ibm.com/downloads/cas/K90RQOW8){: external}.

## How do I migrate my VM from one data center to another (WDC04 to DAL13)?
{: #vm-migration}
{: faq}

To migrate your VM from one data center to another, you must capture and export your VM to Cloud Object Storage. After you successfully capture and export your VM, copy it to the Cloud Object Storage in the destination region, then do an import followed by a deployment.

## What does VM pinning do?
{: #pinning}
{: faq}








You can choose a pinning policy: _soft pin_ or _hard pin_, to pin a VSI to the host where it is running. If pinning is not set or if it is set to _soft pin_, the VSI is automatically migrated or remote restarted during maintenance windows or in case of host failure.

When you _soft pin_ a VSI for high availability, {{site.data.keyword.powerSys_notm}} automatically migrates the VSI to the original host once the host is back to its operating state.

When you _hard pin_ a VSI, the movement of the VSI is restricted during remote restart, automated remote restart, dynamic resource optimization, and live partition migration. The movement of the VSI is also restricted if the VSI has a licensing restriction with the host. If the VSIs are set to _hard pin_, VSIs are stopped if the frame is down.

The default pinning policy is _none_.




## What does it mean to set an affinity or anti-affinity rule?
{: #affinity}
{: faq}

You can apply affinity and anti-affinity policies to both VMs and volumes.

**VM affinity and anti-affinity policy** allow you to spread a group of VMs across different hosts or keep them on a specific host.

Volume affinity and anti-affinity policy allow you to control the placement of a new volume based on an existing PVM instance (VM) or volume. When you set an affinity policy for a new storage volume, the volume is created within the same storage provider as an existing PVM instance or volume. With an anti-affinity policy, the new volume is created in a different storage provider other than the storage provider the existing PVM instance or volume is located in.

The use of volume affinity policy (affinity or anti-affinity) requires the availability of multiple storage providers. You might experience the following errors when you use a volume affinity policy:

- If an additional storage provider is not available to fulfill the requested policy, you might receive an error. The error indicates the inability to locate a storage provider to create a volume by using the requested volume affinity policy.

- If additional storage providers exist but the storage providers do not have sufficient space to fulfill the requested policy, you might receive an error. The error indicates the inability to locate a storage provider with enough free capacity to satisfy the requested volume size.

## How to set a PVM instance to allow attaching mixed storage?
{: #mixed_storage}
{: faq}

You can now attach storage volumes to a PVM instance from different storage tiers and pools, other than the storage pool the PVM instance's root (boot) volume is deployed in. To attach storage volumes to a PVM, modify the PVM instance and set the _storagePoolAffinity_ property of the new PVM instance to false. By default, the _storagePoolAffinity_ property of the PVM instance is set to true when the PVM instance is deployed and can be changed only by using the modified PVM instance API. Attaching mixed storage to a PVM instance has implications on the PVM instance capture, clone, and snapshot features. For more information about modifying a PVM instance API, see [Modify PVM Instance](/apidocs/power-cloud#pcloud-pvminstances-put).

## Does IBM provide maintenance for the AIX, IBM i, or Linux operating systems?
{: #licensing-os}
{: faq}

No. It is the customer's responsibility to maintain, update, and manage the AIX, IBM i, or Linux operating system.

## How does licensing work for the AIX, IBM i, or Linux operating systems?
{: #os-support}
{: faq}

The license for the AIX and IBM i operating systems is part of the overall cost for the workspace. You cannot use an existing license that you already purchased. Refer to the AIX section to learn how to [create an AIX VM](/docs/power-iaas?topic=power-iaas-create-vm).

You can use the movable IBM i (IBM i MOL) to move your existing on premises entitlements to {{site.data.keyword.powerSys_notm}}. Contact support to know more about the IBM i MOL, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

{{site.data.keyword.powerSys_notm}} supports multiple levels of RHEL and SLES. You can either use IBM provided stock Linux images with IBM Full Linux Subscription or bring your own custom Linux image with vendor-provided subscription.

For more information about supported versions of OS, see [What versions of AIX, IBM i, and Linux&reg; are supported?](/docs/power-iaas?topic=power-iaas-powervs-faqs#os-versions).

## How does third-party licensing work?
{: #third-party}
{: faq}

Clients are responsible for third-party licensing.

## What are the hardware specifications?
{: #hardware-specs}
{: faq}
{: support}

For more information, see [Hardware specifications for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-on-cloud-architecture#hardware-specifications-on-cloud) and [Hardware and software specifications for {{site.data.keyword.on-prem-fname}}](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-private-cloud-architecture#hardware-software-specs-private-cloud).

## Do {{site.data.keyword.powerSys_notm}} run in a multi-tenant environment?
{: #multi}
{: faq}

[{{site.data.keyword.off-prem}}]{: tag-blue}

The {{site.data.keyword.powerSys_notm}} runs in a multi-tenant environment. If you have signed up for a dedicated host, you can get single-tenant capabilities.

## Are there bare-metal options?
{: #bare}
{: faq}

No, the bare-metal options are not available. The {{site.data.keyword.powerSys_notm}} offering focuses on virtual instances.

## Can you tell me more about the snapshotting, cloning, and restoring capabilities?
{: #snapshot}
{: faq}

{{site.data.keyword.powerSys_notm}} provides the capability to capture full and point-in-time copies of entire logical volumes or data sets. Using IBM's _FlashCopy_ feature, the [{{site.data.keyword.powerSys_notm}} API](https://cloud.ibm.com/apidocs/power-cloud#introduction){: external} lets you create delta snapshots, volume clones, and restore your disks. To learn more, see [Snapshotting, cloning, and restoring](/docs/power-iaas?topic=power-iaas-snapshots-cloning).

## What are the key differences between a snapshot and a clone?
{: #snap-vs-clone}
{: faq}

The key differences are as follows:

| Context          | Snapshot                                                                                                        | Clone                                                                                                                        |
| ---------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Definition       | A snapshot is a thin-provisioned group of volumes that cannot be attached to a host or accessed or manipulated. | A clone is created from a snapshot and results in independent volumes which surface in the GUI and can be attached to hosts. |
| Primary function | Revert or restore the source disks to a desired state                                                           | Create a complete volume clone                                                                                               |
| Ease of creation | Easy and quick process                                                                                          | Three-step process and takes a long time                                                                                     |
| Pricing          | Charged 30% of the regular storage rate                                                                         | target volume storage plus the GRS costs                                                                                     |
{: caption="Differences between a snapshot and clone" caption-side="bottom"}

See [Snapshots, cloning, and restoring](/docs/power-iaas?topic=power-iaas-snapshots-cloning) for more detailed information.



## Are there any initial snapshot requirements in terms of storage?
{: #snap-storage-req}
{: faq}

None. The storage is allocated on demand.

## Does the snapshot and volume clone support any safeguard policy?
{: #snap-clone-safeguard}
{: faq}

None. {{site.data.keyword.powerSys_notm}} does not (currently) provide any options to safeguarded copy (such as cyber protection).

## Can you tell me more about the backup process by using the PowerHA Toolkit for IBM i?
{: #poweha-toolkit}
{: faq}

The PowerHA Toolkit for IBM i provides the 5250 user interfaces and automation to use them for backups. In a nutshell, it does the following tasks:
- Automates the memory flush
- Create the volumes-clone
- Attach the clones to a host
- Start the host
- Kick-off the backups
- Move the BRMS data back to the production VM and then shut down the backup VM
- Remove the cloned volumes

Using the PowerHA toolkit, you can create an intermediate snap-shot and a volumes-clone before the process enters the long-running volume detach or attach phase. You can pause the process immediately before the volumes are attached.

## How do you set up private networks between Intel&reg; Virtual Servers (x86) and {{site.data.keyword.powerSys_notm}}?
{: #connecting}
{: faq}
{: support}

[{{site.data.keyword.off-prem}}]{: tag-blue}

See the tutorial on [IBM {{site.data.keyword.powerSys_notm}} integration with x86-based workloads](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_and_x86_Integration_Tutorial_v1.pdf).

## How do you set up customer site access to a private network by using VPN?
{: #configuring}
{: faq}
{: support}

[{{site.data.keyword.off-prem}}]{: tag-blue}
For a complete tutorial about site-to-site Virtual Private Network (VPN) connectivity from a private cloud environment to {{site.data.keyword.powerSys_notm}}, see [IBM {{site.data.keyword.powerSys_notm}} Virtual Private Network Connectivity](https://cloud.ibm.com/media/docs/downloads/power-iaas-tutorials/PowerVS_VPN_Tutorial_v1.pdf){: external}.
For more information on VPN, see [Managing VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections).

## What firewall options are there around VPN connectivity?
{: #firewall}
{: faq}

[{{site.data.keyword.off-prem}}]{: tag-blue}
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

[{{site.data.keyword.off-prem}}]{: tag-blue}
**IBM Cloud Classic environment:** Inbound bandwidth is unlimited and not charged. Outbound bandwidth is charged per GB tier with bandwidth offered as an allotment for each month. As an example, for your compute instances, 250 GB is included with each monthly virtual server and 20 TB is included with each monthly bare metal server. Extra bandwidth can also be purchased per package. For more information, see [Bandwidth packages](https://www.ibm.com/cloud/bandwidth){: external}.

**IBM {{site.data.keyword.powerSys_notm}} environment:** Inbound bandwidth is unlimited and not charged. Bandwidth is not charged when you use a public network. If you are using a private network with DirectLink Connect, you are charged **IBM Cloud Classic environment** rates.

## What monitoring services are available?
{: #monitoring}
{: faq}







[{{site.data.keyword.off-prem}}]{: tag-blue}


IBM provides performance monitoring and status monitoring services for {{site.data.keyword.powerSys_notm}} only if the {{site.data.keyword.powerSys_notm}} workspace is registered as an observability instance on the IBM Cloud Monitoring system. The IBM Cloud Monitoring system is a cloud-native and container-intelligence management system. You can get the visibility to the performance and health of your applications, services, and platforms through the IBM Cloud Monitoring system. A {{site.data.keyword.powerSys_notm}} workspace is registered as an observability instance on the IBM Cloud Monitoring system when the **Monitoring** option is set to for the workspace. By default, the **Monitoring** option is set to on when you create an {{site.data.keyword.off-prem-fname}} workspace. You can set the **Monitoring** option to on or off for an existing workspace on the Workspace details page. For more information, see [Monitoring a workspace](/docs/power-iaas?topic=power-iaas-integrate-scc#cloud-monitoring).





For more information about the regions that support IBM Cloud Monitoring, see [Regions for IBM Cloud Monitoring](https://cloud.ibm.com/docs/monitoring?topic=monitoring-regions){: external}.







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




To delete a workspace (and all its resources), use the left navigation to navigate the workspace page. Find the workspace to be deleted and click the overflow menu on the upper right corner of the tile. Click **Delete** and confirm the request from the pull-down menu by typing _Delete_ in the text field. Finally, click the red **Delete** button to initiate the request.





## How do I delete a single virtual server instance?
{: #delete-service-instance}
{: faq}

Deleting a virtual server instance is a manual process. To delete all VSIs, delete the workspace or delete a subset of the virtual server instance.

- Delete a single virtual server instance from the Virtual server instances page.
Click the overflow menu (icon with 3 vertical dots) on the far right of each virtual server instance entry on the table. From the pull-down menu, click **Delete** to open the deleted confirmation modal. Click **Delete instance** to initiate the deletion request. This action cannot be undone.

- Delete a single virtual server instance from the details page.
On the Virtual server instances page, click the virtual server instance name present on the table, and go to the virtual server instance details page. Find and click the trash icon on the upper right of the screen. Confirm the request by clicking **Delete instance**. This action cannot be undone.






## How does the processor compatibility mode work in a VSI?
{: #processor-compatibility-modes-vsi}
{: faq}



You can set the preferred processor compatibility mode for a Virtual Server Instance (VSI) during its creation by using the GUI, CLI, API, or Terraform. For VSIs that are already deployed, you can change the preferred processor compatibility mode by modifying the VSI settings.



On the **Overview** tab of the VSI details page in the Power Virtual Server user interface, you can view the *Preferred* and *Effective* processor compatibility modes. The processor compatibility modes are defined as follows:

-	**Preferred processor compatibility mode**: The processor mode in which you want the VSI to operate. By default, Power Virtual Server sets the preferred processor compatibility mode to the highest mode supported by the targeted host type for the VSI.

-	**Effective processor compatibility mode**: The processor mode that is currently in use for the VSI. The physical host where the VSI is running determines the effective processor compatibility mode.

You cannot dynamically change the effective processor compatibility mode of a VSI. To change the effective processor compatibility mode, you must first change the preferred processor compatibility mode of the VSI, shut down the VSI, and then start the VSI again. During VSI activation, the hypervisor attempts to set the effective processor compatibility mode to match the preferred mode that you have specified for the VSI.
{: important}

{{_include-segments/cpu-compatibility-note.md}}


When the VSI is deployed and activated, the hypervisor on the host server checks the preferred processor compatibility mode and determines whether the operating system that is running in the VSI supports that mode. If the operating system supports the preferred processor compatibility mode, the hypervisor assigns the preferred processor compatibility mode to the VSI. If the operating system does not support the preferred processor compatibility mode, the hypervisor assigns the highest processor compatibility mode to the VSI that is supported by the operating system. After the VSI is activated, you can check the effective processor compatibility mode on the VSI details page.

For example,

- If the VSI runs on a `POWER11` processor-based host and you have set `POWER11` as the preferred processor compatibility mode.
- The operating system that is installed in the VSI supports only the `POWER10` processor capabilities and not the `POWER11` processor capabilities.

In such a scenario, the hypervisor assigns `POWER10` as the effective processor compatibility mode. The `POWER10` mode is the highest mode that both the operating system and firmware on the host server supports and it is lower than the preferred mode of `POWER11`.

If you set the preferred processor compatibility mode to `default`, the hypervisor does not consider `POWER9` mode as a valid effective processor compatibility mode. In the default mode, the effective modes can be `POWER9_Base`, `POWER10` mode, or `POWER11` mode, but it cannot be `POWER9` mode.

Use caution when you select `default` mode as the preferred processor compatibility mode. If the VSI for which the preferred mode is set to `default` migrates to a different host during maintenance operations (or for other reasons) and you subsequently shut down and start the VSI again, the hypervisor might assign a different mode than the one the VSI was previously running in. This reassignment can prevent the VSI from migrating back to its original host.

For more information about how to change the preferred processor compatibility mode for a VSI, see [Changing the preferred processor compatibility mode](/docs/power-iaas?topic=power-iaas-modifying-instance#change-cpu-compatibility).




## How do I open a support ticket for the {{site.data.keyword.powerSys_notm}} workspace?
{: #support-ticket}
{: faq}

To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).

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

[{{site.data.keyword.off-prem}}]{: tag-blue}
Network latency over Direct link is less than 1 millisecond in every location. To know more about network latency, see [Understanding latency](https://cloud.ibm.com/docs/dl?topic=dl-understanding-latency).

## What must be the network latency between the data center and the corresponding IBM Cloud region?
{: #network_latency-private-cloud}
{: faq}

[{{site.data.keyword.on-prem}}]{: tag-red} The network latency between your data center and the corresponding IBM Cloud region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Network latency](/docs/power-iaas?topic=power-iaas-network_latency_main).











## Are we notified about any planned maintenance activities?
{: #planned_maintenance_activity}
{: faq}

For planned maintenance and disruptive changes, the {{site.data.keyword.powerSys_notm}} operations team sends you notifications at least 7 days in advance. Watch the notifications space in the IBM Cloud dashboard for these alerts. You can receive a copy of these notifications directly in your inbox if your email is subscribed for notifications.

## How do I convert existing volumes to replication-enabled volumes?
{: #convert-to-replication-vol}
{: faq}



You can retype the volume to toggle the `replicationEnable` flag of the volume by using [Perform an action on a Volume](/apidocs/power-cloud#pcloud-cloudinstances-volumes-action-post) request. This is possible only when the volume pool of existing volumes supports replication.

## How can I check whether volume is already replication enabled?
{: #check-for-replication-vol}
{: faq}



You need to check the `replicationEnabled` attribute of the volume. A volume is replicationEnabled when it is true.

## How can I check whether a volume is a primary or an auxiliary volume?
{: #check-for-primary-vol}
{: faq}




Volume is an auxiliary when `isAuxiliary` field of volume is true. When `replicationEnabled` is true and `isAuxiliary` is false then the volume is a primary volume.



## Can I update the storage tiers for the Global Replication Services (GRS) enabled volumes?
{: #grs-tier}
{: faq}

You cannot update the storage tiers for the GRS enabled volumes. To change the storage tier type, complete the following steps:

1. Remove the volume from the volume group and disable GRS by completing the steps provided in the [Disabling GRS](/docs/power-iaas?topic=power-iaas-getting-started-GRS#disable-grs) topic.
2. Update the volume to the required storage tier type.
3. Enable the replication on the volume by setting the `replicationEnabled` flag as `True`.
4. Add the replication-enabled volume back to the volume group.



## How can I check the serial number of my virtual server instance?
{: #check-serial-no}
{: faq}

The serial number is available after you deploy your virtual server instance and you can choose to display the serial number system value.



## What should I do if I do not see the latest information in the UI?
{: #ui-not-updated}
{: faq}

Consider the following if you do not see an update in the User Interface(UI):

1. {{site.data.keyword.powerSys_notm}} uses a new caching mechanism for some resources to ensure that UI refresh operations complete in a timely manner.
2. In some scenarios out-dated information might be shown while the cache is updated, for approximately four minutes.
3. You can refresh the page to trigger an update to the cached data, eventually leading to the updated information's display.
4. When the DC has a heavy amount of traffic, and the cache is not refreshed within the last four minutes, {{site.data.keyword.powerSys_notm}} UI might display an error message. A subsequent page refresh retrieves and displays the updated information.

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

[{{site.data.keyword.off-prem}}]{: tag-blue}
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

Both AIX and IBM i support the configurations for custom cloud-init at the time of {{site.data.keyword.powerSys_notm}} instance (VM) deployment.

You can customize the cloud-init configurations only through the {{site.data.keyword.powerSys_notm}} API. The `userData` request parameter specifies the custom cloud-init. For more information, see [Create a new Power VM Instance](/apidocs/power-cloud#pcloud-pvminstances-post).

[{{site.data.keyword.on-prem}}]{: tag-red} The automation of MTU is not supported. The admin must update the MTU value on the virtual machine manually.

## Can I add a user interface to an existing virtual machine?
{: #ui-vm}
{: faq}

Yes, you can add a user interface to an existing virtual machine by performing Operation System administration steps to configure the desired adapter settings.






## How can I search for {{site.data.keyword.powerSys_notm}} resources using the assigned user tags?
{: #search-user-tags}
{: faq}


To view or search for resources that are provisioned in {{site.data.keyword.powerSys_notm}} by using the assigned `user tags`, see [Searching for Resources](/docs/account?topic=account-manage_resource&interface=cli#searching-for-resources). Note that the `user tags` are not included in the response for GET API and CLI requests.
