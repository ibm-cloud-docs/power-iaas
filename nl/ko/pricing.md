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

# Power Systems Virtual Server on IBM Cloud의 가격
{: #pricing-virtual-server}

{{site.data.keyword.powerSysFull}}는 일부 지역에서 최대 15개의 코어와 320GB 메모리의 스케일 확장 논리 파티션(LPAR) 및 최대 143개의 코어와 8192GB 메모리의 엔터프라이즈 LPAR와 함께 제공됩니다. 이러한 옵션을 사용하면 {{site.data.keyword.powerSys_notm}}가 비즈니스의 모든 워크로드 요구사항을 충족할 수 있습니다. 월별 요금으로 청구됩니다.
{:shortdesc}

## 월별 사용량
{: #pricing-monthly-usage}

{{site.data.keyword.powerSys_notm}} 인스턴스에는 시간당 비례 배분된 월별 요금이 부과됩니다. 월 중에 LPAR에 리소스를 추가하면 LPAR의 월별 청구에 리소스 변경사항과 시간당 비례 배분된 LPAR 가격이 반영됩니다.

### 월별 사용량 예제
{: #pricing-monthly-usage-example}

다음 예에서는 8GB 메모리 및 150GB 디스크가 포함된 1개의 코어가 있으며 AIX 7200-03-02를 실행 중인 {{site.data.keyword.powerSys_notm}} 인스턴스를 월별 $250.57(시간당 $0.343)의 기본 가격으로 구매합니다. 해당 월이 진행되는 동안 메모리를 더 추가합니다. LPAR의 새 가격은 월별 $339.45(시간당 $0.465)입니다. 월별 청구는 배치된 리소스에 대해 시간별로 비례 배분됩니다.

| 1개월 내 경과 시간 | 청구액 | LPAR 설명 |
| ----------------------------- | ----------------- | --------------------  |
| 300시간 | 300시간 x $251/월 = $103 | 1개의 코어, 8GB 메모리, 150GB 디스크, AIX |
| 430시간 | 430시간 x $339/월 = $200 | 1개의 코어, 16GB 메모리, 150GB 디스크, AIX |
| 730시간(월별 총계) | $103 + $200 = $303(월별 총계) | 1개의 코어, 16GB 메모리, 150GB 디스크, AIX |
{: caption="표 1. 월별 LPAR 비용 예제" caption-side="top"}

이 예에서는 LPAR 리소스가 해당 월의 300시간 후에 8GB 메모리에서 16GB 메모리로 증가됩니다. LPAR의 가격은 LPAR의 최종 월별 가격($303)에 대해 시간별로 비례 배분됩니다.

## 기본 인스턴스 가격
{: #pricing-base-instance-prices}

기본 인스턴스 청구는 {{site.data.keyword.powerSys_notm}}를 작성할 때 선택하는 머신 유형, 코어 수 및 메모리 크기와 같은 옵션에 따라 다릅니다. 가상 서버 인스턴스를 작성할 때 연관된 월별 요금이 표시됩니다. 자세한 정보는 [{{site.data.keyword.powerSys_notm}} 작성](/docs/infrastructure/power-iaas?topic=power-iaas-creating-power-virtual-server#creating-power-virtual-server)을 참조하십시오.

## 운영 체제
{: #pricing-operating-systems}

다음은 IBM에서 제공하는 스톡 이미지입니다.
* AIX
  * 7200-03-02
  * 7100-05-03

* IBM i
  * 7.3 TR5
  * 7.2 TR9

고유한 사용자 정의 이미지를 가져와서 {{site.data.keyword.powerSys_notm}} 인스턴스에서 사용할 수 있지만 운영 체제 라이센스는 여전히 IBM Cloud용으로 구매됩니다. {{site.data.keyword.powerSys_notm}} 인스턴스의 LPAR에는 기존 AIX 또는 IBM i 라이센스를 사용할 수 없습니다. 사용자 정의 이미지 또는 스톡 이미지를 사용하는 경우 모두 동일한 가격이 청구됩니다. 자세한 정보는 [사용자 정의 이미지 구성](/docs/infrastructure/power-iaas?topic=power-iaas-configuring-custom-image#configuring-custom-image)을 참조하십시오.

## 청구 종료
{: #pricing-end-of-billing}

LPAR을 삭제하면 월별 청구 주기가 종료됩니다. 워크로드 요구사항에 따라 인프라를 확장 및 축소하는 경우 청구는 LPAR 프로비저닝 변경 시점에 따릅니다. LPAR을 중지해도 청구 프로세스는 중지되지 않습니다. 청구 주기를 중지하려면 LPAR을 삭제해야 합니다.
