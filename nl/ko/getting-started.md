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

# Power Systems Virtual Servers 시작하기
{: #getting-started}


{{site.data.keyword.powerSysFull}}는 몇 분 안에 논리 파티션(LPAR)이라고도 하는 가상 서버를 배치하는 데 사용할 수 있는 IaaS(Infrastructure as a Service) 오퍼링입니다.
{:shortdesc}

특정 비즈니스 요구사항에 맞게 {{site.data.keyword.powerSys_notm}}를 빠르게 배치할 수 있습니다. {{site.data.keyword.powerSys_notm}}를 사용하여 워크로드 요구사항을 쉽게 제어할 수 있도록 하는 하이브리드 클라우드 환경을 작성할 수 있습니다.

{{site.data.keyword.powerSys_notm}}는 여러 지리적 위치에서 AIX 또는 IBM i 워크로드를 실행할 수 있습니다.

## 용어
{: #gs-terminology}

가상 서버를 작성하기 전에 {{site.data.keyword.powerSys_notm}} **서비스**와 {{site.data.keyword.powerSys_notm}} **인스턴스** 간 용어의 차이점을 이해해야 합니다. {{site.data.keyword.powerSys_notm}} **서비스**를 특정 지리적 위치의 모든 {{site.data.keyword.powerSys_notm}} **인스턴스**에 대한 컨테이너라고 생각하십시오. {{site.data.keyword.powerSys_notm}} **서비스**는 {{site.data.keyword.cloud}} UI의 **리소스 목록**에서 사용할 수 있습니다. 서비스에는 여러 {{site.data.keyword.powerSys_notm}} **인스턴스**가 포함될 수 있습니다.

예를 들어, 두 개의 {{site.data.keyword.powerSys_notm}} **서비스**(댈러스에 하나, 워싱턴 DC에 다른 하나)가 있을 수 있습니다. 각 서비스에는 여러 {{site.data.keyword.powerSys_notm}} **인스턴스**가 포함될 수 있습니다.

## 시작하기 전에
{: #gs-before-you-begin}

첫 번째 Power Systems Virtual Server 인스턴스를 작성하기 전에 다음 전제조건을 검토하십시오.

1. {: hide-dashboard} IBM Cloud 계정을 작성하십시오. IBM Cloud 계정을 작성하려면 [IBM Cloud에 가입 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/registration){: new_window}을 참조하십시오.

2. {{site.data.keyword.powerSys_notm}}에 안전하게 연결하는 데 사용할 수 있는 공개 및 개인 SSH 키를 작성하십시오. 공개 및 개인 SSH 키를 작성하려면 [SSH 키 추가 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/docs/infrastructure/ssh-keys?topic=ssh-keys-adding-an-ssh-key)를 참조하십시오.

3. (선택사항) AIX 또는 IBM i 운영 체제에 대한 사용자 정의 이미지를 사용하려면 IBM Cloud Object Storage를 작성하고 이미지를 업로드해야 합니다. 자세한 정보는 [사용자 정의 이미지 구성](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)을 참조하십시오.

4. (선택사항) 사설 네트워크를 사용하여 {{site.data.keyword.powerSys_notm}} 인스턴스에 연결하려면 Direct Link Connect 서비스를 주문해야 합니다. 자세한 정보는 [UI 콘솔에서 IBM Cloud Direct Link Connect 주문](/docs/infrastructure/power-iaas?topic=power-iaas-ordering-direct-link-connect)을 참조하십시오.

## 다음 단계
{: #gs-next-steps}

이제 IBM Cloud 계정과 개인 및 공개 SSH 키를 사용하여 [{{site.data.keyword.powerSys_notm}} 서비스를 작성](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)할 준비가 되었습니다.
