---

copyright:
  years: 2024

lastupdated: "2024-06-05"

keywords: returning pod, {{site.data.keyword.powerSys_notm}}, private cloud, decomission, remove pod

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Returning the pod to IBM
{: #returning_pod}

[On-premises]{: tag-red}

If you want to discontinue the {{site.data.keyword.powerSysFull}} Private Cloud services at the end of subscription tenure or because of any other scenario that is permitted by the contract with IBM, you must return the IBM {{site.data.keyword.powerSys_notm}} Private Cloud infrastructure as explained in the following steps:

1. Open a ticket with [IBM Support](/docs/power-iaas?topic=power-iaas-getting-help-and-support) and state your request to discontinue the IBM {{site.data.keyword.powerSys_notm}} Private Cloud services.
2. Back up all the application data and settings from the virtual server instances.
3. Delete all your virtual server instances and workspaces.
4. Delete the corresponding Satellite location instances after IBM completes the steps for pod teardown.

After you open the support ticket, IBM works with you to complete all the necessary operations from the IBM Cloud for the pod teardown, such as:
- Archiving any non-client operating system data.
- Securely and properly disposing of client OS and application residual data according to appropriate rules and regulations.
- Unregistering the pod from your IBM Cloud Satellite location.
- Decommissioning the IBM Direct Link connection that is used for control plane traffic and regional IBM Cloud resources that are associated with the pod.

IBM onsite service engineers will visit your data center to perform the physical uninstallation and packing the infrastructure for return along with logistical support.
