---

copyright:
  years: 2016, 2019
lastupdated: "2019-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:important: .important}
{:note: .note}

# {{site.data.keyword.powerSys_notm}} Activity Tracker 이벤트
{: #at_events}

보안 담당자, 감사자 또는 관리자는 Activity Tracker 서비스를 사용하여 사용자 및 애플리케이션이 {{site.data.keyword.cloud}}의 {{site.data.keyword.powerSys_notm}} 서비스와 상호작용하는 방법을 추적할 수 있습니다.
{: shortdesc}

{{site.data.keyword.at_full_notm}}는 {{site.data.keyword.cloud_notm}} 내 서비스의 상태를 변경하는, 사용자가 시작한 활동을 기록합니다. 이 서비스를 사용하여 비정상 활동 및 중요 조치를 조사하고 규정 감사 요구사항을 준수할 수 있습니다. 또한 발생하는 조치에 대한 경보를 받을 수 있습니다. 수집되는 이벤트는 CADF(Cloud Auditing Data Federation) 표준을 준수합니다. [자세히 보기](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## 이벤트 목록: 읽기
{: #at_actions_read}

다음 이벤트는 {{site.data.keyword.powerSys_notm}} 인스턴스를 읽는 데 사용됩니다.

|조치                        |설명                     |
|:---------------------------|:--------------------------------|
|pcloud.cloud-instance.read  |Power 클라우드 인스턴스 읽기     |


## 이벤트 목록: 이미지
{: #at_actions_images}

다음은 {{site.data.keyword.powerSys_notm}} 인스턴스의 이미지에 대해 작업하기 위한 이벤트입니다.

|조치                        |설명                     |
|:---------------------------|:--------------------------------|
|pcloud.image.read           |하나의 이미지 또는 모든 이미지 읽기 |
|pcloud.image.create         |새 이미지 작성                   |
|pcloud.image.update         |이미지 업데이트                  |
|pcloud.image.delete         |이미지 삭제                      |
|pcloud.image.capture        |이미지 내보내기                  |


## 이벤트 목록: 네트워크
{: #at_actions_networks}

다음은 {{site.data.keyword.powerSys_notm}} 인스턴스의 네트워크에 대해 작업하기 위한 이벤트입니다.

|조치                        |설명                           |
|:---------------------------|:--------------------------------------|
|pcloud.network.read         |하나의 네트워크 또는 모든 네트워크 읽기|
|pcloud.network.create       |새 네트워크(공용/사설) 작성            |
|pcloud.network.update       |네트워크 업데이트                      |
|pcloud.network.delete       |네트워크 삭제                          |
{: caption="표 3. 이벤트를 생성하는 조치" caption-side="top"}

## 이벤트 목록: {{site.data.keyword.powerSys_notm}}
{: #at_actions_virtual_servers}

다음은 {{site.data.keyword.powerSys_notm}} 인스턴스 내의 각 가상 서버에 대해 작업하기 위한 이벤트입니다.

|조치                           |설명                          |
|:------------------------------|:-------------------------------------|
|pcloud.pvm-instance.read       |Power 가상 서버 인스턴스 읽기                          |
|pcloud.pvm-instance.create     |Power 가상 서버 인스턴스 작성                          |
|pcloud.pvm-instance.update     |Power 가상 서버 인스턴스 업데이트                      |
|pcloud.pvm-instance.delete     |Power 가상 서버 인스턴스 삭제                          |
|pcloud.pvm-instance.start      |Power 가상 서버 인스턴스 시작                          |
|pcloud.pvm-instance.stop       |Power 가상 서버 인스턴스 중지                          |
|pcloud.pvm-instance.renew      |Power 가상 서버 인스턴스 다시 부팅                     |
|pcloud.pvm-instance.unknown    |Power 가상 서버 인스턴스에 대한 알 수 없는 조치        |
|pcloud.pvm-instance.monitor    |Power 가상 서버 인스턴스에 대한 콘솔 액세스            |
|pcloud.pvm-instance.capture    |Power 가상 서버 인스턴스를 이미지로 캡처               |

## 이벤트 목록: SSH 키
{: #at_actions_ssh_keys}

다음은 {{site.data.keyword.powerSys_notm}} 인스턴스의 계정 및 SSH 키에 대해 작업하기 위한 이벤트입니다.

|조치                      |설명                 |
|:-------------------------|:----------------------------|
|pcloud.tenant.read        |테넌트 정보 읽기             |
|pcloud.ssh-key.read       |하나 이상의 SSH 키 읽기      |
|pcloud.ssh-key.create     |SSH 키 작성                  |
|pcloud.ssh-key.update     |SSH 키 업데이트              |
|pcloud.ssh-key.delete     |SSH 키 삭제                  |

## 이벤트 목록: 데이터 볼륨
{: #at_actions_data_volumes}

다음은 {{site.data.keyword.powerSys_notm}} 인스턴스의 데이터 볼륨에 대해 작업하기 위한 이벤트입니다.

|조치                      |설명                 |
|:-------------------------|:----------------------------|
|pcloud.volume.read        |하나 이상의 볼륨 읽기        |
|pcloud.volume.create      |볼륨 작성                    |
|pcloud.volume.update      |볼륨 업데이트                |
|pcloud.volume.delete      |볼륨 삭제                    |
|pcloud.volume.configure   |볼륨 연결 또는 분리          |

## 이벤트 보기
{: #at_ui}

이벤트는 **댈러스** 위치에서 사용할 수 있습니다.

{{site.data.keyword.at_full_notm}}에는 위치당 하나의 인스턴스만 있을 수 있습니다. 이벤트를 보려면 `us-south` 위치에서 {{site.data.keyword.at_full_notm}} 서비스의 웹 UI에 액세스해야 합니다. [자세히 보기](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).
