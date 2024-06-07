---

copyright:
  years: 2024

lastupdated: "2024-06-07"

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

Dedicated host capability on {{site.data.keyword.powerSysFull}} offers you the exclusive ability to provision an entire server for your exclusive use, expanding your computing options significantly. You can handle mission-critical workloads with complete isolation, control, and security. 

Dedicated host on {{site.data.keyword.powerSys_notm}} is metered by the hour of the entire server. You get an extra flexibility to create virtual server instances and control their placement, along with a unique shared processor pool capability.

This means you can optimize your cloud infrastructure by using single-tenant servers to manage software licensing costs. Most importantly, dedicated hosts increase isolation from other users in a cloud environment, ensuring your operations run smoothly and securely. This level of control and security gives you the confidence and reassurance you need.

<!-- Dedicated hosts are ideal for your environment if you need a high level of customization and control over your cloud infrastructure, while also benefiting from the scalability and cost-effectiveness of cloud computing. -->

Create an estimate for deploying a dedicated host by using the [cost estimator](wwww.cloud.ibm.com/power/estimate){: external} or see the pricing page to learn more about the [pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-for-dedicated-hosts).

The dedicated host provides the following features:
1.  Reserve a host server (IBM Power S922 or S1022) for your exclusive use. All cores and memory on the host are provisioned for your use.
2.  Flexibly create virtual server instances and place them on the dedicated host.  
3.  Create virtual server instances and shared processor pools on the dedicated host and flexibly manage resource utilization including the Virtual Processor (VP) to Entitled Capacity (EC) ratio up to 20:1.
4.  Get a detailed GUI-based view of host capacity information such as core, memory capacity, and consumption. This provides the information on the total, free, or used capacity for your dedicated hosts.
5.  Share the dedicated hosts with all or a subset of your workspaces in the same account. You get an extra flexibility to control access to dedicated hosts across your organization.
6.  Set your own custom names for the dedicated hosts and dedicated host groups.
    
<!-- The Dedicated host capability is currently in limited availability and available in select data centers - `DAL10`, `DAL12`, `WDC06`, and `WDC07`. For general availability, dedicated hosts will be available worldwide and will follow the technology preview.
{: note} -->

