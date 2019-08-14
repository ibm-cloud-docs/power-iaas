---

copyright:
  years: 2019

lastupdated: "2019-7-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# 配置自訂映像檔以用於 Power Systems Virtual Server
{: #configuring-custom-image}

您可以使用自帶自訂 AIX 或 IBM i 作業系統映像檔來部署 {{site.data.keyword.powerSysFull}}。
{:shortdesc}

不能將作業系統授權從內部部署系統傳輸到在雲端環境中執行的 {{site.data.keyword.powerSys_notm}}。授權成本已計入整體按小時計費的費率中。
{: note}

## 開始之前
{: #cci-before-you-begin}

要能夠將自訂映像檔用作開機，請首先檢閱下列資訊：

* 必須驗證 AIX 或 IBM i 作業系統技術層次在**機型**欄位中選取的 Power Systems 硬體上是否受支援。若要檢視支援的 AIX 和 IBM i 作業系統技術層次及 Power System 硬體清單，請參閱 [System software maps ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps)。
* 您必須對 **IBM Cloud Object Storage** 概念有基本的瞭解。如需相關資訊，請參閱[關於 IBM Cloud Object Storage](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage)。
* 如果您沒有現有的 AIX 或 IBM i 映像檔，則可以使用 IBM® PowerVC™ 來擷取和匯出映像檔，以用於 {{site.data.keyword.powerSys_notm}}。如需相關資訊，請參閱 [Capturing a virtual machine ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} 和 [Exporting images ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}。

## 將自訂映像檔作為物件上傳
{: #cci-uploading}

1. 建立 IBM Cloud Storage 物件並上傳映像檔。如需相關資訊，請參閱[上傳資料](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload)。
2. 使用雜湊型的訊息鑑別碼 (HMAC) 產生密碼和秘密存取金鑰。您可以在為 IBM Cloud Storage 物件建立服務認證時產生這些金鑰。若要建立服務認證，您必須對 **Object Storage** 儲存空間儲存區具有`撰寫者`存取權。如需相關資訊，請參閱[服務認證](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials)和[儲存區許可權](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions)。
3. 在 [IBM Cloud 型錄 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/catalog){: new_window} 中，按一下 Power Virtual Server 磚以新增映像檔。如果已建立虛擬伺服器實例，請選取**「功能表」圖示 ![「功能表」圖示](../icons/icon_hamburger.svg "「功能表」圖示") > 資源清單 > 裝置**，然後選取現有項目虛擬伺服器。

 填寫下列欄位以建立 {{site.data.keyword.powerSys_notm}}，然後按一下**自訂 AIX 映像檔**或**自訂 IBM i 映像檔**。

|欄位|說明|
| ------| ------------|
|Cloud Object Storage 儲存空間儲存區名稱|若要識別儲存空間儲存區名稱，請選取**「功能表」圖示 ![「功能表」圖示](../icons/icon_hamburger.svg "「功能表」圖示") > 資源清單 > 儲存空間 > Cloud Storage 物件名稱 > 儲存空間儲存區**。|
|Cloud Object Storage 存取金鑰|若要識別存取金鑰，請選取**「功能表」圖示 ![「功能表」圖示](../icons/icon_hamburger.svg "「功能表」圖示") > 資源清單 > 儲存空間 > Cloud Storage 物件名稱 > 服務認證 > 檢視認證**。複製 `access_key_id` 值並將其粘貼到此欄位中。|
|Cloud Object Storage 密碼|若要識別密碼，請選取**「功能表」圖示 ![「功能表」圖示](../icons/icon_hamburger.svg "「功能表」圖示") > 資源清單 > 儲存空間 > Cloud Storage 物件名稱 > 服務認證 > 檢視認證**。複製 `secret_access_key` 值並將其貼上到此欄位中。|
|映像檔路徑|輸入映像檔的完整路徑。完整路徑的格式必須為 `endpoint/bucket_name/file_name`。您必須使用專用端點網域。例如，`s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`。您可以透過選取**「功能表」圖示 ![「功能表」圖示](../icons/icon_hamburger.svg "「功能表」圖示") > 資源清單 > 儲存空間 > Cloud Storage 物件**來識別端點網域、儲存區名稱和檔名。
