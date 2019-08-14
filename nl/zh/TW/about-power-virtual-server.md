---

copyright:
  years: 2019

lastupdated: "2019-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# 關於 Power Systems Virtual Server
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} 使用現有 IBM Cloud 平台來建立 Power Systems 虛擬伺服器，這種虛擬伺服器也稱為邏輯分割區 (LPAR)，透過 PowerVM 系統管理程序在 IBM Power Systems 硬體上執行。
{:shortdesc}

{{site.data.keyword.powerSys_notm}} 是基礎架構即服務 (IaaS) 的一種形式。透過 {{site.data.keyword.powerSys_notm}} 服務，可以快速建立和部署在公用雲端中執行 AIX 或 IBM i 作業系統的一個以上的虛擬伺服器。在雲端中佈建虛擬伺服器後，您應負責確保 AIX 或 IBM i 作業系統安全。

## 主要特性
{: #apvs-key-features}

以下是 {{site.data.keyword.powerSys_notm}} 的一些主要特性。

### 簡單的計費方式
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}} 使用按月計費頻率，其中包含 AIX 和 IBM i 作業系統的授權。按月計費頻率會根據當月部署到 {{site.data.keyword.powerSys_notm}} 實例的資源，依比例以小時計算。建立 {{site.data.keyword.powerSys_notm}} 實例時，可以根據指定的選項來查看配置的總成本。您可以快速確定哪些配置選項提供的價值最符合您的業務需求。如需相關資訊，請參閱[定價](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server)。

### 混合式雲端環境
{: #apvs-hybrid}

您可以使用 {{site.data.keyword.powerSys_notm}} 來執行現有 Power Systems 硬體基礎架構外部部署的任何 AIX 或 IBM i 工作負載。透過在公用雲端中執行工作負載，您可以享受雲端中提供的所有優勢，例如自助服務、快速交付、彈性以及與其他 IBM Cloud 服務的連線功能。雖然 AIX 和 IBM i 工作負載在雲端中執行，但您擁有的可擴展性、彈性和可正式作業特性仍保持與 Power Systems 硬體提供的相同。

### 基礎架構自訂
{: #apvs-customization}

建立 {{site.data.keyword.powerSys_notm}} 時，可以配置和自訂下列選項：
* 虛擬伺服器實例數
* 核心數
* 記憶體數量
* 資料磁區大小和類型（HDD 或 SSD）
* 專用或公用網路

### 自帶映像檔
{: #apvs-own-image}

在建立 {{site.data.keyword.powerSys_notm}} 時，IBM 會提供 AIX 和 IBM i 作業系統的庫存映像檔。但是，您可以使用先前已部署並測試自帶自訂 AIX 或 IBM i 作業系統映像檔。如需相關資訊，請參閱[配置自訂映像檔](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

## 硬體規格
{: #apvs-hardware-specifications}

下列 IBM Power Systems 硬體管理 {{site.data.keyword.powerSys_notm}}：

* 運算
  * [Power System E880 (9119-MHE) ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB 記憶體
    * 8 x 16 Gigabit PCI Express 雙埠光纖通道 (FC)
    * 10 x 10 Gigabit 乙太網路 SR PCI Express 雙埠
  * [Power System S922 (9009-22A) ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB 記憶體
    * 2 x 16 Gigabit PCI Express 雙埠 FC
    * 3 x 10 Gigabit 乙太網路 SR PCI Express 雙埠

* 儲存空間
  * Storewize V7000F(2076-AF6) 雙重控制器
  * Storwize V7000 (2076-624) 雙重控制器

* 網路
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## 公用和專用網路
{: #apvs-public-and-private}

建立 {{site.data.keyword.powerSys_notm}} 時，可以選取專用網路介面或公用網路介面。

* 公用網路
  * 連接至 {{site.data.keyword.powerSys_notm}} 實例的簡單快速方法。
  * IBM 配置網路基礎架構，以啟用從網際網路到 {{site.data.keyword.powerSys_notm}} 實例的安全公用網路連線。
  * 連線功能是使用 IBM Cloud Virtual Router Appliance (VRA) 和 Direct Link Connect 連接來實作。
  * 透過防火牆受保護，並支援下列安全網路通訊協定：
    * SSH
    * HTTPS
    * Ping
    * 使用 SSL 的 IBM i 5250 終端機模擬（埠 992）

* 專用網路
  * 容許 {{site.data.keyword.powerSys_notm}} 實例的資源存取現有 {{site.data.keyword.cloud_notm}} 資源，例如 Bare Metal Server、Kubernetes 容器或雲端儲存空間。
  * 使用 Direct Link Connect 連線來連接至 IBM Cloud 帳戶網路和資源。建立 Direct Link Connect 連線的程序可能需要幾天時間，因為 IBM Cloud 支援中心人員必須配置該鏈結。
  * 不同的 {{site.data.keyword.powerSys_notm}} 實例之間進行通訊需要專用網路。

    如需配置專用網路的不同選項的相關資訊，請參閱[配置專用網路](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring)。
    {: note}

下圖顯示了公用和專用網路的基本配置：

![顯示公用或專用連線的網路資料流量如何流動](/images/power-iaas-network1.svg "顯示公用或專用連線的網路資料流量如何流動"){: caption="圖 1. 專用和公用網路配置" caption-side="bottom"}

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
