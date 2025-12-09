---

copyright:
  years: 2025

lastupdated: "2025-12-08"

keywords: Virtual Persistent Memory, virtual persistent memory, vPMEM, SAP HANA partitions

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}



# Enabling Virtual Persistent Memory in a {{site.data.keyword.powerSys_notm}} instance
{: #vPMEM}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}

---

Virtual Persistent Memory (vPMEM) is a nonvolatile memory that retains the data even when the system is powered off. The vPMEM is an enhancement to the IBM Power advanced virtualization platform (PowerVM) that enables the system to configure the persistent volumes by using the existing DRAM (dynamic RAM) technology. The vPMEM feature is available on IBM Power10 or later systems with IBM AIX&reg;, Linux&reg;, or Linux (SAP HANA) operating systems.

vPMEM is not supported on a {{site.data.keyword.powerSys_notm}} instance (VSI) with IBM i operating system.
{: note}

In the [IBM Cloud Resource List](https://cloud.ibm.com/resources){: external}, you can identify your vPMEM volume under **Compute** resources. If you add a vPMEM volume when you create a VSI and add user tags to the VSI, the tag is also added to the vPMEM volume. If you add a vPMEM volume to an existing VSI, you can add user tags only to the vPMEM volume.


## Before you begin
{: #vpmem-byb}

Before you create and add the vPMEM volumes to a VSI, review the following information:

- When you add vPMEM volumes to a VSI with AIX or Linux OS, the vPMEM volumes use memory in addition to the base memory.

- When you add a vPMEM volume to a VSI that is created by using an SAP certified profile, consider the following points:
  - The SAP certified profile must support vPMEM volume.
  - VSI profile memory is the total memory that includes the vPMEM volume.
  - You cannot resize the VSI.

To add a vPMEM volume to an existing VSI or to delete a vPMEM volume from the VSI, the VSI must be in the `Shutoff` state.
{: important}


## Adding vPMEM volume during VSI provisioning
{: #vPMEM-add-vsi}

To create and add a vPMEM volume to a VSI when you provision a VSI in a Power10 or later system, update the following fields on the Create virtual server instance page.

| Field                 | Action                                          |
| --------------------- | ----------------------------------------------- |
| Operating system      | Select AIX&reg;, Linux&reg;, or Linux for SAP (HANA).     |
| Image                 | Select an image from the list.                  |
| Machine type          | Select Power10 or later system.                 |
| Advance Configuration | - Set **Virtual persistent memory volume** to on.  \n - Click **Create volume** to create a vPMEM volume. The Create virtual persistent memory volume pane appears.  \n - Update the fields that are defined in the [Creating a vPMEM volume](#vPMEM-create) topic.  |
{: caption="Fields and corresponding actions to create a VSI with vPMEM volume" caption-side="top"}


## Adding a vPMEM volume to a VSI
{: #vPMEM-add-vsi-exist}

On the Virtual server instances page, complete the following steps:

1. Click the VSI to which you want to add the vPMEM volume.
2. Complete the following steps on the Overview tab of the VSI page:
   1. Click **Create volume** under the Virtual persistent memory volumes section. The Create virtual persistent memory volume pane appears.
   2. Update the fields that are defined in the [Creating a vPMEM volume](#vPMEM-create) topic.


## Creating a vPMEM volume
{: #vPMEM-create}

Update the following fields to create a vPMEM volume on the Create virtual persistent memory pane.

| Field                 | Action                                          |
| --------------------- | ----------------------------------------------- |
| Name                  | Specify a name for the vPMEM volume.            |
| User tags             | Enter user tags, optionally.                    |
| Size                  | Increment or decrement the size of the vPMEM volume. The values are calculated in gibibyte (GiB).                                                           |
| Total estimated cost  | Review the total estimated cost for your vPMEM volume.  |
| Create                | Create the vPMEM volume. The **Create** field is enabled only if you agree to the estimated cost by selecting the **I agree to the Terms and conditions** checkbox.  |
{: #create-vPMEM-volume-table}
{: caption="Fields and corresponding actions to create a vPMEM volume" caption-side="top"}

You cannot resize the vPMEM volume once you create it.
{: note}

### Creating and adding a vPMEM volume by using API and CLI commands
{: #vPMEM-create-add-API-CLI}

Use the following API and CLI commands to create and add a vPMEM volume to a VSI:

- API: Use the [Create a vPMEM volume to be attached to this PVM Instance](https://cloud.ibm.com/apidocs/power-cloud#pcloud-pvminstances-vpmem-volumes-post){: external} API to create a vPMEM volume for VSI with AIX&reg;, Linux&reg;, or Linux (SAP HANA) OS.
- CLI: Use the [ibmcloud pi instance create](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-create) command to create a vPMEM volume. You can use [ibmcloud pi instance vpmem-volume](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-vpmem-volume) to perform `attach`, `detach`, `get`, or `list` operations.


## Deleting a vPMEM volume
{: #vPMEM-delete}

You can delete a vPMEM volume from a VSI only if the VSI is in a **Shutoff** state.
{: note}

On the Virtual server instances page, click the VSI from which you want to delete the vPMEM volume. From the Virtual persistent memory volumes section, click the delete icon that is associated with the vPMEM volume to be deleted.

If the vPMEM volume was associated with the VSI with AIX or Linux OS, the vPMEM volume memory is reduced from the total memory and the total cost is reduced.

If the vPMEM volume was associated with the VSI with Linux for SAP (HANA) OS, the vPMEM volume memory is returned to the VSI. The total cost remains unchanged.


### Deleting a vPMEM volume by using API and CLI commands
{: #vPMEM-delete-API-CLI}

Use the following API and CLI commands to delete a vPMEM volume:

- API: Use the [Delete a vPMEM volume attached to this PVM Instance](https://cloud.ibm.com/apidocs/power-cloud#pcloud-pvminstances-vpmem-volumes-delete){: external} API command to delete a vPMEM volume.
- CLI: Use the [ibmcloud pi instance delete](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-instance-delete) to delete a vPMEM volume.


## Pricing for vPMEM volumes
{: vpmem-price}

The cost of a vPMEM volume is calculated based on the OS type of the VSI. For more information, refer to the following examples:

- For a VSI with SAP (HANA) profile, the memory for vPMEM volume is allocated from the total memory of the SAP (HANA) profile. For example, consider a VSI with `sh2-25x1000` SAP profile that has 1000 GB memory. You add a vPMEM volume of 200 GB to the VSI. The 200 GB memory is allocated to the vPMEM volume from the `sh2-25x1000` profile size and 800 GB memory is retained with the VSI. So, the VSI with 800 GB memory has a vPMEM volume of 200 GB attached to it. No additional cost is incurred. When you delete the vPMEM volume, the memory that is used from the total profile size is returned and the cost remains the same.
- For a VSI with AIX or Linux OS, the total cost is calculated based on the total memory usage. For example, consider a VSI with 1000 GB memory. When you add a vPMEM volume of 200 GB to the VSI, the total memory changes to 1200 GB so the cost is calculated for 1200 GB memory. When you delete the vPMEM volume, the memory is reduced from the total memory and the total cost reduces.

For more information about the part numbers for vPMEM volumes, see [Pricing for IBM Power Virtual Server in IBM data centers](/docs/power-iaas?topic=power-iaas-pricing-ibm-data-center).

## Limitations of vPMEM
{: #vPMEM-limitations}

vPMEM has the following limitations:

- You can create and add vPMEM volume to a VSI on IBM Power10 or later systems with AIX&reg;, Linux&reg;, or Linux (SAP HANA) operating systems.
- You can add or detach a vPMEM volume to a VSI only when the VSI is shut down.
- You can add one vPMEM volume to a VSI with SAP (HANA) profile and add four vPMEM volumes to a VSI with AIX or Linux OS.
- You cannot add a vPMEM volume to a VSI with IBM i operating system.
- You cannot resize a VSI with SAP (HANA) profile if a vPMEM volume is added to it.
- You cannot edit the size of a vPMEM volume.
- You cannot enable global replication services (GRS) on vPMEM volumes.
