---

copyright:
  years: 2016, 2019
lastupdated: "2019-05-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# {{site.data.keyword.powerSys_notm}} Activity Tracker 事件
{: #at_events}

身為安全性管理者、審核員或管理員的您，可以使用 Activity Tracker 服務追蹤使用者和應用程式與 {{site.data.keyword.cloud}} {{site.data.keyword.powerSys_notm}} 服務互動的情況。
{:shortdesc}

{{site.data.keyword.at_full_notm}} 服務記錄了由使用者起始且變更 {{site.data.keyword.cloud_notm}} 中服務狀態的活動。您可以使用此服務來調查異常活動及重要動作，以及符合法規審核需求。此外，您可以在動作發生時收到警示。所收集的事件符合「雲端審核資料聯合 (CADF)」標準。[進一步瞭解](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)。

## 事件清單：讀取
{: #at_actions_read}

下列事件用來讀取 {{site.data.keyword.powerSys_notm}} 實例。

|動作|說明|
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read |讀取 Power Cloud 實例|


## 事件清單：映像檔
{: #at_actions_images}

下列事件是針對在您的 {{site.data.keyword.powerSys_notm}} 實例中使用映像檔。

|動作|說明|
|:---------------------------|:--------------------------------|
| pcloud.image.read          |讀取一個映像檔或所有映像檔|
| pcloud.image.create        |建立新的映像檔|
| pcloud.image.update        |更新映像檔|
| pcloud.image.delete        |刪除映像檔|
| pcloud.image.capture       |匯出映像檔|


## 事件清單：網路
{: #at_actions_networks}

下列事件是針對在您的 {{site.data.keyword.powerSys_notm}} 實例中使用網路。

|動作|說明|
|:---------------------------|:--------------------------------------|
| pcloud.network.read        |讀取網路或所有網路|
| pcloud.network.create      |建立新的網路（公用/專用）|
| pcloud.network.update      |更新網路|
| pcloud.network.delete      |刪除網路|
{: caption="表 3. 產生事件的動作" caption-side="top"}

## 事件清單：{{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

下列事件是針對在 {{site.data.keyword.powerSys_notm}} 實例中使用每部虛擬伺服器。

|動作|說明|
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      |讀取 Power 虛擬伺服器實例|
| pcloud.pvm-instance.create    |建立 Power 虛擬伺服器實例|
| pcloud.pvm-instance.update    |更新 Power 虛擬伺服器實例|
| pcloud.pvm-instance.delete    |刪除 Power 虛擬伺服器實例|
| pcloud.pvm-instance.start     |啟動 Power 虛擬伺服器實例|
| pcloud.pvm-instance.stop      |停止 Power 虛擬伺服器實例|
| pcloud.pvm-instance.renew     |重新啟動 Power 虛擬伺服器實例|
| pcloud.pvm-instance.unknown   |對 Power 虛擬伺服器實例的不明動作|
| pcloud.pvm-instance.monitor   |對 Power 虛擬伺服器實例的主控台存取|
| pcloud.pvm-instance.capture   |將 Power 虛擬伺服器實例擷取成映像檔|

## 事件清單：SSH 金鑰
{: #at_actions_ssh_keys}

下列事件是針對在您的 {{site.data.keyword.powerSys_notm}} 實例中使用 SSH 金鑰。

|動作|說明|
|:-------------------------|:----------------------------|
| pcloud.tenant.read       |讀取承租戶資訊|
| pcloud.ssh-key.read      |讀取一個或數個 SSH 金鑰|
| pcloud.ssh-key.create    |建立 SSH 金鑰|
| pcloud.ssh-key.update    |更新 SSH 金鑰|
| pcloud.ssh-key.delete    |刪除 SSH 金鑰|

## 事件清單：資料磁區
{: #at_actions_data_volumes}

下列事件是針對在您的 {{site.data.keyword.powerSys_notm}} 實例中使用資料磁區。

|動作|說明|
|:-------------------------|:----------------------------|
| pcloud.volume.read       |讀取一個磁區或數個磁區|
| pcloud.volume.create     |建立磁區|
| pcloud.volume.update     |更新磁區|
| pcloud.volume.delete     |刪除磁區|
| pcloud.volume.configure  |連接或分離磁區|

## 檢視事件
{: #at_ui}

事件提供於**達拉斯**位置。

{{site.data.keyword.at_full_notm}} 在每個位置只能有一個實例。若要檢視事件，您必須在 `us-south` 位置存取 {{site.data.keyword.at_full_notm}} 服務的 Web 使用者介面。[進一步瞭解](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2)。
