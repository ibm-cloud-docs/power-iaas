---

copyright:
  years:  2024
lastupdated: "2024-03-22"

keywords: IBM Power VS, Power VS monitoring, Sysdig for Power VS, monitoring a virtual server

subcollection: monitoring

content-type: tutorial
services: monitoring
account-plan: lite
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring a {{site.data.keyword.powerSysFull}} instance
{: #pvs-monitoring}
{: toc-content-type="tutorial"}
{: toc-services="monitoring"}
{: toc-completion-time="30m"}

Use this tutorial to learn how to configure a {{site.data.keyword.powerSys_notm}} instance to forward metrics to the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

For a list of collected metrics, see [{{site.data.keyword.powerSys_notm}} metrics dictionary](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-metrics-dictionary).

## Before you begin
{: #pvs_prereqs}

To get started, you can [read about {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

You must work in a supported region, for example the `US South` region.

Always use a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} {{site.data.keyword.IBM_notm}}ID, go to [Create an account](https://cloud.ibm.com/login){: external}.

Your {{site.data.keyword.IBM_notm}}ID must have assigned IAM policies for each of the following resources:

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **default**           |  Resource group            | Viewer  | `US South`  | This policy is required to allow the user to see service instances in the **default** resource group.    |
| {{site.data.keyword.mon_full_notm}} service |  Resource group            | Editor  | `US South`  | This policy is required to allow the user to provision and administer the {{site.data.keyword.mon_full_notm}} service in the **default** resource group.   |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"}

The {{site.data.keyword.cloud_notm}} CLI must be installed. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

## Provisioning an {{site.data.keyword.mon_full_notm}} instance
{: #pvs_step1}
{: step}

To provision an instance of {{site.data.keyword.mon_full_notm}} through the {{site.data.keyword.cloud_notm}} UI, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click **Catalog**. The list of the services that are available in {{site.data.keyword.cloud_notm}} opens.

3. To filter the list of services that is displayed, select the **Logging and Monitoring** category.

4. Click the **{{site.data.keyword.mon_full_notm}}** tile. The *Observability* dashboard opens.

5. Select the **Create** tab.

6. Select a region for the service instance.

7. Select the **Lite** service plan.

   By default, the **Lite** plan is set.

   For more information about other service plans, see [Pricing](/docs/monitoring?topic=monitoring-pricing_plans).

8. Enter a **Service name** for the service instance.

9. Select the **default** resource group.

   By default, the **default** resource group is set.

10. (Optional) Specify any [tags](/docs/account?topic=account-tag) that you want to use.

11. Select whether of not the service instance receives platform metrics for all service instances in the region.

12. To provision the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}} resource group where you are logged in, click **Create**.

After you provision an instance, the **Monitoring** dashboard opens.

**Note:** To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/monitoring?topic=monitoring-provision#provision_cli).

## Opening the monitoring UI
{: #pvs_step2}
{: step}

Complete the following steps to open the web UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**.

3. Select **Monitoring**.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select your instance. Then, click **Open dashboard**.

It can take some time before you see the server entry while the information is initially collected and processed by the monitoring agent.
{: note}

You can only monitor one instance per browser. You might have multiple tabs for the same instance.
{: tip}

## Viewing and monitoring your {{site.data.keyword.powerSys_notm}} instance
{: #pvs_step3}
{: step}

You can view and monitor your {{site.data.keyword.powerSys_notm}} instance by using the following methods:
- [Accessing metrics from Power Virtual Server workspace](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ui)
- [Accessing metrics from the Observability page](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ob)

See the [{{site.data.keyword.powerSys_notm}} metrics dictionary](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-metrics-dictionary) to learn about the various metrics that you can monitor.

## Next steps
{: #pvs_next_steps}

- Create a custom dashboard. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards#dashboards).

- Learn about alerts. For more information, see [Working with alerts](/docs/monitoring?topic=monitoring-monitoring#monitoring_alerts).

- Learn about the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} functions to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions, and compliance from source to run. See [Getting started with {{site.data.keyword.sysdigsecure_full}}](/docs/workload-protection?topic=workload-protection-getting-started).

- Learn about the [IBM Cloud monitoring limitations on {{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-limits) for {{site.data.keyword.powerSys_notm}}.