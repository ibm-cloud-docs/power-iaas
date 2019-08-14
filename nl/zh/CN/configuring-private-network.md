---

copyright:
  years: 2019

lastupdated: "2019-07-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 配置 Power Systems Virtual Server 使用专用网络
{: #cpn-configuring}

您可以将专用网络用于 {{site.data.keyword.powerSysFull}}，以安全地将内部部署环境与外部部署 {{site.data.keyword.cloud_notm}} 环境相连接。在专用网络中，可能访问 {{site.data.keyword.cloud_notm}} 资源，并与其他虚拟服务器互连。
{:shortdesc}

可以使用以下其中一个选项来创建用于将内部部署环境与 {{site.data.keyword.cloud_notm}} 环境相连接的专用网络：

1. **{{site.data.keyword.cloud_notm}} SSL VPN（使用跳板机）**
   * 可以使用 {{site.data.keyword.cloud_notm}} SSL VPN 服务来连接到现有 {{site.data.keyword.cloud_notm}} 网络。在 {{site.data.keyword.cloud_notm}} 网络中，可以将 {{site.data.keyword.cloud_notm}} 虚拟机 (VM) 用作跳板机来连接到 {{site.data.keyword.powerSys_notm}} 实例。
   * 必须使用跳板机，因为无法使用 VPN 连接直接连接到 {{site.data.keyword.powerSys_notm}} 实例。
   * 此选项通常用于管理环境。对于生产工作负载，建议不要使用此选项。
   * 有关如何配置此选项的更多信息，请参阅[设置 SSL VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) 和[订购虚拟路由器设备](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)。

2. **{{site.data.keyword.cloud_notm}} IPSec VPN（使用 IBM Cloud 虚拟路由器设备）**
   * 可以使用 {{site.data.keyword.cloud_notm}} IPSec VPN 服务来连接到现有 {{site.data.keyword.cloud_notm}} 网络。在 {{site.data.keyword.cloud_notm}} 网络中，可以使用 IBM Cloud 虚拟路由器设备 (VRA) 来连接到 {{site.data.keyword.powerSys_notm}} 实例。
   * 必须使用 VRA，因为无法使用 VPN 连接直接连接到 {{site.data.keyword.powerSys_notm}} 实例。
   * 此选项通常用于管理环境。对于生产工作负载，建议不要使用此选项。
   * 有关如何配置此选项的更多信息，请参阅[设置 IPSec VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) 和[订购虚拟路由器设备](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)。

3. **使用 IBM Cloud 虚拟路由器设备的 Direct Link Connect**
   * 可以向 IBM 订购 Direct Link Connect 服务，以使用 IBM Cloud 虚拟路由器设备 (VRA) 将内部部署网络连接到 IBM Cloud 网络。
   * 此选项可在内部部署和 IBM Cloud 网络之间提供高性能。
   * 要订购 Direct Link Connect，请完成[通过 UI 控制台订购 IBM Cloud Direct Link Connect](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect) 主题中的步骤。
   * 有一些特定 IP 地址不能用于 Direct Link Connect 服务。有关更多信息，请参阅[对 IP 分配的严格限制](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)。
