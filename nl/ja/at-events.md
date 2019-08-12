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

# {{site.data.keyword.powerSys_notm}} Activity Tracker イベント
{: #at_events}

セキュリティー担当者、監査員、または管理者として、お客様は Activity Tracker サービスを使用して、ユーザーおよびアプリケーションが {{site.data.keyword.cloud}} の {{site.data.keyword.powerSys_notm}} サービスとどのように対話しているかをトラッキングすることができます。{:shortdesc}

{{site.data.keyword.at_full_notm}} は、{{site.data.keyword.cloud_notm}} 内のサービスの状態を変更するユーザー開始アクティビティーを記録します。このサービスを使用して、異常なアクティビティーや重大なアクションがないかを調査し、規制監査要件を遵守することができます。さらに、アクションが発生した際にそれに関するアラートが通知されるようにすることもできます。収集されるイベントは、Cloud Auditing Data Federation (CADF) 標準に準拠しています。[詳細はこちら](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started)。

## イベントのリスト: 読み取り
{: #at_actions_read}

以下のイベントは、{{site.data.keyword.powerSys_notm}} インスタンスの読み取りに使用されます。

| アクション                     | 説明                     |
|:---------------------------|:--------------------------------|
| pcloud.cloud-instance.read | Power Cloud インスタンスの読み取り     |


## イベントのリスト: イメージ
{: #at_actions_images}

以下のイベントは、{{site.data.keyword.powerSys_notm}} インスタンス内のイメージを処理するためのものです。

| アクション                     | 説明                     |
|:---------------------------|:--------------------------------|
| pcloud.image.read          | 1 つまたはすべてのイメージの読み取り |
| pcloud.image.create        | 新規イメージの作成              |
| pcloud.image.update        | イメージの更新                  |
| pcloud.image.delete        | イメージの削除                  |
| pcloud.image.capture       | イメージのエクスポート          |


## イベントのリスト: ネットワーク
{: #at_actions_networks}

以下のイベントは、{{site.data.keyword.powerSys_notm}} インスタンス内のネットワークを処理するためのものです。

| アクション                     | 説明                           |
|:---------------------------|:--------------------------------------|
| pcloud.network.read        | 1 つまたはすべてのネットワークの読み取り |
| pcloud.network.create      | 新規ネットワークの作成 (パブリック/プライベート) |
| pcloud.network.update      | ネットワークの更新                    |
| pcloud.network.delete      | ネットワークの削除                    |
{: caption="表 3. イベントを生成するアクション" caption-side="top"}

## イベントのリスト: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

以下のイベントは、{{site.data.keyword.powerSys_notm}} インスタンス内の仮想サーバーをそれぞれ処理するためのものです。

| アクション                        | 説明                          |
|:------------------------------|:-------------------------------------|
| pcloud.pvm-instance.read      | Power 仮想サーバー・インスタンスの読み取り |
| pcloud.pvm-instance.create    | Power 仮想サーバー・インスタンスの作成 |
| pcloud.pvm-instance.update    | Power 仮想サーバー・インスタンスの更新 |
| pcloud.pvm-instance.delete    | Power 仮想サーバー・インスタンスの削除 |
| pcloud.pvm-instance.start     | Power 仮想サーバー・インスタンスの開始 |
| pcloud.pvm-instance.stop      | Power 仮想サーバー・インスタンスの停止 |
| pcloud.pvm-instance.renew     | Power 仮想サーバー・インスタンスのリブート |
| pcloud.pvm-instance.unknown   | Power 仮想サーバー・インスタンス上の不明アクション |
| pcloud.pvm-instance.monitor   | Power 仮想サーバー・インスタンスへのコンソール・アクセス |
| pcloud.pvm-instance.capture   | Power 仮想サーバー・インスタンスのイメージへのキャプチャー |

## イベントのリスト: SSH 鍵
{: #at_actions_ssh_keys}

以下のイベントは、{{site.data.keyword.powerSys_notm}} インスタンス内のアカウントおよび SSH 鍵を処理するためのものです。

| アクション                   | 説明                 |
|:-------------------------|:----------------------------|
| pcloud.tenant.read       | テナント情報の読み取り      |
| pcloud.ssh-key.read      | SSHKey または SSH 鍵の読み取り |
| pcloud.ssh-key.create    | SSH 鍵の作成                |
| pcloud.ssh-key.update    | SSH 鍵の更新                |
| pcloud.ssh-key.delete    | SSH 鍵の削除                |

## イベントのリスト: データ・ボリューム
{: #at_actions_data_volumes}

以下のイベントは、{{site.data.keyword.powerSys_notm}} インスタンス内のデータ・ボリュームを処理するためのものです。

| アクション                   | 説明                 |
|:-------------------------|:----------------------------|
| pcloud.volume.read       | 1 つ以上のボリュームの読み取り |
| pcloud.volume.create     | ボリュームの作成            |
| pcloud.volume.update     | ボリュームの更新            |
| pcloud.volume.delete     | ボリュームの削除            |
| pcloud.volume.configure  | ボリュームの接続または切り離し|

## イベントの表示
{: #at_ui}

イベントは、**ダラス**で使用可能です。

{{site.data.keyword.at_full_notm}} では、場所ごとに存在できるインスタンスは 1 つだけです。イベントを表示するには、ロケーション `us-south` で {{site.data.keyword.at_full_notm}} サービスの Web UI にアクセスする必要があります。[詳細はこちら](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2)。
