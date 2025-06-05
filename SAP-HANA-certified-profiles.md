---

copyright:
  years: 2019, 2025

lastupdated: "2025-06-04"

keywords: power, SAP HANA, profiles, certified profiles, sr2, sh2, bh2, ch2, ch1, bh1, ush1, umh

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# SAP HANA certified profiles
{: #SAP-hana-certified-profiles}

---

{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---





You can deploy SAP HANA on the following IBM® Power® servers:

- **Power10**: S1022, E1050, and E1080
- **Power9**: E980

You can use the UI, CLI, API, and Terraform interfaces to deploy certified SAP HANA profiles.

## Power10 profiles
{: #power10-profiles}

The following SAP HANA profiles are available for IBM Power10 processor-based servers:

| Profile | Profile type | Description                                                                                                                |
| ------- | ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| SR2     | Custom       | SR2 profiles are custom profiles that support selection of any combination of physical CPU cores and memory. Combinations that are certified by SAP for productive usage are documented in the [SAP Note 2947579 - SAP HANA on IBM Power Virtual Servers](https://launchpad.support.sap.com/#/notes/2947579) and in the [Certified and Supported SAP HANA Hardware]( https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/#/solutions?filters=v:deCertified;v:60ed2297-5cdd-4387-89c2-b0d3651d1206&sort=Latest%20Certification&sortDesc=true&id=s:2837) directory. Custom profiles must be deployed by using the CLI or API interface.         |
| SH2     | Small        | Suitable for balanced workloads that require less CPU and storage consumption.                                           |
| CH2     | Compute      | Suitable for CPU-intensive workloads, such as high web traffic, production batch processing, and front-end web servers. |
| BH2     | Balanced     | Suitable for midsize databases and common cloud applications with moderate traffic.                                      |
{: caption="Power10 SAP HANA certified profiles " caption-side="bottom"}

SR2 profiles must be deployed and edited by using the CLI, API, and Terraform interfaces. You cannot switch from an SR2 profile to a different SAP HANA profile. When an SR2 profile is deployed, you can edit the core value and memory size of the virtual machine by using the UI.
{: note}

## Power9 profiles
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

For more information about SAP HANA profiles, see [IBM Power Virtual Server certified profiles for SAP HANA](https://cloud.ibm.com/docs/sap?topic=sap-hana-iaas-offerings-profiles-power-vs). For more information about pricing, see [Pricing for Power Virtual Servers](https://cloud.ibm.com/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).





## SAP NetWeaver profiles
{: #sap-nw-profiles}

You can use the CLI, API, and Terraform interfaces and specify an sr2 profile ID that matches a NetWeaver profile to deploy certified SAP NetWeaver profiles.

You can use the following commands to get the details of an SAP profile:

* **CLI** : [ibmcloud pi image](/docs/power-iaas?topic=power-iaas-power-iaas-cli-reference-v1#ibmcloud-pi-image){:external}
* **API** : [Get list of SAP profiles](/apidocs/power-cloud#pcloud-sap-getall){:external}

The `Type` property of an SAP NetWeaver profile has the value `sap-rise-app`.
{: note}





For more information about SAP NetWeaver profiles, see [IBM Power Virtual Server certified profiles for SAP NetWeaver.](/docs/sap?topic=sap-nw-iaas-offerings-profiles-power-vs){:external}
