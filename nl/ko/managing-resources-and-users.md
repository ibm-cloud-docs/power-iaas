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
{:tip: .tip}
{:download: .download}
{:note: .note}

# {{site.data.keyword.powerSys_notm}} 리소스 및 사용자 관리
{: #managing-resources-and-users}

{{site.data.keyword.powerSysFull}} 권한 및 리소스 관리 방법은 IBM Cloud Identity and Access Management(IAM) 서비스에 맞게 조정됩니다. IAM을 사용하면 사용자를 안전하게 인증하고 리소스 그룹을 통해 {{site.data.keyword.powerSys_notm}} 리소스에 대한 액세스를 제어하며 액세스 그룹을 통해 사용자 세트가 특정 리소스에 액세스하도록 허용할 수 있습니다. 즉, IAM은 {{site.data.keyword.cloud_notm}}의 모든 사용자 및 리소스 관리를 위한 원스톱 상점입니다.
{: shortdesc}

다음 기준에 따라 IAM 권한을 지정할 수 있습니다.

* 개별 사용자
* 액세스 그룹(사용자 그룹)
* 특정 유형의 리소스
* 리소스 그룹

IAM에 대한 자세한 정보는 다음 정보를 검토하십시오.

* [IAM 시작하기](https://cloud.ibm.com/docs/iam?topic=iam-getstarted#getstarted)
* [IAM 개념](https://cloud.ibm.com/docs/iam?topic=iam-iamoverview)
* [리소스 그룹 관리](https://cloud.ibm.com/docs/resources?topic=resources-rgs)
* [액세스 그룹 설정](https://cloud.ibm.com/docs/iam?topic=iam-groups)

## 플랫폼 액세스 역할
{: #platform-access-roles}

플랫폼 액세스 역할을 사용하여 사용자가 {{site.data.keyword.cloud_notm}} 리소스에 대한 태스크(예: 사용자 작성 또는 서비스 추가)를 완료하도록 할 수 있습니다.

다음 표에는 IAM 플랫폼 액세스 역할과 {{site.data.keyword.powerSys_notm}}에서 허용되는 해당 제어 유형이 표시되어 있습니다.

|플랫폼 액세스 역할 |허용되는 제어 유형 |
|-----------|-------------------------|
|뷰어 |인스턴스 보기 및 인스턴스 나열 |
|운영자 |인스턴스 보기 및 인스턴스 나열 |
|편집자 |인스턴스 보기, 인스턴스 나열, 인스턴스 작성 및 인스턴스 삭제 |
|관리자 |인스턴스 보기, 인스턴스 나열, 인스턴스 작성, 인스턴스 삭제 및 다른 사용자에게 정책 지정 |

## 서비스 액세스 역할
{: #service-access-roles}

서비스 액세스 역할을 사용하여 사용자가 {{site.data.keyword.powerSys_notm}} 서비스 기능에 대해 수행할 수 있는 작업을 정의할 수 있습니다.

다음 표에는 IAM 서비스 액세스 역할과 사용자가 {{site.data.keyword.powerSys_notm}}에 대해 완료할 수 있는 해당 조치가 표시되어 있습니다.

|서비스 액세스 역할 |조치에 대한 설명 |
|-----------|-------------------------|
|독자 |SSH 키, 스토리지 볼륨 및 네트워크 설정과 같은 모든 리소스를 볼 수 있습니다. 리소스를 변경할 수는 없습니다. |
|관리자 |모든 리소스를 구성할 수 있습니다. 다음은 수행할 수 있는 몇 가지 조치입니다.<ul><li>인스턴스 작성</li><li>스토리지 볼륨 크기 늘리기</li><li>SSH 키 작성</li><li>네트워크 설정 수정</li><li>부트 이미지 작성</li><li>스토리지 볼륨 삭제</li>
</ul>

## 사용자 액세스 시나리오
{: #user-access-scenarios}

다음 액세스 시나리오는 새 사용자를 추가하고 기존 사용자의 권한을 수정하는 데 필요한 단계를 다룹니다.

### {{site.data.keyword.powerSys_notm}} 리소스를 볼 수 있도록 새 사용자 초대
{: #inviting-a-new-user-to-create-or-manage-resources}

IBM Cloud 사용자를 계정에 초대하고 {{site.data.keyword.powerSys_notm}} 리소스를 볼 수 있는 액세스 권한을 부여해야 합니다. 서비스 액세스 역할에 따라 {{site.data.keyword.powerSys_notm}} 리소스에 대한 사용자의 액세스 레벨이 결정됩니다.

사용자가 {{site.data.keyword.powerSys_notm}} 리소스를 볼 수 있도록 하려면 IAM에서 다음 단계를 완료하십시오.

1. IBM Cloud 콘솔에서 [IAM 사용자 UI ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/iam/users){: new_window}로 이동하여 **사용자 초대**를 클릭하십시오.

      ![IAM UI의 사용자 초대 아이콘을 표시함](/images/invite_users.png "IAM UI에서 사용자 초대")

2. **사용자** 섹션의 **이메일 주소** 필드에 원하는 사용자 이메일 주소를 입력하십시오.
3. 다음으로 **다음 대상에 액세스 권한 지정** 필드에서 **리소스**를 선택하고 **서비스** 필드에서 **{{site.data.keyword.powerSys_notm}}**를 선택하십시오.

    ![서비스 필드를 표시함](/images/invite_users2.png "IAM UI에서 새 사용자에 대한 {{site.data.keyword.powerSys_notm}} 서비스 선택")

4. 사용자에게 지정할 플랫폼 액세스 역할을 선택하십시오. 이 시나리오에서는 사용자가 {{site.data.keyword.cloud_notm}} 및 {{site.data.keyword.powerSys_notm}} 리소스만 볼 수 있습니다.

    ![IAM 역할에 대한 UI를 표시함](/images/invite_users3.png "IAM UI에서 새 사용자의 역할 선택")

5. **사용자 초대**를 클릭하십시오. 사용자가 계정에 추가되려면 초대를 수락해야 합니다. 초대가 성공적으로 전송되면 메시지가 표시됩니다.

    ![성공적인 초대 메시지를 표시함](/images/invite_users4.png "성공적인 초대 메시지")

### 기존 사용자에게 {{site.data.keyword.powerSys_notm}} 리소스 관리 권한 부여
{: #giving-an-existing-user-permission-to-manage-resources}

계정의 기존 사용자에게 {{site.data.keyword.powerSys_notm}} 리소스를 구성할 수 있는 권한을 제공하려면 다음 단계를 완료하십시오.

1. IBM Cloud 콘솔에서 [IAM 사용자 UI ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/iam/users){: new_window}로 이동하십시오.
2. 사용자 목록에서 권한을 변경할 사용자를 선택하십시오.
3. **액세스 정책**을 클릭하고 사용자의 현재 역할을 클릭하십시오. 이 시나리오에서는 **뷰어, 독자**를 클릭하십시오.

    ![기존 사용자의 권한을 변경하는 방법을 표시함](/images/existing_user1.png "IAM UI에서 사용자의 권한 변경")

4. **역할 선택** 필드에서 **관리자**를 클릭하십시오. **독자** 역할을 선택된 상태로 둘 수 있습니다.

    ![기존 사용자의 관리자 역할 추가를 표시함](/images/existing_user2.png "IAM UI에서 관리자 역할 선택")

5. **저장**을 클릭하십시오.

   이제 사용자에게 {{site.data.keyword.powerSys_notm}} 리소스를 구성할 수 있는 권한이 부여되었습니다. 그러나 이 사용자는 {{site.data.keyword.cloud_notm}} 플랫폼에 특정한 서비스 및 리소스를 관리할 수 없습니다. 예를 들어, 새 사용자를 추가할 수 없습니다.
   {: note}
