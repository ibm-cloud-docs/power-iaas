---

copyright:
  years: 2019, 2023

lastupdated: "2023-09-14"

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
<!-- {{site.data.keyword.powerSys_notm}} -->



# Monitoring metrics for {{site.data.keyword.powerSys_notm}}
{: #monitor-sysdig}

You can monitor various platform metrics of {{site.data.keyword.powerSysFull}} with IBM Cloud® Monitoring dashboards that are operated by Sysdig in partnership with IBM.
{:shortdesc}

{{site.data.keyword.mon_full_notm}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Measure the platform metrics such as compute, storage, networks at a {{site.data.keyword.powerSys_notm}} instance level.

The data center that sysdig currently supports are `WDC06`, `SYD05`, `WDC04`, and `DAL13`.
{: note}

## Platform metrics overview
{: #sysdig-ov}
{: #platform_metrics}

You can view platform metrics when you enable {{site.data.keyword.mon_full_notm}} on your IBM Cloud platform. A monitoring instance must be configured in a region to monitor these metrics. For more information, see [Enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

Before you enable {{site.data.keyword.mon_full_notm}} on your platform, consider the following points:

* You can configure only one instance of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics.
* Platform metrics are regional. Metrics are monitored only from {{site.data.keyword.mon_full_notm}} services, which are in the same region of the instance that you want to monitor.
* Metrics are collected automatically and are available for monitoring through the {{site.data.keyword.mon_full_notm}}-enabled instance.

To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the {{site.data.keyword.powerSys_notm}} instance is provisioned.
{: important}

## Creating an IBM Cloud monitoring instance
{: #sysdig-create-monitor}

Create an IBM Cloud monitoring instance and enable the platform metrics to get and operational visibility into the performance and health of applications, services, and infrastructure.

To creating an IBM Cloud monitoring instance, perform the following steps:
1. Log in to [IBM Cloud](https://cloud.ibm.com/login) console.
2. Search for **IBM Cloud monitoring** and select it.
3. Select your location and enter your custom values for **Service name** and other fields.
   To monitor platform metrics, select the location where your {{site.data.keyword.powerSys_notm}} instance is provisioned.
{: important}
4. Select the **Enable** indicator for **IBM platform metrics**.
5. Select the license agreements indicator and click **Create**.

You can also create the IBM Cloud monitoring instance from the **Integration (Optional)** section when you create a workspace, if no IBM Cloud monitoring instance is already created for that region.

## Viewing metrics
{: #sysdig-view}

The two different ways to access the Sysdig web user interface to see the metrics dashboards are as follows:
- Access the Sysdig web user interface from the {{site.data.keyword.powerSys_notm}} user interface.
- Access the Sysdig web user interface from the **Observability** page.

To view data in your dashboard, the platform metrics must be enabled and you must boot a {{site.data.keyword.powerSys_notm}} instance at least one time. To enable platform metrics, see: [Enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).
{: important}

### Accessing Sysdig dashboard from the {{site.data.keyword.powerSys_notm}} interface
{: #sysdig-view-ui}

From the left navigation menu of the {{site.data.keyword.powerSys_notm}} user interface, perform the following steps:
1.  click **workspaces**.
2.  Select the workspace for which a monitoring instance is present.
3.  From the **workspace details** page, click **Launch monitoring**.

### Accessing Sysdig dashboard from the Observability page
{: #sysdig-view-ob}

To access the dashboard, perform the following steps:
1.  Log in to [IBM Cloud](https://cloud.ibm.com/login) console.
2.  Expand the left navigation window.
3.  Click **Resource list**.
4.  Click **Observability** **>** **Monitoring**.
5.  Click the desired instance.
6.  Click **Launch monitoring**.

## {{site.data.keyword.powerSys_notm}} metrics dictionary
{: #sysdig-metrics-dictionary}

### CPU utilisation
{: cpu-metric}

The CPU utilization of a {{site.data.keyword.powerSys_notm}} instance in percentage.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_cpu_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 1: CPU utilization metrics of a VM" caption-side="top"}

### Memory utilisation
{: mem-metric}

The memory utilisation of a {{site.data.keyword.powerSys_notm}} instance.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_mem_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `ibm_service_instance`, `ibm_resource`|
{: caption="Table 2: Memory utilisation metrics of a VM" caption-side="top"}

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

Question: what are segmentation attributes?

### Global attributes
{: #sysdig-attributes-global}

The following global attributes are available for segmenting all the metrics that are listed in the metrics dictionary:

| Metric label name | Metric description | Valid values |
|----------------|-----------------------|--------------|
| `ibm_ctype` | Type of Cloud    | Valid value is `public`. |
| `ibm_location` | Location of the monitored resource | You can specify a region or a data center |
| `ibm_resource_group_name` | Resource group that is associated to the service instance | Choose a resource group from the ones that are available in your account |
| `ibm_scope` | The extent of the data samples that are considered  | The valid value is the IBM Cloud account ID |
| `ibm_service_name` | Name of the service that generates this metric | The valid value is `power-iaas` |
{: caption="Table 7: Global segmentation attributes" caption-side="top"}

### Additional attributes
{: #sysdig-attributes-add}

The following additional attributes are available for segmenting all the metrics that are listed in the metrics dictionary:
| Metric label name | Metric description | Valid values |
|----------------|-----------------------|--------------|
| `ibm_service_instance` | The workspace ID | Valid value is the Power System {{site.data.keyword.powerSys_notm}} workspace ID |
| `ibm_service_instance_name` | The workspace name | Valid value is the defined name of the workspace |
| `ibm_resource_type` | The type of {{site.data.keyword.powerSys_notm}} resource | Valid value is "{{site.data.keyword.powerSys_notm}} instance" |
| `ibm_resource` | The {{site.data.keyword.powerSys_notm}} instance ID | Valid value is the alphanumeric ID |
| `ibm_resource_name` | Name of the {{site.data.keyword.powerSys_notm}} instance | Valid value is the name of the {{site.data.keyword.powerSys_notm}} instance | Valid value is {{site.data.keyword.powerSys_notm}} ID |
| `ibm_power_iaas_pvm_instance_network_mac_address` | The MAC address of the network interface that is attached to the {{site.data.keyword.powerSys_notm}} instance | Valid value is an IP address |
{: caption="Table 8: Additional segmentation attributes" caption-side="top"}

## Considerations from IBM Cloud monitoring
{: #sysdig-limits}

There are some predefined limits around metrics ingestion. When limits are hit, rate-limited requests respond with a `503 Service Unavailable`. Following are the limitations:
- **Time range**: IBM Cloud monitoring accepts data within a specific time range, called the window of acceptance that is fixed to 5 minutes.
- **{{site.data.keyword.powerSys_notm}} instances booted once**: The platform metrics are visible on the dashboard when you boot a {{site.data.keyword.powerSys_notm}} instance at least one time.
- **Instance in error state**: Metric data of a {{site.data.keyword.powerSys_notm}} instance in error state is not available in the dashboard.

## Additional information
{: #sysdig-add-info}

- Learn more about the Sysdig dashboard user interface, see [About the Dashboard UI](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/using-dashboards/about-the-dashboard-ui/){: external}.
- See the [IBM Cloud monitoring](/docs/monitoring?topic=monitoring-getting-started#getting-started) documentation in IBM Cloud.