---

copyright:
  years: 2022, 2024

lastupdated: "2024-06-12"

keywords: Shared processor pool, SPP, pool placement group, create SPP, SPP PG

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Managing the shared processor pool
{: #manage-SPP}

A shared processor Pool (SPP) is a pool of processor capacity that is shared between a group of virtual server instances.
{: shortdesc}

Unlike a virtual server instance that has a dedicated and defined maximum amount of processing capacity, you can set the reserved cores in SPP that is available at the pool level.

The following table shows how an SPP is used to reduce the licensing cost when you pay per core:
|Use of SPP|VM 1|VM 2|Reserved cores in Pool (User defined)|License requirement per core|
|-----|-----------|-----------|-----------|-----------|
|No|Maximum cores = 5 \n Mode = Dedicated|Maximum cores = 6 \n Mode = Dedicated|NA|5+6 = 11|
|Yes|Maximum cores = 5 \n Mode = Shared/Uncapped \n Entitled capacity = 4.25|Maximum cores = 6 \n Mode = Shared/Uncapped \n Entitled capacity = 5.25|Maximum cores = 10|10, Determined by reserved cores in pool|
{: class="simple-table"}
{: caption="Table 1. SPP helps to reduce the licensing cost" caption-side="bottom"}

The benefits of using an SPP are as follows:

* Get control over licensing costs by limiting the number of processors an uncapped partition can use, which reduces the number of software licenses.
* Get a better overall ability to manage processor resources.

The {{site.data.keyword.powerSys_notm}} always has at least one defined SPP as the default pool. You can add up to 63 more SPPs to a single {{site.data.keyword.powerSys_notm}} host. The SPP is used and shared by a set of virtual server instances of the same machine type (host).




[On-premises]{: tag-red}

For IBM {{site.data.keyword.powerSys_notm}} Private Cloud, the minimum core-to-virtual core ratio is 1:20. The minimum entitled capacity must be 0.05 and can be incremented by 0.05.

[Off-premises]{: tag-blue}

In a {{site.data.keyword.powerSys_notm}} user-defined SPP, you can set the core-to-virtual core ratio to 1:3. Using the 1:3 ratio, you can deploy Oracle licensing use cases without purchasing a dedicated host. Note the following limitations when your use core-to-virtual core ratio:

* You can set the ratio only on a user-defined SPP.
* For non-dedicated hosts on Power10, you can increase the limit of core-to-virtual core ratio to 1:3 for entitled capacities less than or equal to 2.
* For Power9 and for virtual machines with entitled capacities greater than 2, the core-to-virtual core ratio is 1:1.



You can specify the host affinity and anti-affinity between two or more SPPs with shared processor pool placement groups. For more information, see [Configuring shared processor pool placement group](/docs/power-iaas?topic=power-iaas-manage-SPP#configure-SPP-PG).

## Pricing for shared processor pool
{: #price-spp}

When you use SPP, you pay for the following items:

* SPP reserved cores that use the shared capped part number.
* Virtual server instance cores that are deployed into the SPP that use shared uncapped part number.

The SPP helps you to manage CPU cores only. Pricing for memory and storage remains the same as earlier. The total estimated cost page does not show the SPP reserved cores-related costs because of service-level estimator limitations. For more information about pricing for SPP in IBM {{site.data.keyword.powerSys_notm}}, see [Pricing for {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud). For more information about pricing for SPP in IBM {{site.data.keyword.powerSys_notm}} Private Cloud, see [FAQ on pricing](/docs/power-iaas?topic=power-iaas-pricing-private-cloud#faq).
{: note}

## Configuring a shared processor pool
{: #configure-spp}

SPP is a separate resource within a {{site.data.keyword.powerSys_notm}} workspace. You can manage the entire SPP lifecycle with the {{site.data.keyword.powerSys_notm}} user interface.

The SPP and your {{site.data.keyword.powerSys_notm}} workspace are linked and thus shared resource pools are not visible from different accounts. You can create one or more SPPs per workspace.

Create an SPP by specifying the following parameters:

* A unique name
* Host group or the machine type
* Number of processors to reserve.

When you define these parameters, a backend process determines the best host for the new SPP.

When the SPP you create is not configured successfully on the host, the SPP will not have any allocated processing cores. Delete such SPPs manually as they do not get cleaned up automatically.
{: note}

### Creating a shared processor pool
{: #create-spp}

To create an SPP, complete the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Create pool**.
3. In the **Create new shared processor pool** window, define the following preferences based on your requirements:
    |Field|Description|
    |----|----|
    |Name|Enter a name that is unique within your cloud account.\n Use a name of minimum 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and underscore (‘_’) is only allowed as a special character.|
     |Add to a pool placement group|Select the checkbox if you want to deploy the SPP directly into an existing pool placement group. \n If the pool has the required affinity relation with other pools, the best practice is to deploy the pool directly into the placement group. You must create the pool placement group first. It prevents the pool from being deployed on a host that does not satisfy the affinity requirements, and having to move it later.|
    |Select machine type|Specify the machine type. For more information about hardware specifications, see [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}, and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}.|
    |Reserved processing cores[^1]|[Off-premises]{: tag-blue} For {{site.data.keyword.powerSys_notm}}, the core-to-virtual core ratio is 1:1 by default. \n [On-premises]{: tag-red} For IBM {{site.data.keyword.powerSys_notm}} Private Cloud, the minimum core-to-virtual core ratio is 1:20. The minimum entitled capacity must be 0.05 and can be incremented by 0.05.|
     {: caption="Table 2. Creating a new SPP fields and descriptions" caption-side="bottom"}

    [^1]: The Reserved processing cores are the number of cores that are reserved for processing and must always be a whole number.


1. Click **Create**.

### Updating or deleting a shared processor pool
{: #update-delete-spp}

To update or delete an SPP, navigate to **Compute** > **Shared processor pools**. Then, select the SPP that you want to edit, and click the edit icon. You will receive a notification after the SPP is deleted successfully.

You can update or delete the following details of an existing SPP:

* Name of the SPP - Follow the same naming conventions that you used while creating an SPP. For more information, see [Creating a shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP#create-spp).
* Number of cores - You can update the number of reserved cores based on resource availability and allocation.
* Delete an existing SPP - You can delete any existing SPP. Before deleting, ensure that no virtual server instances exist in the SPP. If virtual server instances are present, it must be deleted or moved with a support ticket.

## Managing a virtual server instance of a shared processor pool
{: #manage-vm-inside-spp}

When you deploy a virtual server instance, you can choose an SPP instead of a host. As you cannot move a virtual server instance into or out of an SPP, you can deploy a virtual server instance directly into an SPP as a best practice. You can also deploy a virtual server instance into a server placement group; the selected SPP host must be compatible with the affinity policy of the placement group that you selected.

When you deploy multiple virtual server instances simultaneously, a new server placement group is created automatically.
{: note}

During any planned maintenance activity or when you want to perform a remote restart operation, ensure that the virtual server instances are linked to an SPP based on your requirements.

### Deploying a virtual server instance into a shared processor pool
{: #deploy-pvm-in-spp}

To add virtual server instances to an existing SPP, complete the following steps:

1. Open the **Virtual server instances** page in the {{site.data.keyword.powerSys_notm}} user interface.
2. Click **Create instance**.
3. Complete the input fields under the **General** tile based on your requirement.
4. Select the checkbox **Add to a Shared processor pool**.
5. Select an existing shared processor pool.
6. Continue with the process of creating a virtual server instance. For more information, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

## Configuring a shared processor pool placement group
{: #configure-SPP-PG}

You can configure an SPP with the shared processor pool placement group (SPP PG) to control the host in which SPPs are deployed.

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
{: caption="Table 3. Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-1}
{: tab-title="When SPP PG is non-empty"}

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|A new SPP is configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy|
|Different server (Anti-affinity) |A new SPP is configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Table 3. Host selection when SPP PG is empty and non-empty" caption-side="top"}
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
    |Name |Enter a name that is unique within your cloud account. \n Use a minimum of 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and underscore (‘_’) is only allowed as a special character.|
    |Policy|Same Server (Affinity) \n Different server (Anti-affinity)|
    {: caption="Table 4. Create a new SPP PG field description" caption-side="top"}

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
{: caption="Table 5. Add SPP to an SPP PG: field description" caption-side="top"}

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
