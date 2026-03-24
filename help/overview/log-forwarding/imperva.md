---
title: 로그 전달 - Imperva
description: LLM Optimizer의 에이전틱 트래픽 데이터 수집을 위해 Imperva에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법에 대해 알아봅니다.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: ht
source-wordcount: '352'
ht-degree: 100%

---


# 로그 전달: Imperva {#log-forwarding-imperva}

이 안내서에서는 에이전틱 트래픽 데이터 수집을 위해 Imperva에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법을 설명합니다. LLM Optimizer CDN 구성 페이지를 사용하여 LLM Optimizer에 온보딩합니다. 온보딩 프로세스가 완료되면 이 페이지에 제공된 단계를 따라 Imperva 웹 콘솔에서 로그 전달을 구성합니다.

## 1단계: LLM Optimizer에서 온보딩 {#step-1}

LLM Optimizer 페이지([https://llmo.now/](https://llmo.now/))로 이동합니다.

1. **구성**&#x200B;으로 이동합니다.

   ![구성 버튼](/help/overview/assets/log-forwarding/common/config-button.png)

1. **CDN 구성** 탭을 클릭합니다.

   ![CDN 구성 탭](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. **시작하기**&#x200B;를 클릭합니다.
1. **AI 트래픽 인사이트 활성화** 옆의 **구성**&#x200B;을 클릭합니다.

   ![구성](/help/overview/assets/log-forwarding/common/configure.png)
1. **Imperva(BYOCDN)**&#x200B;를 선택합니다.

   ![Imperva 선택](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. **온보딩**&#x200B;을 클릭합니다.

## 2단계: Imperva에서 로그 전달 구성 {#step-2}

[Imperva 콘솔](https://my.imperva.com)로 이동합니다.

>[!NOTE]
>
>로그는 매일 전달되어야 합니다.

1. [https://my.imperva.com](https://my.imperva.com)에서 Imperva 계정에 로그인합니다.

2. 사이드바에서 **로그** > **로그 설정**(또는 **로그 통합**)으로 이동합니다.

3. 연결 유형(로그 대상)으로 **Amazon S3 ARN**&#x200B;을 선택합니다.

4. 다음을 입력합니다.

   | 필드 | 설명 | 메모 |
   |---|---|---|
   | **연결 이름** | 연결에 대한 설명적인 이름입니다(예: 프로덕션 S3 로그). 기본 이름을 바꿀 수 있습니다. | |
   | **경로** | 로그 파일이 저장되는 폴더의 위치입니다. `<Amazon S3 bucket name>/<log folder>` 형식을 사용합니다. 예: `MyBucket/MyImpervaLogFolder`. | `Amazon S3 bucket name`은 LLM Optimizer 구성 페이지의 **버킷 이름**&#x200B;입니다. ![버킷 이름](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) 로그 폴더는 LLM Optimizer 구성 페이지의 **경로**&#x200B;입니다. ![경로](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. **연결 테스트**&#x200B;를 클릭합니다. Imperva는 테스트 파일(실제 데이터 없음)을 지정된 폴더로 전송한 후 전송이 완료되면 제거되는 전체 테스트를 실행합니다.

   - **사용 가능** — 스토리지 세부 정보가 유효합니다. 이 연결을 사용하도록 로그를 구성할 수 있습니다.
   - **정의되지 않음** — 필요한 세부 정보가 없거나 테스트가 실패했습니다.

6. 구성을 저장하려면 **저장**&#x200B;을 클릭합니다.

7. 로그 옵션(로그 유형, 로그 수준, 형식, 압축) 및 **로그 수준**&#x200B;을 구성합니다. LLM Optimizer 구성 페이지에서 값을 가져올 수 있습니다.

   | 필드 | 메모 |
   |---|---|
   | 로그 통합 모드 | ![로그 통합 모드](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | 게재 방법 | ![게재 방법](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | 로그 유형 | ![로그 유형](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | 로그 수준 | ![로그 수준](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | 형식 | ![형식](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | 로그 압축 | ![로그 압축](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
