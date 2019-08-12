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

# Power Systems Virtual Server を使用したカスタム・イメージの構成
{: #configuring-custom-image}

AIX または IBM i オペレーティング・システムの、独自にカスタマイズしたイメージを持ち込んで、{{site.data.keyword.powerSysFull}} をデプロイできます。
{:shortdesc}

オンプレミスのシステムからクラウド環境で稼働している {{site.data.keyword.powerSys_notm}} にオペレーティング・システム・ライセンスを転送することはできません。ライセンス・コストは、全体の毎時請求レートに組み込まれます。
{: note}

## 始めに
{: #cci-before-you-begin}

カスタム・イメージをブート・ボリュームとして使用する前に、以下の情報を確認してください。

* AIX または IBM i オペレーティング・システムのテクノロジー・レベルが、**「マシン・タイプ (Machine Type)」**フィールドで選択した Power Systems ハードウェアでサポートされていることを確認する必要があります。サポートされている AIX および IBM i オペレーティング・システムのテクノロジー・レベルと Power System ハードウェアのリストを表示するには、[システム・ソフトウェア・マップ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps)を参照してください。
* **IBM Cloud Object Storage** の概念についての基本的な知識が必要です。詳しくは、[IBM Cloud Object Storage について](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage)を参照してください。
* 既存の AIX または IBM i イメージがない場合は、IBM® PowerVC™ を使用して、{{site.data.keyword.powerSys_notm}} で使用するイメージをキャプチャーおよびエクスポートできます。詳しくは、[仮想マシンの取り込み![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window}および[イメージのエクスポート![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}を参照してください。

## オブジェクトとしてのカスタム・イメージのアップロード
{: #cci-uploading}

1. IBM Cloud ストレージ・オブジェクトを作成し、イメージをアップロードします。詳しくは、[データのアップロード](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload)を参照してください。
2. ハッシュ・ベースのメッセージ認証コード (HMAC) を使用して、秘密鍵とアクセス・キーを生成します。IBM Cloud ストレージ・オブジェクトのサービス資格情報を作成するときに、これらの鍵を生成できます。サービス資格情報を作成するには、**オブジェクト・ストレージ**・バケットに対する`ライター`・アクセス権限が必要です。詳しくは、[サービス資格情報](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials)および[バケット許可](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions)を参照してください。
3. [IBM Cloud カタログ ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/catalog){: new_window} で、Power Virtual Server のタイルをクリックして、イメージを追加します。仮想サーバー・インスタンスを既に作成済みの場合は、**「メニュー」アイコン![「メニュー」アイコン](../icons/icon_hamburger.svg "「メニュー」アイコン") >「リソース・リスト」>「デバイス」**を選択し、既存の仮想サーバーを選択します。

 以下のフィールドに入力して {{site.data.keyword.powerSys_notm}} を作成し、**「カスタム AIX イメージ (Custom AIX image)」**または**「カスタム IBM i イメージ (Custom IBM i Image)」**をクリックします。

| フィールド | 説明 |
| ------| ------------|
| Cloud Object Storage バケット名 (Cloud Object Storage bucket name) |バケット名を識別するには、**「メニュー」アイコン![「メニュー」アイコン](../icons/icon_hamburger.svg "「メニュー」アイコン") >「リソース・リスト」>「ストレージ」>「Cloud ストレージ・オブジェクト名」>「バケット」**を選択します。|
| Cloud Object Storage アクセス・キー (Cloud Object Storage access key) | アクセス・キーを識別するには、**「メニュー」アイコン![「メニュー」アイコン](../icons/icon_hamburger.svg "「メニュー」アイコン") >「リソース・リスト」>「ストレージ」>「Cloud ストレージ・オブジェクト名」>「サービス資格情報」>「資格情報の表示」**を選択します。`access_key_id` 値をコピーして、このフィールドに貼り付けます。|
| Cloud Object Storage 秘密鍵 (Cloud Object Storage secret key) | 秘密鍵を識別するには、**「メニュー」アイコン![「メニュー」アイコン](../icons/icon_hamburger.svg "「メニュー」アイコン") >「リソース・リスト」>「ストレージ」>「Cloud ストレージ・オブジェクト名」>「サービス資格情報」>「資格情報の表示」**を選択します。`secret_access_key` 値をコピーして、このフィールドに貼り付けます。|
| イメージ・パス (Image Path) | イメージ・ファイルの完全修飾パスを入力します。完全修飾パスは、`endpoint/bucket_name/file_name` という形式でなければなりません。プライベート・エンドポイント・ドメインを使用する必要があります。例えば、`s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz` のようになります。**「メニュー」アイコン ![「メニュー」アイコン](../icons/icon_hamburger.svg "「メニュー」アイコン") >「リソース・リスト」>「ストレージ」>「Cloud ストレージ・オブジェクト (Cloud Storage Object)」**を選択して、エンドポイント・ドメイン、バケット名、およびファイル名を識別できます。
