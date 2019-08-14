---

copyright:
  years: 2019

lastupdated: "2019-07-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# 訂購 IBM Cloud Direct Link Connect for Power Systems Virtual Servers
{: #ordering-direct-link-connect}

用 {{site.data.keyword.powerSys_notm}} 配置專用網路的一個選項是使用 Direct Link Connect 服務。Direct Connect Link 服務會建立連線，容許從您的 {{site.data.keyword.powerSys_notm}} 實例存取 {{site.data.keyword.cloud}} 資源。Direct Link Connect 服務也用來使用 IBM Cloud Virtual Router Appliance (VRA) 將您的內部部署網路連接至 IBM Cloud 網路。
{:shortdesc}

您可以使用 {{site.data.keyword.cloud_notm}} 使用者介面主控台來訂購 Direct Link Connect 服務。Direct Link Connect 服務與 {{site.data.keyword.powerSys_notm}} 服務不同。若要檢閱 Direct Link Connect 的費用，請參閱 [IBM Cloud Direct Link 的定價](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect)。

IBM 建議您訂購另一個 Direct Link Connect 連線以用作備份。

## 開始之前
{: #before-direct-link-connect}

* 驗證您的 {{site.data.keyword.cloud}} 帳戶有正確的授權可以訂購 Direct Link Connect 服務。
* 檢閱下列主題以瞭解 Direct Link Connect 服務的基本網路概念：
    * [Direct Link Connect 概念](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
    * [Direct Link Connect 詳細資料](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Direct Link Connect 限制](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [IP 指派的嚴格限制](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## 訂購 Direct Link Connect 的步驟
{: #steps-to-order-direct-link-connect}

若要訂購建立 {{site.data.keyword.powerSys_notm}} 實例連線的 Direct Link Connect 服務，請完成下列步驟：

1. 使用 IBM Cloud 帳戶認證登入 [IBM Cloud 型錄 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/catalog){: new_window}。您的帳戶必須有正確的授權，可以訂購 Direct Link Connect 服務。

2. 在**網路**區段中，按一下 **Direct Link Connect** 磚。
![顯示 Direct Link 型錄磚](/images/directlink1.png "顯示 Direct Link 型錄磚"){: caption="圖 1. 來自 IBM Cloud 型錄的 Direct Link Connect 磚。" caption-side="bottom"}

1. 從 Direct Link Connect 型錄項目，按一下**建立**。

1. 從 IBM Cloud Direct Link 頁面，按一下**訂購 Direct Link Connect**。

1. 從「建立 IBM Cloud Direct Link Connect 連線」頁面，完成下列欄位。

   完成下列欄位以便建立 Direct Link Connect 服務之後，價格會自動更新以反映您的選擇。
   {: note}

   <dl>
   <dt><strong>Direct Link 實例名稱</strong><dt>
   <dd>輸入說明 Direct Link Connect 用途的名稱。</dd>
   <dt><strong>位置</strong><dt>
   <dd>選取與 {{site.data.keyword.powerSys_notm}} 實例相同的位置。下表識別出 {{site.data.keyword.powerSys_notm}} 實例位置，及對應的 Direct Link 連線選項：
   <table>
   <caption>表 1. Direct Link 連線位置選項</caption>
   <tr>
   <th>Power Systems Virtual Server 位置</th>
   <th>Direct Link Connect 位置</th>
   </tr>
   <tr>
   <td>美國德州達拉斯</td>
   <td>達拉斯 4</td>
   </tr>
   <tr>
   <td>美國華盛頓特區</td>
   <td>華盛頓 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>網路提供者</strong><dt>
   <dd>您必須從清單選取 <strong>MEGAPORT</strong>。</dd>
   <dt><strong>鏈結速度</strong><dt>
   <dd>選取鏈結速度以符合您的工作負載需求。此欄位的建議選擇是 1000 Mbps。</dd>
   <dt><strong>遞送選項</strong><dt>
   <dd>選取<strong>本端遞送（免費）</strong>以存取連接到您在<strong>位置</strong>欄位中指定之位置的所有資料中心。選取<strong>廣域遞送</strong>以存取全球所有 IBM Cloud 資料中心。</dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>您必須針對下表特定 Direct Link Connect 位置，輸入 BGP ASN 號碼。
   <table>
   <caption>表 2. 特定位置的 BGP ASN 號碼</caption>
   <tr>
   <th>Direct Link Connect 位置</th>
   <th>BGP ASN 號碼</th>
   </tr>
   <tr>
   <td>達拉斯 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>華盛頓 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>選取 VRF</strong><dt>
   <dd>選取連線的虛擬遞送及轉遞選項。如果您的帳戶沒有已識別的 VRF，則不會顯示此欄位。您仍然可以建立 Direct Link Connect 服務而不選取 VRF。下圖是 Direct Link Connect 欄位的範例。</dd>
   <dd>

   ![顯示已完成的 Direct Link Connect 欄位](/images/directlink2.png "顯示已完成的 Direct Link Connect 欄位"){: caption="圖 2. Direct Link Connect 欄位。" caption-side="bottom"}
   </dd>
   </dl>
2. 閱讀**主要服務合約**，然後選取相應勾選框。您必須閱讀並瞭解**主要服務合約**，因為其中包含重要的技術資訊。

3. 按一下**建立**。當您的要求已順利提交時，會顯示下列訊息。
![顯示已順利提交 Direct Link Connect 的訊息](/images/directlink3.png "顯示已順利提交 Direct Link Connect 的訊息"){: caption="圖 3. Direct Link Connect 成功訊息。" caption-side="bottom"}

1. 按一下 Direct Link Connect 服務的**案例號碼**鏈結。案例號碼中的資訊會用來識別 Direct Link Connect 資訊，以便連接您的 {{site.data.keyword.powerSys_notm}} 實例。

  IBM Cloud 支援中心可能需要三個營業日才能建立 Direct Link Connect 連線。
  {: note}

2. 若要使用 Direct Link Connect 服務建立與 {{site.data.keyword.powerSys_notm}} 實例的連線，請向 {{site.data.keyword.powerSys_notm}} 支援團隊開立[新案例](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support)。

      1. 在新案例的說明欄位中，新增 Direct Link Connect 案例號碼。
      2. 複製系統自動產生的 {{site.data.keyword.powerSys_notm}} 案例 IAM 服務 ID。

3. 將 {{site.data.keyword.powerSys_notm}} 案例中的 IAM 服務 ID 輸入到 Direct Link Connect 案例中。建立 Direct Link Connect 連線時，會關閉 Direct Link Connect 案例號碼。以下是案例中顯示的網路資訊範例：

  ```shell
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. 請使用來自 Direct Link Connect 案例號碼的此項資訊，並將下列網路資訊輸入到 {{site.data.keyword.powerSys_notm}} 案例：

  ```shell
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. 當 Direct Link Connect 連線配置為與您的 {{site.data.keyword.powerSys_notm}} 實例通訊時，{{site.data.keyword.powerSys_notm}} 案例會關閉。
