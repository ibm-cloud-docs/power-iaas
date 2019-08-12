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

# 사설 네트워크로 Power Systems Virtual Servers 구성
{: #cpn-configuring}

{{site.data.keyword.powerSysFull}}에 사설 네트워크를 사용하여 온프레미스 환경을 오프프레미스 {{site.data.keyword.cloud_notm}} 환경과 안전하게 연결할 수 있습니다. 사설 네트워크에서 {{site.data.keyword.cloud_notm}} 리소스에 액세스하고 다른 가상 서버와 상호 연결할 수 있습니다.
{:shortdesc}

다음 옵션 중 하나를 사용하여 온프레미스 환경을 {{site.data.keyword.cloud_notm}} 환경과 연결하는 사설 네트워크를 작성할 수 있습니다.

1. **점프 서버를 사용하는 {{site.data.keyword.cloud_notm}} SSL VPN**
   * {{site.data.keyword.cloud_notm}} SSL VPN 서비스를 사용하여 기존 {{site.data.keyword.cloud_notm}} 네트워크에 연결할 수 있습니다. {{site.data.keyword.cloud_notm}} 네트워크 내부에서 {{site.data.keyword.cloud_notm}} 가상 머신(VM)을 점프 서버로 사용하여 {{site.data.keyword.powerSys_notm}} 인스턴스에 연결할 수 있습니다.
   * VPN 연결을 사용하여 {{site.data.keyword.powerSys_notm}} 인스턴스에 직접 연결할 수 없으므로 점프 서버를 사용해야 합니다.
   * 이 옵션은 일반적으로 환경을 관리하는 데 사용됩니다. 프로덕션 워크로드에는 이 옵션이 권장되지 않습니다.
   * 이 옵션을 구성하는 방법에 대한 자세한 정보는 [SSL VPN 설정](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ssl-vpn-connections) 및 [VRA(Virtual Router Appliance) 주문](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)을 참조하십시오.

2. **IBM Cloud VRA(Virtual Router Appliance)를 사용하는 {{site.data.keyword.cloud_notm}} IPSec VPN**
   * {{site.data.keyword.cloud_notm}} IPSec VPN 서비스를 사용하여 기존 {{site.data.keyword.cloud_notm}} 네트워크에 연결할 수 있습니다. {{site.data.keyword.cloud_notm}} 네트워크 내부에서 IBM Cloud VRA(Virtual Router Appliance)를 사용하여 {{site.data.keyword.powerSys_notm}} 인스턴스에 연결할 수 있습니다.
   * VPN 연결을 사용하여 {{site.data.keyword.powerSys_notm}} 인스턴스에 직접 연결할 수 없으므로 VRA를 사용해야 합니다.
   * 이 옵션은 일반적으로 환경을 관리하는 데 사용됩니다. 프로덕션 워크로드에는 이 옵션이 권장되지 않습니다.
   * 이 옵션을 구성하는 방법에 대한 자세한 정보는 [IPSec VPN 설정](/docs/infrastructure/iaas-vpn?topic=VPN-setup-ipsec-vpn) 및 [VRA(Virtual Router Appliance) 주문](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started#order-vra)을 참조하십시오.

3. **IBM Cloud VRA(Virtual Router Appliance)를 사용하는 Direct Link Connect**
   * IBM Cloud VRA(Virtual Router Appliance)를 사용하여 온프레미스 네트워크를 IBM Cloud 네트워크에 연결하는 IBM의 Direct Link Connect 서비스를 주문할 수 있습니다.

   * 이 옵션은 온프레미스와 IBM Cloud 네트워크 간에 고성능을 제공합니다.
   * Direct Link Connect를 주문하려면 [UI 콘솔에서 IBM Cloud Direct Link Connect 주문](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect) 주제의 단계를 완료하십시오.
   * Direct Link Connect 서비스에 사용할 수 없는 특정 IP 주소가 있습니다. 자세한 정보는 [IP 지정에 대한 엄격한 제한사항](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)을 참조하십시오.
