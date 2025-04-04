---

copyright:
  years: 2019, 2024

lastupdated: "2025-04-02"

keywords: activity tracker service, regulatory audit requirements, abnormal activity, view events, IBM Cloud Logs

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Logs events for IBM Power Virtual Server
{: #at-events}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}



---








{{site.data.keyword.logs_full}} is a scalable logging service that persists logs and provides users with capabilities for querying, tailing, and visualizing logs.

Logs are comprised of events that are typically human-readable and have different formats, for example, unstructured text, JSON, delimiter-separated values, and key-value pairs. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. {{site.data.keyword.powerSysFull}} automatically generates events so that you can track activity on your service.


For more information, see [Getting started with IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-getting-started){: external}.












## Management events
{: #at-actions-management}


### Instance events
{: #at-actions-read}

The following events are used to read the {{site.data.keyword.powerSys_notm}} instance.

| Action   | Description                                      |
|:---------|:-------------------------------------------------|
| power-iaas.event.list | Lists all the {{site.data.keyword.powerSys_notm}} instances     |
| power-iaas.event.read | Reads a {{site.data.keyword.powerSys_notm}} instance     |
{: caption="List of events: Instance" caption-side="top"}

### Images events
{: #at-actions-images}

The following events are to work with images in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                     |
|:---------------------------|:--------------------------------|
| power-iaas.image.list          | Lists all the images |
| power-iaas.image.read          | Reads an image |
| power-iaas.image.create        | Creates an image              |
| power-iaas.image.update        | Updates an image                 |
| power-iaas.image.delete        | Deletes an image                 |
| power-iaas.image.capture       | Exports an image                |
{: caption="List of events: Images" caption-side="top"}

### Network events
{: #at-actions-networks}

The following events are to work with networks in your {{site.data.keyword.powerSys_notm}} instance.

| Action                     | Description                           |
|:---------------------------|:--------------------------------------|
| power-iaas.network.list        | Lists all the networks    |
| power-iaas.network.read        | Reads a network   |
| power-iaas.network.create      | Creates a network (Public or Private) |
| power-iaas.network.update      | Updates a network                      |
| power-iaas.network.delete      | Deletes a network                      |
{: caption="List of events: Network" caption-side="top"}

### {{site.data.keyword.powerSys_notm}} events
{: #at-actions-servers}

The following events are to work with each {{site.data.keyword.powerSys_notm}} instance.

| Action                        | Description                          |
|:------------------------------|:-------------------------------------|
| power-iaas.pvm-instance.list      | Lists all the {{site.data.keyword.powerSys_notm}} instances                |
| power-iaas.pvm-instance.read      | Reads a {{site.data.keyword.powerSys_notm}} instance                  |
| power-iaas.pvm-instance.create    | Creates a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.update    | Updates a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.delete    | Deletes a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.start     | Start a {{site.data.keyword.powerSys_notm}} instance                 |
| power-iaas.pvm-instance.stop      | Stop a {{site.data.keyword.powerSys_notm}} instance                  |
| power-iaas.pvm-instance.renew     | Restart a {{site.data.keyword.powerSys_notm}} instance                |
| power-iaas.pvm-instance.unknown   | Unknown action on a {{site.data.keyword.powerSys_notm}} instance     |
| power-iaas.pvm-instance.monitor   | Console access to a {{site.data.keyword.powerSys_notm}} instance     |
| power-iaas.pvm-instance.capture   | Capture a {{site.data.keyword.powerSys_notm}} instance into an image |
| power-iaas.pvm-instance.immediate-shutdown     | Shut down a {{site.data.keyword.powerSys_notm}} instance immediately |
| power-iaas.pvm-instance.clone   | Clone a {{site.data.keyword.powerSys_notm}} instance |
| power-iaas.pvm-instance.snapshot     |  Creates a {{site.data.keyword.powerSys_notm}} instance snapshot |
| power-iaas.pvm-instance-network.read      |  Reads a {{site.data.keyword.powerSys_notm}} instance network |
| power-iaas.pvm-instance-network.create     |  Creates a {{site.data.keyword.powerSys_notm}} instance network  |
| power-iaas.pvm-instance-network.delete      |  Deletes a {{site.data.keyword.powerSys_notm}} instance network  |
{: caption="List of events: {{site.data.keyword.powerSys_notm}}" caption-side="top"}

### SSH keys events
{: #at-actions-ssh}

The following events are to work with your account and SSH keys in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ssh-key.list      | Lists all the SSH keys |
| power-iaas.ssh-key.read      | Reads an SSH key  |
| power-iaas.ssh-key.create    | Creates an SSH key           |
| power-iaas.ssh-key.update    | Updates an SSH key           |
| power-iaas.ssh-key.delete    | Deletes an SSH key           |
{: caption="List of events: SSH keys" caption-side="top"}

### Data volumes events
{: #at-actions-volumes}

The following events are to work with data volumes in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.volume.list       | Lists all the volumes    |
| power-iaas.volume.read       | Reads a volume    |
| power-iaas.volume.create     | Creates a volume            |
| power-iaas.volume.update     | Updates a volume            |
| power-iaas.volume.delete     | Deletes a volume            |
| power-iaas.volume.configure  | Attaches or Detaches a volume   |
{: caption="List of events: Data volumes" caption-side="top"}

### Storage capacity events
{: #at-storage-capacity}

The following events are to work with storage capacity in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.storage-capacity.list       | Lists all the storage capacity     |
| power-iaas.storage-capacity.read       | Reads a storage capacity     |
| power-iaas.pod-capacity.list [{{site.data.keyword.on-prem}}]{: tag-red} | Lists system and storage capacity for an {{site.data.keyword.on-prem}} pod|
{: caption="List of events: Storage capacity" caption-side="top"}

### Storage pools events
{: #at-storage-pools}

The following events are to work with storage pools in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.system-pools.list       | Lists all the system pool information     |
| power-iaas.system-pools.read       | Reads a system pool information     |
{: caption="List of events: Storage pool" caption-side="top"}


### Tenant events
{: #at-tenants}

The following events are to work with tenants in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.tenant.read   |  Reads a tenant |
| power-iaas.tenant-sshkey.read   |   Reads a tenant SSH Key  |
| power-iaas.tenant-sshkey.create  |   Creates a tenant SSH Key  |
| power-iaas.tenant-sshkey.update  | Updates a tenant SSH Key |
| power-iaas.tenant-sshkey.delete   |  Deletes a tenant SSH Key  |
{: caption="List of events: Tenant" caption-side="top"}

### List of events: Job
{: #at-job}

The following events are to work with jobs in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.job.list       |  Lists all the jobs |
| power-iaas.job.read       |  Reads a job |
| power-iaas.job.create  |   Creates a job  |
| power-iaas.job.delete   |  Deletes a job  |
{: caption="List of events: Job" caption-side="top"}

### List of events: Network ports
{: #at-network-ports}

The following events are to work with network ports in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.port.list       |  Lists all the network ports |
| power-iaas.port.read       |  Reads a network port   |
| power-iaas.port.create  |   Creates a network port   |
| power-iaas.port.update  |   Updates a network port   |
| power-iaas.port.delete   | Deletes a network port  |
{: caption="List of events: network ports" caption-side="top"}

### List of events: SAP
{: #at-sap}

The following events are to work with SAP in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.sap.list       |  Lists all the SAP information |
| power-iaas.sap.read       |  Reads a SAP information |
| power-iaas.sap.create  |   Creates a SAP PVM instance   |
{: caption="List of events: SAP" caption-side="top"}

### List of events: Cloud connections
{: #at-cloud-connection}

The following events are to work with Cloud connections in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.cloud-connection.list       |  Lists all the cloud connections  |
| power-iaas.cloud-connection.read       |  Reads a cloud connection  |
| power-iaas.cloud-connection.create     |   Creates a cloud connection    |
| power-iaas.cloud-connection.update     |   Updates a cloud connection    |
| power-iaas.cloud-connection.delete       |   Deletes a cloud connection    |
{: caption="List of events: Cloud connections" caption-side="top"}

### List of events: Placement groups
{: #at-placement-groups}

The following events are to work with placement groups in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.placement-groups.list       |  Lists all the placement groups  |
| power-iaas.placement-groups.read       |  Reads a placement group |
| power-iaas.placement-groups.create     |   Creates a placement group     |
| power-iaas.placement-groups.update     |   Updates a placement group     |
| power-iaas.placement-groups.delete       |   Deletes a placement group     |
{: caption="List of events: Placement groups" caption-side="top"}

### List of events: IKE policy
{: #at-ike-policy}

The following events are to work with IKE policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ike-policy.list       |  Lists all the IKE policies   |
| power-iaas.ike-policy.read       |  Reads an IKE policy   |
| power-iaas.ike-policy.create     |   Creates an IKE policy      |
| power-iaas.ike-policy.update     |   Updates an IKE policy      |
| power-iaas.ike-policy.delete       |   Deletes an IKE policy      |
{: caption="List of events: IKE policy" caption-side="top"}

### List of events: IPsec policy
{: #at-ipsec-policy}

The following events are to work with IPsec policy in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.ipsec-policy.list       |  Lists all the IPsec policies   |
| power-iaas.ipsec-policy.read       |  Reads an IPsec policy   |
| power-iaas.ipsec-policy.create     |   Creates an IPsec policy      |
| power-iaas.ipsec-policy.update     |   Updates an IPsec policy      |
| power-iaas.ipsec-policy.delete       |   Deletes an IPsec policy      |
{: caption="List of events: IPsec policy" caption-side="top"}

### List of events: VPN connection
{: #at-vpn-connection}

The following events are to work with VPN Connection in your {{site.data.keyword.powerSys_notm}} instance.

| Action                   | Description                 |
|:-------------------------|:----------------------------|
| power-iaas.vpn-connection.list       |  Lists all the VPN connections   |
| power-iaas.vpn-connection.read       |  Reads a VPN connection          |
| power-iaas.vpn-connection.create     |   Creates a VPN connection       |
| power-iaas.vpn-connection.update     |   Updates a VPN connection       |
| power-iaas.vpn-connection.delete       |   Deletes a VPN connection       |
{: caption="List of events: VPN connection" caption-side="top"}

## Viewing events
{: #at-viewing-events}

Events are automatically forwarded to North America, Europe, Tokyo, or Sydney geographic locations. You can access the {{site.data.keyword.logs_full_notm}} as follows:
- All North America and South America data centers from Dallas.
- All Europe data centers from Frankfurt.
- All Sydney data center from Sydney, and
- All Japan data center from Tokyo.








## {{site.data.keyword.logs_full_notm}} sample response format
{: #at-response-sample}

The response format that is used in {{site.data.keyword.logs_full_notm}} adheres to the CADF (Cloud Auditing Data Federation) standard. Hence, auditing events can be collected and routed in a standardized format, ensuring consistency and interoperability across different cloud platforms.


The CADF standard is significant in auditing security in cloud environments. It defines a comprehensive event model that includes the necessary information for certifying, managing, and auditing the security of applications and services in the cloud.
{: note}

The following code snippet shows the response format.


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
    "message": "Power Virtual Server: read tenant xxxxxxxxxxxxxxxxxxxx ",
    "observer": {
        "name": "IBM Cloud Logs"
    }
}
```

## {{site.data.keyword.logs_full_notm}} regions
{: #at-regions}

You can create an {{site.data.keyword.logs_full_notm}} instance and provision it in the same region where your data center is located.


The {{site.data.keyword.powerSys_notm}} workspaces that runs in various regions or data centers sends events to {{site.data.keyword.logs_full_notm}} instances in their respective regions. You must create and provision instances of {{site.data.keyword.logs_full_notm}} in the respective regions where your workspaces reside for continued access to {{site.data.keyword.powerSys_notm}} {{site.data.keyword.logs_full_notm}} events. If you want to export {{site.data.keyword.logs_full_notm}} data, see [Exporting data](/docs/cloud-logs?topic=cloud-logs-export-data).


The following table shows the data center and its corresponding regions where you can deploy an {{site.data.keyword.logs_full_notm}} instance:


|Datacenter | Current {{site.data.keyword.logs_full_notm}} region | New {{site.data.keyword.logs_full_notm}} region |
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
{: caption="List of DCs and their corresponding IBM Cloud log instance region" caption-side="top"}
