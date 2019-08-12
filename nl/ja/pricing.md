---

copyright:
  years: 2019

lastupdated: "2019-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server on IBM Cloud の料金
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}} は選択した地域でのみ提供されており、論理パーティション (LPAR) は最大 15 個のコアと 320 GB のメモリーまでスケールアウトできます。また、エンタープライズ LPAR の場合には最大 143 個のコアと 8192 GB のメモリーまでスケールアウトできます。こうしたオプションによって、{{site.data.keyword.powerSys_notm}} はお客様の事業のあらゆるワークロード要件を満たすことができます。請求は月額で行われます。
{:shortdesc}

## 月々の使用量
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} インスタンスは、時間単位の比例配分として月額で請求されます。月の途中で LPAR にリソースを追加する場合、LPAR の月額請求にはそのリソース変更と、時間単位の比例配分である LPAR 料金が反映されます。

### 月々の使用量の例
{: #pricing-monthly-usage-example}

以下の例では、購入する {{site.data.keyword.powerSys_notm}} インスタンスには 1 コア、8 GB メモリー、150 GB ディスクが含まれ、AIX 7200-03-02 を実行していて、基本料金は月額 $250.57 (時間単位 $0.343) です。月の途中で、さらにメモリーを追加します。LPAR の新しい料金は月額 $339.45 (時間単位 $0.465) となります。月ごとの請求は、デプロイされるリソースを時間で比例配分します。

| 1 カ月間に使用した時間       | 請求額   |  LPAR の説明     |
| ----------------------------- | ----------------- | --------------------  |
| 300 時間        | 300 時間 x $251/月 = $103  | 1 コア、8 GB メモリー、150 GB ディスク、AIX    |
| 430 時間        | 430 時間 x $339/月 = $200  | 1 コア、16 GB メモリー、150 GB ディスク、AIX  |
| 730 時間 (月合計)  | $103 + $200 = $303 (月合計)  |   1 コア、16 GB メモリー、150 GB ディスク、AIX |
{: caption="表 1. LPAR の月額請求の例" caption-side="top"}

この例では、LPAR リソースは月 300 時間、8 GB メモリーの使用後、16 GB メモリーに増やされています。LPAR の最終月額 ($303) は時間で比例配分されています。

## インスタンスの基本料金
{: #pricing-base-instance-prices}

インスタンスの基本請求額は、{{site.data.keyword.powerSys_notm}} の作成時に選択するマシン・タイプ、コア数、メモリー量などのオプションによって異なります。仮想サーバー・インスタンスを作成すると、関連する月額が表示されます。詳しくは、[{{site.data.keyword.powerSys_notm}} の作成](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)を参照してください。

## オペレーティング・システム
{: #pricing-operating-systems}

IBM によって提供されているストック・イメージを以下に示します。
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

独自のカスタム・イメージを {{site.data.keyword.powerSys_notm}} インスタンスで使用できますが、その場合でも IBM Cloud 用にオペレーティング・システム・ライセンスを購入する必要があります。{{site.data.keyword.powerSys_notm}} インスタンスの LPAR で既存の AIX ライセンスまたは IBM i ライセンスを使用することはできません。カスタム・イメージまたはストック・イメージを使用する場合にも、同じ価格が請求されます。詳しくは、[カスタム・イメージの構成](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)を参照してください。

## 請求の終了
{: #pricing-end-of-billing}

LPAR を削除すると、月ごとの請求サイクルが終了します。ワークロード要件に基づいてインフラストラクチャーをスケールアップまたはスケールダウンする場合、LPAR プロビジョン変更のタイミングに従って請求されます。LPAR を停止しても、請求処理は停止されません。請求サイクルを停止するには、LPAR を削除する必要があります。
