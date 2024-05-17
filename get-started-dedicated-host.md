---

copyright:
  years: 2024

lastupdated: "2024-05-17"

keywords: dedicated host, primary workspace, secondary workspace

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

# Getting started with dedicated host
{: #dedicated-host}

The dedicated host feature on IBM {{site.data.keyword.powerSysFull}} significantly expands the range of computing options available by providing the ability to provision a dedicated host for your exclusive use. Dedicated hosts are metered by the hour for the entire capacity of the host. 

A dedicated host provides an additional flexibility to create virtual server instances, control their placement, and utilize the unique shared processor pool capabilities that are offered by {{site.data.keyword.powerSys_notm}}. With dedicated hosts, you can easily optimize your cloud infrastructure by utilizing single tenant servers to manage software licensing costs while increasing isolation from other users in a cloud environment.   

<!-- Dedicated hosts are ideal for your environment if you need a high level of customization and control over your cloud infrastructure, while also benefiting from the scalability and cost-effectiveness of cloud computing. -->

Visit the pricing page to learn more about the [pricing for dedicated hosts](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-dedicated-hosts).

The dedicated host provides the following features:
1.	Reserve a host server (IBM Power S922 or S1022) for your exclusive use. All cores and memory on the host are provisioned for your use.
2.	Get a detailed GUI-based view of host capacity information such as core, memory capacity and consumption. This provides the information on total, free, or used capacity for your dedicated hosts.
3. Share the dedicated hosts with all or a subset of your workspaces in the same account. You get an additional flexibility to control access to dedicated hosts across your organization.
4.	Flexibly create virtual server instances and place them on the dedicated host.  
5.	Create shared processor pools on the dedicated host and flexibly manage resource utilization including the Virtual Processor (VP) to Entitled Capacity (EC) ratio up to 20:1.
6.	Set your own custom names for the dedicated hosts and dedicated host groups.
    
Dedicated hosts are rolled out in two phases – Select Availability and General Availability. Select Availability is in `DAL10`, `DAL12`, `WDC06`, and `WDC07` data centers. General Availability will expand the reach of dedicated host capabilities further around the world.
{: note}

## Primary workspace
{: #primary-ws}

A primary workspace is the owning tenant of a dedicated host or storage reservation and is allowed full control over the associated resources. The primary workspace will have the capability to remove, delete, or share the dedicated resources that are owned by the workspace under the IBM Cloud account.  

With the same IBM Cloud account, the primary workspace user will have the control over sharing the dedicated resources with all (or a subset) of their workspaces (in the same account).  

The primary workspace will receive billing charges associated with the reservation of dedicated reservations.

## Secondary workspace
{: #secondary-ws}

A secondary workspace is a workspace that a dedicated resource has been shared with.  

This workspace can deploy the virtual server instances (in the case of dedicated hosts) or volumes (in the case of dedicated storage) against the dedicated resources that have been shared with the workspace.  

A secondary workspace cannot further share a resource (that it does not own) with another workspace.

## Reserving a dedicated host
{: #reserv-dh}

To reserve a dedicated host, perform the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select your desired workspace.
3. Click **Dedicated hosts** on the left navigation menu.
        All your existing dedicated host that you have created are shown.
4. Click **Reserve host**.
5. Select the desired **Dedicated host group** from the available list of host group created before.
        Click **Create new** if you have not created a dedicated host before.
6. Enter your **Host name** and select from the available **Machine type**.
        Dedicated hosts cannot be reserved into host groups for which the current workspace has secondary access. You can create multiple dedicated host at once.
        {: note}

## Accessing the dedicated host group details
{: #details-dh}

## Releasing a dedicated host
{: #release-dh}

## Sharing a dedicated host
{: #share-dh}

## Deploying a virtual server in dedicated host
{: #vsi-dh}

## Creating SPP in dedicated host
{: #spp-dh}

## APIs and CLIs
{: #api-cli-dh}

## Maintenace in dedicated host
{: #mainetnance-dh}

