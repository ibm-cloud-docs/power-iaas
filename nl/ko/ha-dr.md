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

# Power Systems Virtual Servers의 고가용성 및 재해 복구 옵션
{: #ha-dr}

하드웨어 장애가 발생하면 {{site.data.keyword.powerSys_notm}} 인스턴스가 다른 호스트 시스템에서 가상 서버를 다시 시작합니다. 이 프로세스는 {{site.data.keyword.powerSys_notm}} 서비스에 대한 기본 고가용성(HA) 기능을 제공합니다.
{:shortdesc}

고급 HA 또는 재해 복구(DR) 솔루션을 원하는 경우 {{site.data.keyword.powerSys_notm}} 환경에 다음 애플리케이션을 배치할 수 있습니다.

## PowerHA SystemMirror for AIX Standard Edition
{: #ha-dr-ha-standard}

PowerHA SystemMirror for AIX Standard Edition을 구매하면 월별 구독 모델을 사용할 수 있습니다. 자세한 정보는 [Standard Edition 월별 가격 옵션 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/8/897/ENUS219-288/index.html)을 참조하십시오.

소프트웨어를 구매한 후 [IBM ESS(Entitled Systems Support) ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/eserver/ess)에서 다운로드할 수 있습니다. {{site.data.keyword.powerSys_notm}} 환경에서 실행 중인 가상 서버에 PowerHA SystemMirror for AIX를 설치할 수 있습니다. 설치 지시사항은 [PowerHA SystemMirror 설치 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/install/ha_install.html)를 참조하십시오.

{{site.data.keyword.powerSys_notm}} 환경에서 PowerHA SystemMirror for AIX를 구현하는 경우 다음 정보를 검토하십시오.

* PowerHA SystemMirror 클러스터의 일부인 가상 서버를 작성 중인 경우 **코로케이션 규칙** 필드에서 **다른 서버**를 선택해야 합니다. ![코로케이션 규칙 필드를 표시함](/images/hadr2.png "코로케이션 규칙 필드를 표시함")

* PowerHA SystemMirror 클러스터의 일부인 가상 서버에 대한 스토리지 볼륨(디스크)을 작성 중인 경우 **공유 가능** 필드에서 **설정**을 선택해야 합니다.
![공유 가능 규칙 필드를 표시함](/images/hadr1.png "공유 가능 필드를 표시함")

* {{site.data.keyword.powerSys_notm}} 서비스를 사용하여 HMC, VIOS 및 호스트 시스템에 액세스할 수 없습니다. 따라서 이러한 기능에 액세스해야 하는 모든 PowerHA SystemMirror 기능(예: ROHA(Resource Optimized High Availability) 및 ANHP(Active Node Halt Policy))을 사용할 수 없습니다. 

<!--* When you deploy PowerHA SystemMirror, you must verify that the Service IP address is defined as a private IP address. This Service IP address can be accessed by another {{site.data.keyword.powerSys_notm}} instance or from other {{site.data.keyword.cloud}} applications. You cannot use a public IP address because it cannot be moved from one interface to another interface within a virtual server or across different virtual servers. -->

<!--When you deploy PowerHA SystemMirror for AIX Enterprise Edition clusters in the {{site.data.keyword.powerSys_notm}} environment, you can only use the Geographic Logical Volume Manager (GLVM) functions. You cannot use storage mirroring functions that are part of PowerHA SystemMirror for AIX Enterprise Edition because you do not have access to the subsystem storage in the {{site.data.keyword.powerSys_notm}} environment. For more information, see [Geographic Logical Volume Manager ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSPHQG_7.2/glvm/ha_glvm_kick.html).
{:note}
[Enterprise Edition monthly pricing options ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS219-286) -->

## 백업 및 복원을 통한 비즈니스 연속성
{: #ha-dr-ha-business}

{{site.data.keyword.powerSys_notm}} 구성 및 데이터는 {{site.data.keyword.cloud}}에서 백업되지 않습니다.

{{site.data.keyword.cloud_notm}} UI를 사용하여 가상 서버를 {{site.data.keyword.cloud_notm}} Object Storage에 백업할 수 있습니다. 심각한 장애가 발생한 경우 이 프로세스를 사용하여 가상 서버를 복원할 수 있습니다. 자세한 정보는 [Cloud Object Storage ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/cloud-object-storage?topic=cloud-object-storage-getting-started)를 참조하십시오.
