---

copyright:
  years: 2019, 2022

lastupdated: "2022-06-23"

keywords: release notes, announcements, feature updates, changes, power systems virtual server

---

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

## June 2022
{: #jun-2022}

- {{site.data.keyword.powerSys_notm}} now supports Linux (RHEL and SLES) stock images for non-SAP applications by using full Linux subscription. See [Full Linux® subscription for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-set-full-Linux).
- IBM i 7.5 is supported on {{site.data.keyword.powerSys_notm}}s.
- With virtual appliances independent software vendors (ISV) can offer OVA (ISV software plus operating system of your choice) for quick deployment of {{site.data.keyword.powerSys_notm}} workloads. See [Managing virtual appliances](/docs/power-iaas?topic=power-iaas-virtual-appliances).
  
## April 2022
{: #apr-2022}

- Snapshots that are created is monitored hourly and priced depending on the disk space used. See [Metering and pricing of snapshot](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone#metering-snapshot).

## March 2022
{: #march-2022}

- The Power Systems Virtual Server now supports [AIX 7.3](/docs/power-iaas?topic=power-iaas-deploy-custom-image#aix-details).
- You can view best practices and guidelines on [AIX backup performance on IBM Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-backup-strategies#backup-aix).

## December 2021
{: #dec-2021}

- You can now configure [Virtual private network (VPN)](/docs/power-iaas?topic=power-iaas-VPN-connections) by using the Power Systems Virtual Server GUI.
- You can now configure [Placement groups](/docs/power-iaas?topic=power-iaas-placement-groups) by using the Power Systems Virtual Server GUI.
- You can now set [10 Gbps speed for Cloud connection](/docs/power-iaas?topic=power-iaas-cloud-connections) by using the Power Systems Virtual Server GUI.
- You can now set [affinity policy for storage pools](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) by using the Power Systems Virtual Server GUI.

## October 2021
{: #oct-2021}

- You can now use [Virtual private network (VPN)](/docs/power-iaas?topic=power-iaas-VPN-connections) to connect an on-premises VPN gateway to an IBM Cloud™ VPN gateway that is created within a Power Systems Virtual Server VPN service. 
- You can now use [Virtual tape libraries](/docs/power-iaas?topic=power-iaas-virtual-tape-libraries) to backup IBM i data. 

## September 2021
{: #sep-2021}

- You can now use [Capturing and exporting a virtual machine](/docs/power-iaas?topic=power-iaas-capturing-exporting-vm) to view the new Job feature and view restrictions for VM capture, image import, and image export.
- You can now use [Mixed storage](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#mixed_storage) to attach storage volumes to a PVM instance from different storage tiers and pools.

## June 2021
{: #jun-2021}

- You can now use [Placement groups](/docs/power-iaas?topic=power-iaas-placement-groups) to add your servers into groups and apply affinity or anti-affinity policies.

## May 2021
{: #may-2021}

- You can now use [Cloud connections](/docs/power-iaas?topic=power-iaas-managing-cloud-connections) to automate the way you connect your Power Systems Virtual Server instances to the IBM Cloud resources.
- Power Systems Virtual Server now supports SAP HANA applications in IBM-provided RHEL stock images. For more information, see [Preparing Linux OS on IBM Power VS for SAP HANA](/docs/sap?topic=sap-power-vs-sles-hana).


## March 2021
{: #mar-2021}

- You can now deploy a Red Hat Enterprise Linux (RHEL) 8.1 and 8.2 virtual machine (VM) on a VM instance. For more information, see [Using RHEL within the Power Systems Virtual Server service](/docs/power-iaas?topic=power-iaas-linux-with-powervs).
- {{site.data.keyword.powerSys_notm}} provides a community-supported CentOS image under Linux operating system. However, IBM does not provide any support for this image. For more information, see [Configuring a Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance ).
- You can now choose *OSA21* data center to deploy your {{site.data.keyword.powerSys_notm}}.

## February 2021
{: #feb-2021}

- You can now choose *MON01* data center to deploy your {{site.data.keyword.powerSys_notm}}.
- The Power Systems Virtual Server offering now supports IBM i 7.1. For more information, see [Minimium PTF levels for IBM i](/docs/power-iaas?topic=power-iaas-minimum-levels).
- You can clone a volume or multiple volumes to create a consistent full copy of the volume. For more information, see [Cloning a volume](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone#cloning-volume).
- You can resize the memory and core counts to a maximum of 8 times of the specified values, and to a minimum of 1/8 times of the specified values when the VM was provisioned. For more information see [Resizing the virtual machine core count and memory](/docs/power-iaas?topic=power-iaas-modifying-server#resize-core-mem).
