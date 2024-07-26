---

copyright:
  years: 2023, 2024

lastupdated: "2024-07-26"

keywords: network latency, {{site.data.keyword.powerSys_notm}}, private clouds

subcollection: power-iaas

---

{{site.data.keyword.attribute-definition-list}}

# Network latency
{: #network_latency_main}

---

IBM {{site.data.keyword.powerSys_notm}} Private Cloud: [On-premises]{: tag-red}

---

The network latency between your data center and the corresponding IBM Cloud region must maintain a network round-trip time (RTT) of less than or equal to 200 milliseconds.
{: shortdesc}

You can note the IP addresses for the IBM Cloud region that you want to test from the following table:

| IBM Cloud region | IP address |
| ---------------- | ---------- |
| Dallas | 52.117.39.146, 169.48.134.66, 169.63.36.210 |
| Frankfurt | 149.81.188.122, 158.177.88.18, 161.156.38.122 |
| London | 158.175.120.210, 141.125.97.106, 158.176.139.66 |
| Madrid | 13.120.67.114, 13.121.67.98, 13.122.67.106 |
| Osaka | 163.68.73.50, 163.69.65.242, 163.73.67.10 |
| Sao Paulo | 163.107.67.18, 163.109.71.82, 169.57.144.42 |
| Sydney | 130.198.65.82, 135.90.66.194, 168.1.58.90 |
| Tokyo | 161.202.104.226, 128.168.67.106, 165.192.108.10 |
| Toronto| 163.74.65.138, 163.75.70.50, 169.53.160.154 |
| Washington, DC | 169.63.123.154, 169.63.110.114, 169.62.13.2, 169.60.123.162, 169.59.152.58, 52.117.93.26 |
{: caption="Table 1. IBM Cloud Region and IP address" caption-side="bottom"}

To check the latency requirements of a connection, complete the following steps:

1. From a computer in the data center where you place the pod, ping the IP address of the IBM Cloud region that is closest to the physical location of your data center. Run the ping test from a compute endpoint as close as possible to the potential region where the pod is placed.

   For example,
   ```text
   ping <ip_address>
   ```

2. Close the connection when the transmission of a few packets is complete. For example, from the command-line, enter `ctrl+c`.

3. In the **ping statistics** output, note the average (avg) round-trip distance in milliseconds (ms) between the host and the IBM Cloud region. Compare whether the connection meets the latency requirement of less than or equal to 200 milliseconds (<= 200 ms).

If you are selecting the IBM Direct Link 2.0 Connect to connect the Virtual Private Cloud (VPC) on IBM Cloud and the router on pod, the minimum speed must be 1 Gbps.
{: note}

The following example meets the latency requirements as the round-trip time is 77.716 ms:
```text
--- 169.xx.xxx.xxx ping statistics ---
25 packets transmitted, 25 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 48.131/77.716/181.397/27.893 ms
```

The following example does not meet the latency requirements as the round-trip time is 217.37 ms:
```text
--- 158. xx.xxx.xxx ping statistics ---
9 packets transmitted, 9 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 138.453/217.370/419.901/108.211 ms
```
