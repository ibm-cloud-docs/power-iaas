---

copyright:
  years: 2022, 2024

lastupdated: "2025-06-03"

keywords: Shared processor pool, SPP, pool placement group, create SPP, SPP PG

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing the shared processor pool
{: #manage-SPP}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

A Shared Processor Pool (SPP) is a pool of processor capacity that is shared between a group of virtual server instances (VM).
{: shortdesc}


In SPP, reserved cores can be adjusted based on availability, unlike a VM with a fixed processing capacity.

The following table shows how an SPP is used to reduce the licensing cost when you pay per core:

|Use of SPP|VM 1|VM 2|Reserved cores in Pool (User defined)|License requirement per core|
|-----|-----------|-----------|-----------|-----------|
|No|Maximum cores = 5  \n Mode = Dedicated|Maximum cores = 6  \n Mode = Dedicated|NA|5+6 = 11|
|Yes|Maximum cores = 5  \n Mode = Shared/Uncapped  \n Entitled capacity = 4.25|Maximum cores = 6  \n Mode = Shared/Uncapped  \n Entitled capacity = 5.25|Maximum cores = 10|10, Determined by the reserved cores in a pool|
{: class="simple-table"}
{: caption="SPP helps to reduce the licensing cost" caption-side="bottom"}

The benefits of using an SPP are as follows:
- Control licensing costs by limiting the number of processors an uncapped partition can use, reducing the number of software licenses.
- A better overall ability to manage processor resources.

{{site.data.keyword.powerSys_notm}} always has at least one defined SPP as the default pool. You can add up to 63 more SPPs to a single {{site.data.keyword.powerSys_notm}} host. A set of VMs that belongs to the same machine type (host) can use and share an SPP.


## Managing the core-to-virtual core ratio
{: #ec-vp-ratio}



[{{site.data.keyword.on-prem}}]{: tag-red}

For {{site.data.keyword.on-prem-fname}}, the minimum core-to-virtual core ratio is 1:20. The minimum Entitled Capacity (EC) must be 0.05 and can be incremented by 0.05.

[{{site.data.keyword.off-prem}}]{: tag-blue}

In a {{site.data.keyword.powerSys_notm}} with Power10, you can provision a VM inside an SPP with Virtual Cores (VC) up to 3.0 cores. For any Entitled Capacity (EC) up to 3.0 cores, you can select the ceiling of cores in VC up to 3.0 cores. For EC more than 3.0, VC is rounded off to the next higher integer value. VC is always equal or greater to EC.

For example, the following table shows how your VC is determined based of EC selection:

| User-defined EC value | Possible VC value |
|-----------------------|-------------------|
| EC is set to 1.5      | VPs can be 2 or 3 |
| EC is set to 2.25     | VP is 3           |
| EC is set to 3.5      | VPs is 4          |
{: caption="Example showing core-to-virtual core ratio" caption-side="top"}

Review the following points when you use core-to-virtual core ratio:
* You can set EC in increments of 0.25.
* You can set VC in increments of 1.
* The ratio can be set only on a user-defined SPP.
* For non-dedicated hosts on Power10, you can set up to 3.0 cores.
* For Power9 and for virtual machines with entitled capacities greater than 2, the core-to-virtual core ratio is 1:1.



You can specify the host affinity and anti-affinity between two or more SPPs with SPP placement groups. For more information, see [Configuring shared processor pool placement group](/docs/power-iaas?topic=power-iaas-manage-SPP#configure-SPP-PG).


## Pricing for Shared Processor Pool
{: #price-spp}

When you use SPPs, you can optimize the cost by using reserved cores that are shared by VMs in the SPP. For more information about the pricing for VMs within SPPs, see the following topics:
- [Pricing for shared processor pool](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud#price-spp) if you are using {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}}
- [Pricing for shared processor pool](/docs/power-iaas?topic=power-iaas-pricing-private-cloud#pricing-spp-private-cloud) if you are using {{site.data.keyword.on-prem-fname}} in {{site.data.keyword.on-prem}}






## Configuring a shared processor pool
{: #configure-spp}

SPP is a separate resource within a {{site.data.keyword.powerSys_notm}} workspace. You can manage the entire SPP lifecycle with the {{site.data.keyword.powerSys_notm}} user interface.

The SPP and your {{site.data.keyword.powerSys_notm}} workspace are linked and thus shared resource pools are not visible from different accounts. You can create one or more SPPs per workspace.

Create an SPP by specifying the following parameters:

* A unique name
* Host group or the machine type
* Number of processors to reserve.

When you define these parameters, a backend process determines the best host for the new SPP.

If the SPP is not configured successfully on the host, the SPP is not allocated with any processing cores. These SPPs must be removed manually, as they are not automatically deleted.
{: note}



### Creating a shared processor pool
{: #create-spp}

To create an SPP, complete the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Create pool**.
3. In the **Create new shared processor pool** window, define the following preferences based on your requirements:

    |Field|Description|
    |----|----|
    |Name|Enter a name that is unique within your cloud account.  \n Use a name of minimum 2 characters and a maximum of 12 characters. Special characters are not allowed except underscore (‘_’).|
     |Add to a pool placement group|Select the checkbox if you want to deploy the SPP directly into an existing pool placement group.  \n If the pool has the required affinity relation with other pools, the best practice is to deploy the pool directly into the placement group. You must create the pool placement group first. It prevents the pool from being deployed on a host that does not satisfy the affinity requirements, and having to move it later.|
    |Select machine type|Specify the machine type. For more information about hardware specifications, see [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}, and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}.|
    |Reserved processing cores[^1]|[{{site.data.keyword.off-prem}}]{: tag-blue} For {{site.data.keyword.powerSys_notm}}, the core-to-virtual core ratio is 1:1 by default.  \n [{{site.data.keyword.on-prem}}]{: tag-red} For {{site.data.keyword.on-prem-fname}}, the minimum core-to-virtual core ratio is 1:20. The minimum entitled capacity must be 0.05 and can be incremented by 0.05.|
     {: caption="Creating a new SPP fields and descriptions" caption-side="bottom"}

    [^1]: The Reserved processing cores are the number of cores that are reserved for processing and must always be a whole number.


4. Click **Create**.

### Updating or deleting a shared processor pool
{: #update-delete-spp}

To update or delete an SPP, navigate to **Compute** > **Shared processor pools**. Then, select the SPP that you want to edit, and click the edit icon. You will receive a notification after the SPP is deleted successfully.

You can update or delete the following details of an existing SPP:

* Name of the SPP: Follow the same naming conventions that you used when you created an SPP. For more information, see [Creating a shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP#create-spp).
* Number of cores: You can update the number of reserved cores based on resource availability and allocation.



* Delete an existing SPP: You can delete any existing SPP. Before you delete, ensure that VMs do not exist in the SPP. If VMs are present in the SPP, delete all VMs in the SPP.




## Managing a VM of a shared processor pool
{: #manage-vm-inside-spp}

When you deploy a VM, you can choose an SPP instead of a host. As you cannot move a VM into or out of an SPP, you can deploy a VM directly into an SPP as a best practice. You can also deploy a VM into a server placement group; the selected SPP host must be compatible with the affinity policy of the placement group that you selected.

When you deploy multiple VMs simultaneously, a new server placement group is created automatically.
{: note}

During any planned maintenance activity or when you want to perform a remote restart operation, ensure that the VMs are linked to an SPP based on your requirements.

### Deploying a VM into a shared processor pool
{: #deploy-pvm-in-spp}

To add VMs to an existing SPP, complete the following steps:

[{{site.data.keyword.on-prem}}]{: tag-red} Use the API and CLI for bulk deployment of VMs in an SPP. However, you cannot provision more than 3 VMs within an SPP in both small and medium pods.
{: important}

1. Open the **Virtual server instances** page in the {{site.data.keyword.powerSys_notm}} user interface.
2. Click **Create instance**.
3. Complete the input fields under the **General** tile based on your requirement.
4. Select the checkbox **Add to a Shared processor pool**.
5. Select an existing SPP.
6. Continue with the process of creating a VM. For more information, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

## Configuring a shared processor pool placement group
{: #configure-SPP-PG}

You can configure an SPP with the SPP placement group (SPP PG) to control the host in which SPPs are deployed.

SPP PGs are different from server placement groups. They serve the same purpose but cannot combine resource types.
{: note}

You must define the following parameters to define an SPP PG:

* A unique name - The SPP PG name must be unique in your cloud instance.
* Policy - You can set the colocation policy of the SPP PG as the same server (affinity) or a different server (anti-affinity).

The following table explains how the host selection is determined based on the different options of SPP PG policy selection:

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|The new SPP is configured on the same host as determined by the existing PG SPP members.|The new SPP is automatically added as a member of the PG policy.|
|Different server (Anti-affinity) |Configure the new SPP on a different host than all host identified by all the existing PG members.|The new SPP is automatically added as a member of the PG policy.|
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-1}
{: tab-title="When SPP PG is non-empty"}

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|A new SPP is configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy|
|Different server (Anti-affinity) |A new SPP is configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-2}
{: tab-title="When SPP PG is empty"}

### Creating a shared processor pool placement group
{: #create-new-pg}

To create an SPP PG, complete the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click the **Pool placement groups** tab.
3. Click **Create group**.
4. In the **Create new pool placement group** window, enter the following details:

    |Field|Description                                             |
    |-----|--------------------------------------------------------|
    |Name |Enter a name that is unique within your cloud account.  \n Use a minimum of 2 characters and a maximum of 12 characters. Special characters are not allowed except underscore (‘_’).|
    |Policy|Same Server (Affinity)  \n Different server (Anti-affinity)|
    {: caption="Create a new SPP PG field description" caption-side="top"}

5. Click **Create**.

You receive a notification when the new SPP PG is created.

### Adding a shared processor pool to a placement group
{: #add-spp-inside-spp-pg}

You can add an SPP as a member to an existing SPP PG if the host of the SPP follows the affinity policy of the group. If the PG policy is set to **Same server** (affinity), all SPPs that are added as a member of the placement group must remain on the same host. If the PG policy is set to **Different server** (anti-affinity), the SPP is deployed on a different host other than all its group members.

To add an SPP to an existing SPP PG, complete the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click the **Pool placement groups** tab.
3. Select an existing pool placement group to which you want to add an SPP.
4. Select one of the following options:

|    Field         |                 Description                           |
|------------------|-------------------------------------------------------|
|Add existing      |You can choose from existing SPPs.     |
|Create new        |You can create an SPP from scratch by defining pool name, machine type, and number of cores. For more information, see [Create a new SPP](/docs/power-iaas?topic=power-iaas-manage-SPP#create-spp)|
{: caption="Add SPP to an SPP PG: field description" caption-side="top"}

You will receive a notification after the new SPP PG is created.

### Deleting a shared processor pool placement group
{: #delete-spp-pg}

To delete an SPP PG, complete the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click the **Pool placement groups** tab.
3. Click the SPP PG that you want to delete.
4. In the details page, click the delete icon.

Deleting a placement group does not delete its members or change the host in which the placement groups are deployed.
{: note}
