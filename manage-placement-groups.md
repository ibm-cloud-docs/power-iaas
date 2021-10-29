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

Server placement groups provide you control over the host or server on which a new virtual machine (VM) is placed. By using server placement groups, you can build high availability within a data center, even though your virtual servers are isolated from each other.
{: shortdesc}

You can apply an affinity or anti-affinity policy to each VM instance within a server placement group. After you create a placement group, you can provision a new VM instance in the placement group. Ensure that the new VM instance is not on the same server as any of your other VM instances. When you provision VMs with an affinity policy, all VMs are launched on the same server. When you provision VMs with an anti-affinity policy, all VMs are launched on different servers.

## Creating server placement groups
{: #creating-placement-groups}

You can create server placement groups and provision VMs in this placement group. The VMs in this group can be set to have affinity or anti-affinity policy with each other. Each placement group that you create must have a unique name. You can create a maximum of 25 placement groups. If you need to create more than 25 placement groups, raise a support ticket to increase the maximum limit. Use the following API to create a placement group:
[Create a server placement group](/apidocs/power-cloud#pcloud-placementgroups-post).

You cannot change the policy or name of a placement group after it is created. You can only add or remove VMs within the placement group.

When you can create a VM and add it to a placement group, ensure that the placement group does not contain member instances that are in a **Build** state. You cannot concurrently create VMs within placement groups. All VMs deploy in an error state when you are running concurrent deployments in a placement group.
{: note}

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

When you add a VM to the server placement group, the request might not be complete due to a conflict (409) with the affinity policy of the server placement group. In this case, you might need to open a DLPAR operations support ticket. To open a support ticket, see [Getting help and support](/docs/power-iaas?topic=power-iaas-getting-help-and-support)
{: note}
