---

copyright:
  years: 2019, 2025

lastupdated: "2025-09-01"

keywords: power, SAP HANA, profiles, certified profiles, sr2, sh2, bh2, ch2, ch1, bh1, ush1, umh

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}



# SAP certified profiles
{: #SAP-certified-profiles}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---







You can deploy SAP certified profiles on IBM POWER9 or later servers by using a single custom OS boot image. You can use the UI, CLI, API, and Terraform interfaces to deploy SAP certified profiles.



## SAP certified profiles for SAP HANA
{: #sap-certpro-hana}

The SAP certified profiles for SAP HANA are a set of profiles with defined attributes such as CPU cores and RAM.



You can deploy SAP HANA on the following IBM&reg; Power&reg; server types:



- **Power10**: S1022, E1050, and E1080
- **Power9**: E980









### Power10 profiles
{: #power10-profiles}

The following SAP HANA profiles are available for IBM Power10 processor-based servers:

| Profile | Profile type | Description                                                                                                                |
| ------- | ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| SR2     | Custom       | SR2 profiles are custom profiles that support selection of any combination of physical CPU cores and memory. Combinations that are certified by SAP for productive usage are documented in the [SAP Note 2947579 - SAP HANA on IBM Power Virtual Servers](https://launchpad.support.sap.com/#/notes/2947579) and in the [Certified and Supported SAP HANA Hardware]( https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/#/solutions?filters=v:deCertified;v:60ed2297-5cdd-4387-89c2-b0d3651d1206&sort=Latest%20Certification&sortDesc=true&id=s:2837) directory. Custom profiles must be deployed by using the CLI or API interface.         |
| SH2     | Small        | Suitable for balanced workloads that require less CPU and storage consumption.                                           |
| CH2     | Compute      | Suitable for CPU-intensive workloads, such as high web traffic, production batch processing, and front-end web servers. |
| BH2     | Balanced     | Suitable for midsize databases and common cloud applications with moderate traffic.                                      |
| MH2      | Very high memory            |  Suitable for server Online Analytical Processing (OLAP) databases, such as SAP NetWeaver.|
{: caption="Power10 SAP HANA certified profiles " caption-side="bottom"}

SR2 profiles must be deployed and edited by using the UI, CLI, API, and Terraform interfaces. You cannot switch from an SR2 profile to a different SAP HANA profile. When an SR2 profile is deployed, you can edit the core value and memory size of the virtual machine by using the UI. SR2 profiles are not available with the E980 machine type.
{: note}



### Power9 profiles
{: #power9-profiles}

The following SAP HANA profiles are available for IBM Power9 processor-based servers:

| Profile | Profile type | Description                                                                                                                                      |
| ------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| CNP     | Custom       | Ideal for test or development use only. These profiles are not intended for production use and are not supported or certified for SAP production. |
| USH1    | Small        | Suitable for balanced workloads that require less CPU and storage consumption.                                                                 |
| UMH     | Ultra Memory | Provides the highest vCPU-to-memory ratios for serving in-memory OLTP databases, such as SAP HANA.                                                |
| BH1     | Balanced     | Suitable for midsize databases and common cloud applications with moderate traffic.                                                            |
| CH1     | Compute      | Suitable for CPU-intensive workloads, such as high web traffic, production batch processing, and front-end web servers.                       |
{: caption="Power9 SAP HANA certified profiles " caption-side="bottom"}

For more information about SAP certified profiles for SAP HANA, see [IBM Power Virtual Server certified profiles for SAP HANA](https://cloud.ibm.com/docs/sap?topic=sap-hana-iaas-offerings-profiles-power-vs){: external}. For more information about pricing, see [Pricing for Power Virtual Servers](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).





## SAP Application Server profiles
{: #sap-appser-profiles}

When you use SAP Application Server profiles, you can deploy a certified profile for SAP Application Servers or SAP NetWeaver on {{site.data.keyword.powerSys_notm}}. The SAP Application Server profiles are available on IBM Power S1022 systems.

To deploy a certified profile for SAP Application Servers or SAP NetWeaver by using CLI, API, or Terraform interfaces, specify an sr2 profile ID that matches an SAP Application Server profile.

You can use the following commands to get the details of an SAP profile:

* **CLI** : [ibmcloud pi image](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image){:external}
* **API** : [Get list of SAP profiles](/apidocs/power-cloud#pcloud-sap-getall){:external}

The `Type` property of an SAP Application Server profile has the value `sap-rise-app`.
{: note}





For more information about SAP Application Server profiles, see [SAP Application Server certified instances on IBM Power Virtual Server.](/docs/sap?topic=sap-nw-iaas-offerings-profiles-power-vs){:external}



## Generating an estimate of a Power Virtual Server instance
{: #sap-hana-prof-est}

When you are generating an estimate of a {{site.data.keyword.powerSys_notm}} instance, you can select SAP certified profiles. For more information about generating an estimate of a {{site.data.keyword.powerSys_notm}} instance with SAP certified profiles, see [Estimating SAP workloads](/docs/power-iaas?topic=power-iaas-generating-an-estimate#est-sap-workloads).


## Creating a Power Virtual Server instance
{: #create-sap-hana-inst}

When you are creating a {{site.data.keyword.powerSys_notm}} instance, you can select SAP certified profiles. For more information about creating a {{site.data.keyword.powerSys_notm}} instance with SAP certified profiles, see [Configuring a Power Virtual Server instance](/docs/power-iaas?topic=power-iaas-creating-power-virtual-server#configuring-instance).
