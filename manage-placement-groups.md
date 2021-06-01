---

copyright:
  years: 2021

lastupdated: "2021-05-31"

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

# Managing VM placement groups
{: #placement-groups}

VM placement groups provide you control over the host or server on which a new VM is placed. By using VM placement groups, you can build high availability within a data center, even though your virtual servers are isolated from each other.
{: shortdesc}

You can apply an affinity or anti-affinity policy to each VM instance within a placement group. After you create a placement group, you can provision a new VM instance into the placement group and ensure that the VM instance is not on the same server as any of your other VM instances. 
<!--You can manage placement groups by using the Placement groups page or the Server details page in the IBM Power Systems Virtual Server console.-->

You cannot change the policy or name of a placement group after creating it. You can only add or remove member instances.
When you can create a VM and add it to a placement group, ensure that the placement group does not contain a VM with **Build** state. Otherwise, the VM will not be added to the placement group.
{: note}

## Creating placement groups
{: #creating-placement-groups}

Use the following API to create a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-post).

## Get all server placement groups
{: #all-placement-groups}

Use the following API to display all existing placement groups:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-getall).

## Get server placement group detail
{: #placement-group-detail}

Use the following API to display details about a specific placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-cloud-placementgroups-get).

## Delete server placement group
{: #delete-placement-group}

Use the following API to delete a server to a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-delete).
You must remove assigned servers from the placement group before the placement group can be deleted. 

## Add server to placement group
{: #add-server-pgroup}

Use the following API to add a server to a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-members-post).

## Remove server from placement group
{: #remove-server-pgroup}

Use the following API to remove a server from a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-members-delete).
To remove an instance from a placement group, you must delete or reclaim the instance.
