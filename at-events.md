---

copyright:
  years: 2019, 2023

lastupdated: "2023-08-24"

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

As a security officer, auditor, or manager, you can use the {{site.data.keyword.atracker_short}} service to track how users and applications interact with the {{site.data.keyword.powerSysFull}} in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.atracker_short}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.atracker_short}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

{{site.data.keyword.powerSysFull}} automatically generates events so that you can track activity on your service.


## Management events
{: #at-actions-management}


### Instance events
{: #at-actions-read}

The following event is used to read the {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                                      |
|:---------------------------|:-------------------------------------------------|
| power-iaas.event.read | Read a Power Systems Virtual Server Instance     |
{: caption="Table 1. List of events: Read" caption-side="top"}

### Images events
{: #at-actions-images}

The following events are for working with images in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| power-iaas.image.read          | Read an Image or all Images     |
| power-iaas.image.create        | Create an Image              |
| power-iaas.image.update        | Update an Image                 |
| power-iaas.image.delete        | Delete an Image                 |
| power-iaas.image.capture       | Exports an Image                |
{: caption="Table 2. List of events: Images" caption-side="top"}

### Network events
{: #at-actions-networks}

The following events are for working with networks in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| power-iaas.network.read        | Read a Network or all Networks        |
| power-iaas.network.create      | Create a Network (Public or Private) |
| power-iaas.network.update      | Update a Network                      |
| power-iaas.network.delete      | Delete a Network                      |
{: caption="Table 3. List of events: Network" caption-side="top"}

### Power Systems Virtual Server events
{: #at-actions-servers}

The following events are for working with each {{site.data.keyword.powerSys_notm}} instance.

| Action                        | Description                          |
|:------------------------------|:-------------------------------------|
| power-iaas.pvm-instance.read      | Read a Power virtual server instance                  |
| power-iaas.pvm-instance.create    | Create a Power virtual server instance                |
| power-iaas.pvm-instance.update    | Update a Power virtual server instance                |
| power-iaas.pvm-instance.delete    | Delete a Power virtual server instance                |
| power-iaas.pvm-instance.start     | Start a Power virtual server instance                 |
| power-iaas.pvm-instance.stop      | Stop a Power virtual server instance                  |
| power-iaas.pvm-instance.renew     | Restart a Power virtual server instance                |
| power-iaas.pvm-instance.unknown   | Unknown action on a Power virtual server instance     |
| power-iaas.pvm-instance.monitor   | Console access to a Power virtual server instance     |
| power-iaas.pvm-instance.capture   | Capture a Power virtual server instance into an image |
| power-iaas.pvm-instance.immediate-shutdown     | Shut down a Power virtual server instance immediately |
| power-iaas.pvm-instance.clone   | Clone a Power virtual server instance |
| power-iaas.pvm-instance.snapshot     |  Create a Power virtual server instance Snapshot |
| power-iaas.pvm-instance-network.read      |  Read a Power virtual server instance Network |
| power-iaas.pvm-instance-network.create     |  Create a Power virtual server instance Network  |
| power-iaas.pvm-instance-network.delete      |  Delete a Power virtual server instance Network  |
{: caption="Table 4. List of events: Power Systems Virtual Server" caption-side="top"}

### SSH keys events
{: #at-actions-ssh}

The following events are for working with your account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ssh-key.read      | Read an SSH key or SSH keys |
| power-iaas.ssh-key.create    | Create an SSH key           |
| power-iaas.ssh-key.update    | Update an SSH key           |
| power-iaas.ssh-key.delete    | Delete an SSH key           |
{: caption="Table 5. List of events: SSH keys" caption-side="top"}

### Data volumes events
{: #at-actions-volumes}

The following events are for working with data volumes in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.volume.read       | Read a Volume or Volumes    |
| power-iaas.volume.create     | Create a Volume            |
| power-iaas.volume.update     | Update a Volume            |
| power-iaas.volume.delete     | Delete a Volume            |
| power-iaas.volume.configure  | Attach or Detach a Volume   |
{: caption="Table 6. List of events: Data volumes" caption-side="top"}

### Storage capacity events
{: #at-storage-capacity}

The following events are for working with storage capacity in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.storage-capacity.read       | Read Storage Capacity     |
{: caption="Table 7. List of events: Storage capacity" caption-side="top"}

### Storage pools events
{: #at-storage-pools}

The following events are for working with storage pools in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.system-pools.read       | Read System Pools Information     |
{: caption="Table 8. List of events: Storage pools" caption-side="top"}



### Tenant events
{: #at-tenants}

The following events are for working with tenants in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.tenant.read       |  Read your Tenant Information |
| power-iaas.tenant-ssh.read   |   Read SSH Key or SSH Keys |
| power-iaas.tenant-ssh.create  |   Create an SSH Key  |
| power-iaas.tenant-ssh.update  | Update an SSH Key |
| power-iaas.tenant-ssh.delete   |  Delete an SSH Key  |
{: caption="Table 9. List of events: Tenant" caption-side="top"}

### List of events: Job
{: #at-job}

The following events are for working with jobs in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.job.read       |  Read a Job or all Jobs |
| power-iaas.job.create  |   Create a Job  |
| power-iaas.job.delete   |  Delete a Job  |
{: caption="Table 10. List of events: Job" caption-side="top"}

### List of events: Network ports
{: #at-network-ports}

The following events are for working with network ports in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.port.read       |  Read a Network Port or all Network Ports |
| power-iaas.port.create  |   Create a Network Port   |
| power-iaas.port.update  |   Update a Network Port   |
| power-iaas.port.delete   | Delete a Network Port  |
{: caption="Table 11. List of events: Network ports" caption-side="top"}

### List of events: SAP
{: #at-sap}

The following events are for working with SAP in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.sap.read       |  Read SAP Information |
| power-iaas.sap.create  |   Create an SAP PVM Instance   |
{: caption="Table 12. List of events: SAP" caption-side="top"}

### List of events: Cloud Connections
{: #at-cloud-connection}

The following events are for working with Cloud connections in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.cloud-connection.read       |  Read a Cloud Connection or all Cloud Connections  |
| power-iaas.cloud-connection.create     |   Create a Cloud Connection    |
| power-iaas.cloud-connection.update     |   Update a Cloud Connection    |
| power-iaas.cloud-connection.delete       |   Delete a Cloud Connection    |
{: caption="Table 13. List of events: Cloud connections" caption-side="top"}

### List of events: Placement Groups
{: #at-placement-groups}

The following events are for working with placement groups in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.placement-groups.read       |  Read a Placement Group or all Placement Groups  |
| power-iaas.placement-groups.create     |   Create a Placement Group     |
| power-iaas.placement-groups.update     |   Update a Placement Group     |
| power-iaas.placement-groups.delete       |   Delete a Placement Group     |
{: caption="Table 14. List of events: Placement groups" caption-side="top"}

### List of events: IKE Policy
{: #at-ike-policy}

The following events are for working with IKE Policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ike-policy.read       |  Read an IKE Policy   |
| power-iaas.ike-policy.create     |   Create an IKE Policy      |
| power-iaas.ike-policy.update     |   Update an IKE Policy      |
| power-iaas.ike-policy.delete       |   Delete an IKE Policy      |
{: caption="Table 15. List of events: IKE policy" caption-side="top"}

### List of events: IPSec Policy
{: #at-ipsec-policy}

The following events are for working with IPsec Policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ipsec-policy.read       |  Read an IPsec Policy   |
| power-iaas.ipsec-policy.create     |   Create an IPsec Policy      |
| power-iaas.ipsec-policy.update     |   Update an IPsec Policy      |
| power-iaas.ipsec-policy.delete       |   Delete an IPsec Policy      |
{: caption="Table 16. List of events: IPsec policy" caption-side="top"}

### List of events: VPN Connection
{: #at-vpn-connection}

The following events are for working with VPN Connection in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.vpn-connection.read       |  Read a VPN Connection or all VPN Connections   |
| power-iaas.vpn-connection.create     |   Create a VPN Connection       |
| power-iaas.vpn-connection.update     |   Update a VPN Connection       |
| power-iaas.vpn-connection.delete       |   Delete a VPN Connection       |
{: caption="Table 17. List of events: VPN Connection" caption-side="top"}

## Viewing events
{: #at-viewing-events}

Events are automatically forwarded to North America, Europe, Tokyo, or Sydney geographic locations. You can access the activity tracker logs for all North America and South America data centers from Dallas, all Europe data centers from Frankfurt, Sydney data center from Sydney, and all Japan data center from Tokyo. For a list of locations where Power Systems Virtual Server services are enabled to send events to IBM Cloud Activity Tracker, see [Activity Tracker events by location](/docs/activity-tracker?topic=activity-tracker-cloud_services_locations&interface=cli#cloud_services_locations_power-iaas).

{{site.data.keyword.at_short}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_short}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/activity-tracker?topic=activity-tracker-launch). 

## Activity tracker sample response format
{: #at-response-sample}

The following code snippets shows the differences between the old and new activity tracker response format.

`New response format`
```
{
    "logSourceCRN": "crn:v1:bluemix:public:power-iaas:us-east:a/xxxxxxxxxxxxxxxxxxxx:yyyyyyyyyyyyyyyyyyyyyy::",
    "saveServiceCopy": true,
    "dataEvent": false,
    "outcome": "success",
    "eventTime": "2022-06-30T03:12:49.63+0000",
    "action": "power-iaas.tenant.read",
    "correlationId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "severity": "normal",
    "initiator": {
        "id": "IBMid-xxxxxxxxxx",
        "name": "xxxxm@us.ibm.com",
        "typeURI": "service/security/account/user",
        "authnId": "",
        "authnName": "",
        "host": {
            "agent": "PostmanRuntime/7.28.4",
            "address": "127.0.0.1",
            "addressType": "IPv4"
        },
        "credential": {
            "type": "user"
        }
    },
    "target": {
        "id": "crn:v1:bluemix:public:power-iaas:us-east:a/xxxxxxxxxxxxxxxxxxxx:yyyyyyyyyyyyyyyyyyyyyy::",
        "name": "testName",
        "typeURI": "power-iaas/tenant",
        "resourceGroupId": "crn:v1:bluemix:public:resource-controller::a/xxxxxxxxxxxxxxxxxxxx::resource-group:zzzzzzzzzzzzzzzzzzzzzzz"
    },
    "reason": {
        "reasonCode": 200,
        "reasonType": "OK"
    },
    "requestData": null,
    "responseData": {
        "cloudInstances": [
            {
                "capabilities": [],
                "cloudInstanceID": "yyyyyyyyyyyyyyyyyyyyyy",
                "enabled": true,
                "href": "/pcloud/v1/cloud-instances/yyyyyyyyyyyyyyyyyyyyyy",
                "initialized": false,
                "name": "testName",
                "region": "us-east"
            }
        ],
        "creationDate": "2019-05-21T21:32:00.746Z",
        "enabled": true,
        "sshKeys": [],
        "tenantID": "xxxxxxxxxxxxxxxxxxxx"
    },
    "message": "Power Systems Virtual Server: read tenant xxxxxxxxxxxxxxxxxxxx ",
    "observer": {
        "name": "ActivityTracker"
    }
}
````
{: codeblock}


`Old response format`
```
{
    "payload": {
        "outcome": "success",
        "eventTime": "2019-05-31T19:33:02.97+0000",
        "action": "pcloud.tenant.read",
        "severity": "normal",
        "initiator": {
            "id": "IBMid-xxxxxxxxxx",
            "name": "xxxxm@us.ibm.com",
            "typeURI": "service/security/account/user",
            "host": {
                "agent": "PostmanRuntime/7.13.0",
                "address": "127.0.0.1"
            },
            "credential": {
                "type": "user"
            }
        },
        "target": {
            "id": "crn:v1:bluemix:public:power-iaas:us-east:a/xxxxxxxxxxxxxxxxxxxx:yyyyyyyyyyyyyyyyyyyyyy::",
            "name": "testName",
            "typeURI": "pcloud/tenant/read",
            "host": {
                "address": "100.64.24.72"
            }
        },
        "reason": {
            "reasonCode": 200
        },
        "responseData": "{\"cloudInstances\":[{\"cloudInstanceID\":\"yyyyyyyyyyyyyyyyyyyyyy\",\"enabled\":true,\"href\":\"/pcloud/v1/cloud-instances/yyyyyyyyyyyyyyyyyyyyyy\",\"initialized\":false,\"name\":\"testName\",\"region\":\"us-east\"}],\"creationDate\":\"2019-05-21T21:32:00.746Z\",\"enabled\":true,\"sshKeys\":[{\"creationDate\":\"2019-05-21T22:13:49.806Z\",\"name\":\"Test\",\"sshKey\":\"Foo\"}],\"tenantID\":\"xxxxxxxxxxxxxxxxxxxx\"}",
        "message": "pcloud: read tenant 9cdad2e857d442d49853e484e9b91d24 success"
    },
    "logSourceCRN": "crn:v1:bluemix:public:power-iaas:us-east:a/xxxxxxxxxxxxxxxxxxxx:yyyyyyyyyyyyyyyyyyyyyy::",
    "saveServiceCopy": true,
    "meta": {
        "serviceProviderName": "power-iaas",
        "serviceProviderRegion": "ng",
        "serviceProviderProjectId": "power-iaas",
        "userAccountIds": [
            "a/xxxxxxxxxxxxxxxxxxxx"
        ],
        "userSpaceRegion": "ng"
    }
}
````
{: codeblock}

