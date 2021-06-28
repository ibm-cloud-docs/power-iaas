---

copyright:
  years: 2021

lastupdated: "2021-06-24"

keywords: managing placement groups, placement groups, add placement group, delete placement group

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

# Managing server placement groups
{: #placement-groups}

Server placement groups provide you control over the host or server on which a new VM is placed. By using server placement groups, you can build high availability within a data center, even though your virtual servers are isolated from each other.
{: shortdesc}

You can apply an affinity or anti-affinity policy to each VM instance within a placement group. After you create a placement group, you can provision a new VM instance into the placement group. Ensure that the new VM instance is not on the same server as any of your other VM instances. When you provision VMs with an affinity group then all VMs are launched on the same server. When you provision VMs with an anti-affinity group then all VMs are launched on different servers. 
<!--You can manage placement groups by using the Placement groups page or the Server details page in the IBM Power Systems Virtual Server console.-->

## Creating server placement groups
{: #creating-placement-groups}

You can create placement groups and provision VMs in this placement group. The VMs in this group can be set to have affinity or anti-affinity with each other. Each placement group that you are creating must have a unique name. You can create a maximum of 25 placement groups. If you need to create more than 25 placement groups, raise a support ticket to increase the maximum limit. Use the following API to create a placement group:
[Create a server placement group](/apidocs/power-cloud#pcloud-placementgroups-post).

You cannot change the policy or name of a placement group after it is created. You can only add or remove member instances.
When you can create a VM and add it to a placement group, ensure that the placement group does not contain members in a **Build** state. Concurrently creating VMs within the placement groups is not supported. All the VMs deploy in an error state when you are running concurrent deployments with the placement group.
{: note}

## Get all server placement groups
{: #all-placement-groups}

You can view all the placement groups that are created. Use the following API to display all existing placement groups:
[Get all server placement groups](/apidocs/power-cloud#pcloud-placementgroups-getall).

## Get server placement group detail
{: #placement-group-detail}

You can view details of a specific placement group. Use the following API to display details about a specific placement group:
[Get server placement group detail](/apidocs/power-cloud#pcloud-cloud-placementgroups-get).

## Delete server placement group
{: #delete-placement-group}

You can delete an existing placement group. You can delete placement groups at any time even if they contain members. Use the following API to delete a server to a placement group:
[Delete server placement group](/apidocs/power-cloud#pcloud-placementgroups-delete).
  
## Add server to placement group
{: #add-server-pgroup}

You can add VMs to the placement group that are created. The VMs that you add to the placement group must be in an **Active** state. Use the following API to add a server to a placement group:
[Add server to placement group](/apidocs/power-cloud#pcloud-placementgroups-members-post).

When you are adding a server to placement group, the request might not be completed due to a conflict (409) with the placement group affinity policy. In this case, you might need to open a DLPAR operations support ticket.
{: note}

## Remove server from placement group
{: #remove-server-pgroup}

You can remove a VM from a placement group. Use the following API to remove a server from a placement group:
[Remove server from placement group](/apidocs/power-cloud#pcloud-placementgroups-members-delete).

