---

copyright:
  years: 2019, 2024

lastupdated: "2025-07-25"

keywords: sysdig metrics, Power VS, PowerVS metrics, IBM Cloud metrics

---

{{site.data.keyword.attribute-definition-list}}








# Monitoring metrics for IBM {{site.data.keyword.powerSys_notm}}
{: #monitor-sysdig}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

You can monitor platform metrics from resources in your {{site.data.keyword.powerSysFull}} workspace by enabling [{{site.data.keyword.mon_full}}](#sysdig-create-monitor) for basic platform metrics or by installing the [Cloud Monitoring agent for Linux operating systems](#monitor-agnt). The Linux based agent can fetch over 100 infrastructure metrics.
{: shortdesc}

{{site.data.keyword.mon_full_notm}} is an enterprise-grade monitoring service that is used for application visibility, alerting, and troubleshooting. {{site.data.keyword.mon_full_notm}} powered by Sysdig is used by enterprise development and IT teams that build, ship, and run business-critical applications at scale.








## Installing the {{site.data.keyword.mon_short}} agent for Linux VMs
{: #monitor-agnt}

You must provision the {{site.data.keyword.mon_full}} service instance in the {{site.data.keyword.cloud_notm}}. Then, you can deploy the {{site.data.keyword.mon_short}} agent on your Linux hosts in a {{site.data.keyword.powerSys_notm}} workspace to collect the data and metrics from the active VMs.

The {{site.data.keyword.mon_short}} can collect over 100 metrics that includes additional CPU, memory, file, file system, and network data points. The metrics that are collected from the VMs are routed to the Sysdig backend and then displayed on the Cloud Monitoring dashboards for the selected account. You can configure the metrics to be monitored in each environment. For more information about deploying, updating, and troubleshooting the agent, see [Managing the IBM Cloud Monitoring Linux agent on a PowerVS workspace](https://cloud.ibm.com/docs/monitoring?topic=monitoring-linux_powervs){: external}. For more information about configuring your environment for metrics, see [Monitoring Linux on a PowerVS workspace](https://cloud.ibm.com/docs/monitoring?topic=monitoring-powervs){: external}.

By default, the Linux based agent collects core infrastructure and network time series metrics. You can use the collected metrics to monitor the host. For more information about a list of collected metrics, see [Metrics Available for non-orchestrated environments](https://docs.sysdig.com/en/docs/installation/sysdig-agent/agent-configuration/configure-agent-modes/metrics-available-in-monitor-light/){: external}.

For more information about basic metrics, see [Platform metrics overview](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-ov).



## Integrating IBM Cloud Monitoring service with Power Virtual Server workspaces
{: #monitor-pvsw}



The IBM Cloud&reg; Monitoring system is a cloud-native and container-intelligence management system. You can gain operational visibility about the performance and health of your applications, services, and platforms through the IBM Cloud Monitoring system. It offers administrators, DevOps teams, and developers a full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. For more information, see [IBM Cloud Monitoring](https://cloud.ibm.com/docs/monitoring){: external}.


You can register a {{site.data.keyword.powerSys_notm}} workspace as an observability instance on the IBM Cloud Monitoring system. Integration costs are based on the usage and vary based on the hourly consumption for nodes and virtual machines. Review the cost that is associated with Monitoring in the IBM Cloud catalog. For more information about the costs associated with monitoring, see [Pricing](https://cloud.ibm.com/docs/monitoring?topic=monitoring-pricing_plans){: external}. You can review the estimated cost on the Summary page and generate an estimate before you enable the IBM Cloud Monitoring service. For more information about generating an estimate, see [Cloud Monitoring](https://cloud.ibm.com/observability/catalog/ibm-cloud-monitoring){: external}.


### Enabling IBM Cloud Monitoring in a Power Virtual Server workspace
{: #monitor-enable}

The **Monitoring** option is enabled by default when you create an {{site.data.keyword.off-prem-fname}} workspace.

To enable the IBM Cloud Monitoring service in an existing {{site.data.keyword.powerSys_notm}} workspace, complete the following steps:

1. Log in to the [IBM Cloud](https://cloud.ibm.com/login?state=%2Fpower%2Foverview) Power Virtual Server user interface.
2. Click **Workspaces** in the navigation panel.
3. Select a workspace on which you want to enable the IBM Cloud Monitoring service. The Workspace details pane is displayed.
4. Click **Monitoring** in the Integrations section to enable the IBM Cloud Monitoring service.
5. Click **View Monitoring** to view the monitoring metrics if the IBM Cloud Monitoring service is already enabled on the workspace.

For more information about the regions that support IBM Cloud Monitoring, see [Regions for IBM Cloud Monitoring](https://cloud.ibm.com/docs/monitoring?topic=monitoring-regions){: external}.





## Platform metrics overview
{: #sysdig-ov}
{: #platform_metrics}

You can view platform metrics for {{site.data.keyword.powerSys_notm}} after you create an {{site.data.keyword.mon_full_notm}} instance in the same region that is enabled for platform monitoring. For more information, see [Enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

Before you create an {{site.data.keyword.mon_full_notm}} instance on your platform, consider the following points:

* You can configure only one instance of the {{site.data.keyword.mon_full_notm}} service per region on your platform.
* To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the {{site.data.keyword.powerSys_notm}} instance is provisioned.
* Platform metrics are collected automatically and are available for monitoring through the {{site.data.keyword.mon_full_notm}}-enabled instance.


## Creating an {{site.data.keyword.mon_full_notm}} instance
{: #sysdig-create-monitor}

Create an {{site.data.keyword.mon_full_notm}} instance and enable the platform metrics to capture various performance metrics.

To create an {{site.data.keyword.mon_full_notm}} instance, complete the following steps:

To monitor platform metrics, select the region where your {{site.data.keyword.powerSys_notm}} workspace is provisioned.
{: important}

1. Log in to [IBM Cloud](https://cloud.ibm.com/login) console.
2. Search for **{{site.data.keyword.mon_full_notm}}** and select it.
3. Select your location and enter your custom values for **Service name** field and other fields.
4. Select the **Enable** indicator for **IBM platform metrics**.
5. Select the license agreements indicator and click **Create**.

You can also create the IBM Cloud monitoring instance from the **Integration (Optional)** section when you create a workspace, if no {{site.data.keyword.mon_full_notm}} instance is already created for that region.

## Viewing metrics
{: #sysdig-view}

To view the metrics dashboards, access the user interface of the {{site.data.keyword.mon_full_notm}} in the following ways:
- [Access the IBM Cloud monitoring user interface from your Power Systems Virtual Server workspace](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ui).
- [Access the IBM Cloud monitoring user interface from the **Observability** page](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ob).

To view metrics in your dashboard, you must enable the platform metrics of the {{site.data.keyword.mon_full_notm}} instance.
{: important}


### Accessing metrics from {{site.data.keyword.powerSys_notm}} workspace
{: #sysdig-view-ui}

From the navigation panel of the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:
1.  Click **workspaces**.
2.  Select the workspace for which a monitoring instance is available.
3.  From the **workspace details** page, click **Launch monitoring**.
      The {{site.data.keyword.mon_full_notm}} dashboard opens.
4.  Click **Dashboards** > **Dashboard Library** > **IBM** and select your dashboard to view.

### Accessing metrics from the **Observability** page.
{: #sysdig-view-ob}

To access the dashboard, complete the following steps:
1.  Log in to [IBM Cloud](https://cloud.ibm.com/login) console.
2.  Expand the navigation panel.
3.  Click **Resource list**.
4.  Click **Observability** **>** **Monitoring**.
5.  Click the instance.
6.  Click **Open dashboard**.
      The {{site.data.keyword.mon_full_notm}} dashboard opens.
7.  Click **Dashboards** > **Dashboard Library** > **IBM** and select your dashboard to view.

## {{site.data.keyword.powerSys_notm}} metrics dictionary
{: #sysdig-metrics-dictionary}

### CPU utilization
{: #cpu-metric}

The CPU utilization of a {{site.data.keyword.powerSys_notm}} instance in percentage.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_cpu_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 1: CPU utilization metrics of a VM" caption-side="top"}

### Memory utilization
{: #mem-metric}

The memory utilization of a {{site.data.keyword.powerSys_notm}} instance in percentage.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_mem_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 2: Memory utilization metrics of a VM" caption-side="top"}

### Incoming network bytes
{: #in-net-metric}

The incoming bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface (or per MAC address).

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_incoming_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`, `ibm_power_iaas_pvm_instance_network_mac_address`|
{: caption="Table 3: Incoming byte metrics of a VM per network interface " caption-side="top"}

### Outgoing network bytes
{: #out-net-metric}

The outgoing bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_outgoing_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`, `ibm_power_iaas_pvm_instance_network_mac_address`|
{: caption="Table 4: Outgoing byte metrics of a VM per network interface " caption-side="top"}

### Disk read bytes
{: #disk-rd-metric}

The total disk read bytes at {{site.data.keyword.powerSys_notm}} instance level.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_read_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 5: Total disk read bytes metrics at a VM" caption-side="top"}

### Disk write bytes
{: #disk-wrt-metric}

The total disks write bytes at {{site.data.keyword.powerSys_notm}} instance level.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_write_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 6: Total disk write bytes metrics at a VM" caption-side="top"}



## Attributes for segmentation
{: #sysdig-attributes}

See the global and additional attributes that are available for segmentation.

### Global attributes
{: #sysdig-attributes-global}

The following global attributes are available for segmenting all the metrics that are listed in the metrics dictionary:

| Metric label name | Metric description | Valid values |
|----------------|-----------------------|--------------|
| `ibm_ctype` | Type of Cloud    | `public`. |
| `ibm_location` | Location of the monitored resource | All the supported data center such as `WDC06` |
| `ibm_resource_group_name` | Resource group that is associated to the service instance. | All the resource groups that are available in your account |
| `ibm_scope` | The extent of the data samples that are considered.  | IBM Cloud account ID |
| `ibm_service_name` | Name of the service that generates this metric. | `power-iaas` |
{: caption="Table 7: Global segmentation attributes" caption-side="top"}

### Additional attributes
{: #sysdig-attributes-add}

The following additional attributes are available for segmenting all the metrics that are listed in the metrics dictionary:

| Metric label name | Metric description | Valid values |
|----------------|-----------------------|--------------|
| `ibm_service_instance` | The workspace ID | Power System {{site.data.keyword.powerSys_notm}} workspace ID |
| `ibm_service_instance_name` | The workspace name | Defined name of the workspace |
| `ibm_resource_type` | The type of {{site.data.keyword.powerSys_notm}} resource for which metric is available |  "pvm-instance" |
| `ibm_resource` | ID of a resource | "pvm-instance" ID |
| `ibm_resource_name` | Name of the resource | The name of the {{site.data.keyword.powerSys_notm}} instance |
| `ibm_power_iaas_pvm_instance_network_mac_address` | The MAC address of the network interface that is attached to the {{site.data.keyword.powerSys_notm}} instance | Valid mac address |
{: caption="Table 8: Additional segmentation attributes" caption-side="top"}

## IBM Cloud monitoring limitations
{: #sysdig-limits}

IBM Cloud Monitoring has the following limitations:

- The Ipv6 interface usage metrics of a {{site.data.keyword.powerSys_notm}} instance are for internal management network. Additionally, these metrics are available even though you did not configure it.
- When the memory utilization cannot be determined due to various reasons such as communication problem with the {{site.data.keyword.powerSys_notm}} instance, the memory utilizations can show 100%.
- The memory utilization is zero if the {{site.data.keyword.powerSys_notm}} instance is in a shut-off state.
- Metrics are available for {{site.data.keyword.powerSys_notm}} instance that are deleted. Based on the {{site.data.keyword.mon_full_notm}} retention policy, you can see the historical platform metrics of deleted instance. For more information, see [Sysdig documentation on retention limit](https://docs.sysdig.com/en/docs/administration/data-retention/#sysdig-monitor-metric-retention-limits){: external}.
- Metrics of {{site.data.keyword.powerSys_notm}} instances are not available if the instance was never initialized before, error in the instance, or issue with the host.


## Additional information
{: #sysdig-add-info}

- Learn more about the Sysdig dashboard user interface, see [About the Dashboard UI](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/){: external}.
- See the [IBM Cloud monitoring](/docs/monitoring?topic=monitoring-getting-started#getting-started) documentation in IBM Cloud.
- Refer to [sample pricing](/docs/monitoring?topic=monitoring-pricing_plans#pricing_example3) in IBM Cloud Monitoring documentation.
