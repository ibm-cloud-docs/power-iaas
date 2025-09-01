---

copyright:
  years: 2024

lastupdated: "2025-07-29"

keywords: Microsoft Azure, Power-iaas multi cloud, PowerVS Azure, Megaport and Azure, megaport

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Connecting IBM {{site.data.keyword.powerSys_notm}} to Microsoft Azure with Megaport
{: #connect-azure-with-megaport}

This topic provides architectural solution guidelines for running {{site.data.keyword.powerSysFull}}s and IBM Cloud with private connectivity between IBM Cloud and Microsoft Azure by using Megaport.

The solution is based on publicly available documentation from:

- [IBM Cloud](https://www.ibm.com/cloud){: external}
- [Microsoft Azure](https://azure.microsoft.com/){: external}
- [Megaport](https://www.megaport.com/){: external}


## Solution architecture overview
{: #solution-architecture-overview}

This section provides an overview of the solution architecture, and includes an overview of the solution components and cloud services that are used.

This solution provides private network connectivity between IBM {{site.data.keyword.powerSys_notm}} and Microsoft Azure for high-performance peer-to-peer connection of cross-cloud workloads. The architecture uses private connection services through IBM Cloud Direct Link, which is coupled with Microsoft Azure ExpressRoute, and joined by the Megaport Cloud Router.

![Private connectivity between IBM Power Virtual Server and Microsoft Azure](./images/pvs_azure_architechture.svg "Private connectivity between IBM Power Virtual Server and Microsoft Azure"){: caption="Private connectivity between IBM Power Virtual Server and Microsoft Azure" caption-side="bottom"}

{{site.data.keyword.powerSys_notm}} workspace
:   A container of all the virtual machines, storage volumes, network configurations, and so on, at a specific geographic region.

IBM Cloud Transit Gateway
:   Provides interconnectivity across various IBM Cloud platforms. You can create single or multiple transit gateways to connect VPCs, {{site.data.keyword.powerSys_notm}} workspaces, or IBM Cloud classic infrastructure.

IBM Cloud Direct Link
:   A routed, OSI L3 service that offers a direct connection to the IBM Cloud Private network backbone, with low latency and uses BGP as the routing protocol.

Megaport Cloud Router (MCR)
:   A managed virtual router service that enables direct networking between endpoints on the Megaport network, which can be purchased without the user having a physical presence in that data center.

Virtual Cross Connect (VXC)
:   A connection between any two endpoints on the Megaport network. Most connections support capacity ranging from 1 Mbps to 10 Gbps.

Microsoft Azure ExpressRoute (ER)
:   Extends your {{site.data.keyword.on-prem}} networks into the Microsoft cloud over a private connection with the help of a connectivity provider.

Microsoft Azure virtual network gateway
:   A service that enables you to establish connectivity between your `virtual network (vNet)` in Microsoft Azure and your {{site.data.keyword.on-prem}} infrastructure.

### Building the interconnectivity
{: #build-interconnect}

To provide private connectivity to IBM Cloud, you can use IBM Cloud Direct Link (DL) and Transit Gateway (TGW). In Microsoft Azure, the equivalent offerings are called ExpressRoute and Virtual network gateway. In addition to these core cloud services, you need a connectivity provider. This example uses Megaport offerings, Megaport Cloud Router (MCR), and Virtual Cross Connects (VXC).
This solution focuses on providing connectivity with IBM {{site.data.keyword.powerSys_notm}}, but you might have other workload needs. IBM Cloud VPC, IBM Cloud classic infrastructure, and various VMware Solutions integrate in a similar way by using IBM Cloud Transit Gateway as the core routing service between the platforms.

The following diagram shows a high-level overview of the solution and explains how the solution components are used.

![Building interconnectivity between IBM Power Virtual Server and Microsoft Azure](./images/building_interconnectivity.svg "Building interconnectivity between IBM Power Virtual Server and Microsoft Azure"){: caption="Building interconnectivity between IBM {{site.data.keyword.powerSys_notm}} and Microsoft Azure" caption-side="bottom"}

1. `IBM Cloud Transit Gateway` provides interconnectivity across various IBM Cloud platforms. You can create single or multiple transit gateways to connect VPCs, {{site.data.keyword.powerSys_notm}} workspaces, or IBM Cloud classic infrastructure. New networks connected to a TGW are automatically made available to every other network connected to it. You can also provision Unbound GRE tunnels to your TGW that can be used to connect various network appliances or either self-managed or IBM-managed VMware Cloud Foundation (VCF) instances to the TGW.
2. `IBM Cloud Direct Link` service is a routed, OSI L3 service. It offers a direct connection to the IBM Cloud Private network backbone, with low latency and uses BGP as the routing protocol. IBM Cloud Direct Link can be attached to most IBM Cloud IaaS platforms, or you can attach it to a Transit Gateway where it can provide private interconnectivity to all connections attached to a TGW. IBM Cloud does not provide built-in connection redundancy as part of the product. To establish redundant connectivity, you must acquire two connections on diverse cross-connect routers (XCRs) and configure BGP on each IBM Cloud Direct Link.
3. `Megaport Cloud Router (MCR)` is a managed virtual router service that enables direct networking between endpoints on the Megaport network. MCR can be purchased as a stand-alone service to route traffic between different cloud environments without the user having a physical presence in that data center. It can also be connected to user Ports to route pertinent traffic back to a physical location. BGP is used as the routing protocol to learn and advertise routes to its connections.
4. `A Port` is the physical point of connection between your organization’s network and the Megaport network. After you have configured a Port or an MCR, you can create `Virtual Cross Connects (VXCs)` to connect to services on the Megaport network. A VXC is a private point-to-point Ethernet connection between your A-End Port (MCR) and a B-End destination (CSPs, Ports, Megaport Marketplace services, or IX). In this scenario, the B-End destinations are IBM Cloud and Microsoft Azure.
5. `Microsoft Azure ExpressRoute (ER)` extends your {{site.data.keyword.on-prem}} networks into the Microsoft cloud over a private connection with the help of a connectivity provider. With ExpressRoute, you can establish OSI L3 connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365. Redundancy is built in ExpressRoute in every peering location for high availability. ExpressRoute uses BGP as the routing protocol to advertise and learn routes from Microsoft Azure to the connected router, and to/from MCR in this example.
6. `Microsoft Azure virtual network gateway`is a service that enables you to establish connectivity between your `virtual network (vNet)` in Microsoft Azure and your {{site.data.keyword.on-prem}} infrastructure. It acts as a router between your vNets and your {{site.data.keyword.on-prem}} network (in this case, IBM Cloud).

## Configuring the solution architecture
{: #configure-sol-arch}

The following sections provide links to external resources with the detailed steps and examples on what is needed to configure and validate end-to-end connectivity:

1. [Configure IBM {{site.data.keyword.powerSys_notm}} environment](#configure-pvs-env).
2. [Configure a Megaport Cloud Router (MCR)](#megaport-portal).
3. [Configure IBM Cloud Direct Links and Virtual Cross Connections (VXC)](#create-connection-mcr).
4. [Configure Microsoft Azure ExpressRoute circuits](#expressroute).

See the architecture diagram for [private connectivity between IBM {{site.data.keyword.powerSys_notm}} and Microsoft Azure](#build-interconnect) to get a high-level information.

This solution uses the following networks as shown in the table:

| Platform or service                 | Network details |
|-------------------------------------|-----------------|
| {{site.data.keyword.powerSys_notm}} | 10.100.10/24    |
| Microsoft Azure                               | 10.200.10/24    |
| {{site.data.keyword.on-prem}} networks                | 10.0.10/24      |
{: caption="Network details" caption-side="bottom"}

## Configuring the {{site.data.keyword.powerSys_notm}} environment and Transit Gateway in IBM Cloud
{: #configure-pvs-env}

### IBM Cloud Account configuration
{: #ibm-account-config}

#### Obtaining IBM Cloud Account ID
{: #obtain-ibm-cloud-account-id}

To establish private connectivity by using cloud connectivity providers, you need to obtain the IBM Cloud Account ID. This 32-character unique identifier identifies your IBM Cloud account that owns the IBM Cloud Direct Link service.

To obtain your IBM Cloud Account ID, follow the instructions that are provided in the [IBM Cloud Docs pages](https://cloud.ibm.com/docs/account?topic=account-accountfaqs#account-details).




### Configuring the {{site.data.keyword.powerSys_notm}}
{: #configure-pvs}

#### Provisioning a workspace and instance
{: #provision-ws-vm}

{{site.data.keyword.powerSys_notm}} resources reside in IBM data centers with dedicated networking and Storage area network (SAN)-attached Fibre Channel storage. You can choose one of the regions that is listed in the specifications that are nearest to your data center. In the data centers, the {{site.data.keyword.powerSys_notm}}s are separated from the rest of the IBM Cloud servers with separate networks and direct-attached storage, and you can use IBM Cloud interconnectivity offerings to provide connectivity to IBM Cloud infrastructure or private cloud environments.

To provision and configure your IBM {{site.data.keyword.powerSys_notm}} environment in IBM Cloud, you need to create the following IBM {{site.data.keyword.powerSys_notm}} items:

- A workspace
- A private network subnet
- An SSH Key
- An instance

For more information, see IBM Cloud docs pages [how to configure networking](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-configuring-subnet) and [how to create {{site.data.keyword.powerSys_notm}}](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-creating-power-virtual-server).


### Configuring IBM Cloud Transit Gateway
{: #configure-tgw}

#### Provisioning a Transit Gateway
{: #provision-tgw}

Transit gateway provides routed L3 private interconnectivity to your {{site.data.keyword.powerSys_notm}} instances to other IBM Cloud IaaS platforms or your private networks via Transit Gateway that is attached to IBM Cloud Direct Link. To provision a Transit Gateway, you need to:
   - Create an IBM Cloud Transit Gateway Instance

For more information on how to create a Transit Gateway, see the [IBM Cloud Docs pages](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-ordering-transit-gateway&interface=ui).

#### Adding {{site.data.keyword.powerSys_notm}} environment to Transit gateway
{: #add-tgw-pvs}

Before your {{site.data.keyword.powerSys_notm}} workspace can use Transit Gateway, it must be added as a Transit Gateway connection. If required, you might optionally configure prefix filtering, if you do not want to advertise all Power PV subnets to the selected Transit Gateway.

To configure a Transit Gateway, you need to:

- Create a connection between TGW and your IBM {{site.data.keyword.powerSys_notm}} workspace instance
- Configure prefix filtering on the {{site.data.keyword.powerSys_notm}} Transit Gateway connection

For more information on how to add a {{site.data.keyword.powerSys_notm}} connection to your Transit Gateway, see [IBM Cloud Docs pages](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-adding-connections&interface=ui).


## Configuring hybrid cloud connectivity with Megaport
{: #configure-hybrid-cloud}

### Configuring Megaport portal
{: #megaport-portal}

In this section, you configure the connectivity between Megaport and IBM Cloud. You need to:

- Create a Megaport Cloud Account
- Provision a Megaport Cloud Router
- Create a Megaport Virtual Cross Connect
- Create IBM Cloud Direct Link Authorization of Megaport VXC connection

This section provides an overview of the configuration steps. For a more detailed explanation, refer to [Megaport documentation](https://docs.megaport.com/getting-started/){: external}.

#### Creating a Megaport account
{: #create-mega-ac}

The first step is to log in to the Megaport portal: [https://portal.megaport.com/login](https://portal.megaport.com/login){: external} and configure your account, or you can skip to the next step “**Creating a Megaport Cloud Router**”.


**Setting up a new Megaport Account** ([https://docs.megaport.com/setting-up/](https://docs.megaport.com/setting-up/){: external})

1. Create a company profile

2. Add technical support contact details

3. Set up a billing account and assign a user role to a finance contact for invoice purposes.

4. After you complete these steps, you can provision new services, test connectivity, and verify service pricing.


#### Creating a Megaport Cloud Router
{: #create-mega-router}

The Megaport Cloud Router (MCR) is a managed virtual router service that establishes Layer 3 connectivity on the worldwide Megaport software-defined network (SDN). MCR instances are preconfigured in data centers in key global routing zones. An MCR enables data transfer between multi-cloud or hybrid cloud networks, network service providers, and cloud service providers.

An MCR joins two or more independent Virtual Cross Connect (VXC) services into a single routing domain, providing connectivity between all the VXCs attached to the MCR. In this example, two VXCs are needed; one for IBM Cloud Direct Link and one for Microsoft Azure ExpressRoute. VCXs are configured after the MCR is provisioned.

To create an MCR, you need to make a few decisions for the connectivity. The following table is a worksheet of some of the configuration options that you customize based on your solution.


| Configurable Field | Description of Option | Example Choice |
| -------------------| ----------------------| ---------------|
| MCR Location | Geo Location to be used | Equinox EQ1 |
| Rate Limit | What network speed you would like to order| 1 Gbps to 10 Gbps|
| MCR Name | Specify a name for the MCR that is easily identifiable | IBM-Azure-MCR |
| Minimum Term | Select your term length |- No Minimum Term  \n - 12 Months  \n - 24 Months  \n - 36 Months  |
| BGP State | Select whether BGP connections are enabled  \n or shut down by default | Enabled |
{: caption="Megaport Cloud Router Worksheet" caption-side="bottom"}


For a detailed explanation of the steps required, refer to [Megaport documentation](https://docs.megaport.com/mcr/creating-mcr/).

To find details for IBM Cloud Direct Link connectivity locations, see the [IBM Cloud Docs pages](https://cloud.ibm.com/docs/dl?topic=dl-locations#connect-locations).

### Creating a connection from MCR to IBM Cloud Direct Link
{: #create-connection-mcr}

IBM Direct Link lets you seamlessly create private connections between your {{site.data.keyword.on-prem}} and cloud resources. Direct Link Connect with Megaport extends your organizations data center network to public clouds to offer better performance, higher throughput, and security to IBM Cloud environments.

#### Creating a Megaport connection to IBM Direct Link
{: #create-megaport-to-dl}

To set up IBM Direct Link with Megaport, you need to create a Virtual Cross Connect (VXC) from your MCR in the Megaport Portal to the IBM Direct Link cloud location.

Design considerations when setting up your Direct Link to IBM Cloud:

Redundancy
:   The megaport supports redundant connections. In each of the Direct Link peering locations, Megaport established two diverse Direct Links with IBM Cloud. In the [Megaport Portal](https://portal.megaport.com/){: external}, the Ports are noted as Port 1 and Port 2. A redundant IBM Cloud Direct Link configuration requires two or more VXCs.

Local and Global routing options
:   The Local Routing option provides access to data centers with the same three-letter prefix as the Point of Presence (such as DAL, AMS, and MEL). The Global Routing option is required as an add-on to reach data centers outside of those locations. For more information on local and global routing options, see the [IBM cloud documentation](https://cloud.ibm.com/docs/direct-link).

Port speed
:    Port speed options for IBM Direct Link Connect are 50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, or 5 Gbps.

#### Creating a VXC to the IBM Direct Link Connect
{: #create-vxc-dl}

A VXC is a point-to-point Layer 2 circuit between two endpoints that is mapped with a VLAN ID on each end. You can order VXCs to reach any destination in the Megaport network just like the VXCs used with the physical Ports.

This section describes how to connect to IBM Direct Link from an MCR. For more information on connecting from a Port, see [Connecting to IBM Cloud Direct Link](https://docs.megaport.com/cloud/megaport/ibm/direct-link-2.0/).

You can also watch this [Private Connectivity to IBM Cloud](https://www.youtube.com/watch?v=FK8ZDjlZsSM){: external} video, which shows how quick and easy to connect to IBM Cloud using Megaport.

See the documentation outlined in [Megaport documentation](https://docs.megaport.com/cloud/mcr/ibm-2.0/), by using the worksheet fields that you entered previously.

After your connection is added, the next steps are to authorize on the IBM Cloud Console.

| Configurable Field | Description of Option | Example Choice |
| -------------------| ----------------------| ---------------|
|Cloud Connection | Choose your cloud provider | IBM Cloud |
| VXC Connection name | Unique name | IBM-Cloud-MCR-1|
| Rate Limit | The speed of your connection in Mbps | |
| Minimum Term | Select your term length |- No Minimum Term  \n - 12 Months  \n - 24 Months  \n - 36 Months |
| IBM Account ID | Your IBM Cloud account ID. Learn more on the [Managing your account, resources, and access documentation](/docs/account?topic=account-accountfaqs#account-details) | The account ID is a 32-character, unique account identifier. |
{: caption="Megaport Virtual Cloud Connection: IBM Cloud Worksheet" caption-side="bottom"}



### IBM Cloud Direct Link Configuration
{: #dl-config}

Before following to this step, make sure that all services are being properly provisioned in Megaport.

#### Approving Megaport Direct Connection in IBM Cloud Portal
{: #approve-mega-dl}

After the Megaport VXC has been successfully ordered in the previous step, you will be able to see the IBM Cloud Direct Link connection ready for approval. Take the following steps.

1. Log in to your [IBM cloud](https://cloud.ibm.com/login){: external} account.
2. Click menu on the upper left of the page, then click **Interconnectivity**.
3. Click **Direct Link** in the navigation pane.
4. Click the name of the direct link that you want to change the connection.
5. Click the **Review** button.
6. Specify the resource group.
7. Choose your routing (local).
8. Click **Next**, then **Next** again on AS prepends and route filtering.
9. Click **Create** and wait for the status to change to **“Provisioned”**

#### Adding Direct Link Connection to IBM Cloud Transit Gateway
{: #add-dl-tgw}

After the Megaport and IBM Cloud Direct Link have been provisioned successfully in the previous steps, the next step is to add the IBM Cloud Direct Link to the IBM Cloud Transit Gateway.

1. Log in to your [IBM cloud](https://cloud.ibm.com/login){: external} account.
2. Click menu on the upper left of the page, then click **Interconnectivity**.
3. Click **Transit Gateway** in the navigation pane.
4. Click the name of the **Transit Gateway** that you want to change the connection type for.
5. Click Create Connection.
    1. In the drop-down list menu, select **Direct Link**.
6. Select the Direct Link connection and Connection name.
7. Click **Create**, and then wait for the **Available Status**.

Repeat the add connection steps to add {{site.data.keyword.powerSys_notm}}

1. Click Create Connection.
2. In the drop-down list menu, select **Power Systems Virtual Server**.
3. Select the {{site.data.keyword.powerSys_notm}} Location and Connection name.
4. Click Add, and then wait for the **Available Status**.

#### Verifying IBM Cloud and Megaport are sharing routing information
{: #verify-routing-info}

Verification of the network routes being shared can be done both in IBM Cloud and Megaport.

For IBM Cloud from the Transit Gateway interface, select the Routes tab. This interface displays the {{site.data.keyword.powerSys_notm}} network subnet. Check for the network of {{site.data.keyword.powerSys_notm}} “azure-power-test-1” and the learned routes.

1. Log in to your [IBM cloud](https://cloud.ibm.com/login){: external} account.
2. Click menu on the upper left of the page, then click **Interconnectivity**.
3. Click **Transit Gateway** in the navigation pane.
4. Click the name of the **Transit Gateway** whose routes you want to check.
5. Click the **Routes** tab and generate a route report.
6. On the **Routes** tab, filter the {{site.data.keyword.powerSys_notm}} allocated subnet ranges to see the learned routes.
7. On the **BGP** tab, filter the {{site.data.keyword.powerSys_notm}} allocated subnet ranges to see the BGP AS-path.

For more information about Route Reports on Transit Gateway, see [IBM Cloud Docs pages](/docs/transit-gateway?topic=transit-gateway-route-reports&interface=ui).

You can also check the routing and BGP tables by using Megaport Cloud Router Looking Glass.

1. Log in to your [Megaport](https://portal.megaport.com/){: external} account.
2. Click Services on the upper tabs.
3. You can filter based on your MCR name.
4. Click the **Megaport Cloud Router Looking Glass** icon on the MCR.
5. Select your **BGP session towards IBM Cloud Direct Link** and click **Neighbor routes**. Select **Received** to see the routes the MCR has learned from IBM Cloud Direct Link. You might optionally filter based on the specific prefix, if you have several advertised routes.

For more information about MCR Looking Glass, see [Megaport documentation](https://docs.megaport.com/mcr/mcr-looking-glass/){: external}.

#### Performing route filtering and AS-path prepends
{: #route-filtering}

In some cases, you might need to filter some routes to be advertised to Megaport from IBM Cloud Transit Gateway connections, or you might want to prioritize your preferred routing paths with AS-prepends, if you have multiple Direct Links attached. The following diagram depicts an overview of how route filtering and AS-prepends work in the IBM Cloud interconnectivity solutions.

![Route filtering and AS-prepending with Transit Gateway and Direct Links](./images/route_filterig_tgw_dl.svg "Route filtering and AS-prepending with Transit Gateway and Direct Links"){: caption="Route filtering and AS-prepending with Transit Gateway and Direct Links" caption-side="bottom"}

For route filtering, you can use either use Transit Gateway’s route filtering capabilities or apply route filtering on Direct Link, depending on where you want to filter the routes. With Transit Gateway, you can only filter learned prefixes (import) from the connections. With Direct link, you can apply route filters for both learned (import) and advertisements (export). You can also attach GRE tunnels to a Transit Gateway. With GRE tunnels, the route filtering is done with BGP from the connecting router/gateway.

For more information on route-filtering, see the IBM Cloud Docs pages for [Transit Gateway](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-adding-prefix-filters&interface=ui){: external} and [Direct Link](https://cloud.ibm.com/docs/dl?topic=dl-filter-routes&interface=ui){: external}.

For AS-prepends, you can use Direct Link’s AS-prepend capabilities to alter the length of the learned (import) or advertised (export) AS-paths. When using GRE tunnels, it is recommended to connect to all Transit Gateway routers in the multizone region, and you might want to control your preferred GRE tunnels with BGP metrics/attributes. With GRE tunnels, the AS-prepends are done with BGP from the connecting router/gateway.

For more information AS-prepending, see the following IBM Cloud Docs pages for [Direct Link](https://cloud.ibm.com/docs/dl?topic=dl-prepend-as-paths&interface=ui){: external}. For GRE tunnels, see the [Transit Gateway pages](https://cloud.ibm.com/docs/transit-gateway?topic=transit-gateway-helpful-tips#gre-considerations){: external} in IBM Cloud Docs.

## Creating ExpressRoute through Microsoft Azure portal
{: #expressroute}

Complete the following steps to create and provision a Microsoft Azure ExpressRoute circuit.

1. Sign in to the [Microsoft Azure portal](https://portal.azure.com/){: external}.
2. Create a new ExpressRoute circuit. On the Microsoft Azure portal menu, select **+ Create a resource**. Search for **ExpressRoute** and then select Create.
3. On the Create ExpressRoute page, provide the **Resource Group**, **Region**, and **Name** for the circuit. Then, select **Next: Configuration >**.
4. Enter the required values for the ExpressCircuit. For more information, see [Microsoft Azure documentation](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager?pivots=expressroute-current){: external}.
5. Select **Review + create** and then select **Create** to deploy the ExpressRoute circuit.

After provisioning is complete, view the circuits and properties.

1. Search for **ExpressRoute circuits** in the search box at the top of the portal.
2. Select your circuit and view the properties of the circuit by selecting it.
3. On the Overview page for your circuit, find the **Service Key**. Provide the service key to the service provider to complete the provisioning process. The service key is unique to your circuit.

For more information about Microsoft Azure ExpressRoute, see [Microsoft Azure documentation](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager?pivots=expressroute-current){: external}.


### Creating a connection from the Megaport Cloud Router to Microsoft Azure ExpressRoute
{: #create-mcr-expressroute}

Next, you can create a VXC from an MCR to Microsoft Azure ExpressRoute through the [Megaport Portal](https://portal.megaport.com/){: external}. You can create the VXC to Microsoft Azure from the MCR and establish either private or Microsoft peering.

To connect to ExpressRoute using MCR, you need an ExpressRoute service key that is obtained from the Azure Resource Manager (ARM) portal. Follow the steps in the Microsoft topic [Tutorial: Create and modify an ExpressRoute circuit](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-circuit-portal-resource-manager){: external} to get this key.

To create a VXC from a Megaport Cloud Router (MCR) to Microsoft Azure:

1. In the [Megaport Portal](https://portal.megaport.com/){: external}, go to the **Services** page and select the MCR you want to use.
2. Add a new **VXC connection** for the MCR. Click **+Connection**, click **Cloud**, and click **Azure ExpressRoute**.
3. Provide the Azure Service Key (from Microsoft Azure Portal, see [Microsoft Azure documentation](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager?pivots=expressroute-current){: external}).

For more information, see [Megaport documentation](https://docs.megaport.com/mcr/mcr-looking-glass/){: external}.



### Configuring peering and virtual network gateway through the Microsoft Azure portal
{: #config-peering-azure}

#### Creating and modify peering for an ExpressRoute circuit
{: #create-peering-expressroute}

Create a routing configuration for an Azure Resource Manager ExpressRoute circuit by using the Microsoft Azure portal. Follow the steps for Microsoft Azure private peering. You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit. Follow the documentation steps in [Microsoft Azure documentation](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager?pivots=expressroute-current){: external}.

#### Configuring a virtual network gateway for ExpressRoute
{: #config-vnetwork}

Add a virtual network gateway for a virtual network (VNet). Follow the documentation steps in [Microsoft Azure documentation](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager?pivots=expressroute-current){: external}. For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-about-virtual-network-gateways){: external}.

#### Connecting a virtual network to ExpressRoute circuits
{: #conect-vnetwork}

Create a connection to link a virtual network to Microsoft Azure ExpressRoute circuits by using the Microsoft Azure portal. Follow the documentation steps in [Microsoft Azure documentation](https://learn.microsoft.com/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager?pivots=expressroute-current){: external}.

#### Verifying Microsoft Azure and Megaport are sharing routing information
{: #verify-routs-info}

Check the routing and BGP tables by using MCR Looking Glass.

1. Log in to your [Megaport](https://portal.megaport.com/){: external} account.
2. Click **Services** on the upper tabs.
3. You can **filter** based on your MCR name.
4. Click the **MCR Looking Glass** icon on the MCR.
5. Select your **BGP session toward IBM Cloud Direct Link** and click **Neighbor routes**. Select **Received** to see the routes MCR has learned from IBM Cloud Direct Link. You might optionally filter based on the specific prefix, if you have several advertised routes.

For more information about MCR Looking Glass, see [Megaport documentation](https://docs.megaport.com/mcr/mcr-looking-glass/){: external}.

## Verification of end-to-end connectivity
{: #ver-ete-conn}

### Checking routing tables and BGP
{: #rou-tab-BGP}

Check the routing and BGP tables by using MCR Looking Glass.
1.	Log in to your [Megaport](https://portal.megaport.com/login){: external} account.
2.	Click the **Services** tab.
3.	You can filter based on your MCR name.
4.	Click the **MCR Looking Glass** icon on the MCR.
5.	Click the **Routes Table** tab and filter the routes that are assigned to IBM {{site.data.keyword.powerSys_notm}}.
6.	Click the **Routes Table** tab and filter the routes that are assigned to Microsoft Azure.
7.	Click the **BGP Table** tab and filter the routes that are assigned to IBM {{site.data.keyword.powerSys_notm}}.
8.	Click the **BGP Table** tab and filter the routes that are assigned to Microsoft Azure.

For more information about MCR Looking Glass, see [Megaport documentation](https://docs.megaport.com/mcr/mcr-looking-glass/){: external}.

### Connectivity tests
{: #conn-tests}

When the routes are correctly advertised between IBM Cloud, Megaport, and Microsoft Azure, you should have an end-to-end connectivity path between the platforms. You can verify connectivity with common tools such as ping or netcat.

From a Microsoft Azure virtual machine, use the following ping command to test the connectivity to a default gateway:

```codeblock
# ping 10.100.10.1
```

From a Microsoft Azure virtual machine, use the following netcat command to test the connectivity to a {{site.data.keyword.powerSys_notm}} instance with IP address 10.100.10.10 to TCP port 22:

```codeblock
# nc -vz 10.100.10.10 22
```
