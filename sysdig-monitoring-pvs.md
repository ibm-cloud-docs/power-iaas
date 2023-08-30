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

{{site.data.keyword.mon_full_notm}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}

## Platform metrics overview
{: #sysdig-ov}
{: #platform_metrics}

You can view platform metrics when you enable {{site.data.keyword.mon_full_notm}} on your IBM Cloud platform. A monitoring instance must be configured in a region to monitor these metrics. For more information, see [Enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

Before you enable {{site.data.keyword.mon_full_notm}} on your platform, consider the following:

* You can configure only one instance of the {{site.data.keyword.mon_full_notm}} service per region to collect platform metrics.
* Platform metrics are regional. Metrics are monitored only from {{site.data.keyword.mon_full_notm}} services, which are in the same region of the instance that you want to monitor.
* Metrics are collected automatically and are available for monitoring through the {{site.data.keyword.mon_full_notm}}-enabled instance.

To monitor platform metrics, check that the {{site.data.keyword.mon_full_notm}} instance is provisioned in the same region where the {{site.data.keyword.powerSys_notm}} instance is provisioned.
{: important}


## Viewing metrics
{: #sysdig-view}

Various ways you can launch the Sysdig web UI to see the metrics dashboards:
1.  Launch the Sysdig web UI from the {{site.data.keyword.powerSys_notm}} UI.
2.  Launching Sysdig web UI from the Observability page.


[Validate with Anu]{: tag-dark-teal}
### Launching Sysdig web UI from the {{site.data.keyword.powerSys_notm}} UI
{: #sysdig-view-ui}

[Validate with Anu]{: tag-dark-teal}

### Launching Sysdig web UI from the Observability page
{: #sysdig-view-ob}

[Validate with Anu]{: tag-dark-teal}

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
| `Segment By` | `-` |
{: caption="Table 1: CPU utilization metrics of a VM" caption-side="top"}

### Memory utilisation
{: mem-metric}

The memory utilisation of a {{site.data.keyword.powerSys_notm}} instance.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | ` ibm_power_iaas_pvm_instance_mem_util`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `-` |
{: caption="Table 2: Memory utilisation metrics of a VM" caption-side="top"}

### Incoming network bytes
{: in-net-metric}

The incoming bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface (or per mac address).
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_incoming_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
{: caption="Table 3: Incoming byte metrics of a VM per network interface " caption-side="top"}

### Outgoing network bytes
{: out-net-metric}

The outgoing bytes of a {{site.data.keyword.powerSys_notm}} instance per network interface.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_network_outgoing_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
{: caption="Table 4: Outgoing byte metrics of a VM per network interface " caption-side="top"}

### Disk read bytes
{: disk-rd-metric}

The total disk read bytes at {{site.data.keyword.powerSys_notm}} instance level.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_read_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
{: caption="Table 5: Total disk read bytes metrics at a VM" caption-side="top"}

### Disk write bytes
{: disk-wrt-metric}

The total disk write bytes at {{site.data.keyword.powerSys_notm}} instance level.
| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_power_iaas_pvm_instance_disk_write_bytes`|
| `Metric Type` | `counter` |
| `Value Type`  | `byte` |
{: caption="Table 6: Total disk write bytes metrics at a VM" caption-side="top"}



## Attributes for segmentation
{: #sysdig-attributes}

Question: what are segmentation attributes?

### Global attributes
{: #sysdig-attributes-global}

The following attributes are available for segmenting all of the metrics listed above

| Attribute | Attribute Name | Attribute Description | Valid values |
|-----------|----------------|-----------------------|--------------|
| `Cloud type` | `ibm_ctype` | Type of Cloud         | Valid values are `public`, `dedicated`, or `local`. |
| `Location` | `ibm_location` | Location of the monitored resource | You can specify a region, a data center, or `global`. |
| `Resource` | `ibm_resource` |  |  |
| `Resource name` | `ibm_resource_name` |  |  |
| `Resource group` | `ibm_resource_group_name` | Resource group that is associated to the service instance. | Choose a resource group from the ones that are available in your account. |
| `Resource group ID` | `ibm_resource_group_id` |
| `Resource type` | `ibm_resource_type` |  | |
| `Scope` | `ibm_scope` | The extent of the data samples that are considered  | You can choose the scope to be the account, an organization, or a space GUID that is associated with this metric. |
| `Service name` | `ibm_service_name` | Name of the service that generates this metric | `ibm_eventstreams` |
| `Service instance` | `ibm_service_instance` |  |  |
| `Service instance name` | `ibm_service_instance_name` |  |  |
| `Virtual server instance mac addrees` | `ibm_power_iaas_pvm_instance_network_mac_address` |  |  |

{: caption="Global segmentation attributes" caption-side="top"}

### Additional attributes
{: #sysdig-attributes-add}

required?
serv ins name
mac add
res grp name

ser ins, mac add