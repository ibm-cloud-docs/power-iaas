---

copyright:
  years: 2023, 2024

lastupdated: "2024-07-22"

keywords: power systems, satellite location

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# IBM Satellite location
{: #satellite-location-spec-private-cloud}

[On-premises]{: tag-red}

The following IBM Cloud regions can host connections from the pods for IBM {{site.data.keyword.powerSys_notm}} (On-premises) in your data center:

- Dallas (satcon_dal)
- Frankfurt (satcon_fra)
- London (satcon_lon)
- Madrid (satcon_mad)
- Osaka (satcon_osa)
- Sao Paulo (satcon_sao)
- Sydney (satcon_syd)
- Tokyo (satcon_tok)
- Toronto (satcon_tor)
- Washington, DC (satcon_wdc)

Selection of IBM Cloud region is one of the factors for computing pricing.
{: Note}

Create a Satellite location associated with an IBM Cloud region. Select the IBM Cloud region that is closest to the physical location of your data center. The network latency between your data center and the selected IBM Cloud region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Create a Satellite location overview](https://cloud.ibm.com/docs/satellite?topic=satellite-locations){: external}.
