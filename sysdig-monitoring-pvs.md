---

copyright:
  years: 2019, 2023

lastupdated: "2023-08-29"

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

{{site.data.keyword.mon_full_notm}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full-stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by *Sysdig* in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}

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

Perform the following steps:
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

The two different ways to access the *Sysdig* web user interface to see the metrics dashboards are as follows:
- Launch the *Sysdig* web user interface from the {{site.data.keyword.powerSys_notm}} user interface.
   
- Accessing Sysdig web user interface from the **Observability** page.

### Accessing *Sysdig* dashboard from the {{site.data.keyword.powerSys_notm}} interface
{: #sysdig-view-ui}

From the left navigation menu of the {{site.data.keyword.powerSys_notm}} user interface, perform the following steps:
1.  click **workspaces**.
2.  Select the workspace for which a monitoring instance is present.
3.  From the **workspace details** page, click **Launch monitoring**.

### Accessing *Sysdig* dashboard from the Observability page
{: #sysdig-view-ob}

Perform the following steps:
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
| `Segment by`  | `Service instance`, `Resource type`|
{: caption="Table 1: CPU utilization metrics of a VM" caption-side="top"}

### Memory utilisation
{: mem-metric}

The memory utilisation of a {{site.data.keyword.powerSys_notm}} instance.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | ` ibm_power_iaas_pvm_instance_mem_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment by`  | `Service instance`, `Resource type`|
{: caption="Table 2: Memory utilisation metrics of a VM" caption-side="top"}

### Incoming network bytes
{: in-net-metric}

The incoming bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface (or per mac address).
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_incoming_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `Service instance`, `Resource type`, `Virtual server instance mac address`|
{: caption="Table 3: Incoming byte metrics of a VM per network interface " caption-side="top"}

### Outgoing network bytes
{: out-net-metric}

The outgoing bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_outgoing_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `Service instance`, `Resource type`, `Virtual server instance mac address`|
{: caption="Table 4: Outgoing byte metrics of a VM per network interface " caption-side="top"}

### Disk read bytes
{: disk-rd-metric}

The total disk read bytes at {{site.data.keyword.powerSys_notm}} instance level.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_read_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `Service instance`, `Resource type`|
{: caption="Table 5: Total disk read bytes metrics at a VM" caption-side="top"}

### Disk write bytes
{: disk-wrt-metric}

The total disk write bytes at {{site.data.keyword.powerSys_notm}} instance level.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_write_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
| `Segment by`  | `Service instance`, `Resource type`|
{: caption="Table 6: Total disk write bytes metrics at a VM" caption-side="top"}



## Attributes for segmentation
{: #sysdig-attributes}

Question: what are segmentation attributes?

### Global attributes
{: #sysdig-attributes-global}

The following attributes are available for segmenting all the metrics that are listed above in the metrics dictionary:

| Attribute | Attribute Name | Attribute Description | Valid values |
|-----------|----------------|-----------------------|--------------|
| `Cloud type` | `ibm_ctype` | Type of Cloud         | Valid value is `public`. |
| `Location` | `ibm_location` | Location of the monitored resource | You can specify a region or a data center |
| `Resource group` | `ibm_resource_group_name` | Resource group that is associated to the service instance | Choose a resource group from the ones that are available in your account |
| `Scope` | `ibm_scope` | The extent of the data samples that are considered  | The valid value is the IBM Cloud account ID |
| `Service name` | `ibm_service_name` | Name of the service that generates this metric | The valid value is `power-iaas` |
{: caption="Table 7: Global segmentation attributes" caption-side="top"}

### Additional attributes
{: #sysdig-attributes-add}

The following attributes are available as additional attributes for segmenting all of the metrics listed above in the metrics dictionary:
| Attribute | Attribute Name | Attribute Description | Valid values |
|-----------|----------------|-----------------------|--------------|
| `Service instance` | `ibm_service_instance` | The workspace ID | Valid value is the Power System Virtual Server workspace ID |
| `Service instance name` | `ibm_service_instance_name` | The workspace name | Valid value is the defined name of the workspace |
| `Resource type` | `ibm_resource_type` | The virtual server instance ID | Valid values is virtual server instance ID |
| `Resource name` | `ibm_resource_name` | Name of the virtual server instance | Valid value is the name of the virtual server instance |
| `Virtual server instance mac address` | `ibm_power_iaas_pvm_instance_network_mac_address` | The MAC address of the virtual server instance whose metrics are collected  | Valid value is `xx.xx.xx.xx` |
{: caption="Table 8: Additional segmentation attributes" caption-side="top"}

## Limitations from IBM Cloud monitoring
{: #sysdig-limits}

There are some predefined limits around metrics ingestion. When limits are hit, rate-limited requests respond with a `503 Service Unavailable`. Following are the limitations:
- **Time range**: IBM Cloud monitoring accepts data within a specific time range, called the window of acceptance. This is fixed to 5 minutes.
- **Sample Rate limit**: The default is 1 M samples per Metric Frequency per service owner.
- **Request rate limit**: The request rate limit is 10k requests per Metric Frequency per service owner and the batch limit is 10 k samples/ request. Hence, samples are pushed in a batch.
- **Concurrent Request limit**: The concurrent Request limit is 100 requests at any time.

## Additional information
{: #sysdig-add-info}

- Learn more about the Sysdig dashboard user interface, see [About the Dashboard UI](https://docs.sysdig.com/en/docs/sysdig-monitor/dashboards/using-dashboards/about-the-dashboard-ui/){: external}.
- See the [IBM Cloud monitoring](/docs/monitoring?topic=monitoring-getting-started#getting-started) documentation in IBM Cloud.

<!-- IBM Service instance id( workspace id) , ibm resource id(vm id) ==> segmented by
Network — + MAC address
Global : all attributtes except MAC address
Addition =-==MAC address -->