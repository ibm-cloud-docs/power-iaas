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

# Power Systems Virtual Servers 정보
{: #about-power-virtual-server}

{{site.data.keyword.powerSysFull}}는 기존 IBM Cloud 플랫폼을 사용하여 PowerVM 하이퍼바이저가 있는 IBM Power Systems 하드웨어에서 실행되는 Power Systems 가상 서버(논리 파티션(LPAR)이라고도 함)를 작성합니다.
{:shortdesc}

{{site.data.keyword.powerSys_notm}}는 IaaS(Infrastructure as a Service)의 한 유형입니다. {{site.data.keyword.powerSys_notm}} 서비스를 사용하면 퍼블릭 클라우드에서 AIX 또는 IBM i 운영 체제를 실행 중인 하나 이상의 가상 서버를 빠르게 작성하고 배치할 수 있습니다. 클라우드에서 가상 서버를 프로비저닝한 후 AIX 또는 IBM i 운영 체제가 안전한지 확인하는 것은 사용자의 책임입니다.

## 주요 기능
{: #apvs-key-features}

다음은 {{site.data.keyword.powerSys_notm}}의 몇 가지 주요 기능입니다.

### 간단한 청구
{: #apvs-billing}

{{site.data.keyword.powerSys_notm}}는 AIX 및 IBM i 운영 체제에 대한 라이센스를 포함하는 월별 청구 요금을 사용합니다. 월별 청구 요금은 해당 월 동안 {{site.data.keyword.powerSys_notm}} 인스턴스에 배치된 리소스를 기반으로 시간별로 비례 배분됩니다. {{site.data.keyword.powerSys_notm}} 인스턴스를 작성할 때 지정한 옵션에 따라 구성의 총 비용을 볼 수 있습니다. 비즈니스 요구사항에 맞는 최상의 가격을 제공하는 구성 옵션을 빠르게 식별할 수 있습니다. 자세한 정보는 [가격](/docs/infrastructure/power-iaas?topic=power-iaas-pricing-virtual-server#pricing-virtual-server)을 참조하십시오.

### 하이브리드 클라우드 환경
{: #apvs-hybrid}

{{site.data.keyword.powerSys_notm}}를 사용하여 기존 Power Systems 하드웨어 인프라에서 오프프레미스로 AIX 또는 IBM i 워크로드를 실행할 수 있습니다. 퍼블릭 클라우드에서 워크로드를 실행하면 셀프 서비스, 빠른 제공, 탄력성 및 다른 IBM Cloud 서비스에 대한 연결과 같은 클라우드가 제공하는 모든 이점을 누릴 수 있습니다. AIX 및 IBM i 워크로드가 클라우드에서 실행 중이지만 Power Systems 하드웨어가 제공하는 동일한 확장 가능하고 복원력이 있으며 프로덕션에 사용 가능한 기능을 계속 유지합니다.

### 인프라 사용자 정의
{: #apvs-customization}

{{site.data.keyword.powerSys_notm}}를 작성할 때 다음 옵션을 구성하고 사용자 정의할 수 있습니다.
* 가상 서버 인스턴스 수
* 코어 수
* 메모리 크기
* 데이터 볼륨 크기 및 유형(HDD 또는 SSD)
* 사설 또는 공용 네트워크

### BYOI(Bring Your Own Image)
{: #apvs-own-image}

{{site.data.keyword.powerSys_notm}}를 작성할 때 IBM에서 AIX 및 IBM i 운영 체제의 스톡 이미지를 제공합니다. 그러나 이전에 배치하고 테스트한 고유한 사용자 정의 AIX 또는 IBM i 운영 체제 이미지를 가져올 수 있습니다. 자세한 정보는 [사용자 정의 이미지 구성](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)을 참조하십시오.

## 하드웨어 스펙
{: #apvs-hardware-specifications}

다음 IBM Power Systems 하드웨어가 {{site.data.keyword.powerSys_notm}}를 호스팅합니다.

* 컴퓨팅
  * [Power System E880(9119-MHE) ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/POWER8/p8hdx/9119_mhe_landing.htm){: new_window}
    * 9TB 메모리
    * 8 x 16기가비트 PCI Express 듀얼 포트 파이버 채널(FC)
    * 10 x 10기가비트 이더넷 SR PCI Express 듀얼 포트
  * [Power System S922(9009-22A) ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/POWER9/p9hdx/9009_22a_landing.htm){: new_window}
    * 384GB 메모리
    * 2 x 16기가비트 PCI Express 듀얼 포트 FC
    * 3 x 10기가비트 이더넷 SR PCI Express 듀얼 포트

* 스토리지
  * Storewize V7000F(2076-AF6) 듀얼 컨트롤러
  * Storwize V7000(2076-624) 듀얼 컨트롤러

* 네트워크
  * Cisco Nexus9000 93180YC-EX(10G)
  * Cisco Nexus9000 C9348GC-FXP(1G)

## 공용 및 사설 네트워크
{: #apvs-public-and-private}

{{site.data.keyword.powerSys_notm}}를 작성할 때 사설 네트워크 인터페이스 또는 공용 네트워크 인터페이스를 선택할 수 있습니다.

* 공용 네트워크
  * {{site.data.keyword.powerSys_notm}} 인스턴스에 연결하는 쉽고 빠른 방법입니다.
  * IBM은 인터넷에서 {{site.data.keyword.powerSys_notm}} 인스턴스로의 보안 공용 네트워크 연결을 사용하도록 네트워크 인프라를 구성합니다.
  * 연결은 IBM Cloud VRA(Virtual Router Appliance) 및 Direct Link Connect 연결을 사용하여 구현됩니다.
  * 방화벽으로 보호되며 다음과 같은 보안 네트워크 프로토콜을 지원합니다.
    * SSH
    * HTTPS
    * Ping
    * SSL을 사용하는 IBM i 5250 터미널 에뮬레이션(포트 992)

* 사설 네트워크
  * {{site.data.keyword.powerSys_notm}} 인스턴스의 리소스가 Bare Metal Server, Kubernetes 컨테이너 또는 클라우드 스토리지와 같은 기존 {{site.data.keyword.cloud_notm}} 리소스에 액세스할 수 있도록 합니다.
  * Direct Link Connect 연결을 사용하여 IBM Cloud 계정 네트워크 및 리소스에 연결합니다. IBM Cloud 지원에서 링크를 구성해야 하므로 Direct Link Connect 연결을 작성하는 프로세스에는 며칠이 걸릴 수 있습니다.
  * 여러 {{site.data.keyword.powerSys_notm}} 인스턴스 간의 통신에 필요합니다.

    사설 네트워크를 구성하는 여러 옵션에 대한 자세한 정보는 [사설 네트워크 구성](/docs/infrastructure/power-iaas?topic=power-iaas-cpn-configuring#cpn-configuring)을 참조하십시오.
    {: note}

다음 그림은 공용 및 사설 네트워크에 대한 기본 구성을 표시합니다.

![공용 또는 사설 연결을 위한 네트워크 트래픽 플로우를 표시함](/images/power-iaas-network1.svg "공용 또는 사설 연결을 위한 네트워크 트래픽 플로우를 표시함")

<!-- Customer A is able to connect to a public network by using a Direct Link Dedicated connection with their {{site.data.keyword.cloud_notm}} Power account. -->
<!-- Customer A is able to connect to a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account. -->
<!-- Customer A can use either a public or private network to access their {{site.data.keyword.powerSys_notm}}. -->
<!-- Customer B is able to connect to only a private network by using a Direct Link Connect connection with their {{site.data.keyword.cloud_notm}} account.  -->
