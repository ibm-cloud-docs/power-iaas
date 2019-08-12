---

copyright:
  years: 2019

lastupdated: "2019-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server について
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}} は、既存の IBM Cloud プラットフォームを使用して、PowerVM ハイパーバイザーを備えた IBM Power Systems ハードウェア上で稼働する Power Systems 仮想サーバー (論理区画 (LPAR) とも呼ばれる) を作成します。
{:shortdesc}

{{site.data.keyword.powerSys_notm}} は、一種の Infrastructure as a Service (IaaS) です。{{site.data.keyword.powerSys_notm}} サービスを使用すると、AIX または IBM i のオペレーティング・システムを実行している 1 台以上の仮想サーバーを、パブリック・クラウドに迅速に作成してデプロイすることができます。クラウドに仮想サーバーをプロビジョンした後、AIX または IBM i のオペレーティング・システムがセキュアであることを確認する必要があります。

## 主要機能
{: #apvs-key-features}

{{site.data.keyword.powerSys_notm}} の主要機能は、以下のとおりです。

### 分かりやすい請求
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}} は、AIX および IBM i のオペレーティング・システムのライセンスを含む月次請求レートを使用します。月次請求レートは、その月の {{site.data.keyword.powerSys_notm}} インスタンスにデプロイされたリソースに基づいて、時間で比例配分されます。{{site.data.keyword.powerSys_notm}} インスタンスを作成すると、指定したオプションに基づいた構成の合計コストを確認できます。ビジネス・ニーズに最適な価値を提供する構成オプションを素早く特定できます。詳しくは、[料金](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server)を参照してください。

### ハイブリッド・クラウド環境
{: #apvs-hybrid}

{{site.data.keyword.powerSys_notm}} を使用すると、既存の Power Systems ハードウェア・インフラストラクチャーから AIX または IBM i の任意のワークロードをオフプレミスで実行することができます。パブリック・クラウドでワークロードを実行すると、セルフサービス、高速配信、弾力性、他の IBM Cloud サービスへの接続など、クラウドが提供するすべての利点を活用できます。AIX および IBM i のワークロードをクラウドで実行しても、Power Systems ハードウェアが提供する、スケーラブルで回復力のある実動用のフィーチャーは同じように維持されます。

### インフラストラクチャーのカスタマイズ
{: #apvs-customization}

{{site.data.keyword.powerSys_notm}} の作成時に、以下のオプションを構成およびカスタマイズできます。
* 仮想サーバー・インスタンスの数
* コアの数
* メモリーの量
* データ・ボリュームのサイズとタイプ (HDD または SSD)
* プライベート・ネットワークまたはパブリック・ネットワーク

### 独自のイメージの持ち込み
{: #apvs-own-image}

IBM は、{{site.data.keyword.powerSys_notm}} の作成時に、AIX および IBM i オペレーティング・システムのストック・イメージを提供します。ただし、AIX または IBM i オペレーティング・システムの、以前にデプロイしてテストした独自のカスタム・イメージを持ち込むこともできます。詳しくは、[カスタム・イメージの構成](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)を参照してください。

## ハードウェアの仕様
{: #apvs-hardware-specifications}

以下の IBM Power Systems ハードウェアが {{site.data.keyword.powerSys_notm}} をホストします。

* コンピュート
  * [Power System E880 (9119-MHE) ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9 TB のメモリー
    * 8 x 16 ギガビット PCI Express デュアル・ポート・ファイバー・チャネル (FC)
    * 10 x 10 ギガビット・イーサネット SR PCI Express デュアル・ポート
  * [Power System S922 (9009-22A) ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384 GB メモリー
    * 2 x 16 ギガビット PCI Express デュアル・ポート FC
    * 3 x 10 ギガビット・イーサネット SR PCI Express デュアル・ポート

* ストレージ
  * Storewize V7000F(2076-AF6) Dual Controller
  * Storwize V7000 (2076-624) Dual Controller

* ネットワーク
  * Cisco Nexus9000 93180YC-EX (10G)
  * Cisco Nexus9000 C9348GC-FXP (1G)

## パブリック・ネットワークとプライベート・ネットワーク
{: #apvs-public-and-private}

{{site.data.keyword.powerSys_notm}} を作成するときに、プライベート・ネットワーク・インターフェースまたはパブリック・ネットワーク・インターフェースを選択できます。

* パブリック・ネットワーク
  * {{site.data.keyword.powerSys_notm}} インスタンスに簡単かつ迅速に接続できます。
  * IBM は、インターネットから {{site.data.keyword.powerSys_notm}} インスタンスへのセキュアなパブリック・ネットワーク接続が可能になるようネットワーク・インフラストラクチャーを構成します。
  * 接続は、IBM Cloud Virtual Router Appliance (VRA) および Direct Link Connect 接続を使用して実装されます。
  * 接続はファイアウォールによって保護され、以下のセキュア・ネットワーク・プロトコルをサポートしています。
    * SSH
    * HTTPS
    * Ping
    * SSL を使用する IBM i 5250 端末エミュレーション (ポート 992)

* プライベート・ネットワーク
  * {{site.data.keyword.powerSys_notm}} インスタンスのリソースが、ベア・メタル・サーバー、Kubernetes コンテナー、クラウド・ストレージなどの既存の {{site.data.keyword.cloud_notm}} リソースにアクセスできるようにします。
  * Direct Link Connect 接続を使用して、IBM Cloud アカウント・ネットワークおよびリソースに接続します。IBM Cloud サポートがリンクを構成する必要があるため、Direct Link Connect 接続を作成するプロセスには数日かかることがあります。
  * 異なる {{site.data.keyword.powerSys_notm}} インスタンス間の通信に必要です。

    プライベート・ネットワークを構成するためのさまざまなオプションについて詳しくは、[プライベート・ネットワークの構成](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring)を参照してください。
    {: note}

以下の図は、パブリック・ネットワークとプライベート・ネットワークの基本構成を示しています。

![パブリック接続とプライベート接続のネットワーク・トラフィック・フローを表示](/images/power-iaas-network1.svg "パブリック接続とプライベート接続のネットワーク・トラフィック・フローを表示")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
