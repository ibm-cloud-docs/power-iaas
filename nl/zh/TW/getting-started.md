---

copyright:
  years: 2019

lastupdated: "2019-7-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}

# Power Systems Virtual Server 開始使用
{: #getting-started}


{{site.data.keyword.powerSysFull}} 是一種基礎架構即服務供應項目，可用於在幾分鐘內部署虛擬伺服器，也稱為邏輯分割區 (LPAR)。
{:shortdesc}

您可以快速部署 {{site.data.keyword.powerSys_notm}}，以符合特定業務需求。透過 {{site.data.keyword.powerSys_notm}}，可以建立混合式雲端環境，使您能夠輕鬆控制工作負載需求。

{{site.data.keyword.powerSys_notm}} 可以在不同地理位置執行 AIX 或 IBM i 工作負載。

## 術語
{: #gs-terminology}

在建立虛擬伺服器之前，您必須瞭解 {{site.data.keyword.powerSys_notm}} **服務**和 {{site.data.keyword.powerSys_notm}} **實例**在術語上的差異。請將 {{site.data.keyword.powerSys_notm}} **服務**視為特定地理位置中所有 {{site.data.keyword.powerSys_notm}} **實例**的容器。{{site.data.keyword.powerSys_notm}} **服務**可透過 {{site.data.keyword.cloud}} 使用者介面中的**資源清單**使用。服務可以包含多個 {{site.data.keyword.powerSys_notm}} **實例**。

例如，您可以有兩個 {{site.data.keyword.powerSys_notm}} **服務**，一個位於達拉斯，另一個位於華盛頓特區。每個服務可以包含多個 {{site.data.keyword.powerSys_notm}} **實例**。

## 開始之前
{: #gs-before-you-begin}

建立第一個 Power Systems Virtual Server 實例之前，請檢閱下列必要條件：

1. {: hide-dashboard}建立 IBM Cloud 帳戶。若要建立 IBM Cloud 帳戶，請參閱[註冊 IBM Cloud ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/registration){: new_window}。

2. 建立可用於安全連接至 {{site.data.keyword.powerSys_notm}} 的公用和專用 SSH 金鑰。若要建立公用和專用 SSH 金鑰，請參閱[新增 SSH 金鑰 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)。

3. （選用）如果要將自訂映像檔用於 AIX 或 IBM i 作業系統，則必須建立 IBM Cloud Object Storage 並上傳該映像檔。如需相關資訊，請參閱[配置自訂映像檔](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

4. （選用）如果要使用專用網路連接至 {{site.data.keyword.powerSys_notm}} 實例，則必須訂購 Direct Link Connect 服務。如需相關資訊，請參閱[透過使用者介面主控台訂購 IBM Cloud Direct Link Connect](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect)。

## 後續步驟
{: #gs-next-steps}

有了 IBM Cloud 帳戶以及專用和公用 SSH 金鑰，現在您已準備好[建立 {{site.data.keyword.powerSys_notm}} 服務](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)。
