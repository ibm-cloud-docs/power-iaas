---

copyright:
  years: 2025

lastupdated: "2025-11-14"

keywords: estimate price, estimate, generating an estimate, {{site.data.keyword.powerSys_notm}}, private cloud, creating estimate, saving estimate, estimate virtual server instance, estimate storage volume, estimate shared processor pool, estimate VPN, estimate virtual tape library

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Creating an estimate for {{site.data.keyword.powerSys_notm}} resources in a {{site.data.keyword.on-prem-lc}}
{: #creating-an-estimate-private}
{: help}
{: support}

You can use the [cost estimator](https://cloud.ibm.com/power/estimate){: external} to estimate the cost of the {{site.data.keyword.powerSysFull}} resources before you deploy them in a {{site.data.keyword.on-prem-lc}} where the infrastructure is hosted and managed by IBM.
{: shortdesc}

You can create an estimate by selecting the required compute and storage configurations based on your business requirement. Based on your selection and configuration, you can view the estimated cost of your {{site.data.keyword.powerSys_notm}} private cloud infrastructure. You can connect with your IBM Business Partner or contact IBM to place your order.

You are not charged for creating an estimate. The resources that you estimate can be deployed only after a workspace is created.
{: note}

## Estimating {{site.data.keyword.powerSys_notm}} infrastructure in a {{site.data.keyword.on-prem-lc}}
{: #off-prem-location-type}

To create an estimate for {{site.data.keyword.powerSys_notm}} infrastructure in a {{site.data.keyword.on-prem-lc}}, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog){: external} with your IBM credentials.

2. Search for **{{site.data.keyword.powerSys_notm}}** in the search box for IBM Cloud catalog.

3. Click the **{{site.data.keyword.powerSys_notm}}** tile.

4. Click **Estimate Cost**. You are redirected to the **Estimate cost** page for {{site.data.keyword.powerSys_notm}}.

5. Select **Client location** from the **Location type** list.

6. Select an IBM Cloud region that is near to your physical location from the **Location** list.

7. In the **Pricing plan** section, select the pricing plan that best suits your workloads. The available options are:

    - **Metered**: The metered pricing plan meters costs hourly for the allocated resources on a monthly basis and the workloads can scale to the full capacity of the infrastructure. However, the metered plan does not support SAP workloads.

    - **Subscription**: The subscription pricing plan provides a monthly subscription with access to 100% of the infrastructure capacity. The capacity is not metered. The subscription plan is best suited for SAP HANA and SAP NetWeaver workloads. However, the subscription plan does not support AIX or IBM i workloads. To use the subscription pricing plan, contact [IBM sales](https://www.ibm.com/products?contactmodule){: external} or your IBM Business Partner representative.

8. In the **Infrastructure configuration** section, specify the infrastructure requirements, such as the machine type, number of systems, memory per system, and the number and type of storage controllers. The **Infrastructure overview** section displays the summary of the selected configuration. The *Deployment size* depends on the machine type, memory per system, and number of systems that you select.

    Currently, IBM Power S1122 (2U), IBM Power E1150 (4U), and IBM Power E1180 (12U) servers are supported by specific memory. Each server type is shipped with a fixed number of cores.

    Machine types cannot be mixed within a rack, and all systems must have the same amount of memory.
    {: note}

9. In the **Committed monthly spend** section, select the number of years from the **Contract commitment term** list. The **Committed monthly spend** value indicates the minimum monthly cost for your {{site.data.keyword.powerSys_notm}} pod.

    A longer contract commitment term reduces the minimum committed spend value. You can contact IBM to learn more about the possible savings with the commitment plans. Metered cost is determined based on the consumption and it is charged only when the consumption rate is greater than the minimum committed spend value.
    {: note}

10. In the **Metered consumption cost** section, click **Model consumption** to set the predicted consumption of the configured infrastructure resources that you plan to use during the contract commitment term. You can specify the predicted memory and core usage for each of the server types. You can also set the predicted storage capacity that you plan to use. After you set the predicted usage and reviewed the estimated metered cost, close the **Model metered consumption on configured infrastructure** window.

    The **Summary** panel displays the estimated costs for the contract commitment years based on your selection of predicted infrastructure resource usage. Metered consumption cost is charged only when the actual metered cost exceeds the **Committed monthly spend** value.

11. In the Summary panel, review the estimated cost and click **Add to estimate**. The **Estimate** panel is displayed.

12. From the **Add product to estimate** list, select **Create new estimate**. The Create new estimate panel is displayed.

13. Enter a name for the estimate in the **Name** field.

14. Optional: Enter a description for the estimate in the **Description (optional)** field.

15. Click **Create**. You are redirected to the Estimate panel.

16. Click **Save**.

17. Click **View estimate** to open the estimate in a new tab. You can use the **Action** menu to export the estimate in XLSX, CSV, or PDF format.

## Contacting IBM to place an order for {{site.data.keyword.powerSys_notm}} Private Cloud in a {{site.data.keyword.on-prem-lc}}
{: #contacting-ibm-private}

To begin the ordering process for IBM Power Virtual Server through an IBM Business Partner, complete the following steps:

1. Share the downloaded estimate with your IBM Business Partner.
2. Initiate a discussion with the partner to:
   - Plan your infrastructure configuration
   - Define data‑center requirements
   - Explore possible savings plans
   - Finalize the order

If you do not work with an IBM Business Partner, contact IBM through email or [book a meeting](https://www.ibm.com/solutions/cloud?schedulerform){: external} with an IBM expert.

Before you place the order for IBM {{site.data.keyword.powerSys_notm}} Private Cloud, verify that the basic criteria to own a pod is met. For more information, see [Prerequisites for installing the pod](/docs/power-iaas?topic=power-iaas-pre_installation_checklist).
{: important}
