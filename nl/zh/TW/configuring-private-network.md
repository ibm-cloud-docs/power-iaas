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

# 配置 Power Systems Virtual Server 使用專用網路
{: #cpn-configuring}

您可以將專用網路用於 {{site.data.keyword.powerSysFull}}，以安全地將內部部署環境與外部部署 {{site.data.keyword.cloud_notm}} 環境相連接。在專用網路中，可能存取 {{site.data.keyword.cloud_notm}} 資源，並與其他虛擬伺服器互連。
{:shortdesc}

可以使用下列其中一個選項來建立用於將內部部署環境與 {{site.data.keyword.cloud_notm}} 環境相連接的專用網路：

1. **{{site.data.keyword.cloud_notm}} SSL VPN（使用躍升伺服器）**
   * 可以使用 {{site.data.keyword.cloud_notm}} SSL VPN 服務來連接到現有 {{site.data.keyword.cloud_notm}} 網路。在 {{site.data.keyword.cloud_notm}} 網路中，可以將 {{site.data.keyword.cloud_notm}} 虛擬機器 (VM) 用作躍升伺服器來連接至 {{site.data.keyword.powerSys_notm}} 實例。
   * 必須使用躍升伺服器，因為無法使用 VPN 連線直接連接至 {{site.data.keyword.powerSys_notm}} 實例。
   * 這個選項一般是用來管理您的環境。不建議針對正式作業工作負載使用這個選項。
   * 如需如何配置此選項的相關資訊，請參閱[設定 SSL VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) 和[訂購虛擬路由器應用裝置](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)。

2. **{{site.data.keyword.cloud_notm}} IPSec VPN（使用 IBM Cloud 虛擬路由器應用裝置）**
   * 可以使用 {{site.data.keyword.cloud_notm}} IPSec VPN 服務來連接到現有 {{site.data.keyword.cloud_notm}} 網路。在 {{site.data.keyword.cloud_notm}} 網路中，可以使用 IBM Cloud 虛擬路由器應用裝置 (VRA) 來連接至 {{site.data.keyword.powerSys_notm}} 實例。
   * 必須使用 VRA，因為無法使用 VPN 連線直接連接至 {{site.data.keyword.powerSys_notm}} 實例。
   * 這個選項一般是用來管理您的環境。不建議針對正式作業工作負載使用這個選項。
   * 如需如何配置此選項的相關資訊，請參閱[設定 IPSec VPN](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) 和[訂購虛擬路由器應用裝置](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)。

3. **使用 IBM Cloud 虛擬路由器應用裝置的 Direct Link Connect**
   * 可以向 IBM 訂購 Direct Link Connect 服務，以使用 IBM Cloud 虛擬路由器應用裝置 (VRA) 將內部部署網路連接至 IBM Cloud 網路。
   * 此選項可在內部部署和 IBM Cloud 網路之間提供高效能。
   * 若要訂購 Direct Link Connect，請完成[透過使用者介面主控台訂購 IBM Cloud Direct Link Connect](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect) 主題中的步驟。
   * 有一些特定 IP 位址不能用於 Direct Link Connect 服務。如需相關資訊，請參閱[對 IP 指派的嚴格限制](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)。
