---

copyright:
  years: 2019, 2023

lastupdated: "2023-10-04"

keywords: sysdig metrics, Power VS, PowerVS metrics, IBM Cloud metrics

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:preview: .preview}
{:external: target="_blank" .external}
{{site.data.keyword.attribute-definition-list}}
<!-- {{site.data.keyword.powerSys_notm}} - Power System Virtual Server-->
<!-- {{site.data.keyword.mon_full_notm}} - IBM Cloud Monitoring -->
<!-- {{site.data.keyword.cloud_notm}} - IBM Cloud -->


# Monitoring metrics for IBM {{site.data.keyword.powerSys_notm}}
{: #monitor-sysdig}

You can monitor platform metrics from resources in your {{site.data.keyword.powerSysFull}} workspace by using IBM Cloud® Monitoring dashboards. 
{:shortdesc}

{{site.data.keyword.mon_full_notm}} is a fully managed enterprise-grade monitoring service for application visibility, alerting, and troubleshooting. {{site.data.keyword.mon_full_notm}} with Sysdig is used by enterprise development and IT teams that build, ship, and run business-critical applications at scale.

Platform metrics for {{site.data.keyword.powerSys_notm}} are currently available in `WDC06`, `SYD05`, `WDC04`, and `DAL13`. As this feature is being sequentially rolled-out, support in other data centers will be available soon.
{: note}

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

You can also create the IBM Cloud monitoring instance from the **Integration (Optional)** section when you create a workspace, if no IBM Cloud monitoring instance is already created for that region.

## Viewing metrics
{: #sysdig-view}

The two different ways to access the {{site.data.keyword.mon_full_notm}} user interface to view the metrics dashboards are as follows:
- [Access the IBM Cloud monitoring user interface from your Power Systems Virtual Server workspace](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ui).
- [Access the IBM Cloud monitoring user interface from the **Observability** page](/docs/power-iaas?topic=power-iaas-monitor-sysdig#sysdig-view-ob).

To view metrics in your dashboard, you must enable the platform metrics of the {{site.data.keyword.mon_full_notm}} instance.
{: important}

### Accessing metrics from {{site.data.keyword.powerSys_notm}} workspace
{: #sysdig-view-ui}

From the left navigation menu of the {{site.data.keyword.powerSys_notm}} user interface, complete the following steps:
1.  Click **workspaces**.
2.  Select the workspace for which a monitoring instance is available.
3.  From the **workspace details** page, click **Launch monitoring**.
      The {{site.data.keyword.mon_full_notm}} dashboard opens.
4.  Click **Dashboards** > **Dashboard Library** > **IBM** and select your dashboard to view.

### Accessing metrics from the **Observability** page.
{: #sysdig-view-ob}

To access the dashboard, complete the following steps:
1.  Log in to [IBM Cloud](https://cloud.ibm.com/login) console.
2.  Expand the left navigation window.
3.  Click **Resource list**.
4.  Click **Observability** **>** **Monitoring**.
5.  Click the instance.
6.  Click **Open dashboard**.
      The {{site.data.keyword.mon_full_notm}} dashboard opens.
7.  Click **Dashboards** > **Dashboard Library** > **IBM** and select your dashboard to view.    

## {{site.data.keyword.powerSys_notm}} metrics dictionary
{: #sysdig-metrics-dictionary}

### CPU utilization
{: cpu-metric}

The CPU utilization of a {{site.data.keyword.powerSys_notm}} instance in percentage.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_cpu_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 1: CPU utilization metrics of a VM" caption-side="top"}

### Memory utilization
{: mem-metric}

The memory utilization of a {{site.data.keyword.powerSys_notm}} instance in percentage.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_mem_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 2: Memory utilization metrics of a VM" caption-side="top"}

### Incoming network bytes
{: in-net-metric}

The incoming bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface (or per MAC address).
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_incoming_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`, `ibm_power_iaas_pvm_instance_network_mac_address`|
{: caption="Table 3: Incoming byte metrics of a VM per network interface " caption-side="top"}

### Outgoing network bytes
{: out-net-metric}

The outgoing bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_outgoing_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`, `ibm_power_iaas_pvm_instance_network_mac_address`|
{: caption="Table 4: Outgoing byte metrics of a VM per network interface " caption-side="top"}

### Disk read bytes
{: disk-rd-metric}

The total disk read bytes at {{site.data.keyword.powerSys_notm}} instance level.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_read_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 5: Total disk read bytes metrics at a VM" caption-side="top"}

### Disk write bytes
{: disk-wrt-metric}

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
| `ibm_ctype` | Type of Cloud    | Valid value is `public`. |
| `ibm_location` | Location of the monitored resource | Valid values are all the supported data center such as `WDC06`. |
| `ibm_resource_group_name` | Resource group that is associated to the service instance. | Valid values are all the resource groups that are available in your account. |
| `ibm_scope` | The extent of the data samples that are considered.  | The valid value is the IBM Cloud account ID. |
| `ibm_service_name` | Name of the service that generates this metric. | The valid value is `power-iaas` |
{: caption="Table 7: Global segmentation attributes" caption-side="top"}

### Additional attributes
{: #sysdig-attributes-add}

The following additional attributes are available for segmenting all the metrics that are listed in the metrics dictionary:
| Metric label name | Metric description | Valid values |
|----------------|-----------------------|--------------|
| `ibm_service_instance` | The workspace ID | Valid value is the Power System {{site.data.keyword.powerSys_notm}} workspace ID |
| `ibm_service_instance_name` | The workspace name | Valid value is the defined name of the workspace |
| `ibm_resource_type` | The type of {{site.data.keyword.powerSys_notm}} resource for which metric is available | Currently valid value is "pvm-instance" |
| `ibm_resource` | ID of a resource | Currently valid value is the "pvm-instance" ID |
| `ibm_resource_name` | Name of the resource | Valid value is the name of the {{site.data.keyword.powerSys_notm}} instance |
| `ibm_power_iaas_pvm_instance_network_mac_address` | The MAC address of the network interface that is attached to the {{site.data.keyword.powerSys_notm}} instance | Valid mac address |
{: caption="Table 8: Additional segmentation attributes" caption-side="top"}

## IBM Cloud monitoring limitations
{: #sysdig-limits}

IBM Cloud Monitoring has the following limitations:

- When you exceed the predefined limits, the rate-limited requests respond with a `503 Service Unavailable` error.
- {{site.data.keyword.mon_full_notm}} accepts data within a specific time range that is called the window of acceptance that is fixed to 5 minutes.
- The {{site.data.keyword.powerSys_notm}} instance's Ipv6 interface usage metrics is for internal management network and are available additionally even though you did not configure it.
- When the memory utilization cannot be determined due to various reasons such as communication problem with the {{site.data.keyword.powerSys_notm}} instance, the memory utilizations can show 100%.
- The memory utilization is zero if the {{site.data.keyword.powerSys_notm}} instance is in a shut-off state.
- Metrics are available for {{site.data.keyword.powerSys_notm}} instance that are deleted. Based on the {{site.data.keyword.mon_full_notm}} retention policy, you can see the historical platform metrics of deleted instance. For more information, see [Sysdig documentation on retention limit](https://docs.sysdig.com/en/docs/administration/data-retention/#sysdig-monitor-metric-retention-limits){: external}.
- Metrics of {{site.data.keyword.powerSys_notm}} instances are not available if the instance was never initialized before, error in the instance, or issue with the host.


## Additional information
{: #sysdig-add-info}

- Learn more about the Sysdig dashboard user interface, see [About the Dashboard UI](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/using-dashboards/about-the-dashboard-ui/){: external}.
- See the [IBM Cloud monitoring](/docs/monitoring?topic=monitoring-getting-started#getting-started) documentation in IBM Cloud.
- Refer to [sample pricing](/docs/monitoring?topic=monitoring-pricing_plans#pricing_example3) in IBM Cloud Monitoring documentation.