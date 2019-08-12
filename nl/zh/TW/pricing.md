---

copyright:
  years: 2019

lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server on IBM Cloud 定價
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} 在精選地區中提供，對於橫向擴充的邏輯分割區 (LPAR)，最多可有 15 個核心數和 320 GB 記憶體；此外對於企業 LPAR，最多可有 143 個核心數和 8192 GB 記憶體。透過這些選項，{{site.data.keyword.powerSys_notm}} 可以符合您業務的任何工作負載需求。將依每月費率向您計費。
{:shortdesc}

## 依每月用量
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} 實例依每月費率收費（依比例以小時計算）。如果在月中將資源新增到 LPAR，則該 LPAR 的依每月帳單將反映出資源變更以及依比例以小時計算的 LPAR 價格。

### 依每月用量範例
{: #pricing-monthly-usage-example}

在下列範例中，您購買的 {{site.data.keyword.powerSys_notm}} 實例具有 1 個核心、8 GB 記憶體、150 GB 磁碟，並執行 AIX 7200-03-02，基礎價格為 250.57 美元/月（0.343 美元/小時）。在該月後面的時間，您新增了更多記憶體。LPAR 的新價格為 339.45 美元/月（0.465 美元/小時）。所部署資源的依每月帳單將依比例以小時計算。

|一個月內耗用的小時數|收費金額|LPAR 說明|
| ----------------------------- | ----------------- | --------------------  |
|300 小時|300 小時 x 251 美元/月 = 103 美元| 1 個核心、8 GB 記憶體、150 GB 磁碟、AIX  |
|430 小時|430 小時 x 339 美元/月 = 200 美元| 1 個核心、16 GB 記憶體、150 GB 磁碟、AIX  |
|730 小時（依每月總計）|103 美元 + 200 美元 = 303 美元（依每月總計）| 1 個核心、16 GB 記憶體、150 GB 磁碟、AIX  |
{: caption="表 1. 依每月 LPAR 計費範例" caption-side="top"}

在此範例中，LPAR 資源在該月使用 300 小時後從 8 GB 記憶體增加到 16 GB 記憶體。LPAR 的價格依比例以小時計算，得出 LPAR 的最終每月價格（303 美元）。

## 基礎實例價格
{: #pricing-base-instance-prices}

基礎實例計費取決於在建立 {{site.data.keyword.powerSys_notm}} 時選取的選項，例如機型、核心數和記憶體數量。建立虛擬伺服器實例時，將顯示關聯的依每月費率。如需相關資訊，請參閱[建立 {{site.data.keyword.powerSys_notm}}](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)。

## 作業系統
{: #pricing-operating-systems}

以下是 IBM 提供的庫存映像檔：
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

您可以在 {{site.data.keyword.powerSys_notm}} 實例上使用自帶自訂映像檔，但仍會向 IBM Cloud 購買作業系統授權。不能將現有 AIX 或 IBM i 授權用於 {{site.data.keyword.powerSys_notm}} 實例中的 LPAR。如果使用自訂映像檔或庫存映像檔，將以相同價格收費。如需相關資訊，請參閱[配置自訂映像檔](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)。

## 計費結束
{: #pricing-end-of-billing}

刪除 LPAR 時，按月計費週期即結束。如果擴展和縮減基礎架構以回應工作負載需求，則計費會根據 LPAR 佈建變更的時間進行計算。如果停止 LPAR，計費處理程序並不會停止。必須刪除 LPAR 才能停止計費週期。
