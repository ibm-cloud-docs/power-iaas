---

copyright:
  years: 2024

lastupdated: "2024-06-11"

keywords: estimate price, estimate, generating an estimate, {{site.data.keyword.powerSys_notm}}, private cloud, creating estimate, saving estimate, estimate virtual server instance, estimate storage volume, estimate shared processor pool, estimate VPN, estimate virtual tape library

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Generating an estimate for a {{site.data.keyword.powerSys_notm}}
{: #generating-an-estimate}
{: help}
{: support}

Use the [cost estimator](https://cloud.ibm.com/power/estimate){: external} tool to estimate the cost of the resources before you deploy them. With the cost estimator tool, you can customize and determine the requirements that align with your business needs.

Use the cost estimator tool for:
1. [Creating an estimate of resources](#est-resources)
2. [Creating, saving, and viewing an estimate](#creating-an-estimate)

## Creating an estimation of resources
{: #est-resources}

You can generate an estimate by specifying the parameters for your virtual server resources and by specifying a projected growth rate. Based on your selection, you can view the estimated cost of your IBM {{site.data.keyword.powerSysFull}} Private Cloud or IBM cloud resources. You can connect with your IBM Business Partner or contact IBM to place your order.
{: shortdesc}

You are not charged for creating an estimate. The resources that you estimate can be deployed only after a workspace creation.
{: note}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. Search for **Workspace for {{site.data.keyword.powerSys_notm}}** in the search box for IBM Cloud catalog.

3. Click **Workspace for {{site.data.keyword.powerSys_notm}}** tile.

4. Click **Estimate Cost** to generate an estimated cost summary. An estimate is the approximate cost of the resources that you want to use in your workspace.
    You are redirected to the **Estimate cost** page for {{site.data.keyword.powerSys_notm}}.

5. Select the type of virtual server from the **Location** drop-down list as [**On-premises**](#on-prem-location-type) or [**Off-premises**](#off-prem-location-type).

6. Select an IBM Cloud region from the **Location** drop-down list. Select an IBM Cloud region.
    For IBM {{site.data.keyword.powerSys_notm}} Private Cloud, select an IBM Cloud region that is closest to your physical location or data center where the pod will reside.

7. On the right-side panel, click **Add to estimate** to review the configuration.

8. If you are not logged in, choose **from catalog** in the **Add product to estimate** drop-down menu.

9.  Click **Save**.

10. Click **View estimate** to view and to take actions on them.


### Off-premises (IBM Cloud)
{: #off-prem-location-type}

[Off-premises]{: tag-blue}

If you select the **Location type** as Off-premises, select one resource from the following list and choose additional configurations based on your requirement:

* [Virtual server instance](#est-vsi)
* [Storage volume](#est-storage-vol)
* [Shared processor pool](#est-spp)
* [VPN connection](#est-vpn)
* [Dedicated host](#est-dh) 


The summary of the selected infrastructure is displayed on the **Summary** page. You can review the total estimated cost per hour and per month that is displayed on the **Summary** page. To create, save, and download the estimate, see [Creating, saving, and viewing an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate#creating-an-estimate).

#### Estimating a virtual server instance
{: #est-vsi}

Before deploying a virtual server instance in a workspace, create an estimate of it. You can create an estimate of a virtual server instance from the estimation page and virtual server instance provisioning page on IBM Cloud.

To learn about the fields and descriptions that you need to enter, see the following table:

| Field	                        | Description                                                                                           |
|-------------------------------|-------------------------------------------------------------------------------------------------------|
| Number of virtual servers	    | (**Required**) Specify the number of instances that you want to estimate for the {{site.data.keyword.powerSys_notm}}. |
| Operating system              |	Select the operating system that meets your requirements from the drop-down.                                |
| Configure for Epic workloads  |	Check this indicator if you want to deploy on E980 or E1080 machines with Tier 1 storage and dedicated cores, at a shared-capped price. \n When you select this indicator, the other dependent fields are automatically filled. To learn more about epic workloads, see [Configuring a VM for Epic workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads).                                |
| Machine type                  |	Specify the machine type.                                                                           |
| Core type                 	| Specify the core type.                                                                                |
| Cores	                        | (**Required**) Define how many cores you need.                                                         |
| Memory (GB)                  | (**Required**) Define how much space you need per core.                                                |
| Storage tiers             	| Attach volumes to your estimate. You can choose from Tier 0, Tier 1, Tier 3, Fixed IOPs or a combination of tiers. \n You cannot add a separate boot volume estimation. Hence, you must enter the storage volume considering the boot volumes and data volume that you might need.|
{: caption="Table 1. UI fields in estimating a VSI" caption-side="top"}


To learn more on how to create an instance, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).


#### Estimating a storage volume
{: #est-storage-vol}

Before deploying a storage volume in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field                         |	Description                                                              |
|-------------------------------|----------------------------------------------------------------------------|
| Number of volumes	Required:   |   Specify the number of volumes that you need.                                  |
| Tier	                        |   Choose from Tier 0, Tier 1, Tier 3, Fixed IOPs or a combination of these tiers.|
| Total storage (GB)	        |   Enter the amount of volume that you need.                                     |
{: caption="Table 2. UI fields in estimating a storage volume" caption-side="top"}


#### Estimating a shared processor pool
{: #est-spp}

Before you deploy a shared processor pool in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	            | Description                                                   |
|-------------------|---------------------------------------------------------------|
| Number of pools	| (**Required**) Specify the number of pools that you need.           |
| Machine type	    | Specify the machine type.                                     |
| Reserved cores 	| (**Required**) Enter the number of cores that you want to reserve.  |
{: caption="Table 3. UI fields in estimating a shared processor pool" caption-side="top"}

To learn more about a shared processor pool, see [Managing a shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).

#### Estimating a VPN connection
{: #est-vpn}

Before you create and attach a VPN connection, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	                |   Description                                                 |
|-----------------------|---------------------------------------------------------------|
| Number of connections	|   Enter the number of VPN connections that you want to estimate.   |
{: caption="Table 4. UI fields in estimating a VPN conection" caption-side="top"}

To learn more about VPN connections, see [Creating VPN connections](/docs/power-iaas?topic=power-iaas-VPN-connections).

#### Estimating a virtual tape library
{: #est-vtl}

Before you deploy a virtual tape library (VTL) in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	            |   Description                                                                 |
|-------------------|-------------------------------------------------------------------------------|
| Number of VTLs 	|   (**Required**) Enter the number of virtual tape library instances that you need.  |
| Licensed repository capacity (TB)	|   Define the size of your repository capacity that determines which software license is needed. |
| Machine type	    |   Specify the machine type.                                                   |
| Core type	        |   Specify the core type.                                                      |
| Cores	            |   (**Required**) Define how many cores you need.                               |
| Memory (GB)	    |   (**Required**) Define how much space you need per core.                      |
|Storage tiers	    |   **Optional**: Attach volumes to your estimate. You can choose from Tier 0, Tier 1, Tier 3, Fixed IOPs or a combination of these tiers. \n You cannot add a separate boot volume estimation. Hence, you should enter the storage volume considering the boot volumes and data volume that you might need. |
{: caption="Table 5. UI fields in estimating a VTL" caption-side="top"}

To learn more about virtual tape libraries, see [Managing a virtual tape library](/docs/power-iaas?topic=power-iaas-manage-vtl).



#### Estimating a dedicated host
{: #est-dh}

Before deploying a dedicated host in a workspace, create an estimate of it. To learn about the fields and descriptions that you need to enter, see the following table:

| Field	            |   Description                                                                 |
|-------------------|-------------------------------------------------------------------------------|
| Number of dedicated hosts	|   (**Required**) Enter the number of dedicated hosts you want to create.  |
| Machine type      |   (**Required**) Select the available machine types where you can crreate dedicated host. |
{: caption="Table 6. UI fields in estimating a dedicated host" caption-side="top"}

To learn more about dedicated host, see [Getting started with dedicated host].



### On-premises (IBM {{site.data.keyword.powerSys_notm}} Private Cloud)
{: #on-prem-location-type}

[On-premises]{: tag-red}

If you select the **Location type** as On-Premises, proceed with the following steps:

1. Specify the infrastructure requirements that include the machine type, number of systems, and storage capacity for your data center in the **Infrastructure configuration** section. The **Infrastructure overview** section displays the summary of the selected configuration. The pod size depends on the number of systems that you select including the total memory and the total number of cores that you plan to use in your data center.

    Currently, IBM Power S1022 (2U), IBM Power E1050 (4U), and IBM Power E1080 (12U) servers are supported by specific memory. Each server type is shipped with a fixed number of cores.


2. The **Minimum committed spend** value indicates the minimum monthly cost for your {{site.data.keyword.powerSys_notm}} pod. Select the number of years for the **Contract commitment term** drop-down list.

    A longer contract commitment term reduces the minimum committed spend value. You can contact IBM to learn more about the possible savings with the commitment plans. Metered cost is determined based on the consumption and it is charged only when the consumption rate is greater than the minimum committed spend value.
    {: note}

3.  Click **Model consumption** to set the predicted consumption of the infrastructure configuration resources that you plan to use during the contract commitment term that you choose in the previous step. You can specify the predicted memory and core usage for each of the server types. You can also set the predicted storage capacity that you plan to use. After you set the predicted usage and reviewed the estimated metered (billing) cost, close the **Model metered consumption** window.

    The summary of estimated costs for the contract commitment years is displayed in the **Summary** page based on your selection of predicted infrastructure resource usage. Metered consumption cost is only charged if the actual metered cost is greater than the **Minimum committed spend** value.

4.  Review the estimated cost in the **Summary** page on the right side of the page. The estimated minimum cost includes the **Minimum committed spend** value and the billing charges, if any.

    The actual cost might increase based on your consumption rates.
    {: note}

5.  Click **Add to estimate** to create an estimate and export your configuration estimate. For instructions about creating an estimate, see [Creating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate#creating-an-estimate).


## Creating, saving, and viewing an estimate
{: #creating-an-estimate}

When you generate the estimate, you can create and export the configuration estimate by completing the following steps:

1. Click **Add to estimate** on the **Summary** page of the **Estimate Cost** page.

2. The **Estimate** window appears.
   - Select an existing estimate from the drop-down list if you want to add the product to an existing estimate.
   - Click **Create a new estimate** if you want to create a new estimate.
        On the **Create a new estimate** window, specify a name for the estimate and an optional description. Click **Create**.

3. In the **Estimate** window, click **Save** to save the product to the selected or created estimate.

4. Click **View estimate** to view an estimate of your {{site.data.keyword.powerSys_notm}} configuration.

5. Click **Download** to export the saved estimate as an XLSX, a CSV, or a PDF file.


## Contacting IBM to place an order
{: #contacting-ibm}

Share the downloaded estimate with your IBM Business Partner to start the ordering process. Initiate the discussion to plan for your infrastructure configuration, data center requirements, to learn about possible savings plans, or to place your order.

If you do not have an IBM Business Partner, contact IBM through email or the contact number that is specified on the window.

Before you place the order for IBM {{site.data.keyword.powerSys_notm}} Private Cloud, verify that the basic criteria to own a pod is met. For more information, see [Prerequisites for installing the pod](/docs/power-iaas?topic=power-iaas-pre_installation_checklist).
{: important}
