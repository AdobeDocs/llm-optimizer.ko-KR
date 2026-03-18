---
title: 로그 전달 - Akamai
description: CDN 로그를 Akamai에서 Adobe의 에이전트 트래픽 데이터 수집을 위해 LLM Optimizer의 S3 버킷으로 전달하는 방법에 대해 알아봅니다.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# 로그 전달: Akamai {#log-forwarding-akamai}

이 페이지에서는 에이전트 트래픽 데이터 수집을 위해 CDN 로그를 Akamai에서 Adobe의 S3 버킷으로 전달하는 방법을 설명합니다. LLM Optimizer CDN 구성 페이지를 사용하여 LLM Optimizer에 온보딩합니다. 온보딩 프로세스가 완료되면 이 페이지에 제공된 단계에 따라 Akamai Campaign 컨트롤 패널에서 로그 전달을 구성합니다.

## 1단계: LLM Optimizer에서 온보드 {#step-1}

LLM Optimizer 페이지 [https://llmo.now/](https://llmo.now/)에서:

1. **고객 구성 대시보드**(으)로 이동합니다.

   ![구성 버튼](/help/overview/assets/log-forwarding/common/config-button.png)

1. **CDN 구성** 탭을 클릭합니다.

   ![CDN 구성 탭](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. **시작하기**&#x200B;를 클릭합니다.

   <!--![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. **AI 트래픽 인사이트 활성화** 옆에 있는 **구성**&#x200B;을 클릭하세요.

   ![구성](/help/overview/assets/log-forwarding/common/configure.png)

1. **Akamai(BYOCDN)**&#x200B;을(를) 선택합니다.

   ![Akamai 선택](/help/overview/assets/log-forwarding/akamai/akamai-select.png)

1. **온보드**&#x200B;를 클릭합니다.

   <!--![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## 2단계: Akamai에서 스트림 만들기 {#step-2}

Akamai 컨트롤 패널 [https://control.akamai.com/](https://control.akamai.com/)에서 공식 Akamai 설명서에서 [스트림 만들기](https://techdocs.akamai.com/datastream2/docs/create-stream)의 단계를 따릅니다.

## 3단계: 데이터 매개 변수 선택 {#step-3}

스트림을 만든 후 Akamai 제어판에서 [다음]을 클릭하여 **데이터 집합** 탭으로 계속합니다. 공식 Akamai 설명서의 단계에 따라 [데이터 매개 변수](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters)를 선택하십시오. LLM Optimizer 구성의 다음 필드가 필요합니다.

![LLMO 구성 필드](/help/overview/assets/log-forwarding/akamai/akamai-llmo-config-fields.png)

매핑은 다음과 같아야 합니다.

* **로그 정보**
reqTimeSec -> 요청 시간
* **지역 데이터**
국가 -> 국가/지역
* **메시지 교환 데이터**
reqHost -> 요청 호스트
reqPath -> 요청 경로
queryStr -> 쿼리 문자열
reqMethod -> Request 메서드
ua -> 사용자 에이전트
statusCode -> HTTP 상태 코드
rspContentType -> Response Content-Type
* **요청 헤더 데이터**
referer -> Referer
* **네트워크 성능 데이터**
timeToFirstByte -> 첫 번째 바이트까지의 시간

Akamai 데이터 세트 필드(ID 포함)는 다음과 같습니다.

1100, # reqTimeSec -> 요청 시간
2012년, # 국가 -> 국가/지역
1011, # reqHost -> 요청 호스트
1013, # reqPath -> 요청 경로
2009, # queryStr -> 쿼리 문자열
1012, # reqMethod -> 요청 메서드
1017, # ua -> 사용자 에이전트
1008, # statusCode -> HTTP 상태 코드
1032, # referer -> Referer
1016, # rspContentType -> 응답 Content-Type
2025 # timeToFirstByte -> 첫 번째 바이트까지의 시간

## 4단계: 대상 구성 {#step-4}

데이터 스트림을 만들고 매개 변수를 선택한 후 대상을 구성해야 합니다. 대상을 구성하려면 다음 단계를 수행합니다.

1. **대상**&#x200B;에서 **S3**&#x200B;을(를) 선택하십시오.
2. **이름**&#x200B;에서 사람이 인식할 수 있는 대상 설명을 입력하십시오.
3. **버킷**&#x200B;의 LLM Optimizer 구성 페이지에서 **버킷 이름**&#x200B;을 복사합니다.

   ![버킷 이름](/help/overview/assets/log-forwarding/common/bucket-name.png)

4. **폴더 경로**&#x200B;의 LLM Optimizer 구성 페이지에서 **경로**&#x200B;을(를) 복사합니다.

   ![경로 구성](/help/overview/assets/log-forwarding/akamai/akamai-path-config.png)

5. **Region**&#x200B;의 LLM Optimizer 구성 페이지에서 **Region**&#x200B;을 복사합니다.

   <!--![Region](/help/overview/assets/log-forwarding/common/region.png)-->

6. **액세스 키 ID** 및 **비밀 액세스 키**&#x200B;에서 LLM Optimizer 구성 페이지에서 두 값을 모두 복사합니다.

   ![액세스 키](/help/overview/assets/log-forwarding/common/access-keys.png)

7. **확인 및 저장**&#x200B;을 클릭하여 대상에 대한 연결을 확인하고 제공한 세부 정보를 저장합니다. 이 유효성 검사 프로세스의 일부로 시스템은 제공된 액세스 키 식별자 및 비밀 액세스 키를 사용하여 S3 폴더에 확인 파일을 만들고, 파일 이름에 `Akamai_access_verification_[TimeStamp].txt` 형식의 타임스탬프를 사용합니다. 유효성 검사 프로세스가 성공하고 로그를 보내려는 Amazon S3 버킷 및 폴더에 액세스할 수 있는 경우에만 이 파일을 볼 수 있습니다.

8. **배달 옵션** 메뉴에서 **파일 이름** 필드를 다음과 같이 편집합니다.

   a. **접두사**&#x200B;을(를) 변경합니다. **로그 파일 접두사** 아래의 LLM Optimizer 구성 페이지에서 값을 복사합니다.

   ```
   {%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000
   ```

   b. **접미사**&#x200B;를 변경합니다. **로그 파일 접미사** 아래의 LLM Optimizer 구성 페이지에서 값을 복사합니다.

9. **푸시 빈도**&#x200B;를 변경합니다. **로그 간격** 아래의 LLM Optimizer 구성 페이지에서 값을 복사합니다.

   ![로그 간격](/help/overview/assets/log-forwarding/akamai/akamai-log-interval.png)

10. **다음**&#x200B;을 클릭하여 프로세스를 완료합니다.

최종 유효성 검사 전에 구성은 다음 예제와 유사해야 합니다.

![구성 유효성 검사](/help/overview/assets/log-forwarding/akamai/akamai-validation.png)
