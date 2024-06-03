---

copyright:
  years: 2019, 2024

lastupdated: "2024-06-03"

keywords: activity tracker service, regulatory audit requirements, abnormal activity, view events

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracker events
{: #at-events}

{{site.data.keyword.powerSys_notm}} Activity Tracker Events will migrate to the CADF Event standard on January 29, 2024. Some of the event fields will not be sent or replaced by the new format. For the code snippets that shows the differences between the old and new format of the activity tracker response, see [Activity tracker sample response format](/docs/power-iaas?topic=power-iaas-at-events#at-response-sample).
{: note}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.atracker_short}} service to track how users and applications interact with the {{site.data.keyword.powerSysFull}} in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.atracker_short}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.atracker_short}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

{{site.data.keyword.powerSysFull}} automatically generates events so that you can track activity on your service.


## Management events
{: #at-actions-management}


### Instance events
{: #at-actions-read}

The following event is used to read the {{site.data.keyword.powerSys_notm}} instance.

| Action   | Description                                      |
|:---------|:-------------------------------------------------|
| power-iaas.event.list | List all {{site.data.keyword.powerSys_notm}} instances     |
| power-iaas.event.read | Read a {{site.data.keyword.powerSys_notm}} instance     |
{: caption="Table 1. List of events: Instance" caption-side="top"}

### Images events
{: #at-actions-images}

The following events are for working with images in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| power-iaas.image.list          | List all images |
| power-iaas.image.read          | Read an image |
| power-iaas.image.create        | Create an image              |
| power-iaas.image.update        | Update an image                 |
| power-iaas.image.delete        | Delete an image                 |
| power-iaas.image.capture       | Exports an image                |
{: caption="Table 2. List of events: Images" caption-side="top"}

### Network events
{: #at-actions-networks}

The following events are for working with networks in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| power-iaas.network.list        | List all networks    |
| power-iaas.network.read        | Read a network   |
| power-iaas.network.create      | Create a network (Public or Private) |
| power-iaas.network.update      | Update a network                      |
| power-iaas.network.delete      | Delete a network                      |
{: caption="Table 3. List of events: Network" caption-side="top"}

### {{site.data.keyword.powerSys_notm}} events
{: #at-actions-servers}

The following events are for working with each {{site.data.keyword.powerSys_notm}} instance.

| Action                        | Description                          |
|:------------------------------|:-------------------------------------|
| power-iaas.pvm-instance.list      | List all {{site.data.keyword.powerSys_notm}} instances                |
| power-iaas.pvm-instance.read      | Read a {{site.data.keyword.powerSys_notm}} instance                  |
| power-iaas.pvm-instance.create    | Create a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.update    | Update a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.delete    | Delete a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.start     | Start a {{site.data.keyword.powerSys_notm}} instance                 |
| power-iaas.pvm-instance.stop      | Stop a {{site.data.keyword.powerSys_notm}} instance                  |
| power-iaas.pvm-instance.renew     | Restart a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.unknown   | Unknown action on a {{site.data.keyword.powerSys_notm}} instance     |
| power-iaas.pvm-instance.monitor   | Console access to a {{site.data.keyword.powerSys_notm}} instance     |
| power-iaas.pvm-instance.capture   | Capture a {{site.data.keyword.powerSys_notm}} instance into an image |
| power-iaas.pvm-instance.immediate-shutdown     | Shut down a {{site.data.keyword.powerSys_notm}} instance immediately |
| power-iaas.pvm-instance.clone   | Clone a {{site.data.keyword.powerSys_notm}} instance |
| power-iaas.pvm-instance.snapshot     |  Create a {{site.data.keyword.powerSys_notm}} instance snapshot |
| power-iaas.pvm-instance-network.read      |  Read a {{site.data.keyword.powerSys_notm}} instance network |
| power-iaas.pvm-instance-network.create     |  Create a {{site.data.keyword.powerSys_notm}} instance network  |
| power-iaas.pvm-instance-network.delete      |  Delete a {{site.data.keyword.powerSys_notm}} instance network  |
{: caption="Table 4. List of events: {{site.data.keyword.powerSys_notm}}" caption-side="top"}

### SSH keys events
{: #at-actions-ssh}

The following events are for working with your account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ssh-key.list      | List all SSH keys |
| power-iaas.ssh-key.read      | Read an SSH key  |
| power-iaas.ssh-key.create    | Create an SSH key           |
| power-iaas.ssh-key.update    | Update an SSH key           |
| power-iaas.ssh-key.delete    | Delete an SSH key           |
{: caption="Table 5. List of events: SSH keys" caption-side="top"}

### Data volumes events
{: #at-actions-volumes}

The following events are for working with data volumes in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.volume.list       | List all volumes    |
| power-iaas.volume.read       | Read a volume    |
| power-iaas.volume.create     | Create a volume            |
| power-iaas.volume.update     | Update a volume            |
| power-iaas.volume.delete     | Delete a volume            |
| power-iaas.volume.configure  | Attach or Detach a volume   |
{: caption="Table 6. List of events: Data volumes" caption-side="top"}

### Storage capacity events
{: #at-storage-capacity}

The following events are for working with storage capacity in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.storage-capacity.list       | List all storage capacity     |
| power-iaas.storage-capacity.read       | Read a storage capacity     |
{: caption="Table 7. List of events: Storage capacity" caption-side="top"}

### Storage pools events
{: #at-storage-pools}

The following events are for working with storage pools in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.system-pools.list       | List all system pool information     |
| power-iaas.system-pools.read       | Read a system pool information     |
{: caption="Table 8. List of events: Storage pool" caption-side="top"}



### Tenant events
{: #at-tenants}

The following events are for working with tenants in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.tenant.read   |  Read a tenant |
| power-iaas.tenant-sshkey.read   |   Read a tenant SSH Key  |
| power-iaas.tenant-sshkey.create  |   Create a tenant SSH Key  |
| power-iaas.tenant-sshkey.update  | Update a tenant SSH Key |
| power-iaas.tenant-sshkey.delete   |  Delete a tenant SSH Key  |
{: caption="Table 9. List of events: Tenant" caption-side="top"}

### List of events: Job
{: #at-job}

The following events are for working with jobs in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.job.list       |  List all jobs |
| power-iaas.job.read       |  Read a job |
| power-iaas.job.create  |   Create a job  |
| power-iaas.job.delete   |  Delete a job  |
{: caption="Table 10. List of events: Job" caption-side="top"}

### List of events: Network ports
{: #at-network-ports}

The following events are for working with network ports in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.port.list       |  List all network ports |
| power-iaas.port.read       |  Read a network port   |
| power-iaas.port.create  |   Create a network port   |
| power-iaas.port.update  |   Update a network port   |
| power-iaas.port.delete   | Delete a network port  |
{: caption="Table 11. List of events: network ports" caption-side="top"}

### List of events: SAP
{: #at-sap}

The following events are for working with SAP in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.sap.list       |  List all SAP information |
| power-iaas.sap.read       |  Read a SAP information |
| power-iaas.sap.create  |   Create a SAP PVM instance   |
{: caption="Table 12. List of events: SAP" caption-side="top"}

### List of events: Cloud connections
{: #at-cloud-connection}

The following events are for working with Cloud connections in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.cloud-connection.list       |  List all cloud connections  |
| power-iaas.cloud-connection.read       |  Read a cloud connection  |
| power-iaas.cloud-connection.create     |   Create a cloud connection    |
| power-iaas.cloud-connection.update     |   Update a cloud connection    |
| power-iaas.cloud-connection.delete       |   Delete a cloud connection    |
{: caption="Table 13. List of events: Cloud connections" caption-side="top"}

### List of events: Placement groups
{: #at-placement-groups}

The following events are for working with placement groups in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.placement-groups.list       |  List all placement groups  |
| power-iaas.placement-groups.read       |  Read a placement group |
| power-iaas.placement-groups.create     |   Create a placement group     |
| power-iaas.placement-groups.update     |   Update a placement group     |
| power-iaas.placement-groups.delete       |   Delete a placement group     |
{: caption="Table 14. List of events: Placement groups" caption-side="top"}

### List of events: IKE policy
{: #at-ike-policy}

The following events are for working with IKE policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ike-policy.list       |  List all IKE policy   |
| power-iaas.ike-policy.read       |  Read an IKE policy   |
| power-iaas.ike-policy.create     |   Create an IKE policy      |
| power-iaas.ike-policy.update     |   Update an IKE policy      |
| power-iaas.ike-policy.delete       |   Delete an IKE policy      |
{: caption="Table 15. List of events: IKE policy" caption-side="top"}

### List of events: IPSec policy
{: #at-ipsec-policy}

The following events are for working with IPsec policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ipsec-policy.list       |  List all IPsec policy   |
| power-iaas.ipsec-policy.read       |  Read an IPsec policy   |
| power-iaas.ipsec-policy.create     |   Create an IPsec policy      |
| power-iaas.ipsec-policy.update     |   Update an IPsec policy      |
| power-iaas.ipsec-policy.delete       |   Delete an IPsec policy      |
{: caption="Table 16. List of events: IPsec policy" caption-side="top"}

### List of events: VPN connection
{: #at-vpn-connection}

The following events are for working with VPN Connection in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.vpn-connection.list       |  List all VPN connections   |
| power-iaas.vpn-connection.read       |  Read a VPN connection          |
| power-iaas.vpn-connection.create     |   Create a VPN connection       |
| power-iaas.vpn-connection.update     |   Update a VPN connection       |
| power-iaas.vpn-connection.delete       |   Delete a VPN connection       |
{: caption="Table 17. List of events: VPN connection" caption-side="top"}

## Viewing events
{: #at-viewing-events}

Events are automatically forwarded to North America, Europe, Tokyo, or Sydney geographic locations. You can access the activity tracker logs for all North America and South America data centers from Dallas, all Europe data centers from Frankfurt, Sydney data center from Sydney, and all Japan data center from Tokyo. For a list of locations where {{site.data.keyword.powerSys_notm}} services are enabled to send events to IBM Cloud Activity Tracker, see [Activity Tracker events by location](/docs/activity-tracker?topic=activity-tracker-cloud_services_locations&interface=cli#cloud_services_locations_power-iaas).

{{site.data.keyword.at_short}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_short}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/activity-tracker?topic=activity-tracker-launch).

## Activity tracker sample response format
{: #at-response-sample}

The new response format used in activity tracking adheres to the CADF (Cloud Auditing Data Federation) standard. Hence, auditing events can be collected and routed in a standardized format, ensuring consistency and interoperability across different cloud platforms.

The CADF standard is significant in auditing security in cloud environments as it defines a comprehensive event model that includes the necessary information for certifying, managing, and auditing the security of applications and services in the cloud.
{: note}

The following code snippets shows the differences between the old and new activity tracker response format.

`New response format`
```json
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
    "message": "{{site.data.keyword.powerSys_notm}}: read tenant xxxxxxxxxxxxxxxxxxxx ",
    "observer": {
        "name": "ActivityTracker"
    }
}
````

`Old response format`
```json
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

## Activity tracker regions
{: #at-regions}

You can create an activity tracker instance and provision it in the same region where your data center is located.

The {{site.data.keyword.powerSys_notm}} workspaces running in various regions or data center will send events to activity tracker instances in their respective regions effective from 29 January 2024. You must create and provision instances of activity tracker in the respective regions where your workspaces reside for continued access to {{site.data.keyword.powerSys_notm}} activity tracker events. If you want to export activity Tracker events, see [Exporting Activity Tracker events](/docs/activity-tracker?topic=activity-tracker-export).
{: important}

The following table shows the data center and its corresponding regions where you can deploy an activity tracker instance:

|Datacenter | Current activity tracker region | New activity tracker region |
|------|----------|---------|
|`WDC04` | us-south | us-east |
|`WDC06` | us-south | us-east |
|`WDC07` | us-south | us-east|
|`MON01` | us-south | ca-tor|
|`TOR04` | us-south | ca-tor|
|`SAO01` | us-south | br-sao|
|`SAO04` | us-south | br-sao|
|`LON04` | eu-de | eu-gb|
|`LON06` | eu-de | eu-gb|
|`OSA21` | jp-tok | jp-osa|
{: caption="Table 18. List of DCs and their corresponding AT instance region" caption-side="top"}
