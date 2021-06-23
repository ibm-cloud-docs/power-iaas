---

copyright:
  years: 2021

lastupdated: "2021-06-22"

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

You can apply an affinity or anti-affinity policy to each VM instance within a placement group. After you create a placement group, you can provision a new VM instance into the placement group and ensure that the VM instance is not on the same server as any of your other VM instances. When you provision VMs with an affinity group then all VMs will be launched on the same server. When you provision VMs with an anti-affinity group then all VMs will be launched on different servers. 
<!--You can manage placement groups by using the Placement groups page or the Server details page in the IBM Power Systems Virtual Server console.-->

## Creating placement groups
{: #creating-placement-groups}

You can create placmenet groups and provision VM's in this placment group. The VMs in this group can be set to have affinity or anti-affinity with each other. Use the following API to create a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-post).

You cannot change the policy or name of a placement group after creating it. You can only add or remove member instances.
When you can create a VM and add it to a placement group, ensure that the placement group does not contain members in a **Build** state. Concurrently creating VMs within the placement groups is not supported. All the VMs will deploy in an error state when you are executing concurrent deployments with the placement group.
{: note}

## Get all server placement groups
{: #all-placement-groups}

You can view all the placememt groups that are created. Use the following API to display all existing placement groups:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-getall).

## Get server placement group detail
{: #placement-group-detail}

You can view details of a specific placement group. Use the following API to display details about a specific placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-cloud-placementgroups-get).

## Delete server placement group
{: #delete-placement-group}

You can delete an existing placement group. You can delete placement groups at any time even if they contain members. Use the following API to delete a server to a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-delete).
  
## Add server to placement group
{: #add-server-pgroup}

You can add VMs to the placement group you have created. The VMs that you add to the placement group must be in an **Active** state. Use the following API to add a server to a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-members-post).

## Remove server from placement group
{: #remove-server-pgroup}

You can remove a VM from a placement group. Use the following API to remove a server from a placement group:
[Create a new data volume](/apidocs/power-cloud#pcloud-placementgroups-members-delete).

