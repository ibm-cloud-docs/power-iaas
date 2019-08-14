---

copyright:
  years: 2019

lastupdated: "2019-7-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:important: .important}
{:tip: .tip}

# Power Systems Virtual Server の概要
{: #getting-started}


{{site.data.keyword.powerSysFull}} は、ほんの数分で仮想サーバー (論理区画 (LPAR) とも呼ばれる) をデプロイするために使用できる Infrastructure as a Service オファリングです。
{:shortdesc}

特定のビジネス・ニーズに合わせた {{site.data.keyword.powerSys_notm}} を素早くデプロイすることができます。{{site.data.keyword.powerSys_notm}} を使用すると、ワークロードの要求を簡単に制御できるハイブリッド・クラウド環境を作成できます。

{{site.data.keyword.powerSys_notm}} は、さまざまな地理的位置で AIX または IBM i ワークロードを実行できます。

## 用語
{: #gs-terminology}

仮想サーバーを作成する前に、{{site.data.keyword.powerSys_notm}}** サービス**という用語と {{site.data.keyword.powerSys_notm}} **インスタンス**という用語の違いを理解しておく必要があります。{{site.data.keyword.powerSys_notm}} **サービス**は、特定の地理的位置にあるすべての {{site.data.keyword.powerSys_notm}} **インスタンス**のコンテナーと考えてください。{{site.data.keyword.powerSys_notm}} **サービス**は、**UI の {{site.data.keyword.cloud}} リソース・リスト**から
選択できます。サービスには、複数の {{site.data.keyword.powerSys_notm}} **インスタンス**が含まれている可能性があります。

例えば、ダラスとワシントン DC の 2 つの {{site.data.keyword.powerSys_notm}} **サービス**を選択できます。それぞれのサービスには、複数の {{site.data.keyword.powerSys_notm}} **インスタンス**が含まれている可能性があります。

## 始める前に
{: #gs-before-you-begin}

初めて Power Systems Virtual Server インスタンスを作成する前に、以下の前提条件を確認してください。

1. {: hide-dashboard}IBM Cloud アカウントを作成します。IBM Cloud アカウントを作成するには、[IBM Cloud に登録 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/registration){: new_window} を参照してください。

2. {{site.data.keyword.powerSys_notm}} に安全に接続するために使用できる SSH 公開鍵と SSH 秘密鍵を作成します。SSH 公開鍵と SSH 秘密鍵の作成については、[SSH 鍵の追加![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)を参照してください。

3. (オプション) AIX または IBM i オペレーティング・システム用のカスタム・イメージを使用する場合は、IBM Cloud オブジェクト・ストレージを作成し、イメージをアップロードする必要があります。詳しくは、[カスタム・イメージの構成](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)を参照してください。

4. (オプション) プライベート・ネットワークを使用して {{site.data.keyword.powerSys_notm}} インスタンスに接続する場合は、Direct Link Connect サービスを注文する必要があります。詳しくは、[UI コンソールからの IBM Cloud Direct Link Connect の注文](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect)を参照してください。

## 次のステップ
{: #gs-next-steps}

IBM Cloud アカウントと、SSH 公開鍵と SSH 秘密鍵を使用して、[{{site.data.keyword.powerSys_notm}} サービスを作成](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)する準備ができました。
