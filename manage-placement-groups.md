---

copyright:
  years: 2019, 2024

lastupdated: "2024-12-03"

keywords: managing placement groups, {{site.data.keyword.powerSys_notm}} as a service, private cloud, terminology, video, how-to, placement groups, add placement group, delete placement group

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing server placement groups
{: #managing-placement-groups}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

Server placement groups provide you control over the host or server on which a new virtual machine (VM) is placed. By using server placement groups, you can build high availability within a data center.
{: shortdesc}

You can apply an affinity or anti-affinity policy to each VM within a server placement group. After you create a placement group, you can provision a new VM in the placement group. When you set a placement group with an affinity policy, all VMs in that placement group are provisioned on the same server. When you set a placement group with an anti-affinity policy, all VMs in that placement group are provisioned on different servers.

You can use the user interface for placement groups only when the total number of VMs in your account is less than 100. If your account has more than 100 VMs, then you must use the CLI or API to create placement groups.
{: important}

## Creating server placement groups
{: #creating-placement-groups}

You can create server placement groups and provision VMs in this placement group. The VMs in this group can be set to have an affinity or anti-affinity policy with each other. Each placement group that you create must have a unique name. You can create a maximum of 25 placement groups. If you need to create more than 25 placement groups, raise a support ticket to increase the maximum limit. Use the following API to create a placement group: [Create a server placement group](/apidocs/power-cloud#pcloud-placementgroups-post).

You can add or remove VMs within the placement group. You cannot change the policy or name of a placement group after it is created.

To create a placement group, complete the following steps:

1. Go to the {{site.data.keyword.powerSys_notm}} user interface, and click **Server placement groups**.
2. In the **Server placement groups** page, click **Create group**.
3. Specify a name for the new placement group. Select a colocation policy to specify whether all the VMs under this placement group must reside in the same server or in a different server.
4. Click **Create**.

In the **Server placement groups** page, the table displays all placement groups. The table also indicates the number of VMs in each group and also the colocation policy.


## Server placement group APIs
{: #all-placement-groups}

You can use the following APIs for managing server placement groups:

- [Get all server placement groups](/apidocs/power-cloud#pcloud-placementgroups-getall): Displays all existing server placement groups.
- [Get server placement group details](/apidocs/power-cloud#pcloud-cloud-placementgroups-get): Displays details about a specific server placement group.
- [Delete server placement group](/apidocs/power-cloud#pcloud-placementgroups-delete): Deletes server placement groups even if they contain member instances.
- [Remove server from placement group](/apidocs/power-cloud#pcloud-placementgroups-members-delete): Removes a virtual server instance from a server placement group.

## Add VMs to a server placement group
{: #add-server-pgroup}

You can add VMs to a server placement group.  You cannot add a VM to a server placement group that contains a VM that is in **Build** state.  In this case, you must wait until the VM in the **Build** state to change to **Active** state, and then add a VM to the server placement group. Use the following API to add a server to a placement group: [Add server to placement group](/apidocs/power-cloud#pcloud-placementgroups-members-post).


When you add a VM to the server placement group, the request might not be complete due to a conflict (409) with the affinity policy of the server placement group. In this case, you might need to open a DLPAR operations support ticket. To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
{: note}

To add a VM to a placement group, complete the following steps:

1. Go to the {{site.data.keyword.powerSys_notm}} user interface and click **Virtual server instances**.
2. In the **Server placement groups** tab, from the placement group table, select a placement group that you want to add to the VM.
3. In the **VMs in placement groups** section, you can [create a new VM](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and add it to the placement group. You can also add an existing VM to the placement group.
4. Click **Add existing VM** to add an existing VM to the placement group. Select one or more VMs from the table and add it to the placement group.

VMs that you select must be on the same server or different server based on the colocation policy of the placement group. A VM can belong to only one placement group and VMs that are already placed in a different placement group is disabled in the table.
{: note}
