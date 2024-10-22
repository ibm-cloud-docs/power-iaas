---

copyright:
  years: 2019, 2024

lastupdated: "2024-10-18"

keywords: power, SAP HANA, sr2, sh2, profiles

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# SAP HANA sr2 and sh2 profiles
{: #SAP-hana-sr2-sh2-profiles}

---



{{site.data.keyword.off-prem-fname}}: [{{site.data.keyword.off-prem}}]{: tag-blue}


---



You can deploy SAP HANA on the following systems:

* S1022: for the workloads that require less than 2 TB RAM.
* E1080: for the workloads that require 2 TB RAM or more.

You can deploy the following types of SAP HANA profiles:

* **SAP HANA**: If you want to deploy SAP HANA in your data center and if no S1022 systems are available, you can select an E1080 system.
* **sh2 profiles**: If you want to deploy SAP HANA profiles on the S1022 system with less than 2 TB memory, you can deploy sh2 profiles.
* **sr2 profiles**: You can deploy SAP workloads by using API, CLI, or Terraform. When the sr2 profile is deployed, you can edit the core value and memory size of the virtual machine by using the UI.
    You cannot switch from sr2 profile to another profile family.
    {: note}

For more information about SAP HANA profiles, see [IBM Power Virtual Server certified profiles for SAP HANA](https://cloud.ibm.com/docs/sap?topic=sap-hana-iaas-offerings-profiles-power-vs){: external}. For more information about pricing, see [Pricing for Power Virtual Servers](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).
