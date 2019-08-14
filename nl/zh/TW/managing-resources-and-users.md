---

copyright:
  years: 2019

lastupdated: "2019-07-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}

# 管理 {{site.data.keyword.powerSys_notm}} 資源和使用者
{: #managing-resources-and-users}

{{site.data.keyword.powerSysFull}} 的授權和資源管理作法會與 IBM Cloud Identity and Access Management (IAM) 服務進行協調。IAM 可讓您能夠安全地鑑別使用者，透過資源群組控制對 {{site.data.keyword.powerSys_notm}} 資源的存取權，並使用存取群組容許一群組使用者存取特定資源。換句話說，IAM 是一站式服務點，用於 {{site.data.keyword.cloud_notm}} 中的所有使用者和資源管理。
{: shortdesc}

您可以根據以下條件來指派 IAM 授權：

* 個別使用者
* 存取群組（使用者群組）
* 特定類型的資源
* 資源群組

如需 IAM 的相關資訊，請檢閱下列資訊：

* [開始使用 IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [IAM 概念](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [管理資源群組](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [設定存取群組](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## 平台存取角色
{: #platform-access-roles}

可以使用平台存取角色來讓使用者在 {{site.data.keyword.cloud_notm}} 資源上完成作業，例如建立使用者或新增服務。

下表顯示了 IAM 平台存取角色以及 {{site.data.keyword.powerSys_notm}} 容許的相應控制類型：

|平台存取角色|容許的存取類型|
|-----------|-------------------------|
|檢視者|檢視實例及列出實例。|
|操作員|檢視實例及列出實例。|
|編輯者|檢視實例、列出實例、建立實例及刪除實例。|
|管理者|檢視實例、列出實例、建立實例、刪除實例及指派原則給其他使用者。|

## 服務存取角色
{: #service-access-roles}

可以使用服務存取角色來定義哪些使用者可以使用 {{site.data.keyword.powerSys_notm}} 服務功能。

下表顯示了 IAM 服務存取角色以及使用者可以透過 {{site.data.keyword.powerSys_notm}} 完成的相應動作：

|服務存取角色 |動作說明|
|-----------|-------------------------|
|讀者|檢視所有資源，例如 SSH 金鑰、儲存空間磁區和網路設定。無法對資源進行任何變更。|
|管理員|可以配置所有資源。以下是可以執行的一些動作：<ul><li>建立實例</li><li>新增儲存空間磁區大小</li><li>建立 SSH 金鑰</li><li>修改網路設定</li><li>建立開機映像檔</li><li>刪除儲存空間磁區</li>
</ul>

## 使用者存取情境
{: #user-access-scenarios}

下列存取情境涵蓋新增使用者和修改現有使用者許可權所需的步驟。

### 邀請新的使用者檢視 {{site.data.keyword.powerSys_notm}} 資源
{: #inviting-a-new-user-to-create-or-manage-resources}

您必須邀請 IBM Cloud 使用者加入帳戶，並向其授予檢視 {{site.data.keyword.powerSys_notm}} 資源的存取權。請記住，服務存取角色用於確定使用者對 {{site.data.keyword.powerSys_notm}} 資源具有的存取層次。

在 IAM 中完成下列步驟，可以讓使用者檢視 {{site.data.keyword.powerSys_notm}} 資源：

1. 導覽至 IBM Cloud 主控台中的 [IAM 使用者使用者介面![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/iam/users){: new_window}，然後按一下**邀請使用者**。

      ![顯示 IAM 使用者介面中的邀請使用者圖示](/images/invite_users.png "在 IAM 使用者介面中邀請使用者"){: caption="圖 1. 在 IAM 使用者介面中邀請使用者" caption-side="bottom"}

2. 在**使用者**區段下的**電子郵件位址**欄位中，輸入所需的使用者電子郵件位址。
3. 接下來，從**指派對以下項目的存取權**欄位中，選取**資源**，然後在**服務**欄位中，選取 **{{site.data.keyword.powerSys_notm}}**。

    ![顯示服務欄位](/images/invite_users2.png "在 IAM 使用者介面中為新使用者選取 {{site.data.keyword.powerSys_notm}} 服務"){: caption="圖 2. 為新使用者選取 Power Systems Virtual Server 服務" caption-side="bottom"}

4. 選取要指派給使用者的平台存取角色。在此情境中，使用者只能檢視 {{site.data.keyword.cloud_notm}} 和 {{site.data.keyword.powerSys_notm}} 資源。

    ![顯示用於 IAM 角色的使用者介面](/images/invite_users3.png "在 IAM 使用者介面中為新使用者選取角色"){: caption="圖 3. 在 IAM 使用者介面中為新使用者選取角色" caption-side="bottom"}

5. 按一下**邀請使用者**。使用者必須接受邀請，才能被新增到帳戶。如果順利傳送了邀請，則會顯示一條訊息。

    ![顯示成功邀請的訊息](/images/invite_users4.png "成功邀請的訊息"){: caption="圖 4. 成功邀請的訊息" caption-side="bottom"}

### 授予現有使用者管理 {{site.data.keyword.powerSys_notm}} 資源的許可權
{: #giving-an-existing-user-permission-to-manage-resources}

要為帳戶中的現有使用者提供配置 {{site.data.keyword.powerSys_notm}} 資源的許可權，請完成下列步驟。

1. 導覽至 IBM Cloud 主控台中的 [IAM 使用者使用者介面![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/iam/users){: new_window}。
2. 從使用者清單中，選取要變更其授權的使用者。
3. 按一下**存取原則**，然後按一下使用者的現行角色。在此情境中，請按一下**檢視者和讀者**。

    ![顯示如何變更現有使用者的許可權](/images/existing_user1.png "在 IAM 使用者介面中變更使用者的許可權"){: caption="圖 5. 在 IAM 使用者介面中變更使用者的許可權" caption-side="bottom"}

4. 在**選取角色**欄位中，按一下**管理員**。可以將**讀者**角色保持已選取。

    ![顯示為現有使用者新增管理員角色](/images/existing_user2.png "在 IAM 使用者介面中選取管理員角色"){: caption="圖 6. 在 IAM 使用者介面中選取管理員角色" caption-side="bottom"}

5. 按一下**儲存**。

   現在，使用者有權配置 {{site.data.keyword.powerSys_notm}} 資源。但是，此使用者無法管理 {{site.data.keyword.cloud_notm}} 平台特定的服務和資源。例如，該使用者無法新增使用者。
   {: note}
