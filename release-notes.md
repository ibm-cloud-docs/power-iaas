---

copyright:
  years: 2019, 2020
lastupdated: "2020-04-08"

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
{:external: target="_blank" .external}

# Release notes
{: #release-notes}

Use these release notes to learn about the latest changes to the {{site.data.keyword.powerSys_notm}} service.
{: shortdesc}

## 01 April 2020
{: #april-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} in the *TOR01* data center.
- You can now provision a {{site.data.keyword.powerSys_notm}} in the *LON06* data center.
- Added a virtual machine (VM) pinning policy (*none*, *soft*, or *hard*). You can choose to *soft pin* or *hard pin* a VM to the host where it is currently running. When you *soft pin* a VM for high availability, PowerVC automatically migrates the VM back to the original host once the host is back to its operating state. If the VM has a licensing restriction with the host, the *hard pin* option restricts the movement of the VM during remote restart, automated remote restart, DRO and live partition migration. The default pinninig policy is *none*. You can add the **pinPolicy** parameter when:
    - [Creating a new PVM Instance](https://cloud.ibm.com/apidocs/power-cloud#create-a-new-pvm-instance){: new_window}{: external}
    - [Getting a PVM Instance's current state or information](https://cloud.ibm.com/apidocs/power-cloud#get-a-pvm-instance-s-current-state-or-information){: new_window}{: external}
    - [Updating a PVM Instance](https://cloud.ibm.com/apidocs/power-cloud#update-a-pcloud-pvm-instance){: new_window}{: external}
<!-- - Added several [snapshot](https://cloud.ibm.com/apidocs/power-cloud#list-all-pvm-instance-snapshots-for-this-cloud-ins) API methods. -->

## 01 March 2020
{: #march-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} with a capped shared processor. For more information, see the [FAQ](/docs/power-iaas?topic=power-iaas-power-iaas-faqs#processor) and [Processor types](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-processor).

## 01 February 2020
{: #feb-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} in the *FRA05* data center.
