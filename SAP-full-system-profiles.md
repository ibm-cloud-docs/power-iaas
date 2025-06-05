---

copyright:
  years: 2019, 2024

lastupdated: "2025-05-27"

keywords: power, SAP, full system profiles

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}


# SAP full system profiles
{: #SAP-full-system-profiles}

---


{{site.data.keyword.off-prem-fname}} in [{{site.data.keyword.off-prem}}]{: tag-blue}


---


SAP HANA profiles that use all or most of the system resources are referred to as 'full system profiles'. You can deploy SAP HANA using full system profiles on a system if no virtual machines are deployed on the system.

No additional billing or metering is charged for full system profiles. The virtual machines with full system profiles are metered against the SAP HANA profile family in the same manner as any other profile from the family. For example, a profile such as sh2-24x1900 is metered by using the core and memory parts for the SH2 family that has 24 cores and 1900 GB of memory.




SAP custom profiles are not supported on POWER10 systems.
{: note}

For more information about pricing, see [Pricing for Power Virtual Servers](/docs/power-iaas?topic=power-iaas-pricing-virtual-server-on-cloud).
