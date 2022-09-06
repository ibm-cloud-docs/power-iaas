---

copyright:
  years: 2022

lastupdated: "2022-09-06"

keywords: Shared processor pool, SPP, pool placement group, create SPP, SPP PG, 

subcollection: power-iaas

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:preview: .preview}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Managing Shared processor pool

{: #manage-SPP}

A Shared processor Pool (SPP) is a pool of processor capacity that is shared between a group of virtual server instances. Unlike a virtual server instance that has a dedicated and defined maximum amount of processing capacity, you can set the reserved cores in SPP that are guaranteed to be available at the pool level.

{: shortdesc}

The following table shows how an SPP is used to reduce the licensing cost when you pay per core:
|Use of SPP|VM 1|VM 2|Reserved cores in Pool (User defined)|License requirement per core|
|-----|-----------|-----------|-----------|-----------|
|No|Maximum cores = 5 \n Mode = Uncapped \n Entitled capacity = 1|Maximum cores = 6 \n Mode = Uncapped \n Entitled capacity = 1|NA|5+6 = 11|
|Yes|Maximum cores = 5|Maximum cores = 6|Maximum cores = 6|Determined by reserved cores in pool = 6|
{: class="simple-table"}
{: caption="Table 1. SPP helps to reduce the licensing cost" caption-side="bottom"}

The benefits of using an SPP are as follows:

* Provides control over licensing costs by limiting the number of processors an uncapped partition can use, which reduces the number of software licenses.
* Provides a better overall ability to manage processor resources.

The {{site.data.keyword.powerSys_notm}} always has at least one defined SPP as the default pool. You can add up to 63 more SPPs in a single {{site.data.keyword.powerSys_notm}} workspace. The SPP is used and shared by a set of virtual server instances of the same machine type (host).

You can specify the host affinity and anti-affinity between two or more SPPs with Shared processor pool placement groups. For more information, see [Configuring Shared processor pool placement group](/docs/power-iaas?topic=power-iaas-managing-shared-processor-pool#configuring-shared-processor-pool-placement-group).

## Pricing for Shared processor pool

{:price-spp}

When you use SPP, you pay for the following items:

* SPP reserved cores that use the shared capped part number.
* Virtual server instance cores that are deployed into the SPP that use shared uncapped part number.

The SPP helps manage CPU cores only. Pricing for memory and storage remains the same as earlier. The total estimated cost page does not show that SPP reserved cores-related costs because of service-level estimator limitations. For more information about pricing, see [Pricing for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-pricing-virtual-server).
{: note}

## Configuring Shared processor pool

{: configure-spp}

SPP is a separate resource within a {{site.data.keyword.powerSys_notm}} workspace. You can manage the entire SPP lifecycle with the {{site.data.keyword.powerSys_notm}} user interface.

The SPP and your {{site.data.keyword.powerSys_notm}} workspace are linked and thus shared resource pools are not visible from different accounts. You can create one or more SPPs per workspace.

You can specify the full name and size of the SPP and choose the host type to deploy the SPP. Create an SPP by specifying the following parameters:

* A unique name
* Host group or the machine type
* Number of processors to reserve.

When you define the three parameters, a backend processing determines the best host for the new SPP.

### Create a Shared processor pool

{: create-spp}

Create an SPP with the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Create pool**.
3. In the **Create new Shared processor pool** window, define the following preferences based on your requirements:
  |Field|Description|
  |----|----|
  |Name|Enter a name that is unique within your cloud account.\n Use a name of minimum 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and underscore (‘_’) is only allowed as a special character.|
  |Add to a pool placement group|Select the checkbox if you want to deploy the SPP directly into an existing pool placement group. \n If the pool have required affinity relations to other pools, the best practice is to deploy the pool directly into the placement group. You must create the pool placement group first. It prevents the pool from being deployed on a host that does not satisfy the affinity requirements, and having to move it later.|
  |Select machine type|Specify the machine type. For more information about hardware specifications, see [E880 (Dallas only)](https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en){: external}, [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}, and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}.|
  |Reserved processing cores|There is a core-to-vCPU ratio of 1:1 by default. |
  {: caption="Table 2. Creating a new SPP fields and descriptions" caption-side="bottom"}

4. Click **Create**.

### Update or delete a Shared processor pool

{: update-delete-spp}

To update or delete an SPP, navigate to **Compute** > **Shared processor pools** > click the desired SPP, and click the edit icon. You get a notification when the SPP is deleted successfully.

You can update or delete the following details in an existing SPP:

* Update the name of the SPP - Follow the same naming conventions that you use when you create an SPP. For more information, see [Create a Shared processor pool](/docs/power-iaas?topic=power-iaas-managing-shared-processor-pool#create-spp).
* Update number of cores - You can update the number of reserved cores based on resource availability and allocation.
* Delete an existing SPP - You can delete any existing SPP. Before deleting, ensure that no virtual server instances exist in the SPP. The virtual server instances if present, must be deleted or moved out with a support ticket.

## Managing a virtual server instance inside Shared processor pool

{: manage-vm-inside-spp}

When you deploy a virtual server instance, you can choose an SPP instead of a host. As you cannot move a virtual server instance into or out of an SPP, you can deploy a virtual server instance directly into an SPP as a best practice. You can also deploy a virtual server instance into a server placement group; the selected SPP host must be compatible with the affinity policy of the placement group that is chosen.

When you deploy multiple virtual server instances simultaneously, a new server placement group is automatically created.
{:note}

During any planned maintenance activity or when you want to do a remote restart, ensure that the virtual server instances are linked to an SPP based on your requirements.

### Deploy a virtual server instance into a Shared processor pool

{:deploy-pvm-in-spp}

To add virtual server instances to an SPP that are already created, complete the following steps:

1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Create instance**.
3. Complete the input fields under the **General** tile based on your requirement.
4. Select the checkbox Add to a **Shared processor pool**.
5. Select a shared processor pool that is already created.
6. Continue with the rest of the process to create a virtual server instance. For more information, see [Configuring a Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

## Configuring Shared processor pool placement group

{: configure-SPP-PG}

You can configure an SPP with the Shared processor pool placement group (SPP PG) to control the host in which SPPs are deployed.

SPP PGs are different from server placement groups. They serve the same purpose but cannot combine resource types.
{:Note}

You must define the following parameters to define an SPP PG:

* A unique name - The SPP PG name must be unique in your cloud instance.
* Policy - You can set the colocation policy of the SPP PG as same server (affinity) or different server (anti-affinity).

The following table explains how the host selection is determined based on the different options of SPP PG policy selection:

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|New SPP is configured on same host as determined by the existing PG SPP members.|The new SPP is automatically added as a member of the PG policy.|
|Different server (Anti-affinity) |Configure the new SPP on a different host than all host identified by all the existing PG members.|The new SPP is automatically added as a member of the PG policy.|
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Table 3. Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-1}
{: tab-title="When SPP PG is non-empty"}

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|New SPP is configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy|
|Different server (Anti-affinity) |New SPP is configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Table 3. Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-2}
{: tab-title="When SPP PG is empty"}

### Create a Shared processor pool placement group

{:create-new-pg}

Create an SPP PG with the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Pool placement groups** tab.
3. Click **Create group**.
4. In the **Create new pool placement group** window, enter the following details:
  |Field|Description                                             |
  |-----|--------------------------------------------------------|
  |Name |Enter a name that is unique within your cloud account. \n Use a minimum of 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and underscore (‘_’) is only allowed as a special character.|
  |Policy|Same Server (Affinity) \n Different server (Anti-affinity)|
  {: caption="Table 4. Create a new SPP PG field description" caption-side="top"}

5. Click **Create**.

You get notified when the new SPP PG is created.

### Add a Shared processor pool inside the placement group

{:add-spp-inside-spp-pg}

An SPP can be added as a member to an existing SPP PG if the host of the SPP follows the affinity policy of the group. If the PG policy is set to **Same server** (affinity), then all SPPs that are added as a member of the placement group must stay on the same host. If the PG policy is set to **Different server** (anti-affinity), then the SPP is deployed on a different host than all the other group members.

Add an SPP inside the SPP PG with the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Pool placement groups** tab.
3. Click the existing pool placement group under which you want to add the SPP.
4. Select one of the following options:

|    Field         |                 Description                           |
|------------------|-------------------------------------------------------|
|Add existing      |Allows you to pick the SPPs that are already created.     |
|Create new        |Helps you to create an SPP from scratch by defining pool name, machine type, and number of cores. For more information, see [Create a new SPP](/docs/power-iaas?topic=power-iaas-managing-shared-processor-pool#create-a-new-spp)|
{: caption="Table 5. Add SPP in SPP PG field description" caption-side="top"}

You get notified when the new SPP PG is created.

### Delete a Shared processor pool placement group

{:delete-spp-pg}

Delete an SPP PG with following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click **Pool placement groups** tab.
3. Click the group that you want to delete.
4. In the details page, click the delete icon.

Deleting a placement group does not delete its members or change the host in which the placement groups are deployed.
{:Note}
