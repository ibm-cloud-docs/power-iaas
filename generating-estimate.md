---

copyright:
  years: 2025

lastupdated: "2025-11-14"

keywords: estimate price, estimate, generating an estimate, {{site.data.keyword.powerSys_notm}}, private cloud, creating estimate, saving estimate, estimate virtual server instance, estimate storage volume, estimate shared processor pool, estimate VPN, estimate virtual tape library

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# Creating an estimate for {{site.data.keyword.powerSys_notm}} resources in an {{site.data.keyword.off-prem}}
{: #creating-an-estimate-public}
{: help}
{: support}

Before you deploy a {{site.data.keyword.powerSys_notm}} with cloud resources, such as virtual server instances, storage volumes, shared processor pools, virtual tape libraries, or dedicated hosts, it is important that you create an estimate to understand the associated costs. You can use the [cost estimator](https://cloud.ibm.com/power/estimate){: external} to estimate the cost of the {{site.data.keyword.powerSysFull}} resources before you deploy them in an IBM data center or in a {{site.data.keyword.on-prem-lc}}.
{: shortdesc}

You can create an estimate by specifying the parameters for your {{site.data.keyword.powerSys_notm}} resources. You can customize the resource quantities based on your business requirement and view the estimated cost. Based on your selection, you can view the estimated cost of your {{site.data.keyword.powerSys_notm}} resources. You can connect with your IBM Business Partner or contact IBM to place your order.

You are not charged for creating an estimate. The resources that you estimate can be deployed only after a workspace is created.
{: note}

## Estimating {{site.data.keyword.powerSys_notm}} resources in an {{site.data.keyword.off-prem}}
{: #off-prem-location-type}

You can create an estimate for {{site.data.keyword.powerSys_notm}} resources in an {{site.data.keyword.off-prem}} where the infrastructure is hosted and managed by IBM. To create an estimate, complete the following steps:


1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. Search for **{{site.data.keyword.powerSys_notm}}** in the search box for IBM Cloud catalog.

3. Click the **{{site.data.keyword.powerSys_notm}}** tile.

4. Click **Estimate Cost**. You are redirected to the **Estimate cost** page for {{site.data.keyword.powerSys_notm}}.

5. Select **{{site.data.keyword.off-prem}}** from the **Location type** list.

6. Select an IBM Cloud region from the **Location** list.

7. From the **Estimate resource** section, select one of the following resources to learn about the available options and fields for generating an estimate. Each section provides detailed guidance to help you configure the resources based on your business needs. After reviewing the relevant section, return here to continue with the estimation process.

    * [Estimating a virtual server instance](#est-vsi)
    * [Estimating a {{site.data.keyword.powerSys_notm}} instance with an {{site.data.keyword.ibmi-vst}}](#est-ibmi-vst)
    * [Estimating SAP workloads](#est-sap-workloads)
    * [Estimating a storage volume](#est-storage-vol)
    * [Estimating a shared processor pool](#est-spp)
    * [Estimating a virtual tape library](#est-vtl)
    * [Estimating a dedicated host](#est-dh) 

8. In the Summary panel, review the estimated cost and click **Add to estimate**. The **Estimate** panel is displayed.

9. From the **Add product to estimate** list, select **Create new estimate**. The Create new estimate panel is displayed.

10. Enter a name for the estimate in the **Name** field.

11. Optional: Enter a description for the estimate in the **Description (optional)** field.

12. Click **Create**. You are redirected to the Estimate panel.

13. Click **Save**.

14. Click **View estimate** to open the estimate in a new tab. You can use the **Action** menu to export the estimate in XLSX, CSV, or PDF format.

### Estimating a virtual server instance
{: #est-vsi}



The following table explains the fields that you can use to create an estimate for a virtual server instance in a {{site.data.keyword.powerSys_notm}} workspace:

| Field                              | Action                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Number of virtual servers          | Specify the number of virtual server instances that you want to estimate in a {{site.data.keyword.powerSys_notm}} workspace.                                                                                                                                                                                                                                                                                                                                |
| Operating system                   | Select an operating system from the list that meets your workload requirements.                                                                                                                                                                                                                                                                                                                                                                             |
| Configure for Epic workloads (AIX) | Select this checkbox if you want to deploy epic workloads on E980, E1080, or E1180 Power Systems with Tier 1 storage and dedicated cores, at a shared-capped price. \n When you select this indicator, the other dependent fields are automatically filled. To learn more about epic workloads, see [Configuring a VM for Epic workloads](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-a-vm-for-epic-workloads){: external}. |
| Add to a shared processor pool     | Select this checkbox if you want to use shared processor pool. A shared processor pool is a pool of processor capacity that is shared between a group of virtual server instances (VM).                                                                                                                                                                                                                                                                     |
| Machine type                       | Select the required Power system from the list.                                                                                                                                                                                                                                                                                                                                                                                                             |
| Core type                          | Select the core type. The available options are: \n - **Shared uncapped**: Shared among other clients. \n - **Shared capped**: Shared, but resources do not expand beyond those that are requested (used mostly for licensing). \n - **Dedicated**: Resources are allocated for a specific client (used for specific third-party considerations).                                                                                                                 |
| Cores                              | Specify the number of cores that you need. The minimum cores that you can specify is 0.25 for shared capped and shared uncapped core types. For dedicated core type, the minimum cores that you can specify is 1.                                                                                                                                                                                                                                           |
| Memory (GiB)                       | Specify the memory size. The minimum memory size that you can specify is 2 GiB.                                                                                                                                                                                                                                                                                                                                                                             |
| Storage tiers                      | Each estimated virtual server instance must have an associated boot volume. Total boot volume storage is multiplied by the number of estimated instances. You can choose from Tier 0, Tier 1, Tier 3, or Fixed IOPs. \n You cannot add a separate boot volume estimation. Hence, you must define the storage volume value by considering the boot volumes and data volume that you might need.                                                             |
{: caption="Fields and corresponding actions for estimating a VSI in Power Virtual Server" caption-side="top"}

You can perform the following actions based on the type of OS:

- **IBM i**: Assign an {{site.data.keyword.ibmi-vst}} to your instance to restrict the number of CPUs and the amount of memory that can be assigned to the instance. For more information, see [Estimating an IBM i workloads with {{site.data.keyword.ibmi-vst}}](#est-ibmi-vst).
- **Linux for SAP (HANA)**: Select an SAP certified profile. For more information, see [Estimating SAP workloads](#est-sap-workloads).


### Estimating a {{site.data.keyword.powerSys_notm}} instance with an {{site.data.keyword.ibmi-vst}}
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











### Estimating SAP workloads
{: #est-sap-workloads}

The following table explains the fields that you can use to create an estimate for a {{site.data.keyword.powerSys_notm}} instance with SAP workloads:

| Field                 | Action                                                                                                                                                                                                                            |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operating system      | - Select **Linux for SAP (HANA)** in the IBM provided subscription section to use the IBM provided Linux subscription.  \n - Select **Linux for SAP (HANA)** in the Client supplied subscription section to use your own license. |
| Linux image type      | Select the required Linux image type. Available options are SUSE and Red Hat Enterprise.                                                                                                                                          |
| Machine type          | \n - Select the required Power system from the list to deploy an SAP HANA profile.  \n - Select an IBM Power10 or later machine type from the list to deploy an SAP certified profile.                                            |
| Advance Configuration | Set **SAP RISE deployment** to on to estimate the cost of a {{site.data.keyword.powerSys_notm}} instance with an SAP certified profile -  Standard RISE or Application Server.                                   |
| Profile               | Select an SAP HANA, a Standard RISE, or an Application Server profile.                                                                                                                                                            |
{: caption="Fields and corresponding actions for estimating an SAP workload in {{site.data.keyword.powerSys_notm}}" caption-side="top"}

The SAP certified profiles are available with IBM Power10 or later servers.
{: note}





To learn more on how to create an instance, see [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).


### Estimating a storage volume
{: #est-storage-vol}

The following table explains the fields that you can use to create an estimate for a storage volume in a {{site.data.keyword.powerSys_notm}} workspace:

| Field              | Action                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------- |
| Number of volumes  | Specify the number of volumes that you need. The minimum number of volumes that you can specify is 1. |
| Tier               | Select Tier 0, Tier 1, Tier 3, or Fixed IOPs from the Tier list.                                      |
| Total storage (GB) | Specify the total storage. The minimum total storage that you can specify is 1 GB.                    |
{: caption="Fields and corresponding actions for estimating a storage volume in {{site.data.keyword.powerSys_notm}}" caption-side="top"}


### Estimating a shared processor pool
{: #est-spp}

The following table explains the fields that you can use to create an estimate for a shared processor pool in a {{site.data.keyword.powerSys_notm}} workspace:

| Field           | Action                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------- |
| Number of pools | Specify the number of pools that you need. The minimum number of pools that you can specify is 1. |
| Machine type    | Select the required Power system from the list.                                                   |
| Reserved cores  | Specify the number of cores that you want to reserve.                                             |
{: caption="Fields and corresponding actions for estimating a shared processor pool in {{site.data.keyword.powerSys_notm}}" caption-side="top"}

To learn more about a shared processor pool, see [Managing a shared processor pool](/docs/power-iaas?topic=power-iaas-manage-SPP).



### Estimating a virtual tape library
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



### Estimating a dedicated host
{: #est-dh}

The following table explains the fields that you can use to create an estimate for a dedicated host in a {{site.data.keyword.powerSys_notm}} workspace:

| Field                     | Action                                                                                                |
| ------------------------- | ----------------------------------------------------------------------------------------------------- |
| Number of dedicated hosts | Specify the number of dedicated hosts that you want to reserve.                                       |
| Machine type              | From the list of available systems, select the Power system that you want to use as a dedicated host. |
{: caption="Fields and corresponding actions for estimating a dedicated host in {{site.data.keyword.powerSys_notm}}" caption-side="top"}


To learn more about dedicated host, see [Getting started with dedicated host](/docs/power-iaas?topic=power-iaas-dedicated-host).




## Contacting IBM to place an order
{: #contacting-ibm}

To begin the ordering process for IBM Power Virtual Server through an IBM Business Partner, complete the following steps:

1. Share the downloaded estimate with your IBM Business Partner.
2. Initiate a discussion with the partner to:
   - Plan your infrastructure configuration
   - Define data‑center requirements
   - Explore possible savings plans
   - Finalize the order

If you do not work with an IBM Business Partner, contact IBM through email or [book a meeting](https://www.ibm.com/solutions/cloud?schedulerform){: external} with an IBM expert.