## Primary and secondary workspaces
{: #pr-sec-ws-dh}

The {{site.data.keyword.powerSys_notm}} workspaces are differentiated into primary and secondary workspace based on which workspace you use to reserve a dedicated host and share it with other multiple workspaces. See [primary workspace](#primary-ws) and [secondary workspace](#secondary-ws) for more details.

### Primary workspace
{: #primary-ws-dh}

A primary workspace is the owning tenant of a dedicated host or storage reservation and is allowed full control over the associated resources. The primary workspace can remove, delete, or share the dedicated resources that are owned by the workspace under the IBM Cloud account.  

With the same IBM Cloud account, the primary workspace user has the control over sharing the dedicated resources with all (or a subset) of their workspaces (in the same account).  

The primary workspace receives billing charges that are associated with the reservation of dedicated reservations.

### Secondary workspace
{: #secondary-ws-dh}

A secondary workspace is a workspace with which the dedicated resources are shared.  

This workspace can deploy the virtual server instances and volumes against the dedicated resources that are shared with the workspace.  

A secondary workspace cannot further share a resource (that it does not own) with another workspace.

## Access and authorization
{: #access-auth-dh}

You can set up authorization for usage of a dedicated host for other workspaces by using the IBM Cloud IAM Service Authorization capabilities. As an administrator of your organization, you can mark the users with the following supported roles:
|Role           | Description                                                                    |
|---------------|--------------------------------------------------------------------------------|
| Reader        | View the workspaces that a dedicated host is shared with.        |
| Manager       | Reserve and delete dedicated hosts, share, and unshare with other workspaces, any other crud (create, read, update, delete) actions possible with dedicated hosts    |
{: caption="Table 1. Roles and permissions in dedicated host" caption-side="bottom"}

## Creating a dedicated host group
{: #create-group-dh}

A dedicated host group in your IBM Cloud account is where all your reserved dedicated hosts are contained. The workspace from where you initiate the creation of a new dedicated host group becomes the primary workspace. You can select the active workspaces in your IBM Cloud account to share making them as secondary workspaces. 

To create a dedicated host group, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.
        You can see all the existing dedicated hosts.
4. Click **Reserve host**.
5. Click **Create new**
6. Enter your custom **Dedicated host group name**.
7. Share this dedicated host group among other workspaces by providing the available workspaces with a secondary access.
        The workspaces that are in the same region as the primary workspace and are in an active state can be selected.
        {: note}

8. Click **Save**. 

You can click a dedicated host group to access the host group details. Further, you can create more dedicated host, share, or unshare workspaces with secondary access.
{: important}

### Sharing or unsharing dedicated host groups among workspaces
{: #share-dh}

You can choose to grant workspaces with secondary access when [creating a dedicated host group](#create-group-dh) and from the dedicated host group details page. You can stop sharing them from the dedicated host group details page.

To share workspaces, perform the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.
        You can see all the existing dedicated hosts.
4. Click a dedicated host group to open the details page.
5. Click **Share** and select the workspaces that you want to share. 
        The workspaces that are in the same region as the primary workspace and are in an active state can be selected.
        {: note}

6. Click **Save**.

You can **Stop sharing** the workspaces with secondary access to the host group from the dedicated host group details page. Make sure that the workspaces do not have any provisioned resources on the dedicated host.

## Reserving a dedicated host
{: #reserv-dh}

You can create multiple dedicated hosts. To reserve a dedicated host, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.
        All your existing dedicated hosts that you have created are shown.
4. Click **Reserve host**.
5. Select the **Dedicated host group** from the available list of host groups already created.
        Click **Create new** if when no dedicated host available.
6. Enter your **Host name** and select from the available **Machine type**.
        Dedicated hosts cannot be reserved into host groups for which the current workspace has secondary access.
        {: note}

7. Click **Finish** and view the summary of estimated cost.
8. Click **Create**.

You can select a dedicated host to access the host details. Further, you can create and manage virtual server instances, create a shared processor pool, or release the dedicated host.
{: important}

### Deploying a virtual server in a dedicated host
{: #vsi-dh}

You can create a virtual server instance in a single-tenant environment on a dedicated host. The virtual server instance that is provisioned on a dedicated host can be deployed with any value up to a 20:1 ratio of Virtual Processor (VP) to Entitled Capacity (EC).  

Open the dedicated host details page, and click **Create instance** to open the **Create virtual server instance** page. You must toggle "ON" to the **Deploy to dedicated host** button.  

Follow the instructions in [Configuring a Power Virtual Server instance](docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) page for detailed instructions.

When you use dedicated hosts, the virtual server instances that are deployed on them are not billed for core and memory charges.

### Creating SPP in a dedicated host
{: #spp-dh}

You can create a shared processor pool (SPP) in a single-tenant environment on a dedicated host. The SPPs provisioned on a dedicated host can be deployed with any value up to a 20:1 ratio of Virtual Processor (VP) to Entitled Capacity (EC).  

Open the dedicated host details page, and click **Create pool** to open the **Create new shared processor pool** page.  

Follow the instructions in the [Managing shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP) page for detailed instructions.

When you use dedicated host to deploy the SPPs, the SPPs are not billed for the reserved capacity.

## Releasing a dedicated host
{: #release-dh}

You can release a dedicated host when no resources are deployed on the host. To release a dedicated host, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.
        You can see all the existing dedicated hosts.
4. Select the dedicated host that you want to release.
        You must remove all the associated resources that are provisioned on the host before releasing the host.
        {: note}

5. Click **Release host**.
        When you are releasing the last dedicated host on a dedicated host group, you get the option to **Release host and delete host group**.
        {: important}

<!-- ## API and CLI support
{: #api-cli-dh}

Do we need to list any phase 1 APIs & CLIs?

## Supporting operating systems
{: #os-support-dh}

The following operating systems are supported for dedicated host:
- 

## Maintenance in dedicated host
{: #mainetnance-dh} -->
