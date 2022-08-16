---

copyright:
  years: 2022

lastupdated: "2022-08-12"

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

# Managing Shared Processor pool

{: #manage-SPP}

Shared Processor Pool (SPP) is a pool of processor capacity shared between a group of virtual machines.
Unlike a virtual machine with a dedicated and defined maximum amount of processing capacity, In SPP, you can set the reserved cores, which will be the reserved processing cores that are guaranteed to be available to the virtual machine.

{: shortdesc}

The following table shows how an SPP is used to reduce the licensing cost when you pay per core:
|Use of SPP|VM 1|VM 2|Reserved cores in Pool (User defined)|License requirement per core|
|-----------|-----------|-----------|-----------|-----------|
|No|Maximum cores 5 \n Mode = Uncapped \n Entitled capacity = 1|Maximum cores 6 \n Mode = Uncapped \n Entitled capacity = 1|NA|5+5 = 11|
|Yes|Maximum cores 5|Maximum cores 6|Maximum cores 6|Determined by reserved cores in pool = 6|

The benefits of using an SPP are as follows:

* Allows you to control how much you will spend on licensing costs by reducing the number of software licenses by limiting the number of processors an uncapped partition can use.
* You have a better overall ability to manage processor resources.

The Power Systems Virtual Server always has at least one defined shared processor pool as the default pool. You can add up to 63 more Shared Processor Pools in a single Power System Virtual Server service instance. The Shared Processor Pool is used and shared by a set of virtual machines of the same machine type (host). You can move the VMs from one workspace to another on the same or a different host. For more information see {Configuring Shared Processor Pool}.

You can specify host affinity and the anti-affinity between two or more of their shared processor pool with the shared processor pool Placement Groups. For more information see {Configuring Shared Processor Pool Placement Group}.

# Pricing for Shared Processor Pool

{:price-spp}

You pay for the following:

* SPP reserved cores using the Shared Capped part number.
* Cores of virtual machines deployed into the SPP using Shared Uncapped part number
The Shared Processor Pool feature helps to manage CPU cores only. Pricing for memory and storage remains the same as before.
{: note}

The Total estimated cost page will not show SPP reserved cores-related costs due to service level estimator limitations.

# Configuring Shared Processor Pool

{: configure-spp}

Shared Processor Pool is a separate resource within a Power Virtual Server workspace. You can manage the entire shared processor pool lifecycle.

The Shared processor pool and your Power Virtual Server workspace are linked. Hence, no other person from a different account will have visibility of each other’s shared resource pools. You can have one or more shared processors pooled per workspace.

You can specify the full name and size of the Shared Processor Pool and choose the host type to deploy the shared processor pool. You can create a new SPP by specifying the following:

* A unique name
* Host group or the machine type
* Number of processors to reserve.

When you define the above three parameters, the backend processing of PowerVC and Novalink is used to determine the best host within the specified host group to place the new SPP where the host group is a grouping of a host of the same system type, such as s922, e980, and so on.

## Create a new SPP

{: create-spp}

1. Click on Shared processor pools under Compute.
2. Click on Create pool.
3. Refer to the Define the following preferences as per your requirements: on the Create new shared processor pool window:

|Field|Description|
|----|----|
|Name|Enter a name that is unique within your cloud account.\n Your name should be a minimum of 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and only underscore (‘_’) as a special character is allowed.|
|Add to a pool placement group|Check this radio button if you want to add a pool placement group that are already created. You can keep it unchecked if you want to create a pool placement group later.|
|Select machine type|see as Creating a Power Systems Virtual Server |
|Reserved processing cores|There is a core-to-vCPU ratio of 1:1 by default that you can customize. For shared processors pool, fractional cores round up to the nearest whole number. For example, 1.25 cores equals 2 vCPUs. |

4. Click on Create.

## Update or delete an SPP

{: update-delete-spp}

To update or delete an SPP, navigate to Shared processor pools > click on the required instance > edit. You get a notification when the SPP is deleted successfully.

You can update or delete the following in an existing SPP:

* The name of the SPP follows the same naming conventions you use while creating a new SPP.
* The number of reserved cores - The amount can be increased (dependent on available resources) or decreased (dependent on currently allocated resources).
* Delete an existing SPP – Make sure there are no virtual machines deployed inside the SPP.

# Managing a virtual machine inside Shared Processor Pool

{: manage-vm-inside-spp}

While deploying a virtual machine, you can choose a shared processor pool instead of a host.  When you use multi create, it will automatically collocate the virtual machines in the group.

The core: vCPU ratio is currently set to 1:1 by default which you can override for a virtual machine while creating one in a Shared Processor Pool.

You cannot move the virtual machines between the Shared Processor Pools. You must first remove the virtual machines from the current pool they are in, and then you can add them to a new pool.

Within a pool, the sum of all the virtual machine's entitled capacity and reserve capacity cannot exceed the pool's maximum capacity.

When there is any planned maintenance activity or a need to perform a remote restart, ensure that the virtual machines are linked to a Shared Processor Pool as per your requirements.

## Deploying a PVM instance into an SPP

{:deploy-pvm-in-spp}

Refer to [Creating a Power Systems Virtual Server](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server) for deploying a virtual machine into an SPP.

# Configuring Shared Processor Pool Placement Group

{: configure-SPP-PG}

You can configure an SPP more advanced manner with the Shared Processor Pool Placement Group (SPP PG), which helps you control the host selection when creating a new Shared Processor Pool.
You should set the following to define an SPP PG:

* A unique name - The SPP PG name should be unique in your cloud instance.
* Policy - You can set the colocation policy of the SPP PG as same server (affinity) or different server (anti-affinity).

The following table explains how the host selection is determined based on the different options of SPP PG policy selection:

|SPP PG Policy|Host selection|Result|
|-------|---------|------------|--------------|
||If SPP PG is non-empty|If SPP PG is empty||
|--------------|---------------|-------------|-----------------------|
|Same server (Affinity)|New SPP configured on same host as determined by the existing PG SPP members|New SPP will be configured on a host that is selected based on the backend processing of PowerVC and Novalink|The new SPP is automatically added as a member of the PG policy|
|Different server (Anti-affinity) |Configure the new SPP on a different host than all host identified by all the existing PG members|New SPP will be configured on a host that is selected based on the backend processing of PowerVC and Novalink.|The new SPP is automatically added as a member of the PG policy |

## Create a new SPP PG

{:create-new-pg}

1. Click on Shared processor pools under Compute.
2. Click on Pool placement groups tab.
3. Click on Create group.
4. On the Create new pool placement group window enter the following:

|Field|Description|
|----------------|--------------------------------------------------------|
|Name|Enter a name that is unique within your cloud account.
Your name should be a minimum of 2 characters and a maximum of 12 characters. Alphanumeric characters are not allowed and only underscore (‘_’) as a special character is allowed.|
|Policy|Same Server (Affinity) \n Different server (Anti-affinity)|

5.Click create.
You get notified when the new SPP PG is created.

## Add an SPP inside the SPP PG

{:add-spp-inside-spp-pg}

You can add an SPP as a member to an existing SPP Placement Group. If the PG policy is ‘affinity,’ then all SPP added as a member of the PG must reside on the same host. If the PG policy is ‘anti-affinity,’ then the SPP will get added. No host check is needed.

1. Click on Shared processor pools under Compute.
2. Click on Pool placement groups tab.
3. Click on the existing pool placement group under which you want to add the SPP.
4. Select between the two options:

|    Field         |                 Description                           |
|------------------|-------------------------------------------------------|
|Add existing      |Allow you to pick an SPP that are already created.     |
|Create new        | Helps you to create an SPP from scratch by defining pool name, machine type, and number of cores. For more information, see {Create a new SPP}|

You get notified when the new SPP PG is created.

## Delete an SPP PG

{:delete-spp-pg}
You can navigate to the SPP PG from the Shared processor pool > Pool placement groups tab. Click on the SPP PG you want to delete to open the details page and click on the delete icon to delete the SPP PG.
