---

copyright:
  years: 2019, 2020

lastupdated: "2020-06-20"

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

## June 2020
{: #june-2020}

- You can now deploy Linux on a {{site.data.keyword.powerSys_notm}}. To learn more, see [Using Linux within the Power Systems Virtual Server service](/docs/power-iaas?topic=power-iaas-using-linux).
- The {{site.data.keyword.powerSys_notm}} service now includes [a highly available 5 Gbps connection](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect) to IBM public cloud services.

## May 2020
{: #may-2020}

- IBM i software keys were cleared out due to an IBM Cloud update. You must re-apply any IBM i software licenses through the {{site.data.keyword.powerSys_notm}} user interace. The following IBM i builds require updates:
    - 7.4 MF99301 SI70544
    - 7.3 MF99207 SI69686
    - 7.2 SI71091
- Created a new article on [Planning a workload migration to an IBM POWER8 or POWER9 system](/docs/power-iaas?topic=power-iaas-system-migration).
- Added [snapshot, clone and restore capabilities](/docs/power-iaas?topic=power-iaas-volume-snapshot-clone) to the {{site.data.keyword.powerSys_notm}} service. You can use these new capabilities by using the [Power Systems Virtual Server API](https://cloud.ibm.com/apidocs/power-cloud#introduction).

  The snapshot, clone, and restore capabilities are currently available only in *DAL13*.
  {: preview}

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

  VM pinning is currently available in all data centers except for *WDC04* or *FRA04*.
  {: preview}

## March 2020
{: #march-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} with a capped shared processor. For more information, see the [FAQ](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor) and [Processor types](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-processor).

## February 2020
{: #feb-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} in the *FRA05* data center.
