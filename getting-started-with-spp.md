---

copyright:
  years: 2022

lastupdated: "2022-08-24"

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

# Managing shared processor pool

{: #manage-SPP}

A Shared Processor Pool (SPP) is a pool of processor capacity shared between a group of virtual server instances. Unlike a virtual server instance with a dedicated and defined maximum amount of processing capacity, In SPP, you can set the reserved cores, which will be the reserved processing cores that are guaranteed to be available at the pool level.

{: shortdesc}

The following table shows how an SPP is used to reduce the licensing cost when you pay per core:
|Use of SPP|VM 1|VM 2|Reserved cores in Pool (User defined)|License requirement per core|
|-----|-----------|-----------|-----------|-----------|
|No|Maximum cores 5 \n Mode = Uncapped \n Entitled capacity = 1|Maximum cores 6 \n Mode = Uncapped \n Entitled capacity = 1|NA|5+5 = 11|
|Yes|Maximum cores 5|Maximum cores 6|Maximum cores 6|Determined by reserved cores in pool = 6|
{: class="simple-table"}
{: caption="Table 1. SPP helps to reduce the licensing cost" caption-side="bottom"}

The benefits of using an SPP are as follows:

* Provides control over licensing costs by limiting the number of processors an uncapped partition can use, which reduces the number of software licenses.
* Provides a better overall ability to manage processor resources.

The {{site.data.keyword.powerSys_notm}} always has at least one defined SPP as the default pool. You can add up to 63 more SPP in a single {{site.data.keyword.powerSys_notm}} workspace. The SPP is used and shared by a set of virtual server instances of the same machine type (host).

You can specify the host affinity and anti-affinity between two or more SPP with shared processor pool placement groups. For more information, see [Configuring shared processor pool placement group](/docs/power-iaas?topic=power-iaas-managing-shared-processor-pool#configuring-shared-processor-pool-placement-group).

## Pricing for Shared processor pool

{:price-spp}

You pay for the following:

* SPP reserved cores using the Shared Capped part number.
* Virtual server instance cores deployed into the SPP using Shared Uncapped part number.

The SPP helps manage CPU cores only. Pricing for memory and storage remains the same as before. The total estimated cost page will not show SPP reserved cores-related costs due to service level estimator limitations. For more information on pricing, see [Pricing for Power Systems Virtual Servers](/docs/power-iaas?topic=power-iaas-pricing-virtual-server).
{: note}

## Configuring Shared processor pool

{: configure-spp}

SPP is a separate resource within a {{site.data.keyword.powerSys_notm}} workspace. You can manage the entire SPP lifecycle.

The SPP and your {{site.data.keyword.powerSys_notm}} workspace are linked, meaning shared resource pools will not be visible from different accounts. You can have one or more SPP per workspace.

You can specify the full name and size of the SPP and choose the host type to deploy the SPP. You can create a new SPP by specifying the following:

* A unique name
* Host group or the machine type
* Number of processors to reserve.

When you define the above three parameters, a backend processing determines the best host for the new SPP.

### Create a new shared processor pool

{: create-spp}

Perform the following steps to create a new SPP:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click on **Create pool**.
3. On the **Create new shared processor pool** window, define the following preferences as per your requirements:
  |Field|Description|
  |----|----|
  |Name|Enter a name that is unique within your cloud account.\n Your name should be a minimum of 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and only underscore (‘_’) as a special character is allowed.|
  |Add to a pool placement group|Select the checkbox if you want to deploy the SPP directly into an existing pool placement group. \n If the pool has required affinity relations to other pools, it is recommended to deploy the pool directly into the placement group. Note that the pool placement group must be created first. This prevents the pool from being deployed on a host that does not satisfy the affinity requirements, and having to move it later.|
  |Select machine type|Specify the machine type. For more information about hardware specifications, see [E880 (Dallas only)](https://www-01.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_sm/5/872/ENUS9119-_h05/index.html&lang=en){: external}, [S922](https://www.ibm.com/downloads/cas/KQ4BOJ3N){: external}, and [E980 (Data centers other than Dallas and Washington)](http://www-01.ibm.com/support/docview.wss?uid=ssm1platformaix9080-M9S-vios-only){: external}.|
  |Reserved processing cores|There is a core-to-vCPU ratio of 1:1 by default. |
  {: caption="Table 2. Creating a new SPP fields and descriptions" caption-side="bottom"}

4. Click on **Create**.

### Update or delete a shared processor pool

{: update-delete-spp}

To update or delete an SPP, navigate to Shared processor pools > click on the desired SPP > edit. You get a notification when the SPP is deleted successfully.

You can update or delete the following in an existing SPP:

* Update the name of the SPP - Follow the same naming conventions you use while creating a new SPP. For more information, see [Create a new SPP Placement Group](/docs/power-iaas?topic=power-iaas-managing-shared-processor-pool#create-a-new-spp-placement-group).
* Update number of cores - The number of reserved cores can be updated based on resource availability and allocation.
* Delete an existing SPP - You can delete any existing SPP. Before deleting, ensure there are no virtual server instances in the SPP; these must be deleted or moved out with a support ticket.

## Managing a virtual server instance inside shared processor pool

{: manage-vm-inside-spp}

While deploying a virtual server instance, you can choose a SPP instead of a host.  Since you cannot move a virtual server instance into or out of an SPP, deploying a virtual server instance straight into an SPP is recommended. You can also deploy a virtual server instance into a server placement group; the selected SPP host must be compatible with the affinity policy of the placement group chosen.

When you deploy multiple virtual server instances simultaneously, a new server placement group is automatically created.
{:note}

When there is any planned maintenance activity or a need to perform a remote restart, ensure that the virtual server instances are linked to a SPP as per your requirements.

### Deploying a virtual server instance into a shared processor pool

{:deploy-pvm-in-spp}

To add virtual server instances to an SPP that you have already created, complete the following steps:

1. Go to **Virtual server instances** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click on **Create instance**.
3. Fill in the input fileds under the **General** tile as per your requirement.
4. Select the checkbox Add to a **shared processor pool**.
5. Select the shared processor pool that you have already created.
6. Continue with the rest of the process to create a virtual server instance. For more information, see [Configuring a Power Systems Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

## Configuring shared processor pool placement group

{: configure-SPP-PG}

You can configure an SPP in a more advanced manner with the shared processor pool placement group (SPP PG). SPP PG can be used to control the host in which SPPs are deployed.

SPP PG are different from server placement groups; they serve the same purpose but cannot combine resource types.
{:Note}

You should set the following to define an SPP PG:

* A unique name - The SPP PG name should be unique in your cloud instance.
* Policy - You can set the colocation policy of the SPP PG as same server (affinity) or different server (anti-affinity).

The following table explains how the host selection is determined based on the different options of SPP PG policy selection:

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|New SPP configured on same host as determined by the existing PG SPP members|The new SPP is automatically added as a member of the PG policy|
|Different server (Anti-affinity) |Configure the new SPP on a different host than all host identified by all the existing PG members|The new SPP is automatically added as a member of the PG policy |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Table 3. Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-1}
{: tab-title="When SPP PG is non-empty"}

|SPP PG Policy|Host selection|Result|
|-------------|--------------|------|
|Same server (Affinity)|New SPP will be configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy|
|Different server (Anti-affinity) |New SPP will be configured on a host that is selected based on the backend processing|The new SPP is automatically added as a member of the PG policy |
{: class="simple-tab-table"}
{: tab-group="host_selection"}
{: caption="Table 3. Host selection when SPP PG is empty and non-empty" caption-side="top"}
{: #host_selection-2}
{: tab-title="When SPP PG is empty"}

### Create a new shared processor pool placement group

{:create-new-pg}

Perform the following steps to create a new SPP PG:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click on **Pool placement groups** tab.
3. Click on **Create group**.
4. On the **Create new pool placement group** window enter the following:
  |Field|Description                                             |
  |-----|--------------------------------------------------------|
  |Name |Enter a name that is unique within your cloud account. \n Your name should be a minimum of 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and only underscore (‘_’) as a special character is allowed.|
  |Policy|Same Server (Affinity) \n Different server (Anti-affinity)|
  {: caption="Table 4. Create a new SPP PG field description" caption-side="top"}

5. Click **Create**.

You get notified when the new SPP PG is created.

### Add an SPP inside the SPP PG

{:add-spp-inside-spp-pg}

An SPP can be added as a member to an existing pool placement group as long as the host of the SPP follows the affinity policy of the group. If the PG policy is **Same server** (affinity), then all SPP added as a member of the placement group must reside on the same host. If the PG policy is **Different server** (anti-affinity), then the SPP is deployed on a different host than all the other group members.

Perform the following steps to add an SPP inside the SPP PG:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click on **Pool placement groups** tab.
3. Click on the existing pool placement group under which you want to add the SPP.
4. Select between the two options:

|    Field         |                 Description                           |
|------------------|-------------------------------------------------------|
|Add existing      |Allow you to pick an SPP that are already created.     |
|Create new        | Helps you to create an SPP from scratch by defining pool name, machine type, and number of cores. For more information, see [Create a new SPP](/docs/power-iaas?topic=power-iaas-managing-shared-processor-pool#create-a-new-spp)|
{: caption="Table 5. Add SPP in SPP PG field description" caption-side="top"}

You get notified when the new SPP PG is created.

### Delete an shared processor pool placement group

{:delete-spp-pg}

To delete an SPP PG, perform the following steps:

1. Go to **Shared processor pools** in the {{site.data.keyword.powerSys_notm}} user interface under **Compute**.
2. Click on **Pool placement groups** tab.
3. Click on the group to be deleted. This will open up its details page.
4. Find a delete icon in the top right of the screen and click on the delete icon.

Deleting a placement group does not delete its members or change the host they are deployed on.
{:Note}
