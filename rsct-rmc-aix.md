---

copyright:
  years: 2019, 2020

lastupdated: "2020-03-06"

keywords: rsct, rmc, IPv6

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
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Recommended Reliable Scalable Cluster Technology (RSCT) package levels for imported AIX image
{: #recommended-rsct-package}

RSCT is a set of software components that together provide a comprehensive clustering environment for AIX&reg;, Linux&reg;, Solaris, and Windows&reg; operating systems. RSCT is the infrastructure that is used by various IBM products to provide clusters with improved system availability, scalability, and ease of use. For the {{site.data.keyword.powerSys_notm}} offering, RSCT 3.1 is the minimum package level that is required for an imported AIX image (added IPv6 support). The {{site.data.keyword.powerSys_notm}} development team, however, recommends you use [RSCT 3.2](https://www.ibm.com/support/knowledgecenter/SGVKBA_3.2/navigation/welcome.html){: new_window}{: external} for optimal performance.

## Resource Managment Control (RMC)
{: #rmc-aix}

The RMC subsystem is the scalable backbone of RSCT that provides a generalized framework for managing resources within a single system or a cluster. Its generalized framework is used by cluster management tools to monitor, query, modify, and control cluster resources. RMC provides a single monitoring and management infrastructure for both RSCT peer domains and management domains.

The {{site.data.keyword.powerSys_notm}} AIX VMs RMC status is presented in the {{site.data.keyword.cloud}} dashboard as a health status. The RMC health status can be either **OK** or **Warning**. **Warning** statuses happen when the RMC subsystem between your VM and the management system is not connected.

The RMC connection between your VM and the system management service is configured when you create the AIX VM. When you deploy an AIX VM, the IPv6 management interface is injected into the VM. If you remove or overwrite this interface, an RMC connection is not possible. The following procedures can cause the injected IPv6 management interface to be lost after you deploy the AIX VM:

- You attach a different boot volume to the VM and boot from it
- You use the `mksysb restore` operation from an on-premises VM
- You use `smitty` to remove the IPv6 interface
