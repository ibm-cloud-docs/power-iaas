---

copyright:
  years: 2019

lastupdated: "2019-07-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Power Systems Virtual Server용 IBM Cloud Direct Link Connect 주문
{: #ordering-direct-link-connect}

{{site.data.keyword.powerSys_notm}}에 사설 네트워크를 구성하는 한 가지 옵션은 Direct Link Connect 서비스를 사용하는 것입니다. Direct Connect Link 서비스는 {{site.data.keyword.powerSys_notm}} 인스턴스에서 {{site.data.keyword.cloud}} 리소스에 액세스할 수 있도록 하는 연결을 작성합니다. 또한 Direct Link Connect 서비스는 IBM Cloud VRA(Virtual Router Appliance)를 사용하여 온프레미스 네트워크를 IBM Cloud 네트워크에 연결하는 데 사용됩니다.
{:shortdesc}

{{site.data.keyword.cloud_notm}} UI 콘솔을 사용하여 Direct Link Connect 서비스를 주문할 수 있습니다. Direct Link Connect는 {{site.data.keyword.powerSys_notm}} 서비스와 별도의 서비스입니다. Direct Link Connect의 비용을 검토하려면 [IBM Cloud Direct Link의 가격](/docs/infrastructure/direct-link?topic=direct-link-pricing-for-direct-link-connect)을 참조하십시오.

IBM에서는 백업용으로 두 번째 Direct Link Connect 연결을 주문하도록 권장합니다.

## 시작하기 전에
{: #before-direct-link-connect}

* {{site.data.keyword.cloud}} 계정에 Direct Link Connect 서비스를 주문할 수 있는 올바른 권한이 있는지 확인하십시오.
* 다음 주제를 검토하여 Direct Link Connect 서비스에 대한 기본 네트워킹 개념을 이해하십시오.
    * [Direct Link Connect 개념](/docs/infrastructure/direct-link?topic=direct-link-direct-link-connect-solution#direct-link-connect-solution)
    * [Direct Link Connect 세부사항](/docs/infrastructure/direct-link?topic=direct-link-ibm-cloud-direct-link-connect-details)
    * [Direct Link Connect 제한사항](/docs/infrastructure/direct-link?topic=direct-link-known-limitations#ibm-cloud-direct-link-exchange-and-direct-link-connect-limitations)
    * [IP 지정에 대한 엄격한 제한사항](/docs/infrastructure/direct-link?topic=direct-link-configure-ibm-cloud-direct-link#strict-limitations-on-ip-assignments)

## Direct Link Connect 주문 단계
{: #steps-to-order-direct-link-connect}

{{site.data.keyword.powerSys_notm}} 인스턴스에 대한 연결을 작성하는 Direct Link Connect 서비스를 주문하려면 다음 단계를 완료하십시오.

1. IBM Cloud 계정 인증 정보를 사용하여 [IBM Cloud 카탈로그 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/catalog){: new_window}에 로그인하십시오. Direct Link Connect 서비스를 주문하려면 계정에 올바른 권한이 있어야 합니다.

2. **네트워킹** 섹션에서 **Direct Link Connect** 타일을 클릭하십시오.
![Direct Link 카탈로그 타일을 표시함](/images/directlink1.png "Direct Link 카탈로그 타일을 표시함")

1. Direct Link Connect 카탈로그 항목에서 **작성**을 클릭하십시오.

1. IBM Cloud Direct Link 페이지에서 **Direct Link Connect 주문**을 클릭하십시오.

1. IBM Cloud Direct Link Connect 연결 작성 페이지에서 다음 필드를 완료하십시오.

   Direct Link Connect 서비스를 작성하기 위해 다음 필드를 완료하면 가격이 선택사항을 반영하도록 자동으로 업데이트됩니다.
   {: note}

   <dl>
   <dt><strong>Direct Link 인스턴스 이름</strong><dt>
   <dd>Direct Link Connect의 용도를 설명하는 이름을 입력하십시오.</dd>
   <dt><strong>위치</strong><dt>
   <dd>{{site.data.keyword.powerSys_notm}} 인스턴스와 동일한 위치를 선택하십시오. 다음 표에는 {{site.data.keyword.powerSys_notm}} 인스턴스 위치와 해당 Direct Link Connection 옵션이 식별되어 있습니다.
   <table>
   <caption>표 1. Direct Link Connection 위치 옵션</caption>
   <tr>
   <th>Power Systems Virtual Server 위치</th>
   <th>Direct Link Connect 위치</th>
   </tr>
   <tr>
   <td>댈러스, 미국 텍사스주</td>
   <td>댈러스 4</td>
   </tr>
   <tr>
   <td>워싱턴 D.C, 미국</td>
   <td>워싱턴 2</td>
   </tr>
   </table>
   </dd>
   <dt><strong>네트워크 제공자</strong><dt>
   <dd>목록에서 <strong>MEGAPORT</strong>를 선택해야 합니다.</dd>
   <dt><strong>링크 속도</strong><dt>
   <dd>워크로드 요구사항에 맞는 링크 속도를 선택하십시오. 이 필드에 대해 권장되는 선택사항은 1000Mbps입니다.</dd>
   <dt><strong>라우팅 옵션</strong><dt>
   <dd><strong>위치</strong> 필드에 지정한 위치에서 연결된 모든 데이터 센터에 액세스하려면 <strong>로컬 라우팅(무료)</strong>을 선택하십시오. 전세계의 모든 IBM Cloud 데이터 센터에 액세스하려면 <strong>글로벌 라우팅</strong>을 선택하십시오. </dd>
   <dt><strong>BGP ASN</strong><dt>
   <dd>다음 표에 있는 특정 Direct Link Connect 위치에 대한 BGP ASN 번호를 입력해야 합니다.
   <table>
   <caption>표 2. 특정 위치에 대한 BGP ASN 번호</caption>
   <tr>
   <th>Direct Link Connect 위치</th>
   <th>BGP ASN 번호</th>
   </tr>
   <tr>
   <td>댈러스 4</td>
   <td>64997</td>
   </tr>
   <tr>
   <td>워싱턴 2</td>
   <td>64999</td>
   </tr>
   </table>
   </dd>
   <dt><strong>VRF 선택</strong><dt>
   <dd>연결에 대한 가상 라우팅 및 전달(VRF) 옵션을 선택하십시오. 계정에 식별된 VRF가 없는 경우 이 필드가 표시되지 않습니다. VRF를 선택하지 않고 Direct Link Connect 서비스를 작성할 수 있습니다. 다음 그림은 Direct Link Connect 필드의 예입니다.</dd>
   <dd>

   ![완료된 Direct Link Connect 필드를 표시함](/images/directlink2.png "완료된 Direct Link Connect 필드를 표시함")
   </dd>
   </dl>
2. **마스터 서비스 계약** 을 읽고 선택란을 선택하십시오. 중요한 기술 정보가 포함되어 있으므로 **마스터 서비스 계약**을 읽고 이해해야 합니다.

3. **작성**을 클릭하십시오. 요청이 성공적으로 제출되면 다음 메시지가 표시됩니다. ![Direct Link Connect가 메시지를 제출했음을 표시함](/images/directlink3.png "Direct Link Connect가 메시지를 제출했음을 표시함")

1. Direct Link Connect 서비스에 대한 **케이스 번호** 링크를 클릭하십시오. 케이스 번호의 정보는 {{site.data.keyword.powerSys_notm}} 인스턴스를 연결하기 위한 Direct Link Connect 정보를 식별하는 데 사용됩니다.

  IBM Cloud 지원에서 Direct Link Connect 연결을 작성하는 데는 최대 3일(영업일 기준)이 소요될 수 있습니다.
  {: note}

2. Direct Link Connect 서비스를 사용하여 {{site.data.keyword.powerSys_notm}} 인스턴스에 대한 연결을 작성하려면 {{site.data.keyword.powerSys_notm}} 지원 팀을 위해 [새 케이스](/docs/infrastructure/power-iaas?topic=power-iaas-getting-help-and-support)를 여십시오.

      1. 새 케이스의 설명 필드에 Direct Link Connect 케이스 번호를 추가하십시오.
      2. 시스템에서 자동으로 생성한 {site.data.keyword.powerSys_notm}} 케이스 IAM 서비스 ID를 복사하십시오.

3. {{site.data.keyword.powerSys_notm}} 케이스의 IAM 서비스 ID를 Direct Link Connect 케이스에 입력하십시오. Direct Link Connect 연결이 작성되면 Direct Link Connect 케이스 번호가 닫힙니다. 다음은 케이스에 표시되는 네트워크 정보의 예입니다.

  ```shell
  Link Speed:                  1000 Mbps
  Location:                    Washington 2
  Network Provider:            MEGAPORT
  IBM IP Address:              10.254.0.25/30
  Customer IP Address:         10.254.0.26/30
  Service Key:                 None
  BGP ASN:                     64999
  Network Identifier:          1748523-1
  Date Created:                2019-06-12T14:56:45-06:00
  ```
  {: screen}

1. Direct Link Connect 케이스 번호에서 이 정보를 사용하고 다음 네트워크 정보를 {{site.data.keyword.powerSys_notm}} 케이스에 입력하십시오.

  ```shell
  Customer name:
  Customer account ID:
  Direct Link Connect subnet:
  Power Systems Virtual Server network IP address:
  IBM Cloud IP address:
  Power Systems Virtual Server network ASN:
  IBM Cloud ASN:
  Private Network ID (1):
  Private Network ID (2):
  Private Network ID (3):
  ```
  {: codeblock}

1. Direct Link Connect 연결이 {{site.data.keyword.powerSys_notm}} 인스턴스와 통신하도록 구성되면 {{site.data.keyword.powerSys_notm}} 케이스가 닫힙니다.
