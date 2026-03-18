---
title: 로그 전달 - Cloudflare
description: LLM Optimizer의 에이전트 트래픽 데이터 수집을 위해 Cloudflare에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법을 알아봅니다.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 로그 전달: Cloudflare {#log-forwarding-cloudflare}

이 페이지에서는 에이전트 트래픽 데이터 수집을 위해 Cloudflare에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법에 대해 자세히 설명합니다. LLM Optimizer CDN 구성 페이지를 사용하여 LLM Optimizer에 온보딩합니다. 온보딩 프로세스가 완료되면 이 페이지에 제공된 단계에 따라 Cloudflare 대시보드 콘솔에서 로그 전달을 구성합니다.

## 1단계: LLM Optimizer에서 온보드 {#step-1}

LLM Optimizer 페이지 [https://llmo.now/](https://llmo.now/)에서:

1. **고객 구성 대시보드**(으)로 이동합니다.

   ![구성 버튼](/help/overview/assets/log-forwarding/common/config-button.png)

1. **CDN 구성** 탭을 클릭합니다.

   ![CDN 구성 탭](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. **시작하기**&#x200B;를 클릭합니다.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png) -->

1. **AI 트래픽 인사이트 활성화** 옆에 있는 **구성**&#x200B;을 클릭하세요.

   ![구성](/help/overview/assets/log-forwarding/common/configure.png)

1. **Cloudflare(BYOCDN)**&#x200B;을(를) 선택합니다.

   ![Cloudflare 선택](/help/overview/assets/log-forwarding/cloudflare/cloudflare-select.png)

1. **온보드**&#x200B;를 클릭합니다.

   <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## 2단계: Cloudflare에서 Logpush 작업 만들기 {#step-2}

[Cloudflare 대시보드](https://dash.cloudflare.com/login)에서 다음 단계를 수행합니다.

1. **도메인(영역)** 수준의 **Logpush** 페이지로 이동합니다.
1. **Logpush 작업 만들기**&#x200B;를 선택합니다.
1. **대상 선택**&#x200B;에서 **Amazon S3**&#x200B;을(를) 선택합니다.
1. 다음 대상 정보를 입력하십시오.

   - **버킷** — S3 버킷 이름. LLM Optimizer CDN 구성 페이지에서 값을 복사합니다.

     ![버킷 이름](/help/overview/assets/log-forwarding/common/bucket-name.png)

   - **경로** — 저장소 컨테이너 내의 버킷 위치입니다. LLM Optimizer CDN 구성 페이지에서 값을 복사합니다.

     ![Cloudflare 경로](/help/overview/assets/log-forwarding/cloudflare/cloudflare-path.png)

   - **로그를 매일 하위 폴더로 구성**(권장).

     ![매일 하위 폴더](/help/overview/assets/log-forwarding/cloudflare/cloudflare-daily-subfolders.png)

   - **버킷 영역** — LLM Optimizer CDN 구성 페이지에서 값을 복사합니다.

     <!-- ![Region](/help/overview/assets/log-forwarding/cloudflare/cloudflare-region.png)-->

   - 서버측 암호화가 필요하지 않은 경우 선택하지 않은 상태로 둡니다.

   위의 단계를 완료한 후 **계속**&#x200B;을 선택합니다.

1. 소유권을 증명하기 위해 Cloudflare는 지정된 대상에 파일을 전송합니다. 토큰을 찾으려면 소유권 문제 파일의 **개요** 탭에서 **열기** 단추를 클릭하십시오. LLM Optimizer CDN 구성 페이지에서 소유권 토큰을 복사한 다음 Cloudflare 대시보드에 붙여넣어 버킷에 대한 액세스를 확인합니다. 소유권 토큰을 입력하고 **계속**&#x200B;을 선택합니다.

   <!--![Ownership token](/help/overview/assets/log-forwarding/cloudflare/cloudflare-ownership-token.png)-->

1. 저장소 서비스로 푸시할 **HTTP 요청** 데이터 집합을 선택하십시오.

1. Logpush 작업을 구성합니다.

   - **작업 이름**&#x200B;을(를) 입력하십시오.

   - **다음 필드 보내기**&#x200B;에서 LLM Optimizer 구성 페이지의 값을 참조하십시오.

     ![Logpush 필드](/help/overview/assets/log-forwarding/cloudflare/cloudflare-logpush-fields.png)

   - **로그 형식**: JSON.

     <!--![JSON format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-json-format.png)-->

1. **고급 옵션**&#x200B;에서:

   - 로그에서 타임스탬프 필드의 형식을 선택하십시오. `RFC3339`.

     ![타임스탬프 형식](/help/overview/assets/log-forwarding/cloudflare/cloudflare-timestamp-format.png)

   - 샘플링 속도를 보려면 **모든 로그**&#x200B;를 선택하십시오.

     ![샘플링 속도](/help/overview/assets/log-forwarding/cloudflare/cloudflare-sampling-rate.png)

1. Logpush 작업 구성이 완료되면 **제출**&#x200B;을(를) 선택하십시오.
