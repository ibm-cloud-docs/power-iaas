---

copyright:
  years: 2023, 2025

lastupdated: "2025-12-18"

keywords: power systems, satellite location

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Supported locations for {{site.data.keyword.on-prem-fname}} Private Cloud
{: #satellite-location-spec-private-cloud}

Specific {{site.data.keyword.cloud}} regions are available so that you can host connections from the pods for {{site.data.keyword.on-prem-fname}} in your data center.
{: shortdesc}

Selecting different {{site.data.keyword.cloud_notm}} regions can affect computing pricing.
{: note}


[{{site.data.keyword.on-prem}}]{: tag-red} The following {{site.data.keyword.cloud_notm}} regions can be used for {{site.data.keyword.on-prem-fname}}. Select the {{site.data.keyword.cloud_notm}} region that is closest to the physical location of your data center.


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



Create an {{site.data.keyword.satellitelong}} location associated with a supported {{site.data.keyword.cloud_notm}} region for use with {{site.data.keyword.on-prem-fname}}. The network latency between your data center and the selected {{site.data.keyword.cloud_notm}} region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds. For more information, see [Create a {{site.data.keyword.satelliteshort}} location overview](/docs/satellite?topic=satellite-locations).
