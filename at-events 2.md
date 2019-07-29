---

copyright:
  years: 2016, 2019
lastupdated: "2019-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# {{site.data.keyword.powerSys_notm}} Activity Tracker events
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.powerSys_notm}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. [Learn more](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## List of events: Read
{: #at_actions_read}

The following event is used to read the {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Read a Power Cloud Instance     |


## List of events: Images
{: #at_actions_images}

The following events are for working with images in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Read an Image or all Images     |
| pcloud.image.create        | Create a new Image              |
| pcloud.image.update        | Update an Image                 |
| pcloud.image.delete        | Delete an Image                 |
| pcloud.image.capture       | Exports an Image                |


## List of events: Networks
{: #at_actions_networks}

The following events are for working with networks in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Read a Network or all Networks        |
| pcloud.network.create      | Create a new Network (Public/Private) |
| pcloud.network.update      | Update a Network                      |
| pcloud.network.delete      | Delete a Network                      |
{: caption="Table 3. Actions that generate events" caption-side="top"}

## List of events: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

The following events are for working with each virtual servers within the {{site.data.keyword.powerSys_notm}} instance.

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
{: #at_actions_ssh_keys}

The following events are for working with account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Read your Tenant Info       |
| pcloud.ssh-key.read      | Read an SSHKey or SSH keys   |
| pcloud.ssh-key.create    | Create an SSH key            |
| pcloud.ssh-key.update    | Update an SSH key           |
| pcloud.ssh-key.delete    | Delete an SSH key           |

## List of events: Data volumes
{: #at_actions_data_volumes}

The following events are for working with data volumes in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | Read a Volume or Volumes    |
| pcloud.volume.create     | Create an Volume            |
| pcloud.volume.update     | Update an Volume            |
| pcloud.volume.delete     | Delete an Volume            |
| pcloud.volume.configure  | Attach or Detach a Volume   |

## Viewing events
{: #at_ui}

Events are available in the **Dallas** location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the `us-south` location. [Learn more](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
