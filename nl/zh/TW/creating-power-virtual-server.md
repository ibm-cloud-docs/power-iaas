---

copyright:
  years: 2019

lastupdated: "2019-08-1"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:table: .aria-labeledby="caption"}

# 建立 Power Systems Virtual Server
{: #creating-power-virtual-server}

若要建立和配置 {{site.data.keyword.powerSysFull}}，請完成下列步驟：

1. 使用 IBM Cloud 帳戶認證登入 [IBM Cloud 型錄 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/catalog){: new_window}。
2. 在型錄的搜尋方框中，輸入 **Power Systems Virtual Server**，然後按一下 {{site.data.keyword.powerSys_notm}} 磚。

    ![IBM Cloud 型錄](./images/catalog-search-bar.png "IBM Cloud 型錄"){: caption="圖 1. IBM Cloud 型錄" caption-side="bottom"}

3. 為服務提供名稱，然後選擇要部署 {{site.data.keyword.powerSys_notm}} 實例的位置。

    ![服務和地區選擇](./images/power-iaas-service-region.png "服務和地區選擇"){: caption="圖 2. 服務和地區選擇" caption-side="bottom"}

4. 按一下網頁底端的**建立**按鈕。

    ![「建立」按鈕](./images/power-iaas-create-button.png "「建立」按鈕"){: caption="圖 3. 「建立」按鈕" caption-side="bottom"}

5. 按一下**建立**按鈕後，會將您重新導向到**資源清單**畫面。
6. 從**資源清單**中的**服務**下選取您的服務，以移至**管理**畫面。

    ![IBM Cloud 資源清單](./images/power-iaas-resource-list.png "IBM Cloud 資源清單"){: caption="圖 4. IBM Cloud 資源清單" caption-side="bottom"}

7. 在此，按一下**佈建新的項目**按鈕。

    ![佈建新的虛擬伺服器](./images/power-iaas-provision-new.png "佈建新的虛擬伺服器"){: caption="圖 5. 佈建新的虛擬伺服器" caption-side="bottom"}

8. 填寫所有必要欄位以順利建立新的實例：

     填寫欄位以建立 {{site.data.keyword.powerSys_notm}} 時，價格會在**訂單摘要**區段中動態更新。這容許您輕鬆建立具有成本效益的 {{site.data.keyword.powerSys_notm}}，以滿足業務需求。
     {: tip}

    1. 填寫**虛擬伺服器**區段下的所有欄位。如果選取了多個實例，則將顯示其他選項。

      ![建立新的 Power Virtual Server 實例](./images/console-virtual-instance.png "建立新的 Power Virtual Server 實例"){: caption="圖 6. 建立新的 Power Virtual Server 實例" caption-side="bottom"}

    1. 選取是需要**專用處理器**還是**共用處理器**。此外，還務必選擇所需的**機型**、核心數和記憶體數量。

      ![選取處理器和系統](./images/console-profile.png "選取處理器和系統"){: caption="圖 7. 選取處理器和系統" caption-side="bottom"}

    1. 最後，依照組織的指示，填寫**啟動磁區**、**連接的磁區**和**網路介面**欄位。

      ![定義磁區和網路介面](./images/console-volume-network.png "定義磁區和網路介面"){: caption="圖 8. 定義磁區和網路介面" caption-side="bottom"}

9. 接受**使用條款**，然後按一下**建立**按鈕以佈建新的 {{site.data.keyword.powerSys_notm}}。

下表提供了有關**虛擬伺服器實例**欄位的資訊：

<table>
<caption>表 1. 新建 Power Virtual Server 實例的欄位</caption>
<tr>
<th>欄位</th>
<th>說明</th>
</tr>
<tr>
<td>實例數</td>
<td>指定要為 {{site.data.keyword.powerSys_notm}} 建立的實例數。如果指定多個實例，則可以選取下列命名慣例和主機代管規則：
  <dl>
    <dt><strong>無喜好設定</strong></dt>
  <dd>如果沒有管理喜好設定，請選取此選項。</dd>
    <dt><strong>不同伺服器</strong></dt>
  <dd>選取此選項可使每個實例在不同的伺服器上管理。如果您擔心發生可能影響所有 {{site.data.keyword.powerSys_notm}} 實例的單伺服器中斷，則可以使用此選項。</dd>
  <dt><strong>數字字首</strong></dt>
  <dd>選取此選項可在虛擬伺服器的名稱前面新增數字。例如，如果第一個 {{site.data.keyword.powerSys_notm}} 名稱為 <kbd>Austin</kbd>，則下一個虛擬實例名稱為 <kbd>1Austin</kbd>。</dd>
  <dt><strong>數字尾碼</strong></dt>
  <dd>選取此選項可在虛擬伺服器的名稱後面新增數字。例如，如果第一個 {{site.data.keyword.powerSys_notm}} 名稱為 <kbd>Rochester</kbd>，則下一個虛擬實例名稱為 <kbd>Rochester1</kbd>。</dd>
  </dl>
  <p>
  <strong>附註：</strong>建立虛擬伺服器的多個實例時，必須在新增的每個資料磁區的<strong>可共享</strong>欄位中選取<strong>開啟</strong>。如果您不希望資料磁區可共享，則可以在建立虛擬伺服器後新增資料磁區。
  </p>
   </td>
</tr>
<tr>
<td>鎖定虛擬機器</td>
<td>選取<strong>開啟</strong>可將 {{site.data.keyword.powerSys_notm}} 鎖定到主機系統上。如果選取<strong>開啟</strong>，則無法將虛擬伺服器移至其他主機。例如，如果選取<strong>開啟</strong>，則在主機維護期間將遇到中斷。</td>
</tr>
<tr>
<td>機型</td>
<td>指定機型。選取的機型將確定可用的核心數和記憶體量。如需硬體規格的相關資訊，請參閱 <a href="https://www.ibm.com/downloads/cas/KQ4BOJ3N" target="_blank">S922</a> 和 <a href="https://www.ibm.com/downloads/cas/EE476WAP" target="_blank">E880</a>。</td>
</tr>
<tr>
<td>核心數</td>
<td>選取 {{site.data.keyword.powerSys_notm}} 的核心數。如果選取了<strong>共用處理器</strong>，則可以依 0.25 的增量指定核心數。例如，有效的核心值為 0.5、1.25 和 2.75。這將為每 0.25 個授權配置一個虛擬 CPU。

如果您擔心效能問題，則可以選取<strong>專用處理器</strong>，因為該處理器將專用於虛擬伺服器，而不會共用。如需相關資訊，請參閱 <a href="https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/How%20does%20Shared%20Processor%20Performance%20Compare%20to%20Dedicated%20Processors" target="_blank">How does Shared Processor Performance Compare to Dedicated Processors</a>。</td>
</tr>
<tr>
<td>記憶體</td>
<td>選取 {{site.data.keyword.powerSys_notm}} 的記憶體數量。可以選取的記憶體數量取決於所選的核心數。對於選取的每個核心，最多可以配置 64 GB。例如，如果選取了四個核心數，則容許您選取最多 256 GB 記憶體。</td>
</tr>
<tr>
<td>建立啟動磁區</td>
<td>選取為您提供的 AIX 或 IBM i 作業系統庫存映像檔的版本，或者選取先前內部部署的自訂 AIX 或 IBM i 作業系統映像檔。如需操作系統授權資訊，請參閱 IBM 的 <a href="https://www-03.ibm.com/software/sla/sladb.nsf" target="_blank">License Information documents</a>。

如果要使用自帶自訂映像檔，則必須使用在<strong>機型</strong>欄位中選取的 Power Systems 硬體所支援的 AIX 或 IBM i 作業系統映像檔技術層次。如需相關資訊，請參閱<a href="/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image">配置自訂映像檔</a>。</td>
</tr>
<tr>
<td>連接的資料磁區</td>
<td>可以建立新的資料磁區，也可以連接已在 IBM Cloud 帳戶中定義的現有資料磁區。<dl>
  <dt><strong>建立資料磁區</strong></dt>
  <dd>按一下<strong>新增</strong>可建立新資料磁區，以用於為 {{site.data.keyword.powerSys_notm}} 實例提供更多儲存空間空間。如果要容許 {{site.data.keyword.powerSys_notm}} 的多個實例將資料寫入相同的資料磁區，則必須在<strong>可共享</strong>欄位中選取<strong>開啟</strong>。</dd>
  <dt><strong>連接現有資料磁區</strong></dt>
  <dd>選取現有項目資料磁區，以用於為 {{site.data.keyword.powerSys_notm}} 實例提供更多儲存空間空間。如果清單中未顯示先前使用過的資料磁區，可能是因為該資料磁區是使用其他 IBM Cloud 帳戶建立的。</dd>
</dl>
</td>
</tr>
<tr>
<td>公用網路</td>
<td>選取此選項可使用 IBM 提供的公用網路。選取此選項會如需聯的成本。如需相關資訊，請參閱<a href="/docs/infrastructure/power-iaas?topic=power-iaas-about-power-virtual-server#apvs-public-and-private" target="_blank">公用和專用網路</a>。</td>
</tr>
<tr>
<td>專用網路</td>
<td>按一下<strong>新增</strong>以識別虛擬伺服器的新專用網路。如果已新增專用網路，則可以從清單中選取該網路。如需相關資訊，請參閱<a href="/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring" target="_blank">配置專用網路</a>。</td>
</tr></table>
