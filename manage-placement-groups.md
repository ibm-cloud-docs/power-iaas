---

copyright:
  years: 2021

lastupdated: "2021-06-24"

keywords: managing placement groups, placement groups, add placement group, delete placement group

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Managing server placement groups
{: #placement-groups}

Server placement groups provide you control over the host or server on which a new virtual machine (VM) is placed. By using server placement groups, you can build high availability within a data center.
{: shortdesc}

You can apply an affinity or anti-affinity policy to each VM instance within a server placement group. After you create a placement group, you can provision a new VM instance in the placement group. When you set a placement group with an affinity policy, all VMs in that placement group are launched on the same server. When you set a placement group with an anti-affinity policy, all VMs in that placement group are launched on different servers.

## Creating server placement groups
{: #creating-placement-groups}

You can create server placement groups and provision VMs in this placement group. The VMs in this group can be set to have affinity or anti-affinity policy with each other. Each placement group that you create must have a unique name. You can create a maximum of 25 placement groups. If you need to create more than 25 placement groups, raise a support ticket to increase the maximum limit. Use the following API to create a placement group:
[Create a server placement group](/apidocs/power-cloud#pcloud-placementgroups-post).

You cannot change the policy or name of a placement group after it is created. You can only add or remove VMs within the placement group.

To create a new placement group, complete the following steps:

1. Go to the Power Systems Virtual Server user interface and click **Server placement groups**.
2. In the **Server placement groups** page, click **Create group**.
3. Specify a name for the new placement group. Select a colocation policy to specify whether all the VMs under this placement group must reside in the same server or in a different server. 
4. Click **Create**.

In the **Server placement groups** page, the table displays all placement groups for this Power Virtual Server instance. The table also indicates the number of VMs in each group and also the colocation policy. 


## Server Placement group APIs
{: #all-placement-groups}

You can use the following for managing server placement groups: 

- [Get all server placement groups](/apidocs/power-cloud#pcloud-placementgroups-getall): Displays all existing server placement groups.
- [Get server placement group detail](/apidocs/power-cloud#pcloud-cloud-placementgroups-get): Displays details about a specific server placement group.
- [Delete server placement group](/apidocs/power-cloud#pcloud-placementgroups-delete): Deletes server placement groups even if they contain member instances.
- [Remove server from placement group](/apidocs/power-cloud#pcloud-placementgroups-members-delete): Removes a server from a server placement group.

## Add VMs to a server placement group
{: #add-server-pgroup}

You can add VMs to a server placement group. The VMs that you add to the server placement group must be in an **Active** state. Use the following API to add a server to a placement group:
[Add server to placement group](/apidocs/power-cloud#pcloud-placementgroups-members-post).

When you add a VM to the server placement group, the request might not be complete due to a conflict (409) with the affinity policy of the server placement group. In this case, you might need to open a DLPAR operations support ticket. To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support).
{: note}

To add a VM to a placement group, complete the following steps:

1. Go to the Power Systems Virtual Server user interface and click **Server placement groups**.
2. In the **Server placement groups** page, click the placement group name in the table that you want to add the VM to.
3. In the **VMs in placement groups** section, you can [create a new VM](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) and add it to the placement group. Or add an existing VM to the placement. 
4. Click **Add existing VM** to add an existing VM to the placement group. Select one or more VMs from the table and add it to the placement group. You can add a maximum of 10 VMs to one placement group. 

VMs that you select must be on the same server or different server depending on the colocation policy of the placement group. A VM can belong to only one placement group and VMs that are already placed in a different placement group is disabled in the table. 
{: note}
