---

copyright:
  years: 2019

lastupdated: "2019-07-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# プライベート・ネットワークを使用した Power Systems Virtual Server の構成
{: #cpn-configuring}

{{site.data.keyword.powerSysFull}} でプライベート・ネットワークを使用して、オンプレミス環境をオフプレミスの {{site.data.keyword.cloud_notm}} 環境に安全に接続できます。プライベート・ネットワークでは、{{site.data.keyword.cloud_notm}} リソースにアクセスしたり、他の仮想サーバーと相互接続したりできます。
{:shortdesc}

以下のいずれかのオプションを使用して、オンプレミス環境を {{site.data.keyword.cloud_notm}} 環境に接続するプライベート・ネットワークを作成できます。

1. **ジャンプ・サーバーを使用する {{site.data.keyword.cloud_notm}} SSL VPN**
   * {{site.data.keyword.cloud_notm}} SSL VPN サービスを使用して、既存の {{site.data.keyword.cloud_notm}} ネットワークに接続できます。{{site.data.keyword.cloud_notm}} ネットワーク内で、{{site.data.keyword.cloud_notm}} 仮想マシン (VM) をジャンプ・サーバーとして使用して、{{site.data.keyword.powerSys_notm}} インスタンスに接続できます。
   * VPN 接続を使用して {{site.data.keyword.powerSys_notm}} インスタンスに直接接続することはできないため、ジャンプ・サーバーを使用する必要があります。
   * このオプションは通常、環境を管理するために使用されます。このオプションは、実動ワークロードでは推奨されません。
   * このオプションの構成方法について詳しくは、[SSL VPN のセットアップ](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections)および [Virtual Router Appliance の注文](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)を参照してください。

2. **IBM Cloud Virtual Router Appliance を使用する {{site.data.keyword.cloud_notm}} IPSec VPN**
   * {{site.data.keyword.cloud_notm}} IPSec VPN サービスを使用して、既存の {{site.data.keyword.cloud_notm}} ネットワークに接続できます。{{site.data.keyword.cloud_notm}} ネットワーク内で、IBM Cloud Virtual Router Appliance (VRA) を使用して、{{site.data.keyword.powerSys_notm}} インスタンスに接続できます。
   * VPN 接続を使用して {{site.data.keyword.powerSys_notm}} インスタンスに直接接続することはできないため、VRA を使用する必要があります。
   * このオプションは通常、環境を管理するために使用されます。このオプションは、実動ワークロードでは推奨されません。
   * このオプションの構成方法について詳しくは、[IPSec VPN のセットアップ](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn)および [Virtual Router Appliance の注文](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)を参照してください。

3. **IBM Cloud Virtual Router Appliance を使用する Direct Link Connect**
   * IBM Cloud Virtual Router Appliance (VRA) を使用して、オンプレミス・ネットワークを IBM Cloud ネットワークに接続する IBM から Direct Link Connect サービスを注文できます。
   * このオプションは、オンプレミス・ネットワークと IBM Cloud ネットワークの間のハイパフォーマンスを提供します。
   * Direct Link Connect を注文するには、[UI コンソールからの IBM Cloud Direct Link Connect の注文](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect)トピックの手順を実行します。
   * Direct Link Connect サービスでは使用できない特定の IP アドレスがあります。詳しくは、[
IP 割り当てに対する厳密な制限](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)を参照してください。

