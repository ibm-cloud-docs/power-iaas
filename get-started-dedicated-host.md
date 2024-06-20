---

copyright:
  years: 2024

lastupdated: "2024-06-20"

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

The hourly billing for a Dedicated host on a Power Virtual Server covers the entire server. Using a dedicated host provides extra flexibility to create virtual server instances and control their placement, along with a unique shared processor pool capability. This means you can optimize your cloud infrastructure by using single-tenant servers to manage software licensing costs. Most importantly, dedicated hosts increase isolation from other users in a cloud environment, ensuring your operations run smoothly and securely.



Create an estimate before deploying a dedicated host by using the [cost estimator](wwww.cloud.ibm.com/power/estimate){: external} or see the [pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#pricing-dh) page to learn more.

Dedicated hosts provide the following features:
1. Ability to reserve a server (IBM Power S922 or S1022) for exclusive use. 
2. Flexibility to provision virtual server instances onto a dedicated host.
3. Flexibility to manage resource utilization, including an increased Virtual Processor to Entitled Capacity ratio of up to 20:1. 
4. Detailed user interface view of host capacity information such as: core, memory capacity, and consumption. 
5. Ability to share dedicated hosts with all or a subset of workspaces on the same account, and the flexibility to control access to dedicated hosts across your organization. 
6. Ability to set custom names for dedicated hosts and dedicated host groups. 
    


## Primary and secondary workspaces
{: #pr-sec-ws-dh}

{{site.data.keyword.powerSys_notm}} workspaces are differentiated into primary and secondary workspaces. This differentiation is determined by whether a workspace was used to reserve the dedicated host (primary) or if the workspace was given access to the dedicated host (secondary). See [primary workspace](#primary-ws-dh) and [secondary workspace](#secondary-ws-dh) for more details.

### Primary workspace
{: #primary-ws-dh}

A primary workspace is the owning tenant of a dedicated host with full control over the associated resources. The primary workspace can remove, delete, or share the dedicated resources that are owned by the workspace under the IBM Cloud account.  

Primary workspace users can control sharing permissions for dedicated resources with all (or a subset) or their workspaces that are located in the same account. 

Billing for dedicated hosts is charged to the primary workspace.

### Secondary workspace
{: #secondary-ws-dh}

A secondary workspace is a workspace with which the dedicated resources are shared.  

This workspace can deploy the virtual server instances on the dedicated resources that are shared with the workspace.  

A secondary workspace cannot further share a resource (that it does not own) with another workspace.

## Access and authorization
{: #access-auth-dh}

You can set up authorization for usage of a dedicated host for other workspaces by using the IBM Cloud IAM Service Authorization capabilities. As an administrator of your organization, you can mark users with the following supported roles:
|Role           | Description                                                                    |
|---------------|--------------------------------------------------------------------------------|
| Reader        | View the workspaces that a dedicated host is shared with.        |
| Manager       | Reserve and delete dedicated hosts, share, and unshare with other workspaces, any other crud (create, read, update, delete) actions possible with dedicated hosts    |
{: caption="Table 1. Roles and permissions in dedicated host" caption-side="bottom"}

## Creating a dedicated host group
{: #create-group-dh}

A dedicated host group in your IBM Cloud account is where all your reserved dedicated hosts are contained. The workspace from where you initiate the creation of a new dedicated host group becomes the primary workspace. You can select active workspaces in your IBM Cloud account to share making them as secondary workspaces. 

To create a dedicated host group, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.  
        Here, you can see all existing dedicated hosts.
4. Click **Reserve host**.
5. Click **Create new**.
6. Enter your custom **Dedicated host group name**.
7. Share this dedicated host group among other workspaces by providing the available workspaces with a secondary access.  

        Workspaces that are in the same region as the primary workspace and are in an active state can be selected.
        {: note}

8. Click **Save**. 

You can click into a dedicated host group to access its details, create more dedicated hosts, share, or stop sharing with secondary workspaces.
{: important}

### Sharing or unsharing dedicated host groups among workspaces
{: #share-dh}

You can choose to grant workspaces with secondary access when [creating a dedicated host group](#create-group-dh) and from the dedicated host group details page. You can stop sharing them from the dedicated host group details page.

To share workspaces, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.  
        Here, you can see all existing dedicated hosts.
4. Click a dedicated host group to open the details page.
5. Click **Share** and select the workspaces that you want to share.  

        Workspaces that are in the same region as the primary workspace and are in an active state can be selected.
        {: note}

6. Click **Save**.

To stop sharing dedicated host access with a secondary workspace, ensure that the selected workspace does not have any provisioned resources on the dedicated host.

## Reserving a dedicated host
{: #reserv-dh}

You can create multiple dedicated hosts. To reserve a dedicated host, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.  
        Here, you can see all existing dedicated hosts.
4. Click **Reserve host**.
5. Select the **Dedicated host group** from the available list of host groups already created.
        Click **Create new** when no dedicated host is available.
6. Enter your **Host name** and select **Machine type** from the drop-down list.    

        Dedicated hosts cannot be reserved into host groups in which the current workspace has secondary access.
        {: note}

7. Click **Finish** and view the summary of estimated cost.
8. Click **Create**.

You can click into a dedicated host to access its details, create and manage virtual server instances, created shared processor pools, or release the host.
{: important}

### Deploying a virtual server in a dedicated host
{: #vsi-dh}

You can create a virtual server instance in a single-tenant environment on a dedicated host. The virtual server instance that is provisioned on a dedicated host can be deployed with any value up to a 20:1 ratio of Virtual Processor (VP) to Entitled Capacity (EC).  

Click into a dedicated host to create a new virtual server instance. You must toggle "ON" the **Deploy to dedicated host** button.  

Follow the instructions in [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) page for detailed instructions.

The virtual server instances that are deployed on the dedicated host are not billed for core and memory charges.

### Creating SPP in a dedicated host
{: #spp-dh}

You can create a shared processor pool (SPP) in a single-tenant environment on a dedicated host. The SPPs provisioned on a dedicated host can be deployed with any value up to a 20:1 ratio of Virtual Processor (VP) to Entitled Capacity (EC).  

Click into a dedicated host to create a new shared processor pool.

Follow the instructions in the [Managing shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP) page for detailed instructions.

When you use dedicated host to deploy the SPPs, the SPPs are not billed for the reserved capacity.

## Releasing a dedicated host
{: #release-dh}

You can release a dedicated host when no resources are deployed on the host. To release a dedicated host, complete the following steps:
1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu.  
        Here, you can see all existing dedicated hosts.
4. Select the dedicated host that you want to release.  

        You must remove all the associated resources that are provisioned on the host before releasing the host.
        {: note}

5. Click **Release host**.  
        When releasing the last dedicated host on a dedicated host group, the dedicated host group will also be deleted. 

        You cannot have empty dedicated host groups on a workspace.
        {: note}



## Maintenance in dedicated host
{: #mainetnance-dh}

When IBM needs to do maintenance on a dedicated host, the VMs are evacuated to another dedicated host specifically for the maintenance operation window. You are not able to see anything unless a host failure that needs the replacement of the original dedicated host.

If a dedicated host suffers from a failure, IBM restarts the VMs on another dedicated host.

When VMs are relocated to another dedicated host for maintenance, you are not charged for an extra dedicated host.
{: note}
