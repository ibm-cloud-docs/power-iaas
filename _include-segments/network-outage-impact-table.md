


| Capability                                                                          | Behavior in disconnected mode                                                                                                                                                        |
| ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Client workload and data                                                            | Client workload is operational and you can access all the data.                                                                                                                   |
| GUI or API for `read` operations                                                    | GUI is operational and uses the most recent cached data.                                                                                                                             |
| GUI or API for `write` operations, such as creating virtual machine (VM) or volumes | You cannot perform `write` operations to the Power Virtual Sever resources until the connectivity to the control plane network is restored.                                                                     |
| Command-line interface (CLI)                                                        | You can perform `read` operations. However, you cannot perform `write` operations until the connectivity to the control plane network is restored.                                        |
| Billing and metering                                                                | Metering uses the most recent cached data. If the infrastructure is disconnected, you cannot perform `write` operations until the connectivity to the control plane network is restored. |
| Dynamic Host Configuration Protocol (DHCP) services for client data networks        | DHCP services are provided by the resident network in the {{site.data.keyword.on-prem-fname}} infrastructure and do not require a connection to the IBM Cloud.                                  |
| IBM remote support                                                                  | IBM remote support team cannot remotely connect to the {{site.data.keyword.on-prem-fname}} infrastructure until the connectivity to the control plane network is restored.               |
{: caption="Impact of unplanned network outage" caption-side="bottom"}
