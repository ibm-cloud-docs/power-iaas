---

copyright:
  years: 2023, 2025

lastupdated: "2025-05-19"

keywords: PER, Power Edge Router, PER workspace, PER and Transit Gateway, IBM PER

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with the Power Edge Router
{: #per}

---



{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


{{site.data.keyword.on-prem-fname}} in [{{site.data.keyword.on-prem}}]{: tag-red}


---

A Power Edge Router (PER) is a high-performance router that provides advanced routing capabilities for {{site.data.keyword.powerSysFull}} users.
{: shortdesc}

PER improves network communication across different parts of the IBM network. The PER solution creates a direct connection to the IBM Cloud Multi Protocol Label Switching (MPLS) backbone, making it easy for different parts of the IBM network to communicate with each other. The PER solution consists of two routers that enable an aggregate connectivity of 400 Gbps to each {{site.data.keyword.powerSys_notm}} Performance Optimized Data (POD) center. A POD is a modular data center.




In a PER and enhanced CRN-enabled workspace, you can also define security rules for network traffic control using the network security group feature. For more information, see [Network security groups](/docs/power-iaas?topic=power-iaas-nsg).





The PER capability will be deployed in all the data centers over time. See [Data centers that support PER](/docs/power-iaas?topic=power-iaas-per#dcs-per) for more information.
{: note}

PER associates specific {{site.data.keyword.powerSys_notm}} networks with unique MPLS route distinguishers (RDs). The association different networks to communicate with each other across the IBM Cloud MPLS backbone.

To facilitate communication between {{site.data.keyword.powerSys_notm}} instances and other parts of the network, such as [Classic infrastructure](/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial), [Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-getting-started), and remote {{site.data.keyword.powerSys_notm}} instances, the [Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started&interface=ui) is used.

By using PER solution, as a {{site.data.keyword.powerSys_notm}} user you can access other IBM Cloud services, such as IBM Cloud domain name server (DNS), Network Time Protocol (NTP), and Cloud Object Storage. You can connect to these services without having to use proxies or virtual routers, as the PER solution includes a Network Address Translation (NAT) device that simplifies the access process.

The following network architecture diagram explains how the PER is integrated into the IBM Cloud environment:

![Power Edge Router network architecture diagram](./images/per-network-arch-diag.svg "Power Edge Router network architecture diagram"){: caption="Power Edge Router network architecture diagram" caption-side="bottom"}

The network traffic in a PER environment can flow in the following two ways:
- Accessing classic infrastructure through the Transit Gateway.
  - `1` - Traffic from ACI tenants is forwarded to the PER.
  - `2` - PER forwards the traffic to classic infrastructure services that use Transit Gateway.

- Accessing cloud services that can access the resources that are attached to each other.
  - `1`	- Traffic from ACI tenants is forwarded to the PER.
  - `3`	- Traffic from PER is forwarded to the NAT services with Service Gateway routers. The Service Gateway converts the destination addresses to ADN and CSE networks.
  - `4`	- The converted traffic from NAT is forwarded to PER.
  - `2` - Traffic from PER is now forwarded to IBM Cloud PPRs for final delivery.

The automation of ACI, PER, and NAT Services provisioning in IBM data centers is designed to simplify network integration and accelerate connection time for IBM {{site.data.keyword.powerSys_notm}} users in the IBM Cloud.

For detailed networking PER use cases and architecture diagrams, see [Power Edge Router use cases](/docs/power-iaas?topic=power-iaas-network-architecture-diagrams#per-use-cases).

## Considerations for using PER
{: #leverage-per}

- You cannot create a Cloud Connection or a VPN connection in a PER workspace.

- You can establish a connection between collocated workspaces if one colocation facility (colo) is PER-enabled (such as `DAL10`) and the second colo (`DAL12` / `DAL13`) uses [Direct Link](/docs/power-iaas?topic=power-iaas-ordering-direct-link-connect). Both collocated workspaces must be connected to the same Transit Gateway.

- When a PER workspace is connected to a Transit Gateway, you can connect a Direct Link to the same Transit Gateway. You can use the connection to achieve an end-to-end connectivity from a network in your client-managed environment to the PER workspace. 

- You can establish a connection between VPC and classic infrastructure with PER by adding them to the Transit Gateway.

- When you create private networks in a PER workspace, a maximum of one DNS server can be specified.

- A GRE (Generic Routing Encapsulation) tunnel is not supported in a PER workspace.

- You cannot create a non-PER workspace in a PER-enabled data center. However, you can still use your old non-PER workspaces that are existing in a PER-enabled data center that are created before PER rollout.

- In certain situations, local connection charges can apply when you connect from a client-managed location to {{site.data.keyword.powerSys_notm}}. To ensure accurate pricing, it is important to use the cost estimator tool. See the [Pricing of Power Edge Router](/docs/power-iaas?topic=power-iaas-migrate-ws-per) to learn more about PER pricing.


## Migrating to PER
{: #migrate-per}






The migration of an existing workspace to PER is supported through CLI by using the [ibmcloud pi workspace action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-action){: external} command with the following values:

- `per-migrate-start`: Initiates the migration of the workspace to PER.
- `per-migrate-validate`: Removes the Cloud Connections for the workspace from the network database. Use this command after you remove the Cloud Connections for the workspace from the Transit Gateway.







Before you migrate the last workspace in the data center to PER, delete any Cloud Connections that are not attached to any networks. After the migration, Cloud Connections can only be deleted using the [IBM Cloud CLI](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-cloud-connection-delete){: external} or [API](/apidocs/power-cloud#pcloud-cloudconnections-delete){: external} from a PER-enabled workspace.
{: note}







Complete the following steps to migrate the workspace to PER:

1. Remove the following connections:

   * Virtual private network (VPN) in your account that is connected to the data center of the workspace.
   * Manually configured VLANs by opening a support ticket.
   * Overlapping subnet CIDRs in your workspace.




2. Set the IBM Cloud Resource Names (CRN) value for the workspace to be migrated by using the `ibmcloud pi workspace target <crn>` CLI command.



3. Initiate the migration by using the `per-migrate-start` value with [ibmcloud pi workspace action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-action){: external} command.

   Use the CLI command [ibmcloud pi workspace get <WORKSPACE_ID> --json](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-get) to get the migration status of your workspace. In the CLI response, once the `migrationStatus` property changes to `migrating` and `state` property changes to `user-validation` you can continue to complete the next steps.

4. Attach the workspace to the Transit Gateway to validate the connectivity of the workspace with other workspaces.

5. Remove the Cloud Connections from the Transit Gateway.

6. Remove the Cloud Connections from the network database by using the `per-migrate-validate` value with [ibmcloud pi workspace action](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-action){: external} command.

   Use the CLI command [ibmcloud pi workspace get <WORKSPACE_ID> --json](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-workspace-get) to view the Cloud Connection clean up progress of the migration process. In the CLI response, once the `migrationStatus` property is not included and `state` property is set to `Active` state, the migration process is complete and the workspace and network operations can be resumed.

   You cannot delete the workspace and add or delete the subnets that are attached to the workspace until you complete the migration process by using the `per-migrate-validate` command.
   {: note}

If an error occurs during the migration process, open a support ticket.

The PER status is displayed in the **PER status** column on the [**Workspaces**](https://cloud.ibm.com/power/workspaces) page. Also, you can select a specific workspace to view its PER status on the **Workspace details** page.

If you are migrating the existing workloads to a new PER-enabled workspace, back up the data from the existing workspace, and restore the data to the new PER-enabled workspace.

Only `CHE01` and `MON01` data centers are not PER-enabled. Therefore, use Cloud Connections for interconnectivity between other parts of the IBM network.



Complete the following steps to connect an existing non-PER workspace to an existing Transit Gateway by using the IBM Cloud command-line interface (CLI):

1. Use the `ibmcloud pi workspaces` command to list the {{site.data.keyword.powerSys_notm}} workspaces in your account.
   Make note of the cloud resource name (CRN) for the workspace that you want to connect to the Transit Gateway.

2. Use the `ibmcloud tg gateways` command to list the Transit Gateways within your account.
   Make a note of the gateway ID that you want to connect to the {{site.data.keyword.powerSys_notm}} workspace.

3. Use the `ibmcloud tg connection-create` command to create a new connection between the Transit Gateway and the PER-enabled workspace.

For example, `ibmcloud tg connection-create aaaa-bbbb-cccc-dddd-eeee —name powervs_per_fra02 —network-id crn:v1:bluemix:public:power-iaas:fra02:a/aaaa:bbbb:: —network-type power_virtual_server` is an executable command, where:
 - Transit Gateway ID is `aaaa-bbbb-cccc-dddd-eeee`
 - The {{site.data.keyword.powerSys_notm}} workspace CRN is `crn:v1:bluemix:public:power-iaas:fra02:a/aaaa:bbbb::`


## Creating a PER workspace
{: #create-per-workspace}



All the data centers, except `CHE01` and `MON01`, are PER-enabled. When you create a workspace in the PER-enabled data center, the workspace is PER-enabled by default.




To create a PER workspace, follow the steps that are mentioned in [Creating a {{site.data.keyword.powerSys_notm}} workspace](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-service) and choose a PER-enabled data center.

You can check whether a workspace is PER-enabled by selecting the workspace and viewing the details of the workspace. The PER-enabled workspace shows an information message on Transit Gateway.
{: note}

You can create, delete, attach, detach, and update private networks by using the **Subnets** and **Virtual server instances** pages on a PER workspace, the same as with a non-PER workspace. However, private networks on PER workspaces in a PER-enabled data center, such as `DAL10`, use upgraded networking technology for higher performance, and seamless connectivity. See, [Configuring and adding a private network subnet](/docs/power-iaas?topic=power-iaas-configuring-subnet) to complete a necessary operation.

Use Transit Gateway only to configure the virtual connections, as opposed to using Cloud connection.

On a PER workspace, if you do not find the **cloud Connections** and **VPN connections** options in the left navigation of the user interface, then PER do not require or support these options.
{: note}

On a PER workspace, you can do the following actions:
* Attach a network without creating a separate Cloud Connection such as Direct Link.
* Attach a connection to the IBM cloud network after you attach the Transit Gateway with your PER workspace.
* Connect to your network in the client-managed environment by creating a Direct Link. Attach the Direct Link with the Transit Gateway that is present on the PER workspace.

To delete the PER workspaces that are connected to the Transit Gateway, you must first delete the Transit Gateway connections.
{: important}

### Using IBM cloud services in a PER workspace
{: #cloud-services-per}

From your PER workspace, you can create a virtual server instance and attach subnets to it. These virtual server instances can then access the IBM Cloud resources such as Cloud Object Storage, Domain Name System (DNS), and other services that use the allocated IP addresses in the range `161.26.0.0/16`. See [IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints) for more information.

Attach the workspace to the Transit Gateway if you want to connect your workspace with the VPC and classic infrastructure.
{: important}

### Attaching Transit Gateway to a PER workspace
{: #tgw-per}

Transit Gateway is required to connect with VPC and classic infrastructure. To attach a virtual server instance from a PER workspace with the Transit Gateway, follow the instructions in the [Ordering IBM Cloud Transit Gateway.](/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui)

Select **{{site.data.keyword.powerSys_notm}}** under connection to attach a virtual server instance that was created on a PER-enabled workspace. You can also add VPC and classic infrastructures as connection.

The connections attached to the Transit Gateway can communicate with each other. For example, a {{site.data.keyword.powerSys_notm}} workspace and VPC added under the Transit Gateway connection can access the resources that are associated with each other.

Make sure that the classic infrastructure is Virtual Routing and Forwarding (VRF) enabled before you attach it to the Transit Gateway.
{: note}

## OS support in a PER workspace
{: #os-per}

AIX, IBM i, and Linux operating systems are supported in a PER workspace.

### AIX and IBM i support on PER
{: #aix-ibmi-per}

AIX and IBM i operating systems operate in PER workspaces in the same way that they do in non-PER workspaces.

### Full Linux Subscription with PER
{: #aix-linux-per}

See [Full Linux® subscription for {{site.data.keyword.powerSys_notm}}s](/docs/power-iaas?topic=power-iaas-set-full-Linux) for {{site.data.keyword.powerSys_notm}} to register `RHEL84`, `SLES SP2`, `SLES SP3` images on a non-PER workspace.
{: note}

Full Linux subscription `RHEL86` and `SLES15 SP4` images can be used in a PER workspace. Follow these instructions for a PER-enabled workspace to let the virtual server instance automatically register a full Linux subscription:
1.  Create a private network.
    1.  Open the {{site.data.keyword.powerSys_notm}} user interface from the IBM Cloud console.
    2.  Click **Subnets** under **Networking** in the left navigation menu.
    3.  Click **Create subnet**.
    4.  Enter a unique name and CIDR.
        Make sure the CIDR being used is not the same as another CIDR already in use or a subset of that CIDR. The host server for the satellite server will be unable to resolve a network conflict as a result.
    5.  Enter `161.26.0.10` in the **DNS server** field.

2. Create a virtual server instance. See, [Configuring a {{site.data.keyword.powerSys_notm}} instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance) for detailed instructions.
3. Attach the private network created in step 1.
4. Verify whether the registration is successful with the following commands:

 For SUSE:
   ```code
   SUSEConnect -s
   ```

 For RHEL:
   ```code
   subscription-manager status
   ```

## CLI and API support with PER
{: #cli-api-per}

PER uses the same existing {{site.data.keyword.powerSys_notm}} network APIs and CLIs.

For more information, refer to the {{site.data.keyword.powerSys_notm}} documentation on:
- API - [Create a new cloud connection](/apidocs/power-cloud#pcloud-cloudconnections-post)
- CLI - [Create a cloud connection](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-cloud-connection)

## Data centers that support PER
{: #dcs-per}

The following table shows the available data centers for {{site.data.keyword.powerSys_notm}} and its corresponding status against PER:

| Data centers | PER available |
|-----|-----|
| `CHE01` | X |
| `DAL10` | ![Checkmark icon](./images/checkmark.svg) |
| `DAL12` | ![Checkmark icon](./images/checkmark.svg) |
| `DAL13` | ![Checkmark icon](./images/checkmark.svg) |
| `DAL14` | ![Checkmark icon](./images/checkmark.svg) |
| `FRA04` | ![Checkmark icon](./images/checkmark.svg) |
| `FRA05` | ![Checkmark icon](./images/checkmark.svg) |
| `LON04` | ![Checkmark icon](./images/checkmark.svg) |
| `LON06` | ![Checkmark icon](./images/checkmark.svg) |
| `MAD02` | ![Checkmark icon](./images/checkmark.svg) |
| `MAD04` | ![Checkmark icon](./images/checkmark.svg) |
| `MON01` | X |
| `OSA21` | ![Checkmark icon](./images/checkmark.svg) |
| `SAO01` | ![Checkmark icon](./images/checkmark.svg) |
| `SAO04` | ![Checkmark icon](./images/checkmark.svg) |
| `SYD04` | ![Checkmark icon](./images/checkmark.svg) |
| `SYD05` | ![Checkmark icon](./images/checkmark.svg) |
| `TOK04` | ![Checkmark icon](./images/checkmark.svg) |
| `TOR01` | ![Checkmark icon](./images/checkmark.svg) |
| `WDC04` | ![Checkmark icon](./images/checkmark.svg) |
| `WDC06` | ![Checkmark icon](./images/checkmark.svg) |
| `WDCO7` | ![Checkmark icon](./images/checkmark.svg) |
{: row-headers}
{: class="comparison-table"}
{: caption="{{site.data.keyword.powerSys_notm}} supported data centers and its status for PER" caption-side="bottom"}
