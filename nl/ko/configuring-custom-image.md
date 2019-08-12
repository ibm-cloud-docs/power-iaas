---

copyright:
  years: 2019

lastupdated: "2019-7-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Power Systems Virtual Server가 포함된 사용자 정의 이미지 구성
{: #configuring-custom-image}

고유한 사용자 정의된 AIX 또는 IBM i 운영 체제 이미지를 가져와서 {{site.data.keyword.powerSysFull}}를 배치할 수 있습니다.
{:shortdesc}

온프레미스 시스템의 운영 체제 라이센스를 클라우드 환경에서 실행 중인 {{site.data.keyword.powerSys_notm}}로 전송할 수 없습니다. 라이센스 비용이 전체 시간별 청구 요금에 반영됩니다.
{: note}

## 시작하기 전에
{: #cci-before-you-begin}

사용자 정의 이미지를 부트 볼륨으로 사용하기 전에 다음 정보를 검토하십시오.

* AIX 또는 IBM i 운영 체제 기술 레벨이 **머신 유형** 필드에서 선택한 Power Systems 하드웨어에서 지원되는지 확인해야 합니다. 지원되는 AIX 및 IBM i 운영 체제 기술 레벨과 Power System 하드웨어 목록을 보려면 [시스템 소프트웨어 맵 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www-01.ibm.com/support/docview.wss?uid=ssm1maps)을 참조하십시오.
* **IBM Cloud Object Storage** 개념에 대한 기본적인 지식이 있어야 합니다. 자세한 정보는 [IBM Cloud Object Storage 정보](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage)를 참조하십시오.
* 기존 AIX 또는 IBM i 이미지가 없는 경우 IBM® PowerVC™를 사용하여 {{site.data.keyword.powerSys_notm}}에 사용할 이미지를 캡처하고 내보낼 수 있습니다. 자세한 정보는 [가상 머신 캡처 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_capturing_hmc.html){: new_window} 및 [이미지 내보내기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/en/SSXK2N_1.4.2/com.ibm.powervc.standard.help.doc/powervc_export_image_hmc.html){: new_window}를 참조하십시오.

## 사용자 정의 이미지를 오브젝트로 업로드
{: #cci-uploading}

1. IBM Cloud Storage 오브젝트를 작성하고 이미지를 업로드하십시오. 자세한 정보는 [데이터 업로드](/docs/services/cloud-object-storage?topic=cloud-object-storage-upload)를 참조하십시오.
2. 해시 기반 메시지 인증 코드(HMAC)를 사용하여 비밀 및 액세스 키를 생성하십시오. IBM Cloud Storage 오브젝트에 대한 서비스 인증 정보를 작성할 때 이러한 키를 생성할 수 있습니다. 서비스 인증 정보를 작성하려면 **Object Storage** 버킷에 대한 `Writer` 액세스 권한이 있어야 합니다. 자세한 정보는 [서비스 인증 정보](/docs/services/cloud-object-storage?topic=cloud-object-storage-service-credentials) 및 [버킷 권한](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-bucket-permissions)을 참조하십시오.
3. [IBM Cloud 카탈로그 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/catalog){: new_window}에서 Power Virtual Server 타일을 클릭하여 이미지를 추가하십시오. 가상 서버 인스턴스를 이미 작성한 경우 **메뉴 아이콘 ![메뉴 아이콘](../icons/icon_hamburger.svg "메뉴 아이콘") > 리소스 목록 > 디바이스**를 선택하고 기존 가상 서버를 선택하십시오.

 다음 필드를 완료하여 {{site.data.keyword.powerSys_notm}}를 작성하고 **사용자 정의 AIX 이미지** 또는 **사용자 정의 IBM i 이미지**를 클릭하십시오.

|필드 |설명 |
| ------| ------------|
|Cloud Object Storage 버킷 이름 |버킷 이름을 식별하려면 **메뉴 아이콘 ![메뉴 아이콘](../icons/icon_hamburger.svg "메뉴 아이콘") > 리소스 목록 > 스토리지 > Cloud Storage Object 이름 > 버킷**을 선택하십시오. |
|Cloud Object Storage 액세스 키 |액세스 키를 식별하려면 **메뉴 아이콘 ![메뉴 아이콘](../icons/icon_hamburger.svg "메뉴 아이콘") > 리소스 목록 > 스토리지 > Cloud Storage Object 이름 > 서비스 인증 정보 > 인증 정보 보기**를 선택하십시오. `access_key_id` 값을 복사하여 이 필드에 붙여넣으십시오. |
|Cloud Object Storage 비밀 키 |비밀 키를 식별하려면 **메뉴 아이콘 ![메뉴 아이콘](../icons/icon_hamburger.svg "메뉴 아이콘") > 리소스 목록 > 스토리지 > Cloud Storage Object 이름 > 서비스 인증 정보 > 인증 정보 보기**를 선택하십시오. `secret_access_key` 값을 복사하여 이 필드에 붙여넣으십시오. |
|이미지 경로 |이미지 파일의 완전한 경로를 입력하십시오. 완전한 경로는 `endpoint/bucket_name/file_name` 형식이어야 합니다. 사설 엔드포인트 도메인을 사용해야 합니다. 예를 들어, `s3.private.us-east.cloud-object-storage.appdomain.cloud/power-iaasprod-images-bucket/Aix_7200-03-02-1846_cldrdy_112018.gz`입니다. **메뉴 아이콘 ![메뉴 아이콘](../icons/icon_hamburger.svg "메뉴 아이콘") > 리소스 목록 > 스토리지 > Cloud Storage Object**를 선택하여 엔드포인트 도메인, 버킷 이름 및 파일 이름을 식별할 수 있습니다.
