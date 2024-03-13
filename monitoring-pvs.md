---

copyright:
  years:  2024
lastupdated: "2024-03-13"

keywords:

subcollection: monitoring

content-type: tutorial
services: monitoring
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring a {{site.data.keyword.powerSysFull}} instance
{: #pvs-monitoring}
{: toc-content-type="tutorial"}
{: toc-services="monitoring"}
{: toc-completion-time="1h"}

Use this tutorial to learn how to configure a {{site.data.keyword.powerSys_notm}} instance to forward metrics to the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

To cconfigure a {{site.data.keyword.powerSys_notm}} instance to forward metrics, you must install a monitoring agent. The agent uses an access key (token) to authenticate with the {{site.data.keyword.mon_full_notm}} instance. The monitoring agent acts as a data collector. It automatically collects metrics.

By default, this agent collects core infrastructure and network time series that you can use to monitor the host. For a list of collected metrics, see [{{site.data.keyword.powerSys_notm}} metrics dictionary](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-metrics-dictionary).

The {{site.data.keyword.mon_short}} agent automatically collects the following types of system metrics per host:

- `System hosts metrics` provide information about CPU, memory, and storage usage metrics, that you can use to analyze the performance and resource utilization of all your processes.

- `File and File System metrics` provide information about files and file system that you can use to analyze file interactions that occur in your system. For example, you can find information about your open files, bytes going in and out, or the percentage of usage of a given file system.

- `Process metrics` provide information about the processes that run in your servers. For example, you can use these metrics to  explore the number of processes, or get client or server information.

- `Network metrics` provide information about the network. They offer insight to the connections that are established between your applications, containers, and servers. For example, you can find information about the bytes that are being sent or received, or the number of HTTP requests, connections, and latency. In addition, for SQL or MongoDB, the agent collects additional information when it is configured in troubleshooting mode.

Through the {{site.data.keyword.mon_short}} UI, you can analyze data in the *Advisor* tab, the *Explore* tab, and in the *Dashboard* tab. You monitor the data through metric views and dashboards.
{: shortdesc}

Consider the following information when monitoring your data:
* In the *Explorer* tab, you can monitor individual metrics.
* In the *Advisor* tab, you can monitor {{site.data.keyword.redhat_openshift_notm}} or host level metrics.

    This tab is only available for users that belong to a team that has access to monitor {{site.data.keyword.redhat_openshift_notm}} or host level metrics.
    {: note}

* In the *Dashboard* tab, you can monitor through panels predefined dashboards or custom ones and get a specialized insight into network data, application data, topology, services, hosts, and containers. A panel displays a metric or group of metrics in a dashboard.


For each metric view and dashboard, you can define the scope of the data, how to aggregate data, and what time and group filters to apply to the data. For more information, see [Managing panels](/docs/monitoring?topic=monitoring-panels).


You can configure a dashboard as the default entry point for a team, unifying a team's experience, and allowing users to focus their immediate attention on the most relevant information for them.
{: tip}

For more information, see [Viewing metrics](/docs/monitoring?topic=monitoring-monitoring).



## Before you begin
{: #pvs_prereqs}

[Read about {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

Work in a supported region, for example the `US South` region.

Use a user ID that is a member or an owner of an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} {{site.data.keyword.IBM_notm}}ID, go to [Create an account](https://cloud.ibm.com/login){: external}.

Your {{site.data.keyword.IBM_notm}}ID must have assigned IAM policies for each of the following resources:

| Resource                             | Scope of the access policy | Role    | Region    | Information                  |
|--------------------------------------|----------------------------|---------|-----------|------------------------------|
| Resource group **default**           |  Resource group            | Viewer  | `US South`  | This policy is required to allow the user to see service instances in the **default** resource group.    |
| {{site.data.keyword.mon_full_notm}} service |  Resource group            | Editor  | `US South`  | This policy is required to allow the user to provision and administer the {{site.data.keyword.mon_full_notm}} service in the **default** resource group.   |
{: caption="Table 1. List of IAM policies required to complete the tutorial" caption-side="top"}

The {{site.data.keyword.cloud_notm}} CLI must be installed. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

## Provision a {{site.data.keyword.powerSys_notm}} instance
{: #pvs_step1}
{: step}

Follow the steps mentioned in the {{site.data.keyword.powerSys_notm}} documentation on [Configuring a Power Virtual Server instance](https://test.cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

## Provision an {{site.data.keyword.mon_full_notm}} instance
{: #pvs_step2}
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

10. (Optional) Specify any [tags](/docs/account?topic=account-tag) you want to use.

11. Select whether of not the service instance receives platform metrics for all service instances in the region.

12. To provision the {{site.data.keyword.mon_full_notm}} service in the {{site.data.keyword.cloud_notm}} resource group where you are logged in, click **Create**.

After you provision an instance, the **Monitoring** dashboard opens.

**Note:** To provision an instance through the CLI, see [Provisioning an instance through the {{site.data.keyword.cloud_notm}} CLI](/docs/monitoring?topic=monitoring-provision#provision_cli).

## Launch the monitoring UI
{: #pvs_step3}
{: step}

Complete the following steps to launch the web UI:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

   After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} Dashboard opens.

2. In the navigation menu, select **Observability**.

3. Select **Monitoring**.

   The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select your instance. Then, click **Open dashboard**.

IIt may take some time before you see the server entry while the information is initally collected and processed by the monitoring agent.
{: note}

You only can monitor one instance per browser. You could have multiple tabs for the same instance.
{: tip}


## View and monitor your {{site.data.keyword.powerSys_notm}} instance
{: #pvs_step4}
{: step}

You can view and monitor your {{site.data.keyword.powerSys_notm}} instance using the following methods:
- [Accessing metrics from Power Virtual Server workspace](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ui)
- [Accessing metrics from the Observability page](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ob)

See the [{{site.data.keyword.powerSys_notm}} metrics dictionary](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-metrics-dictionary) to learn about the various metrices that you can monitor.

## Next steps
{: #pvs_next_steps}

- Create a custom dashboard. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards#dashboards).

- Learn about alerts. For more information, see [Working with alerts](/docs/monitoring?topic=monitoring-monitoring#monitoring_alerts).

- Learn about the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} functionality to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions and compliance from source to run. See [Getting started with {{site.data.keyword.sysdigsecure_full}}](/docs/workload-protection?topic=workload-protection-getting-started).

- Learn about the [IBM Cloud monitoring limitations](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-limits) for {{site.data.keyword.powerSys_notm}}.