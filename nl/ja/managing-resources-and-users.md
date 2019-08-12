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

# {{site.data.keyword.powerSys_notm}} リソースとユーザーの管理
{: #managing-resources-and-users}

{{site.data.keyword.powerSysFull}} の権限とリソース管理のための手法では、IBM Cloud の Identity and Access Management (IAM) サービスを利用します。IAM を使用すると、ユーザーを安全に認証し、リソース・グループによって {{site.data.keyword.powerSys_notm}} リソースへのアクセスを制御し、アクセス・グループによって特定のリソースへのアクセスを特定のユーザー・セットに対して許可できます。つまり、IAM は {{site.data.keyword.cloud_notm}} におけるユーザーとリソースの管理すべてのワンストップ・ショップとなります。
{: shortdesc}

以下の基準に基づいて IAM 許可を割り当てることができます。

* 個別ユーザー
* アクセス・グループ (ユーザーのグループ)
* 特定のタイプのリソース
* リソース・グループ

IAM について詳しくは、以下の情報をご確認ください。

* [IAM の開始](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [IAM の概念](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [リソース・グループの管理](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [アクセス・グループのセットアップ](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## プラットフォーム・アクセス役割
{: #platform-access-roles}

プラットフォーム・アクセス役割を使用すると、ユーザーの作成やサービスの追加など、{{site.data.keyword.cloud_notm}} リソースに対するタスクをユーザーが実行できるようになります。

以下の表に、IAM プラットフォーム・アクセス役割と、それぞれに対応する、{{site.data.keyword.powerSys_notm}} で許可されている制御タイプを示します。

| プラットフォーム・アクセス役割 | 許可されるアクセスのタイプ |
|-----------|-------------------------|
| ビューアー | インスタンスの表示とインスタンスのリスト作成。 |
| オペレーター | インスタンスの表示とインスタンスのリスト作成。 |
| エディター | インスタンスの表示、インスタンスのリスト作成、インスタンスの作成、インスタンスの削除。  |
| 管理者 | インスタンスの表示、インスタンスのリスト作成、インスタンスの作成、インスタンスの削除、および他のユーザーへのポリシーの割り当て。 |

## サービス・アクセスの役割
{: #service-access-roles}

サービス・アクセス役割を使用すると、{{site.data.keyword.powerSys_notm}} サービス機能によってユーザーが実行できる内容を定義できます。

以下の表に、IAM サービス・アクセス役割と、それぞれに対応する、{{site.data.keyword.powerSys_notm}} でユーザーが実行できるアクションを示します。

| サービス・アクセス役割 | アクションの説明 |
|-----------|-------------------------|
| リーダー | SSH 鍵、ストレージ・ボリューム、ネットワーク設定などすべてのリソースの表示。リソースに変更を加えることはできません。 |
| 管理者 | すべてのリソースを構成できます。実行可能なアクションの一部を以下に示します。<ul><li>インスタンスの作成</li><li>ストレージ・ボリューム・サイズの増加</li><li>SSH 鍵の作成</li><li>ネットワーク設定の変更</li><li>ブート・イメージの作成</li><li>ストレージ・ボリュームの削除</li>
</ul>

## ユーザー・アクセスのシナリオ
{: #user-access-scenarios}

以下のアクセス・シナリオでは、新しいユーザーを追加し、既存のユーザーの許可を変更するために必要な手順について取り上げています。

### {{site.data.keyword.powerSys_notm}} リソースを表示するために新規ユーザーを招待する
{: #inviting-a-new-user-to-create-or-manage-resources}

IBM Cloud ユーザーをアカウントに招待し、そのユーザーが {{site.data.keyword.powerSys_notm}} リソースを表示するためのアクセス権を付与する必要があります。サービス・アクセス役割によって、{{site.data.keyword.powerSys_notm}} リソースに関してユーザーが持つアクセス・レベルが決まる点に注意してください。

ユーザーが {{site.data.keyword.powerSys_notm}} リソースを表示できるようにするには、IAM で以下の手順を実行します。

1. IBM Cloud コンソールの [IAM ユーザー UI ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/iam/users){: new_window} に移動し、**「ユーザーの招待」**をクリックします。

      ![IAM UI のユーザーの招待アイコンの表示](/images/invite_users.png "IAM UI からユーザーを招待する")

2. **「ユーザー」**セクションの**「E メール・アドレス」**フィールドに対象となるユーザーの E メール・アドレスを入力します。
3. 次に、**「アクセス権限の割り当て」**フィールドの**「リソース」**と、**「サービス」**フィールドの**「{{site.data.keyword.powerSys_notm}}」**を選択します。

    ![「サービス」フィールドの表示](/images/invite_users2.png "IAM UI で、新規ユーザーの {{site.data.keyword.powerSys_notm}} サービスを選択する")

4. ユーザーに割り当てるプラットフォーム・アクセス役割を選択します。 このシナリオでは、ユーザーが表示できるのは、{{site.data.keyword.cloud_notm}} リソースと {{site.data.keyword.powerSys_notm}} リソースのみです。

    ![IAM 役割の UI の表示](/images/invite_users3.png "IAM UI で、新規ユーザーの役割を選択する")

5. **「ユーザーの招待」**をクリックします。そのユーザーがアカウントに追加されるには、ユーザーの側が招待を受け入れる必要があります。招待が正常に送信されると、メッセージが示されます。

    ![招待が成功したことを示すメッセージの表示](/images/invite_users4.png "招待成功メッセージ")

### 既存のユーザーに {{site.data.keyword.powerSys_notm}} リソースを管理するための許可を付与する
{: #giving-an-existing-user-permission-to-manage-resources}

アカウント内の既存のユーザーに {{site.data.keyword.powerSys_notm}} リソースを構成するための許可を提供するには、以下の手順を実行します。

1. IBM Cloud コンソールの [IAM ユーザー UI ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/iam/users){: new_window} にナビゲートします。
2. ユーザーのリストで、変更する許可を持つユーザーを選択します。
3. **「アクセス・ポリシー」**をクリックし、ユーザーの現在の役割をクリックします。このシナリオでは、**「ビューアー、リーダー」**をクリックします。

    ![既存のユーザーの許可を変更する方法の表示](/images/existing_user1.png "IAM UI で、ユーザーの許可を変更する")

4. **「役割の選択」**フィールドで、**「管理者」**をクリックします。**「リーダー」**役割は選択されたままにできます。

    ![既存のユーザーに管理者役割を追加する方法の表示](/images/existing_user2.png "IAM UI から、管理者役割を選択する")

5. **「保存」**をクリックします。

   ユーザーに、{{site.data.keyword.powerSys_notm}} リソースを構成する許可が与えられました。ただし、このユーザーは、{{site.data.keyword.cloud_notm}} プラットフォームに特有のサービスとリソースを管理することはできません。例えば、新規ユーザーを追加することはできません。
   {: note}
