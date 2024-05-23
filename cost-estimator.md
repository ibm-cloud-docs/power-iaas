---

copyright:
  years: 2019, 2024

lastupdated: "2024-05-23"

keywords: cost estimator tool, power virtual server cost, estimate, estimation,

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

# Getting started with the cost estimator tool
{: #cost-estimator}

Use the cost estimator tool in the home page of {{site.data.keyword.powerSysFull}} in IBM Cloud® to estimate the cost of resources before you deploy them. With the cost estimator tool, you can customize and determine the requirements that align with your business needs.

You do not need to be logged in to create an estimate.

Select a data center that suits your needs and use the cost estimator tool for:
1.	Creating an estimate of resources
2.	Updating an existing estimate
3.	Saving and sharing your estimate

## Creating an estimation of resources
{: #est-resources}

To create an estimate, perform the following steps:

You are not charged for creating an estimate. The resources that you estimate can be deployed only after a workspace creation.
{: note}

1.	Open the {{site.data.keyword.powerSys_notm}} [home page](https://cloud.ibm.com/power/overview){: external} in the IBM Cloud console.
2.	Click **Estimate cost**.
3.	Select a data center from the **Location** drop-down menu.
4.	Select one resource from the following list and choose additional configurations as per your requirement:
    * Virtual server instance
    * Storage volume
    * Shared processor pool
    * VPN connection
    * Virtual tape library
    * Dedicated host
5.	On the right-side panel, click **Add to estimate** to review the configuration.
6.	If you are not logged in, choose **from catalog** in the **Add product to estimate** drop-down menu.
7.	Click **Save**.
8.	Click **View estimate** to view and to take actions on them.


### Estimating a virtual server instance
{: #est-vsi}

Before deploying a virtual server instance in a workspace, create an estimate of it. You can create an estimate of a virtual server instance from the estimation page and virtual server instance provisioning page on IBM Cloud.

To learn about the fields and descriptions that you need to enter, see the following table:

| Field	                        | Description                                                                                           |
|-------------------------------|-------------------------------------------------------------------------------------------------------|
| Number of virtual servers	    | **Required**: Specify the number of instances that you want to estimate for the {{site.data.keyword.powerSys_notm}}. |
| Operating system              |	Select the operating system that meets your requirements from the drop-down.                                |
| Configure for Epic workloads  |	Check this indicator if you want to deploy on E980 or E1080 machines with Tier 1 storage and dedicated cores, at a shared capped price. \n When you select this indicator, the other dependent fields are automatically filled. To learn more about epic, see [Configuring a VM for Epic workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).                                |
| Machine type                  |	Specify the machine type.                                                                           |
| Core type                 	| Specify the core type.                                                                                |
| Cores	                        | **Required**: Define how many cores you need.                                                         |
| Memory (GiB)                  | **Required**: Define how much space you need per core.                                                |
| Storage tiers             	| **Optional**: Attach volumes to your estimate. You can choose from Tier 0, Tier 1, Tier 2, Tier 3, Fixed IOPs or a combination of these. tiers \n You cannot add a separate boot volume estimation. Hence, you should enter the storage volume considering the boot volumes and data volume that you might need.|
{: caption="Table 1. UI fields in estimating a VSI" caption-side="top"}


To learn more on how to create an instance, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).


### Estimating a storage volume
{: #st-storage-vol}

Before deploying a storage volume in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field                         |	Description                                                              |
|-------------------------------|----------------------------------------------------------------------------|
| Number of volumes	Required:   |   Specify the number of volumes that you need.                                  |
| Tier	                        |   Choose from Tier 0, Tier 1, Tier 2, Tier 3, Fixed IOPs or a combination of these tiers.|
| Total storage (GB)	        |   Enter the amount of volume that you need.                                     |
{: caption="Table 2. UI fields in estimating a storage volume" caption-side="top"}

### Estimating a shared processor pool
{: #est-spp}

Before deploying a shared processor pool in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	            | Description                                                   |
|-------------------|---------------------------------------------------------------|
| Number of pools	| **Required**: Specify the number of pools that you need.           |
| Machine type	    | Specify the machine type.                                     |
| Reserved cores 	| **Required**: Enter the number of cores that you want to reserve.  |
{: caption="Table 3. UI fields in estimating a shared processor pool" caption-side="top"}

To learn more about shared processor pool, see [Managing a shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).

### Estimating a VPN connection
{: #est-vpn}

Before you create and attach a VPN connection, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	                |   Description                                                 |
|-----------------------|---------------------------------------------------------------|
| Number of connections	|   Enter the number of VPN connections that you want to estimate.   |
{: caption="Table 4. UI fields in estimating a VPN conection" caption-side="top"}

To learn more about VPN connection, see [Managing VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections).

### Estimating a virtual tape library
{: #est-vtl}

Before deploying a virtual tape library (VTL) in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	            |   Description                                                                 |
|-------------------|-------------------------------------------------------------------------------|
| Number of VTLs 	|   **Required**: Enter the number of virtual tape library instances that you need.  |
| Licensed repository capacity (TB)	|   Define the size of your repository capacity that determines which software license is needed. |
| Machine type	    |   Specify the machine type.                                                   |
| Core type	        |   Specify the core type.                                                      |
| Cores	            |   **Required**: Define how many cores you need.                               |
| Memory (GiB)	    |   **Required**: Define how much space you need per core.                      |
|Storage tiers	    |   **Optional**: Attach volumes to your estimate. You can choose from Tier 0, Tier 1, Tier 2, Tier 3, Fixed IOPs or a combination of these tiers. \n You cannot add a separate boot volume estimation. Hence, you should enter the storage volume considering the boot volumes and data volume that you might need. |
{: caption="Table 5. UI fields in estimating a VTL" caption-side="top"}

To learn more about virtual tape libraries, see [Managing a virtual tape library](/docs/power-iaas?topic=power-iaas-managing-virtual-tape-library).

### Estimating a dedicated host
{: #est-dh}

Before deploying a dedicated host in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	            |   Description                                                                 |
|-------------------|-------------------------------------------------------------------------------|
| NNumber of dedicated hosts	|   **Required**: Enter the number of dedicated hosts you want to create.  |
| Machine type      |   **Required**: Select the available machine types where you can crreate dedicated host. |
{: caption="Table 6. UI fields in estimating a dedicated host" caption-side="top"}

## Updating an existing estimate
{: #update-est}

Open the view estimate page in IBM Cloud and perform the following steps that are mentioned in [updating an existing estimate](/docs/billing-usage?topic=billing-usage-cost#update-estimate). 

## Saving and sharing your estimate
{: #est-share}

Open the view estimate page in IBM Cloud and perform the following steps that are mentioned in [saving and sharing your estimate](/docs/billing-usage?topic=billing-usage-cost#share-estimate).
