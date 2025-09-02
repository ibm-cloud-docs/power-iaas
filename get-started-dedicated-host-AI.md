---

copyright:
  years: 2024, 2025

lastupdated: "2025-09-02"

keywords: dedicated host, primary workspace, secondary workspace

subcollection: power-iaas

---


{{site.data.keyword.attribute-definition-list}}


# Getting started with dedicated hosts on {{site.data.keyword.off-prem-fname}}
{: #dedicated-host}

A dedicated host on {{site.data.keyword.powerSysFull}} in {{site.data.keyword.off-prem}} is a virtualized, single-tenant, dedicated server. It provides you with maximum control over workload placement and flexible post-provisioning options. Dedicated server hosting from {{site.data.keyword.powerSys_notm}} is designed to provide total isolation, control and security for your heavy, mission-critical workloads.
{: shortdesc}

Using the dedicated host capability on {{site.data.keyword.powerSys_notm}} in {{site.data.keyword.off-prem}} you can provision an entire server for your sole use, significantly expanding your computing options. You can handle mission-critical workloads with complete isolation, control, and security.

Using a dedicated host provides extra flexibility in two ways:
- It allows you to create virtual server instances and control their placement, and
- It offers a unique shared processor pool capability.

A dedicated host on a {{site.data.keyword.powerSys_notm}} enables you to optimize your cloud infrastructure by using single-tenant servers to manage software licensing costs. Most importantly, dedicated hosts enhance isolation from other users in a cloud environment, ensuring your operations run smoothly and securely.

Dedicated hosts on a {{site.data.keyword.powerSys_notm}} provide the following features:
- Ability to reserve a compatible server for exclusive use.
- Flexibility to provision virtual server instances onto a dedicated host.
- Flexibility to manage resource utilization, including an increased Virtual Processor to Entitled Capacity ratio of up to 20:1.
- Detailed user interface view of host capacity information such as: core, memory capacity, and consumption.
- Ability to share dedicated hosts with all or a subset of workspaces on the same account, and the flexibility to control access to dedicated hosts across your organization.
- Ability to set custom names for dedicated hosts and dedicated host groups.

## Pricing for dedicated hosts on {{site.data.keyword.powerSys_notm}}
{: #pricing-dedicated}

The hourly billing for a dedicated host on a Power Virtual Server covers the entire server.

You can create a cost estimate of a dedicated host before you deploy it by using the [cost estimator](https://cloud.ibm.com/power/estimate){: external} or see the [pricing](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#pricing-dh) page to learn more.




## Primary workspace in a {{site.data.keyword.powerSys_notm}} for a dedicated host
{: #primary-ws-dh}

A {{site.data.keyword.powerSys_notm}} primary workspace is the owning tenant of a dedicated host with full control over the associated resources.
{: shortdesc}

A primary workspace can delete or share the dedicated resources that it owns under the IBM Cloud account. Primary workspace users can control sharing permissions for dedicated resources with all or a subset of their workspaces within the same account. You can use a primary workspace to reserve a dedicated host.

Billing for dedicated hosts is charged to the primary workspace.

## Secondary workspace in a {{site.data.keyword.powerSys_notm}} for a dedicated host
{: #secondary-ws-dh}

A {{site.data.keyword.powerSys_notm}} secondary workspace is the one with which the dedicated resources are shared.
{: shortdesc}

A secondary workspace can deploy virtual server instances on the shared dedicated resources. You can use a secondary workspace to grant access to the resources in the dedicated host. However, a secondary workspace cannot further share a resource that it doesn't own with another workspace.

## Access and authorization for dedicated hosts on {{site.data.keyword.powerSys_notm}}
{: #access-auth-dh}

You can set up authorization for usage of a {{site.data.keyword.powerSys_notm}} dedicated host for other workspaces by using IBM Cloud IAM Service Authorization capabilities.
{: shortdesc}

As an administrator of your organization, you can assign users the following supported roles:

|Role           | Description                                                                    |
|---------------|--------------------------------------------------------------------------------|
| Reader        | View the workspaces that a dedicated host is shared with.        |
| Manager       | Perform create, read, update, or delete actions on dedicated hosts, including:  \n - Reserve and delete dedicated hosts  \n - Share and unshare with other workspaces  \n - Manage any other aspects of dedicated hosts.    |
{: caption="Roles and permissions in a dedicated host on a {{site.data.keyword.powerSys_notm}}" caption-side="bottom"}

## Deploying a dedicated host to a workspace
{: #create-dh}

To deploy a dedicated host to your workspace, select the server (IBM Power S922 or S1022) and contact the IBM support team. You can create an estimate before you deploy a dedicated host by using the [cost estimator](https://cloud.ibm.com/power/estimate){: external}.
{: shortdesc}




## Creating a dedicated host group on {{site.data.keyword.powerSys_notm}}
{: #create-group-dh}


A dedicated host group in your IBM Cloud account is where all your reserved dedicated hosts are contained.
{: shortdesc}

The workspace from where you initiate the creation of a new dedicated host group becomes the primary workspace. You can select active workspaces in your IBM Cloud account to share making them as secondary workspaces.

To create a dedicated host group, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Select a workspace.

3. Click **Dedicated hosts** on the left navigation menu. Here, you can see all the existing dedicated hosts.

4. Click **Reserve host**.

5. Click **Create new**.

6. Enter a custom name on the **Dedicated host group name** field.

7. (Optional) Grant secondary access to the workspaces to share the dedicated host group.

    Only workspaces in the same region as the primary workspace and in an active state can be selected.
    {: note}

8. Click **Save**.

You can click a dedicated host group to access its details, create more dedicated hosts, share, or stop sharing with secondary workspaces.
{: important}

### Sharing or unsharing dedicated host groups among workspaces
{: #share-dh}

You can choose to grant workspaces with secondary access when [creating a dedicated host group](#create-group-dh) and from the dedicated host group details page. You can stop sharing them from the dedicated host group details page.

To share workspaces, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Select a workspace.

3. Click **Dedicated hosts** on the left navigation menu. Here, you can see all existing dedicated hosts.

4. Click a dedicated host group to open the details page.

5. Click **Share** and select the workspaces that you want to share with.

    Only workspaces in the same region as the primary workspace and in an active state can be selected.
    {: note}

6. Click **Save**.

To stop sharing dedicated host access with a secondary workspace, ensure that the selected workspace does not have any provisioned resources on the dedicated host.

## Reserving a dedicated host on {{site.data.keyword.powerSys_notm}}
{: #reserv-dh}

You can allocate an entire dedicated host exclusively to a single tenant by reserving the host.
{: shortdesc}


To reserve a dedicated host, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.

2. Select a workspace.

3. Click **Dedicated hosts** on the left navigation menu. Here, you can see all existing dedicated hosts.

4. Click **Reserve host**.

5. Select a dedicated host group from the available list of host groups already created.

6. Click **Create new** if no dedicated host group is available.

7. Enter your **Host name** and select the **Machine type** from the drop-down list.

    Dedicated hosts cannot be reserved in host groups where the current workspace has secondary access.
    {: note}

8. Click **Finish** and view the summary of estimated cost.

9.  Click **Create**.

You can click into a dedicated host to access its details, create and manage virtual server instances, created shared processor pools, or release the host.
{: important}

## Deploying a virtual server in a dedicated host on {{site.data.keyword.powerSys_notm}}
{: #vsi-dh}

You can create a virtual server instance in a single-tenant environment on a dedicated host. The virtual server instance that is provisioned on a dedicated host can be deployed with any value up to a 20:1 ratio of Virtual Processor (VP) to Entitled Capacity (EC).

To deploy a virtual server in a dedicated host, complete the following steps:

1. Click a dedicated host to create a new virtual server instance.
2. Set **Deploy to dedicated host** to ON.
3. Follow the instructions in [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) page for detailed instructions.

Virtual server instances that are deployed on the dedicated host are not billed for core and memory charges.
{: note}

## Creating SPP in a dedicated host on {{site.data.keyword.powerSys_notm}}
{: #spp-dh}

A shared processor pool (SPP) is a pool of processor capacity that is shared between a group of virtual server instances (VM). You can create an SPP in a single-tenant environment on a {{site.data.keyword.powerSys_notm}} dedicated host. The SPPs provisioned on a dedicated host can be deployed with any value up to a 20:1 ratio of Virtual Processor (VP) to Entitled Capacity (EC).
{: shortdesc}

To create an SPP in a dedicated host, complete the following steps:

1. Click a dedicated host to create a new shared processor pool.
2. Set **Deploy to dedicated host** to ON. 
3. Follow the instructions in the [Managing shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP) page for detailed instructions.

When you use a dedicated host to deploy SPPs, the SPPs are not billed for the reserved capacity.
{: note}

## Releasing a dedicated host from {{site.data.keyword.powerSys_notm}}
{: #release-dh}

To release a dedicated host is to delete it from your account. You must delete all the associated resources that are provisioned on the host before you release it.
{: shortdesc}


You can release a dedicated host when no resources are deployed on the host.


To release a dedicated host, complete the following steps:

1. Open the {{site.data.keyword.powerSys_notm}} user interface in [IBM Cloud](https://cloud.ibm.com/power/overview){: external}.
2. Select a workspace.
3. Click **Dedicated hosts** on the left navigation menu. Here, you can see all existing dedicated hosts.
4. Select the dedicated host that you want to release. You must remove all associated resources that are provisioned on the host before you release it.
5. Click **Release host**.

     When you release the last dedicated host in a dedicated host group, the group will also be deleted. Empty dedicated host groups are not allowed on a workspace.
     {: note}

## Maintenance in dedicated host
{: #mainetnance-dh}





When IBM needs to perform maintenance on a dedicated host, its virtual server instances (VMs) are live migrated to another dedicated host during the maintenance operation window.

If a dedicated host suffers from a server failure, IBM restarts its VMs on another dedicated host (pending capacity availability). The VM restart capability does not protect against data center, storage, or network-related failures; in such scenarios, the appropriate business continuity procedures (high availability and disaster recovery) should be invoked.




When VMs are relocated to another dedicated host for maintenance, you are not charged for an extra dedicated host.
{: note}




## Using the virtual host identifier for dedicated hosts on {{site.data.keyword.powerSys_notm}}
{: #virtual-host-ID}

You can use the virtual host identifier (ID) to get information about your {{site.data.keyword.powerSys_notm}} dedicated hosts. The virtual host ID follows a standard format to uniquely identify other {{site.data.keyword.powerSys_notm}} resources.
{: shortdesc}

The {{site.data.keyword.powerSys_notm}} dedicated host identifier format is updated to use the virtual host ID format. If you are using dedicated hosts and depend on specific resource identifiers such as API and CLI calls, you must update the logic to use the virtual host ID format. Otherwise, the logic might fail.
{: important}

To map a dedicated host with VMs or SPP resources, you must use the values of the `host` attribute of the VM or the `hostID` attribute of the SPP in the `hostReference` attribute of the dedicated host.

To fetch the virtual host ID of a dedicated host, use the following API or CLI commands:

* API command &ndash; [get the list of all hosts](https://cloud.ibm.com/apidocs/power-cloud#v1-hosts-get) with the `?host_reference=true` query parameter.
* CLI command &ndash; [get the host information](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-host-get){: external} with the `--json` option.

The following code examples provide the old format and new format of the virtual host ID after the format is updated to the standard format:

**Example 1: /v1/hosts/{host_id} format**

**Old format**


```code
[
     {
          "capacity": {
               "cores": {
                         "available": 14.75,
                         "reserved": 5.25,
                         "total": 20,
                         "used": 0
          },
          "memory": {
                         "available": 930.83,
                         "reserved": 93.17,
                         "total": 1024,
                         "used": 0
               }
        },
          "displayName": "myHost3",
          "hostGroup": {
               "access": "primary",
               "href": "/v1/host-groups/b1d71c2c-54fd-49d7-b061-44b663106fec",
               "name": "Fred_HG"
        },
        "id":123,
        "state": "up",
        "status": "enabled",
        "sysType": "s922"
     }
]
```

**New format**


```code
[
     {
          "capacity": {
               "cores": {
                    "available": 14.75,
                    "reserved": 5.25,
                    "total": 20,
                    "used": 0
               },
               "memory": {
                    "available": 930.83,
                    "reserved": 93.17,
                    "total": 1024,
                    "used": 0
               }
          },
          "displayName": "myHost3",
          "hostGroup": {
               "access": "primary",
               "href": "/v1/host-groups/b1d71c2c-54fd-49d7-b061-44b663106fec",
               "name": "Fred_HG"
          },
          "id": d750956e-e22c-4e4d-b0d1-a126c16d1cd0,
          "state": "up",
          "status": "enabled",
          "sysType": "s922"
     }
]
```





**Example 2: /v1/host-groups/{host_group_id} format**

**Old format**


```code
[
     {
        "creationDate": "2024-11-12T16:29:35.000Z",
        "hosts": [
                    "/v1/hosts/123"
        ],
        "id": "d50dd63a-dfda-46a9-854f-e05f461f24ad",
        "name": "nonCrnEnabledHG",
        "primary": "85e6515b-9137-487f-9155-b96aee04b089",
        "secondaries": []
     }
]
```


**New format**


```code
[
     {
        "creationDate": "2024-11-12T16:29:35.000Z",
        "hosts": [
                     "/v1/hosts/d750956e-e22c-4e4d-b0d1-a126c16d1cd0"
        ],
        "id": "d50dd63a-dfda-46a9-854f-e05f461f24ad",
        "name": "nonCrnEnabledHG",
        "primary": "85e6515b-9137-487f-9155-b96aee04b089",
        "secondaries": []
     }
]
```
