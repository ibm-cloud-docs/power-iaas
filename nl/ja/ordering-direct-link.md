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

# Power Systems Virtual Server 用 IBM Cloud Direct Link Connect の注文
{: #ordering-direct-link-connect}

{{site.data.keyword.powerSys_notm}} でプライベート・ネットワークを構成する 1 つの選択肢は、Direct Link Connect サービスを使用する方法です。Direct Connect Link サービスでは、{{site.data.keyword.cloud}} リソースにご使用の {{site.data.keyword.powerSys_notm}} インスタンスからアクセスできる接続が作成されます。また Direct Link Connect サービスで IBM Cloud Virtual Router Appliance (VRA) を使用して、IBM Cloud ネットワークにオンプレミスのネットワークを接続することもできます。
{:shortdesc}

{{site.data.keyword.cloud_notm}} UI コンソールを使用して、Direct Link Connect サービスを注文できます。Direct Link Connect は {{site.data.keyword.powerSys_notm}} サービスとは別個のサービスです。Direct Link Connect の料金については、[IBM Cloud Direct Link の料金](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect)をご確認ください。

バックアップのために 2 つ目の Direct Link Connect 接続を注文することをお勧めします。

## 始める前に
{: #before-direct-link-connect}

* {{site.data.keyword.cloud}} アカウントに、Direct Link Connect サービスを注文する適切な許可があることを確認します。
* 以下のトピックを確認し、Direct Link Connect サービスの基本的なネットワーキング概念を理解してください。
    * [Direct Link Connect の概念](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
    * [Direct Link Connect の詳細](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Direct Link Connect の制限](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [IP 割り当てに対する厳密な制限](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Direct Link Connect を注文するためのステップ
{: #steps-to-order-direct-link-connect}

{{site.data.keyword.powerSys_notm}} インスタンスに対する接続を作成する Direct Link Connect サービスを注文するには、以下のステップを実行します。

1. IBM Cloud アカウント資格情報を使用して [IBM Cloud カタログ ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/catalog){: new_window} にログインします。アカウントには、Direct Link Connect サービスを注文する適切な許可がなければなりません。

2. **「ネットワーキング」**セクションで、**「Direct Link Connect」**タイルをクリックします。
![Direct Link カタログ・タイルの表示](/images/directlink1.png "Direct Link カタログ・タイルの表示")

1. Direct Link Connect カタログ・エントリーで、**「作成」**をクリックします。

1. 「IBM Cloud Direct Link」ページで、**「Direct Link Connect の注文 (Order Direct Link Connect)」**をクリックします。

1. 「IBM Cloud Direct Link Connect 接続の作成 (Create IBM Cloud Direct Link Connect Connection)」ページで、以下のフィールドに入力します。

   Direct Link Connect サービスを作成するために以下のフィールドに入力すると、選択内容に応じて価格が自動的に更新されます。
   {: note}

   <dl>
   <dt><strong>Direct Link インスタンス名</strong><dt>
   <dd>Direct Link Connect の目的を説明する名前を入力します。</dd>
   <dt><strong>場所</strong><dt>
   <dd>{{site.data.keyword.powerSys_notm}} インスタンスと同じ場所を選択します。以下の表は、{{site.data.keyword.powerSys_notm}} インスタンスの場所と対応する Direct Link Connection オプションを示しています。
   <table>
   <caption>表 1. Direct Link Connection の場所のオプション</caption>
   <tr>
   <th>Power Systems Virtual Server の場所</th>
   <th>Direct Link Connect の場所</th>
   </tr>
   <tr>
   <td>ダラス (米国テキサス州)</td>
   <td>ダラス 4</td>
   </tr>
   <tr>
   <td>ワシントン D.C (米国)</td>
   <td>ワシントン 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>ネットワーク・プロバイダー</strong><dt>
   <dd>リストから<strong>「MEGAPORT」</strong>を選択する必要があります。</dd>
   <dt><strong>リンク速度</strong><dt>
   <dd>ワークロード要件を満たすリンク速度を選択します。このフィールドの推奨値は 1000 Mbps です。</dd>
   <dt><strong>ルーティング・オプション</strong><dt>
   <dd><strong>「場所」</strong>フィールドで指定した場所で接続されているすべてデータ・センターにアクセスする場合には、<strong>「ローカル・ルーティング (無料)(Local Routing (Free))」</strong>を選択します。世界中の IBM Cloud データ・センターすべてにアクセスするには、<strong>「グローバル・ルーティング (Global Routing)」</strong>を選択します。</dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>以下の表に記されている、特定の Direct Link Connect の場所の BGP ASN 番号を入力する必要があります。
   <table>
   <caption>表 2. 特定の場所の BGP ASN 番号</caption>
   <tr>
   <th>Direct Link Connect の場所</th>
   <th>BGP ASN 番号</th>
   </tr>
   <tr>
   <td>ダラス 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>ワシントン 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>VRF の選択 (Select VRF)</strong><dt>
   <dd>接続のための仮想ルーティングと転送オプションを選択します。アカウントで VRF が示されていない場合、このフィールドは表示されません。VRF を選択しないで、Direct Link Connect サービスを作成することもできます。以下の図は、Direct Link Connect フィールドの例を示しています。</dd>
   <dd>

   ![入力済みの Direct Link Connect フィールドの表示](/images/directlink2.png "入力済みの Direct Link Connect フィールドの表示")
   </dd>
   </dl>
2. **「マスター・サービス契約」**を読み、チェック・ボックスを選択します。**「マスター・サービス契約」**には重要な技術情報が記されているため、読んで理解する必要があります。

3. **「作成」**をクリックします。 要求が正常に送信されると、以下のメッセージが表示されます。
![Direct Link Connect によって正常に送信されたことを示すメッセージの表示](/images/directlink3.png "Direct Link Connect によって正常に送信されたことを示すメッセージの表示")

1. Direct Link Connect サービスの**「Case 番号」**リンクをクリックします。Case 番号の情報を使用して、{{site.data.keyword.powerSys_notm}} インスタンスに接続するための Direct Link Connect 情報を識別します。

  IBM Cloud サポートが Direct Link Connect 接続を作成するには、最大で 3 営業日必要なことがあります。
  {: note}

2. Direct Link Connect サービスによって {{site.data.keyword.powerSys_notm}} インスタンスへの接続を作成するには、{{site.data.keyword.powerSys_notm}} サポート・チームの[新規 Case](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support) を開きます。

      1. 新しい Case の説明フィールドに、Direct Link Connect Case 番号を追加します。
      2. システムによって自動的に生成された {site.data.keyword.powerSys_notm}} Case IAM サービス ID をコピーします。

3. {{site.data.keyword.powerSys_notm}} Case の IAM サービス ID を Direct Link Connect Case に入力します。Direct Link Connect 接続が作成されると、その Direct Link Connect Case 番号はクローズされます。Case に表示されるネットワーク情報の例を以下に示します。

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

1. Direct Link Connect Case 番号に基づくこの情報を使用して、以下のネットワーク情報を {{site.data.keyword.powerSys_notm}} Case に入力します。

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

1. {{site.data.keyword.powerSys_notm}} Case は、Direct Link Connect 接続が {{site.data.keyword.powerSys_notm}} インスタンスと通信するよう構成されるとクローズされます。
