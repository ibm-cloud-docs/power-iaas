---

copyright:
  years: 2019, 2020

lastupdated: "2020-05-28"

keywords: activity tracker service, regulatory audit requirements, abnormal activity, view events

subcollection: power-iaas

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:term: .term}

# Activity tracker events
{: #at-events}

As a security officer, auditor, or manager, you can use the **Activity Tracker** service to track how users and applications interact with your {{site.data.keyword.powerSysFull}}.
{: shortdesc}

The {{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in the {{site.data.keyword.cloud_notm}}. You can use this service to alert you of abnormal activity and to comply with regulatory audit requirements. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see [IBM Cloud Activity Tracker with LogDNA](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-getting-started#getting-started).

## List of events: Read
{: #at-actions-read}

The following event is used to read the {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                                      |
|:---------------------------|:-------------------------------------------------|
| pcloud.event.read | Read a Power Systems Virtual Server Instance     |
{: caption="Table 1. List of events: Read" caption-side="top"}

## List of events: Images
{: #at-actions-images}

The following events are for working with images in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | Read an Image or all Images     |
| pcloud.image.create        | Create an Image              |
| pcloud.image.update        | Update an Image                 |
| pcloud.image.delete        | Delete an Image                 |
| pcloud.image.capture       | Exports an Image                |
{: caption="Table 2. List of events: Images" caption-side="top"}

## List of events: Networks
{: #at-actions-networks}

The following events are for working with networks in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | Read a Network or all Networks        |
| pcloud.network.create      | Create a Network (Public or Private) |
| pcloud.network.update      | Update a Network                      |
| pcloud.network.delete      | Delete a Network                      |
{: caption="Table 3. List of events: Network" caption-side="top"}

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
| pcloud.pvm-instance.renew     | Restart a Power virtual server instance                |
| pcloud.pvm-instance.unknown   | Unknown action on a Power virtual server instance     |
| pcloud.pvm-instance.monitor   | Console access to a Power virtual server instance     |
| pcloud.pvm-instance.capture   | Capture a Power virtual server instance into an image |
| pcloud.pvm-instance.immediate-shutdown     | Shut down a Power virtual server instance immediately |
| pcloud.pvm-instance.clone   | Clone a Power virtual server instance |
| pcloud.pvm-instance.snapshot     |  Create a Power virtual server instance Snapshot |
| pcloud.pvm-instance.network.read      |  Read a Power virtual server instance Network |
| pcloud.pvm-instance.network.create     |  Create a Power virtual server instance Network  |
| pcloud.pvm-instance.network.delete      |  Delete a Power virtual server instance Network  |
{: caption="Table 4. List of events: Power Systems Virtual Server" caption-side="top"}

## List of events: SSH keys
{: #at-actions-ssh}

The following events are for working with your account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.ssh-key.read      | Read an SSH key or SSH keys |
| pcloud.ssh-key.create    | Create an SSH key           |
| pcloud.ssh-key.update    | Update an SSH key           |
| pcloud.ssh-key.delete    | Delete an SSH key           |
{: caption="Table 5. List of events: SSH keys" caption-side="top"}

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
{: caption="Table 6. List of events: Data volumes" caption-side="top"}

## List of events: Storage capacity
{: #at-storage-capacity}

The following events are for working with storage capacity in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.storage-capacity.read       | Read Storage Capacity     |
{: caption="Table 7. List of events: Storage capacity" caption-side="top"}

## List of events: Storage pools
{: #at-storage-pools}

The following events are for working with storage pools in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.system-pools.read       | Read System Pools Information     |
{: caption="Table 8. List of events: Storage pools" caption-side="top"}

## List of events: Tenant
{: #at-tenants}

The following events are for working with tenants in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       |  Read your Tenant Information |
| pcloud.tenant-ssh.read   |   Read SSH Key or SSH Keys |
| pcloud.tenant-ssh.create  |   Create an SSH Key  |
| pcloud.tenant-ssh.update  | Update an SSH Key |
| pcloud.tenant-ssh.delete   |  Delete an SSH Key  |
{: caption="Table 9. List of events: Tenant" caption-side="top"}

## List of events: Job
{: #at-job}

The following events are for working with jobs in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.job.read       |  Read a Job or all Jobs |
| pcloud.job.create  |   Create a Job  |
| pcloud.job.delete   |  Delete a Job  |
{: caption="Table 10. List of events: Job" caption-side="top"}

## List of events: Network ports
{: #at-network-ports}

The following events are for working with network ports in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.port.read       |  Read a Network Port or all Network Ports |
| pcloud.port.create  |   Create a Network Port   |
| pcloud.port.update  |   Update a Network Port   |
| pcloud.port.delete   | Delete a Network Port  |
{: caption="Table 11. List of events: Network ports" caption-side="top"}

## List of events: SAP
{: #at-sap}

The following events are for working with SAP in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.sap.read       |  Read SAP Information |
| pcloud.sap.create  |   Create an SAP PVM Instance   |
{: caption="Table 12. List of events: SAP" caption-side="top"}

## List of events: Cloud connections
{: #at-cloud-connection}

The following events are for working with Cloud connections in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.cloud-connection.read       |  Read a Cloud Connection or all Cloud Connections  |
| pcloud.cloud-connection.create     |   Create a Cloud Connection    |
| pcloud.cloud-connection.update     |   Update a Cloud Connection    |
| pcloud.cloud-connection.delete       |   Delete a Cloud Connection    |
{: caption="Table 13. List of events: Cloud connections" caption-side="top"}

## List of events: Placement Groups
{: #at-placement-groups}

The following events are for working with placement groups in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.placement-groups.read       |  Read a Placement Group or all Placement Groups  |
| pcloud.placement-groups.create     |   Create a Placement Group     |
| pcloud.placement-groups.update     |   Update a Placement Group     |
| pcloud.placement-groups.delete       |   Delete a Placement Group     |
{: caption="Table 14. List of events: Placement groups" caption-side="top"}

## List of events: IKE Policy
{: #at-ike-policy}

The following events are for working with IKE Policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.ike-policy.read       |  Read an IKE Policy   |
| pcloud.ike-policy.create     |   Create an IKE Policy      |
| pcloud.ike-policy.update     |   Update an IKE Policy      |
| pcloud.ike-policy.delete       |   Delete an IKE Policy      |
{: caption="Table 15. List of events: IKE policy" caption-side="top"}

## List of events: IPsec Policy
{: #at-ipsec-policy}

The following events are for working with IPsec Policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.ipsec-policy.read       |  Read an IPsec Policy   |
| pcloud.ipsec-policy.create     |   Create an IPsec Policy      |
| pcloud.ipsec-policy.update     |   Update an IPsec Policy      |
| pcloud.ipsec-policy.delete       |   Delete an IPsec Policy      |
{: caption="Table 16. List of events: IPsec policy" caption-side="top"}

## List of events: VPN Connection
{: #at-vpn-connection}

The following events are for working with VPN Connection in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| pcloud.vpn-connection.read       |  Read a VPN Connection or all VPN Connections   |
| pcloud.vpn-connection.create     |   Create a VPN Connection       |
| pcloud.vpn-connection.update     |   Update a VPN Connection       |
| pcloud.vpn-connection.delete       |   Delete a VPN Connection       |
{: caption="Table 17. List of events: VPN Connection" caption-side="top"}

## Viewing events
{: #at-viewing-events}

The {{site.data.keyword.at_full_notm}} can have only one instance per geographic location. Separate Activity Trackers are available for North America, Europe, and Sydney geographic locations. To view events, you must access the {{site.data.keyword.at_full_notm}} web user interface. To learn more, see [Starting the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-launch#launch_step2).
