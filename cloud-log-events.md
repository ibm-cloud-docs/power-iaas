---

copyright:
  years: 2019, 2026

lastupdated: "2026-09-11"

keywords: IBM Cloud Logs, log events, regulatory audit requirements, abnormal activity, Power Virtual Server

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Logs events for {{site.data.keyword.powerSys_notm}}
{: #cloud-log-events}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}



---

{{site.data.keyword.logs_full_notm}} is a scalable logging service that stores and manages logs. You can use {{site.data.keyword.logs_full_notm}} to monitor and audit events and operations across your {{site.data.keyword.powerSys_notm}} resources.
{: shortdesc}






{{site.data.keyword.powerSysFull}} automatically generates log events that report on activities that affect your resources. These log events can appear in different formats, including unstructured text, JSON, delimiter-separated values, and key-value pairs. You can use these log events to investigate abnormal activity, track critical actions, and meet regulatory audit requirements.


For more information, see [Getting started with IBM Cloud Logs](/docs/cloud-logs?topic=cloud-logs-getting-started).











## Management events
{: #management-events}

The following events are auto-generated when you create, read, update, or delete {{site.data.keyword.powerSys_notm}} resources, such as instances, networks, and volumes.

### Instance events
{: #instance-events}

The following events are generated when you list or read {{site.data.keyword.powerSys_notm}} instances:

| Event                  | Description                            |
| :---------------------- | :------------------------------------- |
| `power-iaas.event.list` | Lists all events from a cloud instance |
| `power-iaas.event.read` | Reads an event from a cloud instance   |
{: caption="Instance events" caption-side="bottom"}

### Image events
{: #image-events}

The following events are generated when you import, export, update, or delete images in a workspace:

| Event                    | Description      |
| :------------------------ | :--------------- |
| `power-iaas.image.delete` | Deletes an image |
| `power-iaas.image.export` | Exports an image |
| `power-iaas.image.import` | Imports an image |
| `power-iaas.image.list`   | Lists all images |
| `power-iaas.image.read`   | Reads an image   |
| `power-iaas.image.update` | Updates an image |
{: caption="Image events" caption-side="bottom"}

### Network events
{: #network-events}

The following events are generated when you create, read, update, delete, or list network resources such as network address groups, network peers, security groups, and interfaces:

| Event                                        | Description                                       |
| :-------------------------------------------- | :------------------------------------------------ |
| `power-iaas.network-address-group.create`     | Creates a network address group                   |
| `power-iaas.network-address-group.delete`     | Deletes a network address group from a workspace  |
| `power-iaas.network-address-group.list`       | Lists all network address groups for a workspace  |
| `power-iaas.network-address-group.read`       | Reads a network address group                     |
| `power-iaas.network-address-group.update`     | Updates a network address group                   |
| `power-iaas.network-interfaces.create`        | Creates a network interface                       |
| `power-iaas.network-interfaces.delete`        | Deletes a network interface                       |
| `power-iaas.network-interfaces.list`          | Lists all network interfaces                      |
| `power-iaas.network-interfaces.read`          | Reads a network interface       |
| `power-iaas.network-interfaces.update`        | Updates a network interface       |
| `power-iaas.network-peer-route-filter.create` | Creates a network peer route filter               |
| `power-iaas.network-peer-route-filter.delete` | Deletes a network peer route filter               |
| `power-iaas.network-peer-route-filter.read`   | Reads a network peer route filter                 |
| `power-iaas.network-peer.create`              | Creates a network peer                            |
| `power-iaas.network-peer.delete`              | Deletes a network peer                            |
| `power-iaas.network-peer.list`                | Lists all network peers                           |
| `power-iaas.network-peer.read`                | Reads a network peer                              |
| `power-iaas.network-peer.update`              | Updates a network peer                            |
| `power-iaas.network-security-group.clone`     | Clones a network security group                   |
| `power-iaas.network-security-group.create`    | Creates a network security group                  |
| `power-iaas.network-security-group.delete`    | Deletes a network security group from a workspace |
| `power-iaas.network-security-group.list`      | Lists all network security groups for a workspace |
| `power-iaas.network-security-group.read`      | Reads a network security group                    |
| `power-iaas.network-security-group.update`    | Updates a network security group                  |
| `power-iaas.network.create`                   | Creates a network (public or private)             |
| `power-iaas.network.delete`                   | Deletes a network                                 |
| `power-iaas.network.list`                     | Lists all networks                                |
| `power-iaas.network.read`                     | Reads a network                                   |
| `power-iaas.network.update`                   | Updates a network                                 |
| `power-iaas.peer-interfaces.list`             | Lists all interfaces for a network peer           |
{: caption="Network events" caption-side="bottom"}

### {{site.data.keyword.powerSys_notm}} events
{: #power-virtual-server-events}

The following events are generated when you create, start, stop, capture, update, or delete {{site.data.keyword.powerSys_notm}} instances and their associated resources:

| Event                                                 | Description                                                                                                                     |
| :----------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------ |
| `power-iaas.pvm-instance-virtual-serial-number.create` | Assigns a virtual serial number to a {{site.data.keyword.powerSys_notm}} instance                                               |
| `power-iaas.pvm-instance-virtual-serial-number.delete` | Unassigns a virtual serial number from a {{site.data.keyword.powerSys_notm}} instance                                           |
| `power-iaas.pvm-instance-virtual-serial-number.read`   | Reads the virtual serial number information of a {{site.data.keyword.powerSys_notm}} instance                                   |
| `power-iaas.pvm-instance-virtual-serial-number.update` | Updates a virtual serial number of a {{site.data.keyword.powerSys_notm}} instance                                               |
| `power-iaas.pvm-instance-vpmem-volume.create`          | Creates a vpmem volume to be attached to a {{site.data.keyword.powerSys_notm}} instance                                         |
| `power-iaas.pvm-instance-vpmem-volume.delete`          | Deletes a vpmem volume that is attached to a {{site.data.keyword.powerSys_notm}} instance                                               |
| `power-iaas.pvm-instance-vpmem-volume.list`            | Lists all vpmem volumes that are attached to a {{site.data.keyword.powerSys_notm}} instance                                              |
| `power-iaas.pvm-instance-vpmem-volume.read`            | Reads a vpmem volume that is attached to a {{site.data.keyword.powerSys_notm}} instance                                                 |
| `power-iaas.pvm-instance-vpmem-volume.update`          | Updates a vpmem volume that is attached to a {{site.data.keyword.powerSys_notm}} instance                                               |
| `power-iaas.pvm-instance.capture`                      | Captures a {{site.data.keyword.powerSys_notm}} instance as an image                                                           |
| `power-iaas.pvm-instance.create`                       | Creates a {{site.data.keyword.powerSys_notm}} instance                                                                          |
| `power-iaas.pvm-instance.delete`                       | Deletes a {{site.data.keyword.powerSys_notm}} instance                                                                          |
| `power-iaas.pvm-instance.immediate-shutdown`           | Shuts down a {{site.data.keyword.powerSys_notm}} instance immediately                                                           |
| `power-iaas.pvm-instance.list`                         | Lists all {{site.data.keyword.powerSys_notm}} instances and instance snapshots        |
| `power-iaas.pvm-instance.monitor`                      | Lists all supported console languages                                                                                           |
| `power-iaas.pvm-instance.operation`                    | Triggers an operation on a {{site.data.keyword.powerSys_notm}} instance                                                         |
| `power-iaas.pvm-instance.read`                         | Reads a {{site.data.keyword.powerSys_notm}} instance and restores an instance snapshot |
| `power-iaas.pvm-instance.renew`                        | Restarts a {{site.data.keyword.powerSys_notm}} instance                                                                         |
| `power-iaas.pvm-instance.snapshot`                     | Creates a {{site.data.keyword.powerSys_notm}} instance snapshot                                                                 |
| `power-iaas.pvm-instance.start`                        | Starts a {{site.data.keyword.powerSys_notm}} instance                                                                           |
| `power-iaas.pvm-instance.stop`                         | Stops a {{site.data.keyword.powerSys_notm}} instance                                                                            |
| `power-iaas.pvm-instance.unknown`                      | Triggers an unknown action on a {{site.data.keyword.powerSys_notm}} instance                                                    |
| `power-iaas.pvm-instance.update`                       | Updates a {{site.data.keyword.powerSys_notm}} instance                                                                          |
| `power-iaas.pvm-instance-network.create`               | Attaches a network to a {{site.data.keyword.powerSys_notm}} instance                                                            |
| `power-iaas.pvm-instance-network.delete`               | Detaches a network from a {{site.data.keyword.powerSys_notm}} instance                                                          |
| `power-iaas.pvm-instance-network.list`                 | Lists all networks that are attached to a {{site.data.keyword.powerSys_notm}} instance                                                   |
| `power-iaas.pvm-instance-network.read`                 | Reads the information of a network that is attached to a {{site.data.keyword.powerSys_notm}} instance                                   |
| `power-iaas.cloud-instance.read`                       | Reads the current state and configuration of a cloud instance                                                                   |
{: caption="{{site.data.keyword.powerSys_notm}} events" caption-side="bottom"}

### Secure Shell (SSH) key events
{: #secure-shell-ssh-key-events}

The following events are generated when you create, update, or delete SSH keys in a workspace:

| Event                     | Description        |
| :------------------------- | :----------------- |
| `power-iaas.sshkey.create` | Creates an SSH key |
| `power-iaas.sshkey.delete` | Deletes an SSH key |
| `power-iaas.sshkey.list`   | Lists all SSH keys |
| `power-iaas.sshkey.read`   | Reads an SSH key   |
| `power-iaas.sshkey.update` | Updates an SSH key |
{: caption="Secure shell (SSH) key events" caption-side="bottom"}

### Data volume events
{: #data-volumes-events}

The following events are generated when you create, attach, clone, read, update, or delete data volumes and volume groups:

| Event                                | Description                                                                                        |
| :------------------------------------ | :------------------------------------------------------------------------------------------------- |
| `power-iaas.volume-group.delete`      | Deletes a cloud instance volume group                                                              |
| `power-iaas.volume-group.list`        | Lists all volume groups                                                                            |
| `power-iaas.volume-group.post`        | Creates a volume group                                                                             |
| `power-iaas.volume-group.read`        | Lists the remote-copy volume relationships for a volume group                                                             |
| `power-iaas.volume-group.reset`       | Resets an operation on a volume group                                                              |
| `power-iaas.volume-group.start`       | Starts a volume group                                                                              |
| `power-iaas.volume-group.stop`        | Stops a volume group                                                                               |
| `power-iaas.volume-group.unknown`     | Triggers an unknown operation on a volume group                                                    |
| `power-iaas.volume-group.update`      | Updates a volume group                                                                             |
| `power-iaas.volume-onboarding.create` | Adds auxiliary volumes to the target site                                                          |
| `power-iaas.volume-onboarding.list`   | Lists all volume onboarding operations                                                             |
| `power-iaas.volume-onboarding.read`   | Reads information about a volume onboarding operation                                              |
| `power-iaas.volume-snapshot.list`     | Lists all volume snapshots in a workspace                                                       |
| `power-iaas.volume-snapshot.read`     | Reads the details of a volume snapshot                                                             |
| `power-iaas.volume.clone`             | Creates a volume clone for specified volumes                                                       |
| `power-iaas.volume.configure`         | Attaches, detaches, or updates a volume that is attached to a {{site.data.keyword.powerSys_notm}} instance |
| `power-iaas.volume.create`            | Creates a volume                                                                                   |
| `power-iaas.volume.delete`            | Deletes a volume                                                                                   |
| `power-iaas.volume.list`              | Lists all volumes                                                                                  |
| `power-iaas.volume.operation`         | Triggers an action on a volume                                                                     |
| `power-iaas.volume.read`              | Reads a volume, flash copy mappings of a volume, and remote copy volume information                |
| `power-iaas.volume.start`             | Starts an operation on a volume                                                                    |
| `power-iaas.volume.update`            | Updates a volume                                                                                   |
{: caption="Data volumes events" caption-side="bottom"}

### Storage capacity events
{: #storage-capacity-events}

The following events are generated when you list or read storage capacity information for a workspace or pod:

| Event                             | Description                                                 |
| :--------------------------------- | :---------------------------------------------------------- |
| `power-iaas.storage-capacity.list` | Lists storage capacity information for a workspace          |
| `power-iaas.storage-capacity.read` | Reads storage capacity information                          |
| `power-iaas.pod-capacity.list`     | Lists system and storage capacity for a client location pod |
{: caption="Storage capacity events" caption-side="bottom"}

### Storage pool events
{: #storage-pool-events}

The following event is generated when you list storage pools for an IBM data center:

| Event                         | Description                               |
| :----------------------------- | :---------------------------------------- |
| `power-iaas.system-pools.list` | Lists storage pools of an IBM data center |
{: caption="Storage pool events" caption-side="bottom"}

### Tenant events
{: #tenant-events}

The following events are generated when you read or update tenant information and manage tenant SSH keys:

| Event                            | Description                    |
| :-------------------------------- | :----------------------------- |
| `power-iaas.tenant-sshkey.create` | Creates a tenant SSH key       |
| `power-iaas.tenant-sshkey.delete` | Deletes a tenant SSH key       |
| `power-iaas.tenant-sshkey.list`   | Lists the SSH keys of a tenant |
| `power-iaas.tenant-sshkey.read`   | Reads a tenant SSH key         |
| `power-iaas.tenant-sshkey.update` | Updates a tenant SSH key       |
| `power-iaas.tenant.read`          | Reads a tenant                 |
| `power-iaas.tenant.update`        | Updates a tenant               |
{: caption="Tenant events" caption-side="bottom"}

### Cloud instance job events
{: #cloud-instance-job-events}

The following events are generated when you create, delete, list, or read cloud instance jobs:

| Event                  | Description                                                   |
| :---------------------- | :------------------------------------------------------------ |
| `power-iaas.job.create` | Creates a cloud instance job                                  |
| `power-iaas.job.delete` | Deletes a cloud instance job                                  |
| `power-iaas.job.list`   | Lists the last five jobs that were run for the cloud instance |
| `power-iaas.job.read`   | Reads the details of a job                                    |
{: caption="Cloud instance job events" caption-side="bottom"}

### Network port events
{: #network-port-events}

The following events are generated when you create, update, or delete network ports in a workspace:

| Event                   | Description             |
| :----------------------- | :---------------------- |
| `power-iaas.port.create` | Creates a network port  |
| `power-iaas.port.delete` | Deletes a network port  |
| `power-iaas.port.list`   | Lists all network ports |
| `power-iaas.port.read`   | Reads a network port    |
| `power-iaas.port.update` | Updates a network port  |
{: caption="Network port events" caption-side="bottom"}

### SAP events
{: #sap-events}

The following events are generated when you create or read SAP {{site.data.keyword.powerSys_notm}} instances:

| Event                  | Description                                                 |
| :---------------------- | :---------------------------------------------------------- |
| `power-iaas.sap.create` | Creates an SAP {{site.data.keyword.powerSys_notm}} instance |
| `power-iaas.sap.list`   | Lists all SAP {{site.data.keyword.powerSys_notm}} instances |
| `power-iaas.sap.read`   | Reads an SAP {{site.data.keyword.powerSys_notm}} instance   |
{: caption="SAP events" caption-side="bottom"}

### Cloud connections events
{: #cloud-connections-events}

The following events are generated when you create, update, or delete cloud connections in a workspace:

| Event                               | Description                 |
| :----------------------------------- | :-------------------------- |
| `power-iaas.cloud-connection.create` | Creates a cloud connection  |
| `power-iaas.cloud-connection.delete` | Deletes a cloud connection  |
| `power-iaas.cloud-connection.list`   | Lists all cloud connections |
| `power-iaas.cloud-connection.read`   | Reads a cloud connection    |
| `power-iaas.cloud-connection.update` | Updates a cloud connection  |
{: caption="Cloud connections events" caption-side="bottom"}

### Placement groups events
{: #placement-groups-events}

The following events are generated when you create, update, or delete placement groups for {{site.data.keyword.powerSys_notm}} instances:

| Event                               | Description                |
| :----------------------------------- | :------------------------- |
| `power-iaas.placement-group.create`  | Creates a placement group  |
| `power-iaas.placement-group.delete`  | Deletes a placement group  |
| `power-iaas.placement-group.list`    | Lists all placement groups |
| `power-iaas.placement-group.read`    | Reads a placement group    |
| `power-iaas.placement-groups.update` | Updates a placement group  |
{: caption="Placement groups events" caption-side="bottom"}

### Shared processor pool (SPP) placement groups events
{: #spp-placement-groups-events}

The following events are generated when you create, update, or delete SPP placement groups:

| Event                                   | Description                      |
| :--------------------------------------- | :------------------------------- |
| `power-iaas.spp-placement-group.create`  | Creates an SPP placement group   |
| `power-iaas.spp-placement-group.delete`  | Deletes an SPP placement group   |
| `power-iaas.spp-placement-group.list`    | Lists all SPP placement groups   |
| `power-iaas.spp-placement-group.read`    | Reads an SPP placement group     |
| `power-iaas.spp-placement-groups.delete` | Deletes all SPP placement groups in a workspace |
| `power-iaas.spp-placement-groups.update` | Updates an SPP placement group   |
{: caption="SPP placement groups events" caption-side="bottom"}

### Data center events
{: #data-center-events}

The following events are generated when you list or read information and capabilities for {{site.data.keyword.off-prem-fname}} in {{site.data.keyword.off-prem}} or in {{site.data.keyword.on-prem}}:

| Event                               | Description                                                                   |
| :----------------------------------- | :---------------------------------------------------------------------------- |
| `power-iaas.datacenter-private.list` | Lists all data center information at a client location |
| `power-iaas.datacenter-private.read` | Reads the data center information at a client location  |
| `power-iaas.datacenter.list`         | Lists all IBM data center information                       |
| `power-iaas.datacenter.read`         | Reads the IBM data center information                 |
{: caption="Data center events" caption-side="bottom"}

### Host events
{: #host-events}

The following events are generated when you create, read, update, delete, or list dedicated hosts and host groups in a workspace:

| Event                            | Description                                    |
| :-------------------------------- | :--------------------------------------------- |
| `power-iaas.host-group.create`    | Creates a host group with one or more hosts    |
| `power-iaas.host-group.delete`    | Deletes a host group                           |
| `power-iaas.host-group.list`      | Lists all host groups for your workspace       |
| `power-iaas.host-group.read`      | Reads the details of a host group              |
| `power-iaas.host-group.update`    | Updates a host group                           |
| `power-iaas.host.delete`          | Releases a host from its host group            |
| `power-iaas.host.list`            | Lists all hosts that are available to a workspace |
| `power-iaas.host.read`            | Reads the details of a host                    |
| `power-iaas.host.update`          | Updates the display name of a host             |
| `power-iaas.available-hosts.list` | Lists all hosts that can be reserved           |
{: caption="Host events" caption-side="bottom"}

### Route events
{: #route-events}

The following events are generated when you create, update, or delete routes in a workspace:

| Event                    | Description                        |
| :------------------------ | :--------------------------------- |
| `power-iaas.route.create` | Creates a network route                    |
| `power-iaas.route.delete` | Deletes a network route                    |
| `power-iaas.route.list`   | Lists all network routes in a workspace |
| `power-iaas.route.read`   | Reads information about a network route    |
| `power-iaas.route.update` | Updates information for a network route    |
{: caption="Route events" caption-side="bottom"}

### SPP events
{: #spp-events}

The following events are generated when you create, read, update, delete, or list SPPs for a cloud instance:

| Event                                    | Description                                      |
| :---------------------------------------- | :----------------------------------------------- |
| `power-iaas.shared-processor-pool.create` | Creates an SPP                                   |
| `power-iaas.shared-processor-pool.delete` | Deletes an SPP from a cloud instance             |
| `power-iaas.shared-processor-pool.list`   | Lists all SPPs for a cloud instance              |
| `power-iaas.shared-processor-pool.read`   | Reads the details of an SPP for a cloud instance |
| `power-iaas.shared-processor-pool.update` | Updates an SPP for a cloud instance              |
{: caption="SPP events" caption-side="bottom"}

### Snapshot events
{: #snapshot-events}

The following events are generated when you list, read, update, or delete workspace snapshots:

| Event                       | Description                           |
| :--------------------------- | :------------------------------------ |
| `power-iaas.snapshot.list` (deprecated)   | Lists all snapshots in a workspace |
| `power-iaas.snapshot.read` (deprecated)  | Reads the details of a snapshot       |
| `power-iaas.snapshot.delete` | Deletes a snapshot                    |
| `power-iaas.snapshot.update` | Updates a snapshot                    |
{: caption="Snapshot events" caption-side="bottom"}

### Stock image events
{: #stock-image-events}

The following events are generated when you list or read available stock images for a workspace:

| Event                        | Description                                   |
| :---------------------------- | :-------------------------------------------- |
| `power-iaas.stock-image.list` | Lists all available stock images              |
| `power-iaas.stock-image.read` | Reads the details of an available stock image |
{: caption="Stock image events" caption-side="bottom"}

### Virtual serial number events
{: #virtual-serial-number-events}

The following events are generated when you list, read, update, or delete virtual serial numbers:

| Event                                    | Description                                                 |
| :---------------------------------------- | :---------------------------------------------------------- |
| `power-iaas.virtual-serial-number.delete` | Unreserves a retained virtual serial number                 |
| `power-iaas.virtual-serial-number.list`   | Lists all used and retained virtual serial numbers      |
| `power-iaas.virtual-serial-number.read`   | Reads the information for a virtual serial number           |
| `power-iaas.virtual-serial-number.update` | Updates the description of a reserved virtual serial number |
{: caption="Virtual serial number events" caption-side="bottom"}

### Workspace events
{: #workspace-events}

The following events are generated when you enable, disable, list, or read workspaces that belong to a tenant:

| Event                         | Description                                        |
| :----------------------------- | :------------------------------------------------- |
| `power-iaas.workspace.disable` | Disables a workspace                               |
| `power-iaas.workspace.enable`  | Enables a workspace                                |
| `power-iaas.workspace.list`    | Lists all workspace information and capabilities   |
| `power-iaas.workspace.read`    | Reads information of a workspace |
| `power-iaas.workspace.unknown` | Triggers an unknown action on a workspace          |
{: caption="Workspace events" caption-side="bottom"}

An `unknown` event is generated when an unrecognized action is triggered on a workspace.
{: note}

### Disaster recovery events
{: #disaster-recovery-events}

The following event is generated when you read disaster recovery site details for a data center location:

| Event                              | Description                                                                   |
| :---------------------------------- | :---------------------------------------------------------------------------- |
| `power-iaas.disaster-recovery.read` | Reads the disaster recovery site details for the current data center location |
{: caption="Disaster recovery events" caption-side="bottom"}

### Service broker events
{: #service-broker-events}

The following event is generated when you list supported storage tiers for a {{site.data.keyword.powerSys_notm}} instance:

| Event                           | Description                                            |
| :------------------------------- | :----------------------------------------------------- |
| `power-iaas.service-broker.read` | Lists all supported storage tiers for a {{site.data.keyword.powerSys_notm}} instance |
{: caption="Service broker events" caption-side="bottom"}

### Software tiers (IBM i licensing) events
{: #software-tiers-ibmi-licensing-events}

The following event is generated when you list supported software tiers for IBM i licensing:

| Event                          | Description                                            |
| :------------------------------ | :----------------------------------------------------- |
| `power-iaas.software-tier.list` | Lists all supported software tiers for IBM i licensing |
{: caption="Software tiers (IBM i licensing) events" caption-side="bottom"}

### Metadata and identity events
{: #metadata-and-identity-events}

The following events are generated when you create or request identity tokens or read metadata for a virtual server instance:

| Event                                              | Description                                                                       |
| :-------------------------------------------------- | :-------------------------------------------------------------------------------- |
| `power-iaas.metadata-identity-token.create`         | Creates an identity token                                                         |
| `power-iaas.metadata-computeresource-token.request` | Requests an IBM Cloud Identity and Access Management (IAM) access token           |
| `power-iaas.metadata-instance.read`                 | Reads information about the virtual server instance (VSI) that issued the request |
{: caption="Metadata and identity events" caption-side="bottom"}



## Viewing events
{: #at-viewing-events}

Events are automatically forwarded to North America, Europe, Tokyo, or Sydney geographic locations. You can access the {{site.data.keyword.logs_full_notm}} as follows:
- All North America and South America data centers from Dallas.
- All Europe data centers from Frankfurt.
- All Sydney data center from Sydney, and
- All Japan data center from Tokyo.











## {{site.data.keyword.logs_full_notm}} sample response format
{: #cloud-logs-response-sample}

The response format that is used in {{site.data.keyword.logs_full_notm}} follows the Cloud Auditing Data Federation (CADF) standard. This standard ensures that auditing events are collected and routed consistently across cloud platforms.

The CADF standard provides a framework for security auditing in cloud environments. It defines an event model that captures the data that is needed to certify, manage, and audit the security of cloud applications and services.

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

You can create a cloud log instance and provision it in the same region where your data center is located. For more information, see [Provisioning an instance](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui){: external}.


The {{site.data.keyword.powerSys_notm}} workspaces that run in various regions or data centers send events to {{site.data.keyword.logs_full_notm}} instances in their respective regions. You must create and provision instances of {{site.data.keyword.logs_full_notm}} in the regions where your workspaces are located to maintain access to {{site.data.keyword.powerSys_notm}} log events. If you want to export {{site.data.keyword.logs_full_notm}} data, see [Exporting data](/docs/cloud-logs?topic=cloud-logs-export-data){: external}.


The following table lists the data centers and their corresponding regions where you can deploy an {{site.data.keyword.logs_full_notm}} instance:


| Data centers | Current {{site.data.keyword.logs_full_notm}} region | New {{site.data.keyword.logs_full_notm}} region |
| ---------- | --------------------------------------------------- | ----------------------------------------------- |
| `WDC04`    | us-south                                            | us-east                                         |
| `WDC06`    | us-south                                            | us-east                                         |
| `WDC07`    | us-south                                            | us-east                                         |
| `MON01`    | us-south                                            | ca-tor                                          |
| `TOR04`    | us-south                                            | ca-tor                                          |
| `SAO01`    | us-south                                            | br-sao                                          |
| `SAO04`    | us-south                                            | br-sao                                          |
| `LON04`    | eu-de                                               | eu-gb                                           |
| `LON06`    | eu-de                                               | eu-gb                                           |
| `OSA21`    | jp-tok                                              | jp-osa                                          |
{: caption="Data centers and their corresponding IBM Cloud Logs instance regions" caption-side="bottom"}




