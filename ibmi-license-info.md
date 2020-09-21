---

copyright:
  years: 2019, 2020

lastupdated: "2020-02-20"

keywords: ibm i license, operating system, SWMA products, Rational Development Studio

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

# IBM i License Program Products (LPP) and Operating System (OS) feature bundles
{: #ibmi-lpps}

Each LPP in the package contains all of the features, including the optional features. For example, the **5770-BR1** solution includes the **Network Feature** and the **Advanced Feature** in addition to the base product.
{: shortdesc}

The following LPP and OS features are included in the IBM i group Software Maintenance Agreement (SWMA) for the {{site.data.keyword.powerSys_notm}} offering:

- 5770-SS1 IBM i OS processor and includes unlimited users 
- 5770-DG1: HTTP Server for i
- 5770-JV1: Developer Kit for Java 
- 5770-NAE: Network Authentication Enablement for i
- 5733-SC1: Portable Utilities for i 
- 5770-TC1: TCP/IP 
- 5770-TS1: Transform Services for i
- 5770-UME: Universal Manageability Enablement for i
- 5770-XE1: IBM i Access for Windows 
- Zend 
- 5733-ARE: IBM Administration Runtime Expert 
- 5798-FAX: IBM Facsimile Support for i 
- 5770-SM1: IBM System Manager for i 
- 5770-DFH: IBM CICS Transaction Server for i 
- 5770-MG1: IBM Managed System Services for i
- 5770-SS1: IBM i Option 23, OptiConnect 
- 5770-SS1: IBM i Option 44, Encrypted Backup Enablement 
- 5770-SS1: IBM i Option 45, Encrypted ASP Enablement 
- 5770-SS1 IBM i Option 18 Media & Storage Extensions
- 5770-SS1 IBM i Option 26 DB2 Symmetric Multiprocessing
- 5770-SS1 IBM i Option 27 DB2 Multisystem
- 5770-SS1 IBM i Option 38 PSF for IBM i Any Speed Printer Support
- 5770-SS1 IBM i Option 41 HA Switchable Resources
- 5770-SS1 IBM i Option 42 HA Journal Performance
- 5770-AF1: Advanced Function Printing for i 
- 5761-AMT: Rational Application Management Toolset
- 5770-AP1: Advanced DBCS Printer Support 
- 5733-B45: AFP Font Collection for i
- 5770-BR1: Backup, Recovery and Media Services
- 5761-DB1: System/38 Utilities
- 5761-CM1: Communications Utilities
- 5761-DS2: Business Graphics Utility
- 5648-E77: InfoPrint Fonts
- 5769-FN1: AFP DBCS Fonts
- 5769-FNT: AFP Fonts
- 5722-IP1: InfoPrint Server for i
- 5770-JS1: Advanced Job Scheduler for i
- 5770-PT1: Performance Tools
- 5770-QU1: Query for i
- 5770-ST1: Db2 Query Manager and SQL Dev Kit for i
- 5733-XT2: XML Toolkit
- Passport Advantage: You can bring-your-own license to the Power Systems Virtual Server offering. For example, you can bring your current Rational Developer for i (RDi) license that is obtained by using Advanced Administration (AAS) or Passport Advantage (PPA) for the Power Systems Virtual Server offering. If you do not currently have a license, you can obtain a license by using Passport Advantage, and bring it to the Power Systems Virtual Server offering. Other examples are WebSphere MQ, Db2 Connect, and Lotus Notes. For more information, see [licensing and Passport Advantage](https://www.ibm.com/software/passportadvantage/eligible_public_cloud_BYOSL_policy.html).

To include LPPs to your VM instance that are not included in the IBM i group SWMA, complete the following steps:

1. Go to **Virtual server instances** in the Power Systems Virtual Server user interface and click your instance.

2. Click the **Edit details** option in the **Server details** pane. A menu appears.

3. Select the required licenses that you want to include in your VM instance. Currently, you can purchase the following licenses through Power Systems Virtual Server:

  - IBM i Cloud Storage Solution
  - IBM i Power HA
  - IBM DB2 Web Query for i
  - Rational Dev Studio for IBM i

    Adding a licensed program increases the service cost. The selected licensed programs are injected to your VM instance. You can install specific licensed program solutions on your VM instance, and the licensed programs will be automatically set. If you want to use these programs on your IBM i VM instance, you must order these licensed programs through Power Systems Virtual Server; you cannot use existing licensed programs in your VM instance.

4. Check the service agreement box and click **Save edits and order** to complete the instance modification process and to accept the price.

5. View the **Server details** pane to verify your instance modification.
