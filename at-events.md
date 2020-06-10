---

copyright:
  years: 2019,2020

lastupdated: "2020-05-28"

keywords: activity tracker service, regulatory audit requirements, abnormal activity, view events

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

# Activity tracker events
{: #at-events}

As a security officer, auditor, or manager, you can use the **Activity Tracker** service to track how users and applications interact with your {{site.data.keyword.powerSysFull}}.
{: shortdesc}

The {{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}. You can use this service to alert you of abnormal activity and to comply with regulatory audit requirements. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see [IBM Cloud Activity Tracker with LogDNA](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started#getting-started).

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

## List of events: Power Systems Virtual Server
{: #at-actions-servers}

The following events are for working with each {{site.data.keyword.powerSys_notm}} instance.

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

The following events are for working with your account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | Read your Tenant Information|
| pcloud.ssh-key.read      | Read an SSH key or SSH keys |
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
{: #at-viewing-events}

Events are available in all regions. The {{site.data.keyword.at_full_notm}} can have only one instance per region. To view events, you must access the {{site.data.keyword.at_full_notm}} web user interface. To learn more, see [Starting the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-launch#launch_step2).
