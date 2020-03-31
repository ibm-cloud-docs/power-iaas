---

copyright:
  years: 2019, 2020
lastupdated: "2020-04-01"

keywords: release notes, changes, power systems virtual server

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Release notes
{: #release-notes}

Use these release notes to learn about the latest changes to the {{site.data.keyword.powerSys_notm}} service.
{: shortdesc}

<!-- ## 01 April 2020
{: #april-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} in the London 3 (*LON06*) and Toronto (*TOR01*) colocations. -->

## 01 March 2020
{: #march-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} with a capped shared processor. This new functionality is an uncharged early access feature and will become fully available on **April 1, 2020**. The estimator and pricing detail will be updated on that date.
- Added several [snapshot](https://cloud.ibm.com/apidocs/power-cloud#list-all-pvm-instance-snapshots-for-this-cloud-ins) API methods.
- Added a virtual machine (VM) pinning policy (*none*, *soft*, or *hard).* You can choose to *soft pin* or *hard pin* a VM to the host where it is currently running. When you *soft pin* a VM for high availability, PowerVC automatically migrates the VM back to the original host once the host is back to its operating state. If the VM has a licensing restriction with the host, the *hard pin* option restrics the movement of the VM during remote restart, automated remote restart, DRO and live partition migration.

## 01 February 2020
{: #feb-2020}

- You can now provision a {{site.data.keyword.powerSys_notm}} in the Frankfurt 2 (*FRA05*) colocation.
