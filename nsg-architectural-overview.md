---

copyright:
  years: 2025

lastupdated: "2025-07-24"

keywords: nsg, nag, network security group, nsg architectural overview

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Implementing network security groups for securing three-tier web architecture workloads in {{site.data.keyword.powerSys_notm}}
{: #nsg-three-tier-workloads}


---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---

This topic provides the architectural overview of network security groups (NSGs) with the help of illustrations and examples, and explains how NSGs work in your Power Edge Router (PER) and enhanced CRN-enabled {{site.data.keyword.powerSysFull}} workspaces. A network security group (NSG) is used to define security rules to allow or deny specific network traffic that is related to resources provisioned in an IBM® Power® Virtual Server workspace. For more information about NSG and its core components, see [Network security groups](/docs/power-iaas?topic=power-iaas-nsg).

Running a three-tier web application in a {{site.data.keyword.powerSys_notm}} workspace generally requires a network with the following components:

- Application Load Balancer (ALB) in a virtual private cloud (VPC)
- Multiple virtual server instances, such as web servers, application servers, and database (DB) servers
- Jump hosts for management access
- Database replication across {{site.data.keyword.powerSys_notm}} workspaces
- Private endpoints like Domain Name System (DNS) and Secrets Manager

## High-level architecture of a network
{: #high-level-network-architecture}

The following diagram provides a high-level architectural view of a sample network in your {{site.data.keyword.powerSys_notm}} environment and illustrates how various subnets and components are connected. The diagram includes different virtual machines (VMs) as web servers, database servers, and application server. The network also includes components such as subnet ranges, jump hosts, transit gateway, and private endpoints (DNS and Secrets Manager).

![High-level network architecture](./images/nsg-high-level-architecture.svg "NSG: high-Level network architecture"){: caption="High-level network architecture" caption-side="bottom"}

The network components that are depicted in the high-level network architecture diagram is explained in the following table:

| Component                                   | Description                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Transit Gateway (TGW)**                   | Connects the VPC and your {{site.data.keyword.powerSys_notm}} workspaces. The transit gateway enables secure and efficient communication between different subnets and zones. For more information about transit gateway, see [About IBM Cloud Transit Gateway](/docs/transit-gateway?topic=transit-gateway-about).                    |
| **Z1**                                      | {{site.data.keyword.powerSys_notm}} workspace that contains the web servers (VMs), an application Server (VM2), and a database server (VM3) for production workload.                                                                                                                                                                   |
| **Z2**                                      | {{site.data.keyword.powerSys_notm}} workspace that contains another database server (VM4) for database replication and disaster recovery (DR).                                                                                                                                                                                         |
| **Application Load Balancer (ALB)**         | Distributes the incoming network traffic among multiple web server instances to balance the load and provides high availability and performance. The ALB is located in the virtual private cloud (VPC) `10.10.10.0/24` subnet. For more information, see [About application load balancers](/docs/vpc?topic=vpc-load-balancers-about). |
| **Jump Host (VM1)**                         | Provides secure management and administration access to {{site.data.keyword.powerSys_notm}} resources. A jump host is also known as a bastion host. The Jump is located in the `10.10.11.0/24` subnet within the VPC.                                                                                                                  |
| **Web Servers (VMs in Workspace Z1)**       | Manages the incoming HTTP or HTTPS web requests. The web servers (VMs) are hosted in the `10.10.20.0/24` subnet in the Workspace Z1.                                                                                                                                                                                                   |
| **App Server (VM2 in Workspace Z1)**        | Runs the application workload and communicates with the web servers (VMs) and the database server (VM3). The application server (VM2) is located in the same subnet as the web servers (`10.10.20.0/24`).                                                                                                                              |
| **DB Server (VM3 in Workspace Z1)**         | Acts as a database server and stores application data. The DB Sever (VM3) is located in the `10.10.21.0/24` subnet in the Workspace Z1. This instance of the database server is isolated from the web servers (VMs) and the application server (VM2).                                                                                  |
| **DB Server (VM4 in Workspace Z2)**         | Acts as a replica of the database server (VM3) in the Workspace Z1. The DB Server (VM4) is located in the `10.10.30.0/24` subnet in the Workspace Z2. Database replication between workspaces helps ensure redundancy and high availability.                                                                                           |
| **DNS (Private Endpoint)**                  | Used as a private endpoint in the network. The DNS provides internal domain name resolution securely within the cloud environment and is hosted in the `161.26.0.0/16` subnet.                                                                                                                                                         |
| **Secrets Manager (IaaS Private Endpoint)** | Used as an IaaS Private Endpoint to securely store and manage sensitive data such as API keys and login credentials. The Secrets Manager is hosted in the `166.8.0.0/14` subnet. For more information, see [IBM Cloud Secrets Manager](https://www.ibm.com/products/secrets-manager).                                                  |
{: caption="Network components" caption-side="bottom"}

## Network address groups and CIDR members
{: #nag-cidr-members}

The following table lists the network address groups (NAGs) and the associated Classless Inter-Domain Routing (CIDR) members that are used as examples in this topic. A NAG simplifies the NSG rule implementation by using logical groups instead of individual IPs. To more information about NAGs, see [Network address groups](/docs/power-iaas?topic=power-iaas-nsg#nag).

| NAGs                     | CIDR members                       |
| ------------------------ | ---------------------------------- |
| **ALB (Load balancer)**  | `10.10.10.0/24`                    |
| **MGMT (Management)**    | `10.10.11.0/24`                    |
| **REPL (Replication)**   | `10.10.30.0/24`                    |
| **IBM (Cloud services)** | `161.26.0.0/16` and `166.8.0.0/14` |
{: caption="NAGs and CIDR members" caption-side="bottom"}


## Network address group and network security group layout
{: #nag-nsg-layout}

The following diagram illustrates the NAGs and NSGs layout and how the traffic flows in the network.

![NAG and NSG layout](./images/nag-nsg-layout.svg "NAG and NSG layout"){: caption="NAG and NSG layout" caption-side="bottom"}

The following table lists the NAGs and NSGs used in the NAG and NSG layout diagram, and explains the purpose of each component in the layout:

| NAG/NSG      | Associated component                                                         | Purpose                                                                                                                                                                                                              |
| ------------ | ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ALB NAG**  | ALB (`10.10.10.0/24`)                                                        | Contains the ALB and ensures that the ALB can communicate with the web servers (VMs) in the WEB NSG.                                                                                                                  |
| **MGMT NAG** | Jump host (`10.10.11.0/24`)                                                  | Contains the jump host (VM1) and controls SSH access to components in the Production (Z1) and DR (Z2) workspaces.                                                                                                    |
| **REPL NAG** | DR DB Server (`10.10.30.0/24`)                                               | Contains the disaster recovery database server (VM4) and allows MySQL replication from the database server (VM3) in the DB NSG.                                                                                            |
| **IBM NAG**  | DNS (`161.26.0.0/16`) and Secrets Manager (`166.8.0.0/14`) private endpoints | Contains the DNS and Secrets Manager private endpoints and allows DNS and HTTPS traffic.                                                                                                                             |
| **WEB NSG**  | Web Servers (`10.10.20.0/24`)                                                | Groups the web servers (VMs) to apply rules that allow HTTP traffic from the ALB and enable outbound HTTPS traffic to the application server (VM2) in the APP NSG.                                                   |
| **APP NSG**  | App Server (`10.10.20.0/24`)                                                 | Groups the application server (VM2) to apply rules that allow HTTP traffic from the WEB NSG and MySQL traffic to the database server (VM3) in the DB NSG.                                                            |
| **DB NSG**   | DB Server (`10.10.21.0/24`)                                                  | Groups the database server (VM3) to apply rules that allow MySQL traffic from the application server (VM2) in APP NSG and enable replication traffic to the disaster recovery database server (VM4) in the REPL NAG. |
{: caption="NAG and NSG layout" caption-side="bottom"}

## Traffic flow across network components
{: #traffic-flows}

The following table outlines the expected traffic flows among various network components by using different protocols and its purpose, as depicted in the NAG and NSG layout diagram.

| Source                                                                | Destination                      | Protocol | Purpose                                                                                                                                     |
| --------------------------------------------------------------------- | -------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **ALB**                                                               | Web Servers (VMs)                | HTTP     | Distributes and routes incoming HTTP traffic to the web servers (VMs).                                                                      |
| **Jump Host (VM1)**                                                   | Web Servers (VMs)                | SSH      | Controls SSH access to components in the Production (Z1) and DR (Z2) workspaces.                                                            |
| **Web Servers (VMs)**                                                 | App Server (VM2)                 | HTTP     | Sends HTTP requests to the app server (VM2) for further processing.                                                                         |
| **App Server (VM2)**                                                  | DB Server (VM3)                  | MySQL    | Allows traffic that is required for database operations. The app server (VM2) queries the database Server (VM3) to store or retrieve data.  |
| **DB Server (VM3)**                                                   | DB Server (DR) (VM4)             | MySQL    | Allows data replication traffic between the database server (VM3) and the other database server (VM4) for disaster recovery and redundancy. |
| **Web Servers (VMs)**  \n **App Server (VM2)**  \n **DB Server (VM3)** | DNS Private Endpoint             | DNS      | Resolves domain names for internal and external communication.                                                                              |
| **Web Servers (VMs)**  \n **App Server (VM2)**  \n **DB Server (VM3)** | Secrets Manager Private Endpoint | HTTPS    | Stores and manages sensitive data, such as API keys and login credentials.                                                                  |
{: caption="Traffic flow across network components" caption-side="bottom"}

For more information about how network traffic and security rules are processed and prioritized when NSG is implemented in a Power Virtual Server workspace, see [Network traffic rules and precedence in NSG](/docs/power-iaas?topic=power-iaas-nsg#traffic-rules-prec).

## Defining NSG rules for web servers
{: #web-nsg}

This section outlines the rules that can be defined in an NSG to control what traffic is allowed or denied to the Web Servers. Consider the following requirements:

- Deny SSH traffic between other web servers.
- Allow HTTP from the ALB.
- Allow SSH access from the jump host.
- Allow everything from the web servers.
- Allow return DNS packets from IBM resolvers.
- Allow return HTTPS packets from the Secrets Manager.
- Allow return HTTP packets from the application server.
- Define an implicit deny rule to restrict all other unspecified traffic.

Based on the requirements, you can create an NSG and define the security rules with following configurations. Each row in the following table represents an individual security rule.

| Rule                                                  | Action | Protocol | Remote   | Source  | Destination | Flags   |
| ----------------------------------------------------- | ------ | -------- | -------- | ------- | ----------- | ------- |
| Deny SSH between other web servers                    | Deny   | TCP      | WEB NSG  | 1-65535 | 22-22       | –       |
| Allow HTTP from the ALB                               | Allow  | TCP      | ALB NAG  | 1-65535 | 80          | –       |
| Allow SSH from the jump host                          | Allow  | TCP      | MGMT NAG | 1-65535 | 22-22       | –       |
| Allow everything from other web servers               | Allow  | Any      | WEB NSG  | –       | –           | –       |
| Allow return DNS packets from IBM resolvers           | Allow  | UDP      | IBM NAG  | 53      | 1-65535     | –       |
| Allow return HTTPS packets from the Secrets Manager   | Allow  | TCP      | IBM NAG  | 443-443 | 1-65535     | ACK,FIN |
| Allow return HTTP packets from the application server | Allow  | TCP      | APP NSG  | 80-80   | 1-65535     | ACK,FIN |
| Implicit Deny                                         | Deny   | Any      | Any      | –       | –           | –       |
{: caption="NSG rules for web servers" caption-side="bottom"}

## Defining NSG rules for the application server
{: #app-nsg}

This section outlines the rules that can be defined in an NSG to control the traffic that is allowed or denied to the application server. Consider the following requirements:

- Allow HTTP traffic from the web servers.
- Allow SSH from the jump host.
- Allow everything from other application servers.
- Allow return DNS packets from IBM resolvers.
- Allow return HTTPS packets from the Secrets Manager
- Allow return database packets from database servers.
- Define an implicit deny rule to restrict all other unspecified traffic.

Based on the requirements, you can create an NSG and define the security rules with following configurations. Each row in the following table represents an individual security rule.

| Rule                                                | Action | Protocol | Remote   | Source  | Destination | Flags   |
| --------------------------------------------------- | ------ | -------- | -------- | ------- | ----------- | ------- |
| Allow HTTP from the web servers                     | Allow  | TCP      | WEB NSB  | 1-65535 | 80          | –       |
| Allow SSH from the jump host                        | Allow  | TCP      | MGMT NAG | 1-65535 | 22-22       | –       |
| Allow everything from other application servers     | Allow  | Any      | APP NSG  | –       | –           | –       |
| Allow return DNS packets from IBM resolvers         | Allow  | UDP      | IBM NAG  | 53      | 1-65535     | –       |
| Allow return HTTPS packets from the Secrets Manager | Allow  | TCP      | IBM NAG  | 443-443 | 1-65535     | ACK,FIN |
| Allow return database packets from database servers | Allow  | TCP      | DB NSG   | 80-80   | 1-65535     | ACK,FIN |
| Implicit Deny                                       | Deny   | Any      | Any      | –       | –           | –       |
{: caption="NSG rules for the application server" caption-side="bottom"}

## Defining NSG rules for database servers
{: #db-nsg}

This section outlines the rules that can be defined in an NSG to control the traffic that is allowed or denied to database servers. Consider the following requirements:

- Allow MySQL traffic from the application server.
- Allow SSH traffic from the jump host.
- Allow everything from other database servers.
- Allow return DNS packets from IBM resolvers.
- Allow return HTTPS packets from the Secrets Manager
- Allow return database packets from the replication server.
- Define an implicit deny rule to restrict all other unspecified traffic.

Based on the requirements, you can create an NSG and define the security rules with following configurations. Each row in the following table represents an individual security rule.

| Rule                                                   | Action | Protocol | Remote   | Source    | Destination | Flags    |
| ------------------------------------------------------ | ------ | -------- | -------- | --------- | ----------- | -------- |
| Allow MySQL from the application server                | Allow  | TCP      | APP NSG  | 1-65535   | 3306-3306   | –        |
| Allow SSH from the jump host                           | Allow  | TCP      | MGMT NAG | 1-65535   | 22-22       | –        |
| Allow everything from other database servers           | Allow  | Any      | DB NSG   | –         | –           | –        |
| Allow return DNS packets from IBM resolvers            | Allow  | UDP      | IBM NAG  | 53        | 1-65535     | –        |
| Allow return HTTPS packets from the Secrets Manager    | Allow  | TCP      | IBM NAG  | 443-443   | 1-65535     | ACK, FIN |
| Allow return database packets from replication servers | Allow  | TCP      | REPL NAG | 3306-3306 | 1-65535     | ACK, FIN |
| Implicit Deny                                          | Deny   | Any      | Any      | –         | –           | –        |
{: caption="NSG rules for database servers" caption-side="bottom"}

For more information about various aspects of setting up, configuring, and managing NSGs, see [Setting up network security groups in a workspace](/docs/power-iaas?topic=power-iaas-nsg#setting-nsg-ws).
