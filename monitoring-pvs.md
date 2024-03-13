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

By default, this agent collects core infrastructure and network time series that you can use to monitor the host. For a list of collected metrics, see [Metrics Available for non-orchestrated environments](https://docs.sysdig.com/en/docs/installation/sysdig-agent/agent-configuration/configure-agent-modes/metrics-available-in-monitor-light/).

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

Follow the steps mentioned in the P documentation on [Configuring a Power Virtual Server instance](https://test.cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).

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

## Configure your {{site.data.keyword.powerSys_notm}} instance to send metrics to your instance
{: #pvs_step3}
{: step}

To configure your {{site.data.keyword.powerSys_notm}} instance to send metrics to your {{site.data.keyword.mon_full_notm}} instance, you must install a monitoring agent.

Complete the following steps from a command line:

1. Open a terminal. Then, log in to the {{site.data.keyword.cloud_notm}}. Run the following command and follow the prompts:

   ```text
   ibmcloud login -a cloud.ibm.com
   ```
   {: pre}

   Select the account and region where the {{site.data.keyword.mon_full_notm}} instance is available.

2. Access your {{site.data.keyword.powerSys_notm}} instance.

3. Obtain the access key. For more information, see [Getting the access key through the {{site.data.keyword.cloud_notm}} UI](/docs/monitoring?topic=monitoring-access_key#access_key_ibm_cloud_ui).

4. Obtain the ingestion URL. For more information, see [collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

5. Deploy the monitoring agent. Run the following command:

   ```text
   curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key <ACCESS_KEY> --collector <COLLECTOR_ENDPOINT> --collector_port 6443 --secure true --check_certificate false --tags <TAG_DATA> --additional_conf 'sysdig_capture_enabled: false'
   ```
   {: pre}

   Where

   * ACCESS_KEY is the [access key](/docs/monitoring?topic=monitoring-access_key) for the instance.

   * COLLECTOR_ENDPOINT is the ingestion URL for the region where the monitoring instance is available.  To determine the endpoint, see [Collector endpoints](/docs/monitoring?topic=monitoring-endpoints#endpoints_ingestion).

   * TAG_DATA are comma-separated tags that are formatted as `TAG_NAME:TAG_VALUE`. You can associate one or more tags to your monitoring agent. For example, `role:serviceX,location:us-south`. Later on, you can use these tags to identify metrics from the environment where the agent is running.

   * The `sysdig_capture_enabled` is set to *false* to disable the capture feature. By default this is set to *true*. For more information, see [Working with captures](/docs/monitoring?topic=monitoring-captures#captures).

   * The `secure` flag must be set to *true* to use a secure SSL/TLS connection to send metrics to the collector.

   If the monitoring agent fails to install correctly, install the kernel headers manually. Choose a distribution and run the command for that distribution. Then, retry the deployment of the monitoring agent.


   * **For Debian and Ubuntu Linux distributions**, run the following command:

      ```text
      apt-get -y install linux-headers-$(uname -r)
      ```
      {: pre}

   * **For RHEL, CentOS, and Fedora Linux distributions**, run the following command:

      ```text
      yum -y install kernel-devel-$(uname -r)
      ```
      {: pre}

6. Configure the agent for non-orchestrated environments.

    Open the `dragent.yaml` file that is located in `/opt/draios/etc/`.

    Add the following configuration parameter:

    ```yaml
    feature:
      mode: monitor_light
    ```
    {: codeblock}

    Restart the agent. Run the following command:

    ```sh
    service dragent restart
    ```
    {: pre}


## Launch the monitoring UI
{: #pvs_step4}
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


## Monitor your {{site.data.keyword.powerSys_notm}} instance
{: #pvs_step5}
{: step}

You can monitor your Ubuntu server in the **Overview** view that is available through the Web UI. This view is your starting point to troubleshoot and monitor your infrastructure. It is the default homepage of the Web UI.

In the section **Hosts & containers**, you can find the entry for your Ubuntu server. Click **Hosts & containers** ![Hosts & containers](../images/switch_hosts.png) to switch data sources. Then, select your Ubuntu server. The data that is displayed corresponds to the selected server.

To configure color-coding for a column, complete the following steps:

1. Select a column by hovering your mouse over the column title. Then, click the pencil icon.

2. Toggle **Enable** to enable color-coding.

3. Set values for the different thresholds.

## Next steps
{: #pvs_next_steps}

- Create a custom dashboard. For more information, see [Working with dashboards](/docs/monitoring?topic=monitoring-dashboards#dashboards).

- Learn about alerts. For more information, see [Working with alerts](/docs/monitoring?topic=monitoring-monitoring#monitoring_alerts).

- Learn how to manage logs. See [Logging with Linux VPC server instances](/docs/log-analysis?topic=log-analysis-ubuntu).

- Learn about the {{site.data.keyword.mon_full_notm}} {{site.data.keyword.sysdigsecure_short}} functionality to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions and compliance from source to run. See [Getting started with {{site.data.keyword.sysdigsecure_full}}](/docs/workload-protection?topic=workload-protection-getting-started).