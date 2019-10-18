---

copyright:
  years: 2016, 2019

lastupdated: "2019-09-04"

keywords: activity tracker service, regulatory audit requirements, abnormal activity

subcollection: power-iaas

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Power Systems Virtual Servers activity tracker events
{: #at-events}

As a security officer, auditor, or manager, you can use the **Activity Tracker** service to track how users and applications interact with {{site.data.keyword.powerSysFull}} in the {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see[Learn more](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## List of events: Read
{: #at-actions-read}

The following event is used to read the {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Read a Power Cloud Instance     |

## List of events: Images
{: #at-actions-images}

The following events are for working with images in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Read an Image or all Images     |
| pcloud.image.create        | Create a new Image              |
| pcloud.image.update        | Update an Image                 |
| pcloud.image.delete        | Delete an Image                 |
| pcloud.image.capture       | Exports an Image                |

## List of events: Networks
{: #at-actions-networks}

The following events are for working with networks in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Read a Network or all Networks        |
| pcloud.network.create      | Create a new Network (Public/Private) |
| pcloud.network.update      | Update a Network                      |
| pcloud.network.delete      | Delete a Network                      |

## List of events: {{site.data.keyword.powerSys_notm}}
{: #at-actions-servers}

The following events are for working with each virtual server within the {{site.data.keyword.powerSys_notm}} instance.

| Action                        | Description                          |
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Read a Power virtual server instance                  |
| pcloud.pvm-instance.create    | Create a Power virtual server instance                |
| pcloud.pvm-instance.update    | Update a Power virtual server instance                |
| pcloud.pvm-instance.delete    | Delete a Power virtual server instance                |
| pcloud.pvm-instance.start     | Start a Power virtual server instance                 |
| pcloud.pvm-instance.stop      | Stop a Power virtual server instance                  |
| pcloud.pvm-instance.renew     | Reboot a Power virtual server instance                |
| pcloud.pvm-instance.unknown   | Unknown action on a Power virtual server instance     |
| pcloud.pvm-instance.monitor   | Console access to a Power virtual server instance     |
| pcloud.pvm-instance.capture   | Capture a Power virtual server instance into an image |

## List of events: SSH keys
{: #at-actions-ssh}

The following events are for working with account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Read your Tenant Information|
| pcloud.ssh-key.read      | Read an SSHKey or SSH keys  |
| pcloud.ssh-key.create    | Create an SSH key           |
| pcloud.ssh-key.update    | Update an SSH key           |
| pcloud.ssh-key.delete    | Delete an SSH key           |

## List of events: Data volumes
{: #at-actions-volumes}

The following events are for working with data volumes in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Read a Volume or Volumes    |
| pcloud.volume.create     | Create a Volume            |
| pcloud.volume.update     | Update a Volume            |
| pcloud.volume.delete     | Delete a Volume            |
| pcloud.volume.configure  | Attach or Detach a Volume   |

## Viewing events
{: #at-events}

Events are available in the **Dallas** location. {{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the `us-south` location. To learn more, see [Starting the web UI through the IBM Cloud UI](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
