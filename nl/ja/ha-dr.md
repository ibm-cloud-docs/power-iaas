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
{:important: .important}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server の高可用性と災害復旧のオプション
{: #ha-dr}

{{site.data.keyword.powerSys_notm}} インスタンスでは、ハードウェア障害が生じると、別のホスト・システム上にある仮想サーバーを再始動します。このプロセスによって、{{site.data.keyword.powerSys_notm}} サービスの基本的な高可用性 (HA) 機能が提供されます。
{:shortdesc}

より高度な HA ソリューションまたは災害復旧 (DR) ソリューションが必要な場合には、ご使用の {{site.data.keyword.powerSys_notm}} 環境で以下のアプリケーションをデプロイできます。

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

PowerHA SystemMirror for AIX Standard Edition の購入には、月ごとのサブスクリプション・モデルを利用できます。詳しくは、[Standard Edition の月ごとの価格オプション ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html)を参照してください。

ソフトウェアを購入したら、[IBM Entitled Systems Support (ESS) ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/eserver/ess) からダウンロードできます。PowerHA SystemMirror for AIX は、{{site.data.keyword.powerSys_notm}} 環境で実行されている仮想サーバー上にインストールできます。インストールの手順については、[PowerHA SystemMirror のインストール![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html)を参照してください。

ご使用の {{site.data.keyword.powerSys_notm}} 環境に PowerHA SystemMirror for AIX を実装する方法については、以下の情報をご確認ください。

* PowerHA SystemMirror クラスターの一部として仮想サーバーを作成する場合、**「コロケーション・ルール (Colocation Rules)」**フィールドで**「異なるサーバー (Different Server)」**を選択する必要があります。
![「コロケーション・ルール (colocation rules)」フィールドの表示](/images/hadr2.png "「コロケーション・ルール (colocation rules)」フィールドの表示")

* PowerHA SystemMirror クラスターの一部である仮想サーバー用のストレージ・ボリューム (ディスク) を作成する場合、**「共有可能 (Shareable)」**フィールドで**「有効 (On)」**を選択する必要があります。
![「共有可能ルール (shareable rules)」フィールドの表示](/images/hadr1.png "「共有可能 (shareable)」フィールドの表示")

* {{site.data.keyword.powerSys_notm}} サービスを使用する場合、HMC、VIOS、ホスト・システムへのアクセス権がありません。そのため、リソース最適化高可用性 (ROHA) やアクティブ・ノード停止ポリシー (ANHP) といった、それらの機能へのアクセスが必要な PowerHA SystemMirror 機能は使用できません。

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## バックアップとリストアによる事業継続性
{: #ha-dr-ha-business}

ご使用の {{site.data.keyword.powerSys_notm}} 構成とデータは、{{site.data.keyword.cloud}} ではバックアップされません。

{{site.data.keyword.cloud_notm}} UI を使用して、仮想サーバーを {{site.data.keyword.cloud_notm}} Object Storage にバックアップできます。このプロセスを使用すると、重大な障害が発生した場合に仮想サーバーをリストアできます。詳しくは、[Cloud Object Storage ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started) を参照してください。
