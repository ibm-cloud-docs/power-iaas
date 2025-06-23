---

copyright:
  year: 2025

lastupdated: "2025-06-23"

keywords: Security and Compliance Center, SCC, Workload Protection, Workload Protection agent Linux, AIX, PowerVS SCC

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Integrating {{site.data.keyword.powerSys_notm}} with IBM Cloud Security and Compliance Center Workload Protection
{: #integrate-scc}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}





---



{{site.data.keyword.sysdigsecure_full}} offers a comprehensive suite of security solutions to help your organization secure its cloud environments. {{site.data.keyword.compliance_short}} Workload Protection centrally manages your organization’s security, risk, and compliance with regulatory standards and industry benchmarks. For more information about {{site.data.keyword.compliance_short}} Workload Protection, see [Getting started with IBM Cloud Security and Compliance Center Workload Protection](docs/workload-protection?topic=workload-protection-getting-started).

In highly regulated sectors such as financial services, continuous compliance in the cloud environment is crucial to protect customer and application data. Cloud Security Posture Management (CSPM) is one of the key features of the {{site.data.keyword.compliance_short}} {{site.data.keyword.sysdigsecure_short}} service. When this feature is enabled in your workspace, the CSPM ensures that automatic compliance checks are integrated in your development workflow to mitigate such risks on a daily basis.

## IBM Cloud® Security Posture Management (CSPM)
{: #cspm}

CSPM accelerates hybrid cloud adoption by verifying security and regulatory compliance with automated compliance checks for IBM Cloud Framework for Financial Services, Digital Operational Resilience Act (DORA), CIS IBM Cloud Foundations Benchmark, PCI, and many other industry-related or best practice standards. For more information, see [About IBM Cloud Security Posture Management (CSPM)](https://cloud.ibm.com/docs/workload-protection?topic=workload-protection-about). CSPM helps with:

- Continuous validation of compliance
- Vulnerability prioritization
- Detection and response to runtime threats
- Forensics and incident response

You can enable the CSPM feature in your new and existing {{site.data.keyword.powerSys_notm}} workspaces. CSPM provides a unified platform to manage security and compliance across hybrid and multicloud environments and services.

## Integrating CSPM with Power Virtual Server workspaces
{: #integrate-cspm}

To integrate {{site.data.keyword.powerSys_notm}} with Cloud Security and Compliance Center, enable Cloud Security Posture Management (CSPM) feature in your existing or new workspaces:

- [Enabling CSPM in a new workspace](#enable-cspm-new)
- [Enabling CSPM in an existing workspace](#enable-cspm-existing)

### Enabling CSPM in a new workspace
{: #enable-cspm-new}

To enable CSPM in a new Power Virtual Server workspace, complete the following steps:

1. Log in to the [IBM Cloud catalog](https://cloud.ibm.com/catalog) with your credentials.
2. In the search box, type **Power Virtual Server** and click the **Power Virtual Server** tile.
3. Click **Create a workspace**.
4. Select **IBM data center** as the location type.
5. Select an IBM data center from the **Location** drop-down list and click **Continue**.
6. In the Details section, provide a name for the workspace and select the resource group from the **Resource group** drop-down list. You can optionally provide User tags and Access management tags for the workspace.
7. Click **Continue**. The selected workspace details are displayed on the Summary page.



8. In the Integrations (Optional) section, note that the **Cloud security posture management** toggle switch is enabled by default. To disable CSPM, set **Cloud security posture management** to off.






10. Click **Finish**. The selected workspace details are displayed on the Summary page.

11. Select the **I agree to the Terms and conditions** checkbox and click **Create**.

Integration costs are usage based and vary based on the hourly consumption for nodes and virtual machines. You can review the estimated cost on the Summary page. To review the cost associated with CSPM, see [Security and Compliance Center Workload Protection](https://cloud.ibm.com/workload-protection/catalog/security-and-compliance-center-workload-protection) in **IBM Cloud catalog**.
{: important}

### Enabling CSPM in an existing workspace
{: #enable-cspm-existing}

To enable CSPM in an existing Power Virtual Server workspace, complete the following steps:

1. Log in to the [IBM Cloud](https://cloud.ibm.com/login?state=%2Fpower%2Foverview) Power Virtual Server user interface.
2. Click **Workspaces** in the left navigation menu.



3. Select the workspace on which you want to enable CSPM. The Workspace details pane is displayed.
   





4. To enable CSPM, click **Add CSPM** in the Integrations section. The Add cloud security posture management pane is displayed with the predefined SCC Workload Protection instance, Trusted profile, and App Configuration instance.

5. Click **Edit** to change the name, location, and plan for the CSPM instance, and click **Save**.
6. Click **Create**.

## {{site.data.keyword.sysdigsecure_short}} agent in Linux® and AIX® on {{site.data.keyword.powerSys_notm}}
{: #wp-linux-AIX}

After you provision an instance of the {{site.data.keyword.compliance_short}} {{site.data.keyword.sysdigsecure_short}} service in IBM Cloud, you can deploy the {{site.data.keyword.sysdigsecure_short}} agent on your Linux or AIX hosts on {{site.data.keyword.powerSysFull}}. To provision an instance of {{site.data.keyword.sysdigsecure_short}}, see [Provisioning an instance](/docs/workload-protection?topic=workload-protection-provision&interface=ui).

{{site.data.keyword.sysdigsecure_short}} provides the following features to protect your stand-alone Linux or AIX hosts on {{site.data.keyword.powerSys_notm}}.

| Feature | On Linux hosts | On AIX hosts |
| ------- | -------- | ------ |
| Posture management | Scans host configuration files for compliance and benchmarks such as CIS Linux Benchmark |Scans host configuration files for compliance and benchmarks such as CIS AIX Benchmark|
| Host scanning | Scans host packages, detects associated vulnerabilities, and identifies the resolution priority based on available fixed versions and severity |   - |
| Threat detection and response | Identifies threats and suspicious activity based on application, network, and host activity by processing syscall events and investigates with detailed system captures |  - |
{: caption="{{site.data.keyword.sysdigsecure_short}} agent features" caption-side="top"}

For more information about managing and deploying the {{site.data.keyword.sysdigsecure_short}} agent on your Linux hosts, see [Managing the Workload Protection agent in Linux on PowerVS](https://cloud.ibm.com/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs).

For more information about managing and deploying the {{site.data.keyword.sysdigsecure_short}} agent on your AIX hosts, see [Managing the Workload Protection agent in AIX on PowerVS](https://cloud.ibm.com/docs/workload-protection?topic=workload-protection-agent-deploy-aix-powervs).
