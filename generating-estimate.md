---

copyright:
  years: 2024

lastupdated: "2025-11-11"

keywords: estimate price, estimate, generating an estimate, {{site.data.keyword.powerSys_notm}}, private cloud, creating estimate, saving estimate, estimate virtual server instance, estimate storage volume, estimate shared processor pool, estimate VPN, estimate virtual tape library

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating an estimate for IBM {{site.data.keyword.powerSys_notm}} resources
{: #creating-an-estimate}
{: help}
{: support}

Before you deploy a {{site.data.keyword.powerSys_notm}} with cloud resources such as virtual server instances, storage volumes, shared processor pools, virtual tape libraries, or dedicated hosts, it is important that you create an estimate to understand the associated costs. You can use the [cost estimator](https://cloud.ibm.com/power/estimate){: external} tool to estimate the cost of the {{site.data.keyword.powerSysFull}} resources before you deploy them in an IBM data center or in a {{site.data.keyword.on-prem-lc}}.
{: shortdesc}

With the cost estimator tool, you can customize the resource quantities based on your business requirement and view the estimated cost. You can use the cost estimator tool for:
- [Creating an estimation of {{site.data.keyword.powerSys_notm}} resources](#est-resources)
- [Adding, saving, and viewing an estimate](#adding-an-estimate)

## Creating and viewing an estimation of {{site.data.keyword.powerSys_notm}} resources
{: #est-resources}

You can create an estimate by specifying the parameters for your {{site.data.keyword.powerSys_notm}} resources and by specifying a projected growth rate. Based on your selection, you can view the estimated cost of your {{site.data.keyword.powerSys_notm}} resources in an IBM data center or in a {{site.data.keyword.on-prem-lc}}. You can connect with your IBM Business Partner or contact IBM to place your order.

You are not charged for creating an estimate. The resources that you estimate can be deployed only after a workspace is created.
{: note}

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. Search for **{{site.data.keyword.powerSys_notm}}** in the search box for IBM Cloud catalog.

3. Click **{{site.data.keyword.powerSys_notm}}** tile.

4. Click **Estimate Cost** to create an estimated cost summary. An estimate is the approximate cost of the resources that you want to use in your workspace.
    You are redirected to the **Estimate cost** page for {{site.data.keyword.powerSys_notm}}.

5. Select the location type from the **Location type** list as [**{{site.data.keyword.off-prem}}**](#off-prem-location-type) or [**{{site.data.keyword.on-prem}}**](#on-prem-location-type).

6. Select an IBM Cloud region from the **Location** list.
    For IBM {{site.data.keyword.powerSys_notm}} Private Cloud, select an IBM Cloud region that is near to your physical location or data center where the pod will reside.

7. In the Summary panel, click **Add to estimate** to review the configuration.

8. From the **Add product to estimate** list, select **Create new estimate**. Create new estimate panel is displayed.

9. Enter a name for the estimate in the **Name** field.

10. Optional: Enter a description for the estimate in the **Description (optional)** field.

11. Click **Create**. You are redirected to the Estimate panel.

12. Click **Save**.

13. Click **View estimate** to open the estimate in a new tab. You can use the **Action** menu to export the estimate in XLSX, CSV, or PDF format.


### Estimating {{site.data.keyword.powerSys_notm}} resources in an {{site.data.keyword.off-prem}}
{: #off-prem-location-type}

You can create an estimate for {{site.data.keyword.powerSys_notm}} resources in an {{site.data.keyword.off-prem}} where the infrastructure is hosted and managed by IBM.

If you select the **Location type** as **{{site.data.keyword.off-prem}}**, you can select one of the resources that are listed in the Estimate resource section. Refer to the following information to understand the fields that you are presented and their corresponding configurations:

* [Estimating a virtual server instance](#est-vsi)
* [Estimating a {{site.data.keyword.powerSys_notm}} instance with an {{site.data.keyword.ibmi-vst}}](#est-ibmi-vst)
* [Estimating SAP workloads](#est-sap-workloads)
* [Estimating a storage volume](#est-storage-vol)
* [Estimating a shared processor pool](#est-spp)
* [Estimating a virtual tape library](#est-vtl)
* [Estimating a dedicated host](#est-dh) 

The summary of the selected infrastructure is displayed in the **Summary** panel. You can review the total estimated cost per hour and per month that is displayed in the **Summary** panel. To add, save, and download the estimate, see [Adding, saving, and viewing an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate#creating-an-estimate).

#### Estimating a virtual server instance
{: #est-vsi}



The following table explains the fields that you can use to create an estimate for a virtual server instance in a {{site.data.keyword.powerSys_notm}} workspace:

| Field                              | Action                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Number of virtual servers          | Specify the number of virtual server instances that you want to estimate in a {{site.data.keyword.powerSys_notm}} workspace.                                                                                                                                                                                                                                                                                                                                |
| Operating system                   | Select an operating system from the list that meets your workload requirements.                                                                                                                                                                                                                                                                                                                                                                             |
| Configure for Epic workloads (AIX) | Select this checkbox if you want to deploy epic workloads on E980, E1080, or E1180 Power systems with Tier 1 storage and dedicated cores, at a shared-capped price. \n When you select this indicator, the other dependent fields are automatically filled. To learn more about epic workloads, see [Configuring a VM for Epic workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads){: external}. |
| Add to a shared processor pool     | Select this checkbox if you want to use shared processor pool. A shared processor pool is a pool of processor capacity that is shared between a group of virtual server instances (VM).                                                                                                                                                                                                                                                                     |
| Machine type                       | Select the required Power system from the list.                                                                                                                                                                                                                                                                                                                                                                                                             |
| Core type                          | Select the core type. The available options are: \n **Shared uncapped**: Shared among other clients. \n **Shared capped**: Shared, but resources do not expand beyond those that are requested (used mostly for licensing). \n **Dedicated**: Resources are allocated for a specific client (used for specific third-party considerations).                                                                                                                 |
| Cores                              | Specify the number of cores that you need. The minimum cores that you can specify is 0.25 for shared capped and shared uncapped core types. For dedicated core type, the minimum cores that you can specify is 1.                                                                                                                                                                                                                                           |
| Memory (GiB)                       | Specify the memory size. The minimum memory size that you can specify is 2 GiB.                                                                                                                                                                                                                                                                                                                                                                             |
| Storage tiers                      | Each estimated virtual server instance must have an associated boot volume. Total boot volume storage is multiplied by the number of estimated instances. You can choose from Tier 0, Tier 1, Tier 3, or Fixed IOPs. \n You cannot add a separate boot volume estimation. Hence, you must define the storage volume value by considering the boot volumes and data volume that you might need.                                                             |
{: caption="Fields and corresponding actions for estimating a VSI in Power Virtual Server" caption-side="top"}

You can perform the following actions based on the type of OS:

- **IBM i**: Assign an {{site.data.keyword.ibmi-vst}} to your instance to restrict the number of CPUs and the amount of memory that can be assigned to the instance. For more information, see [Estimating an IBM i workloads with {{site.data.keyword.ibmi-vst}}](#est-ibmi-vst).
- **Linux for SAP (HANA)**: Select an SAP certified profile. For more information, see [Estimating SAP workloads](#est-sap-workloads).


##### Estimating a {{site.data.keyword.powerSys_notm}} instance with an {{site.data.keyword.ibmi-vst}}
{: #est-ibmi-vst}

A virtual software tier limits the size of the virtual machines (VMs) for a particular pricing tier, but the tiers can run on any system. The {{site.data.keyword.ibmi-vst}} is used for the software pricing of operating system (OS) and IBM i licensed program products (LPP). When you assign an {{site.data.keyword.ibmi-vst}} to an instance, the number of CPUs and the amount of memory that can be assigned to the instance is restricted by the {{site.data.keyword.ibmi-vst}}. For more information, see [Assigning an IBM i software tier to an IBM i Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-ibmi-vsw-tiers#ibmi-vsw-system-types).

You can create an estimate of the {{site.data.keyword.powerSys_notm}} instance with an {{site.data.keyword.ibmi-vst}} before you deploy the instance. To assign an {{site.data.keyword.ibmi-vst}} to an IBM i {{site.data.keyword.powerSys_notm}} instance, meet the following prerequisites:

- IBM i image version is 7.3 or later
- VSN is assigned to the instance
- Machine type is IBM Power10 or later

The following table explains the fields that you can use to create a {{site.data.keyword.powerSys_notm}} instance with an IBM i software tier:

| Field                       | Action                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operating system            | Select **IBM i** from the **Operating system** list.                                                                                                                                                                                                                                                                                                                                                                                    |
| Version                     | Select the required IBM i version 7.3 or later from the **Version** list.                                                                                                                                                                                                                                                                                                                                                               |
| Virtual serial number (VSN) | Set **Virtual serial number (VSN)** to `Assigned` to assign a VSN to the instance.                                                                                                                                                                                                                                                                                                                                                      |
| IBM i Licenses              | Select the appropriate IBM i licenses. The available options are: \n – IBM i Cloud Storage Solution \n – IBM i Power HA \n – Rational Dev Studio for IBM i                                                                                                                                                                                                                                                                              |
| Machine type                | Select an IBM Power10 or later Power system from the list.                                                                                                                                                                                                                                                                                                                                                                              |
| Cores                       | Specify the number of cores that you need. The minimum cores that you can specify is 0.25 for shared capped and shared uncapped core types. For dedicated core type, the minimum cores that you can select is 1.                                                                                                                                                                                                                        |
| Memory (GiB)                | Specify the memory size. The minimum memory size that you can specify is 2 GiB.                                                                                                                                                                                                                                                                                                                                                         |
| Virtual serial number (VSN) | Select an option to assign VSN from the virtual serial number (VSN) pane. Select **Auto-assign** for the system to assign a VSN. Select **Select from retained VSNs** to assign a VSN from the list of retained VSNs.                                                                                                                                                                                                                   |
| IBM i software tier         | Based on the machine type, a list of supported {{site.data.keyword.ibmi-vst}}s is displayed. A text message with the recommended {{site.data.keyword.ibmi-vst}} is displayed after the **{{site.data.keyword.ibmi-vst}}** field based on the number of cores and memory size you select. You can select the recommended {{site.data.keyword.ibmi-vst}} from the **{{site.data.keyword.ibmi-vst}}** list or other options from the list. |
{: caption="Fields and corresponding actions for estimating a Power Virtual Server instance with IBM i software tier" caption-side="top"}











##### Estimating SAP workloads
{: #est-sap-workloads}

The following table explains the fields that you can use to create an estimate for a {{site.data.keyword.powerSys_notm}} instance with SAP workloads:

| Field                 | Action                                                                                                                                                                                                                            |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operating system      | - Select **Linux for SAP (HANA)** in the IBM provided subscription section to use the IBM provided Linux subscription.  \n - Select **Linux for SAP (HANA)** in the Client supplied subscription section to use your own license. |
| Linux image type      | Select the required Linux image type. Available options are SUSE and Red Hat Enterprise.                                                                                                                                          |
| Machine type          | \n - Select the required Power system from the list to deploy an SAP HANA profile.  \n - Select an IBM Power10 or later machine type from the list to deploy an SAP certified profile.                                            |
| Advance Configuration | Set **SAP RISE deployment** to on to estimate the cost of a {{site.data.keyword.powerSys_notm}} instance with an SAP certified profile -  Standard RISE or Application Server.                  |
| Profile               | Select an SAP HANA, a Standard RISE, or an Application Server profile.                                                                                                                                                            |
{: caption="Fields and corresponding actions for estimating an SAP workload in {{site.data.keyword.powerSys_notm}}" caption-side="top"}

The SAP certified profiles are available with IBM Power10 or later servers.
{: note}




To learn more on how to create an instance, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).


#### Estimating a storage volume
{: #est-storage-vol}

The following table explains the fields that you can use to create an estimate for a storage volume in a {{site.data.keyword.powerSys_notm}} workspace:

| Field              | Action                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------- |
| Number of volumes  | Specify the number of volumes that you need. The minimum number of volumes that you can specify is 1. |
| Tier               | Select Tier 0, Tier 1, Tier 3, or Fixed IOPs from the Tier list.                                      |
| Total storage (GB) | Specify the total storage. The minimum total storage that you can specify is 1 GB.                    |
{: caption="Fields and corresponding actions for estimating a storage volume in {{site.data.keyword.powerSys_notm}}" caption-side="top"}


#### Estimating a shared processor pool
{: #est-spp}

The following table explains the fields that you can use to create an estimate for a shared processor pool in a {{site.data.keyword.powerSys_notm}} workspace:

| Field           | Action                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------- |
| Number of pools | Specify the number of pools that you need. The minimum number of pools that you can specify is 1. |
| Machine type    | Select the required Power system from the list.                                                   |
| Reserved cores  | Specify the number of cores that you want to reserve.                                             |
{: caption="Fields and corresponding actions for estimating a shared processor pool in {{site.data.keyword.powerSys_notm}}" caption-side="top"}

To learn more about a shared processor pool, see [Managing a shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).



#### Estimating a virtual tape library
{: #est-vtl}

The following table explains the fields that you can use to create an estimate for a virtual tape library (VTL) in a {{site.data.keyword.powerSys_notm}} workspace:


| Field                             | Action                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Number of VTLs                    | Specify the number of virtual tape library instances that you need. The minimum number of VTL that you can specify is 1.                                                                                                                                                                                                                    |
| Licensed repository capacity (TB) | Specify the size of your repository capacity that determines which software license is needed. The minimum licensed repository capacity that you can specify is 1 TB.                                                                                                                                                                       |
| Machine type                      | Select the required Power system from the list.                                                                                                                                                                                                                                                                                             |
| Core type                         | Select the core type. The available options are: \n **Shared uncapped**: Shared among other clients. \n **Shared capped**: Shared, but resources do not expand beyond those that are requested (used mostly for licensing). \n **Dedicated**: Resources are allocated for a specific client (used for specific third-party considerations). |
| Cores                             | Specify the number of cores that you need. The minimum cores that you can specify is 0.25 for shared capped and shared uncapped core types. For dedicated core type, the minimum cores that you can select is 1.                                                                                                                            |
| Memory (GB)                       | Specify the memory size. The minimum memory size that you can specify is 2 GiB.                                                                                                                                                                                                                                                             |
| Storage tiers                     | Optional. You can click **Add volume +** to attach storage volumes to your estimate. You can choose from Tier 0, Tier 1, Tier 3, or Fixed IOPs.  \n You cannot add a separate boot volume estimation. Hence, enter the storage volume by considering the boot volumes and data volume that you might need.                                  |
{: caption="Fields and corresponding actions for estimating a virtual tape library (VTL) in {{site.data.keyword.powerSys_notm}}" caption-side="top"}

To learn more about virtual tape libraries, see [Managing a virtual tape library](/docs/power-iaas?topic=power-iaas-manage-vtl).



#### Estimating a dedicated host
{: #est-dh}

The following table explains the fields that you can use to create an estimate for a dedicated host in a {{site.data.keyword.powerSys_notm}} workspace:

| Field                     | Action                                                                                                |
| ------------------------- | ----------------------------------------------------------------------------------------------------- |
| Number of dedicated hosts | Specify the number of dedicated hosts that you want to reserve.                                       |
| Machine type              | From the list of available systems, select the Power system that you want to use as a dedicated host. |
{: caption="Fields and corresponding actions for estimating a dedicated host in {{site.data.keyword.powerSys_notm}}" caption-side="top"}


To learn more about dedicated host, see [Getting started with dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).




### Estimating {{site.data.keyword.powerSys_notm}} resources in a {{site.data.keyword.on-prem-lc}}
{: #on-prem-location-type}

You can create an estimate for {{site.data.keyword.powerSys_notm}} resources in a {{site.data.keyword.on-prem-lc}} where the physical infrastructure, including the IBM Power servers, are deployed and resides in the client's own data center, rather than in IBM's data centers.

If you select the **Location type** as **{{site.data.keyword.on-prem}}**, complete the following steps:

1. Specify the infrastructure requirements that include the machine type, number of systems, and storage capacity for your data center in the **Infrastructure configuration** section. The **Infrastructure overview** section displays the summary of the selected configuration. The pod size depends on the number of systems that you select including the total memory and the total number of cores that you plan to use in your data center.

    Currently, IBM Power S1122 (2U), IBM Power E1150 (4U), and IBM Power E1180 (12U) servers are supported by specific memory. Each server type is shipped with a fixed number of cores.

2. From the **Committed monthly spend** section, select the number of years from the **Contract commitment term** list. The **Committed monthly spend** value indicates the minimum monthly cost for your {{site.data.keyword.powerSys_notm}} pod.

    A longer contract commitment term reduces the minimum committed spend value. You can contact IBM to learn more about the possible savings with the commitment plans. Metered cost is determined based on the consumption and it is charged only when the consumption rate is greater than the minimum committed spend value.
    {: note}

3.  Click **Model consumption** to set the predicted consumption of the infrastructure configuration resources that you plan to use during the contract commitment term that you choose in the previous step. You can specify the predicted memory and core usage for each of the server types. You can also set the predicted storage capacity that you plan to use. After you set the predicted usage and reviewed the estimated metered (billing) cost, close the **Model metered consumption** window.

    The summary of estimated costs for the contract commitment years is displayed in the **Summary** panel based on your selection of predicted infrastructure resource usage. Metered consumption cost is only charged if the actual metered cost is greater than the **Minimum committed spend** value.

4.  Review the estimated cost in the **Summary** panel on the right side of the page. The estimated minimum cost includes the **Minimum committed spend** value and the billing charges, if any.

    The actual cost might increase based on your consumption rates.
    {: note}

5.  Click **Add to estimate** to create an estimate and export your configuration estimate. For instructions about creating an estimate, see [Creating an estimate](/docs/power-iaas?topic=power-iaas-generating-an-estimate#creating-an-estimate).


## Adding, saving, and viewing an estimate
{: #adding-an-estimate}

When you create the estimate, you can create and export the configuration estimate by completing the following steps:

1. Click **Add to estimate** in the **Summary** panel of the **Estimate Cost** page. The **Estimate** panel is displayed.

2. To add the cost information to an existing estimate, select an estimate from the **Add product to estimate** list. Alternatively, to create a new estimate, you can click **Create a new estimate** > specify a name and an optional description for the estimate > Click **Create**.

3. In the **Estimate** window, click **Save** to save the product to the selected or created estimate.

4. Click **View estimate** to view an estimate of your {{site.data.keyword.powerSys_notm}} configuration.

5. Click **Download** to export the saved estimate as an XLSX, a CSV, or a PDF file.


## Contacting IBM to place an order
{: #contacting-ibm}

Share the downloaded estimate with your IBM Business Partner to start the ordering process. Initiate the discussion to plan for your infrastructure configuration, data center requirements, to learn about possible savings plans, or to place your order.

If you do not work with an IBM Business Partner, contact IBM through email or the contact number that is specified on the window.

Before you place the order for IBM {{site.data.keyword.powerSys_notm}} Private Cloud, verify that the basic criteria to own a pod is met. For more information, see [Prerequisites for installing the pod](/docs/power-iaas?topic=power-iaas-pre_installation_checklist).
{: important}
