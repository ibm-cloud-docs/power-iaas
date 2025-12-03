---

copyright:
  years: 2025
lastupdated: "2025-10-30"

keywords: virtual server instances (VSI), vm, power, compute, virtual machines, planning, best practices, instances, virtual machines (VM), virtual machine (VM) instance, Power virtual machine (VM) , maintenance, IBM Power S922, IBM Power E980, IBM Power S1022, IBM Power S1122, S922, E980, S1022, S1122, PowerVS, Power virtual server

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Understanding IBM {{site.data.keyword.powerSys_notm}} cloud maintenance operations
{: #about-cloud-maintenance}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

{{site.data.keyword.powerSysFull}} cloud maintenance operations help ensure the reliability, security, and performance of the infrastructure components within the data centers, including hosts, networks, and storage systems. IBM performs periodic maintenance to maintain optimal service levels and avoid disruptions.
{: shortdesc}

## Data center maintenance
{: #Powervs-data-center-maintenance}

IBM maintains its data centers by updating the network components, storage systems, and compute server infrastructure. Your workloads usually remain unaffected during the data center maintenance. {{site.data.keyword.powerSys_notm}} maintenance includes hosts, dedicated hosts, storage, and network infrastructure resources. The maintenance helps ensure that the IBM Power technology stack remains secure and up-to-date with appropriate security fixes and feature updates.

Most updates do not affect the workloads that are running on the {{site.data.keyword.powerSys_notm}}. If the maintenance is expected to affect your workloads, IBM notifies you in advance.


## Host maintenance
{: #powervs-host-maintenance}


Host maintenance activities, such as a firmware update, require a live partition migration of a virtual service instance (VSI), also known as logical partition (LPAR) from the compute host to another host. In such a scenario, the VSIs continue to run uninterrupted; therefore, IBM does not send you a notification. For more information, see [Viewing notifications](/docs/account?topic=account-viewing-notifications){: external}.

When you use the VSI pinning options, the VSI's availability during a maintenance activities is affected. VSI pinning prevents IBM Cloud from migrating the VSI to another host during the maintenance operation. In such a scenario, the live migration of the VSI is not possible, and the VSI must be in the *Shutoff* state for the host maintenance operation to complete. Therefore, you must use the VSI pinning options cautiously. Any downtime that is caused by VSI pinning during the host maintenance is excluded from the service level agreements. For more information, see [Service Level Agreements for IBM Cloud](https://www.ibm.com/support/customer/csol/terms/?id=i126-9268&lc=en){: external}.

For more information about VSI pinning, see [What does VM pinning do?](/docs/power-iaas?topic=power-iaas-powervs-faqs#pinning).

## Network maintenance
{: #power-vs-network-maintenance}

{{site.data.keyword.powerSys_notm}} infrastructure includes redundant network paths that support nondisruptive network maintenance. Network maintenance operation targets only one network fabric at a time from the set of redundant network fabrics. When one of the network fabrics undergoes maintenance, the system automatically redirects traffic to the alternate fabric. Some network packet loss might occur during any traffic rerouting, including when traffic is redirected from one network fabric to another during maintenance.

If you use IBM Cloud Connections instead of PER, you must configure two Cloud Connections to reduce network disruptions during the maintenance activities. For more information about how to migrate to PER, see [Migrating to PER](/docs/power-iaas?topic=power-iaas-per#migrate-per){: external}.
{: important}

## Storage maintenance
{: #powervs-storage-maintenance}

{{site.data.keyword.powerSys_notm}} infrastructure provides redundant storage I/O paths that allow nondisruptive upgrades of the storage hardware. During the storage maintenance, some of the redundant paths become temporarily unavailable. This behavior aligns with the standard multipath I/O management practices that are supported by AIX, IBM i, and Linux operating systems. Refer to your operating system guidelines for information about the multipath I/O management during the maintenance events.

Confirm that all disk paths are online after the maintenance activity. If any disk paths remain offline, initiate an operating system device scan to restore the offline paths.
{: note}
