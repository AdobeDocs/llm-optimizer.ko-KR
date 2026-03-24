---
title: 로그 전달 - 기타(수동 업로드)
description: 지원되지 않는 CDN 공급자를 사용할 때 LLM Optimizer에서 에이전틱 트래픽 데이터를 수집하기 위해 Adobe의 S3 버킷에 CDN 로그를 수동으로 업로드하는 방법에 대해 알아봅니다.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: ht
source-wordcount: '670'
ht-degree: 100%

---


# 로그 전달: 기타(수동 업로드) {#log-forwarding-other}

**기타 BYOCDN** 프로비저닝 방법은 다음과 같은 경우 LLM Optimizer에 CDN 로그를 제공하려는 고객을 위한 포괄적인 옵션입니다.

- **수동 업로드**&#x200B;를 사용하는 것이 좋습니다. 예를 들어 운영 팀이 로그를 내보내고 정기적으로 업로드합니다.
- 일회성 스크립트, 예약된 내보내기, 서버리스 작업 등 **자동화된 애드혹 프로세스**&#x200B;가 사용됩니다.
- 고객은 기본 제공 로그 전달 통합에서 **기본적으로 지원되지 않는 CDN**&#x200B;을 사용합니다.

이 방법은 “연속 전달” 모델을 모방합니다. 로그가 생성되어 예상되는 S3 위치에 업로드되고, 결국 수집 파이프라인에 의해 자동으로 처리됩니다.

## 1단계: LLM Optimizer에서 온보딩 {#step-1}

[LLM Optimizer](https://llmo.now/)로 이동합니다.

1. **구성**&#x200B;으로 이동합니다.

   ![구성 버튼](/help/overview/assets/log-forwarding/common/config-button.png)

1. **CDN 구성** 탭을 클릭합니다.

   ![CDN 구성 탭](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. **시작하기**&#x200B;를 클릭합니다.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. **AI 트래픽 인사이트 활성화** 옆의 **구성**&#x200B;을 클릭합니다.

   ![구성](/help/overview/assets/log-forwarding/common/configure.png)

1. **기타**&#x200B;를 선택합니다.

   ![기타 선택](/help/overview/assets/log-forwarding/other/other-select.png)

1. **온보딩**&#x200B;을 클릭합니다.

<!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## 2단계: 로그 준비 및 업로드 {#step-2}

### 필수 로그 형식(JSON 라인) {#log-format}

로그는 줄바꿈으로 구분된 JSON(**라인 당 하나의 JSON 오브젝트**)으로 업로드해야 합니다. 각 로그 라인에는 **아래 철자와 정확히 일치하는** 다음 필드가 포함되어야 합니다.

#### 필드별 스키마 {#schema}

| 필드 | 유형 | 설명 | 예 |
|---|---|---|---|
| **timestamp** | 문자열 | **ISO 8601** 형식을 따른 요청의 타임스탬프입니다. | `"2025-02-01T23:00:05Z"` |
| **호스트** | 문자열 | 클라이언트가 요청한 웹 도메인입니다. | `"www.example.com"` |
| **url** | 문자열 | **경로** 및 **쿼리 매개변수**&#x200B;가 필요하지만 도메인을 포함하지 **않아야** 합니다. | `"/home?utm_source=google"` |
| **request_method** | 문자열 | HTTP 요청 메서드(HTTP 동사라고도 함)입니다. | `"GET"` |
| **request_user_agent** | 문자열 | HTTP 사용자-에이전트 요청 헤더입니다. | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | 문자열 | HTTP 레퍼러 요청 헤더입니다(비어 있을 수 있음). | `"https://chatgpt.com"` |
| **response_status** | 정수 | HTTP 응답 상태 코드입니다. | `200` |
| **response_content_type** | 문자열 | HTTP 콘텐츠-유형 응답 헤더입니다. | `"text/html; charset=utf-8"` |
| **time_to_first_byte** | 정수 | 서버에 대한 연결을 만들고 웹 페이지의 콘텐츠를 다운로드하는 시간(**밀리초**)입니다. 알 수 없거나 사용할 수 없는 경우 0으로 설정합니다. | `42` |

#### 로그 라인 예 {#example}

다음 예제는 세 개의 로그 라인을 보여 줍니다.

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### 중요 면책조항(맞춤법 및 유형) {#disclaimer}

수집 및 집계 파이프라인은 **필드 이름 및 데이터 유형**&#x200B;에 대해 엄격합니다.

- 필드 이름은 **정확히** 일치해야 합니다(대/소문자 및 맞춤법).
- 다음과 같이 데이터 유형이 정확해야 합니다.
   - **타임스탬프**&#x200B;는 **ISO 8601** 형식의 문자열이어야 합니다. UNIX 유사 타임스탬프가 작동하지 않을 수 있습니다.
   - **response_status**&#x200B;는 정수여야 합니다.
   - **time_to_first_byte**&#x200B;는 정수여야 하며 밀리초를 사용해야 합니다.
   - 문자열은 유효한 JSON 문자열이어야 합니다.
- 잘못된 JSON 또는 누락되거나 잘못된 필드는 로그를 건너뛰거나 구문 분석에 실패하여 보고서에서 데이터가 누락될 수 있습니다.

### 위치 및 처리 주기 업로드 {#upload-location}

#### 경로 규칙 {#path-rule}

**`yyyy/mm/dd/`**(슬래시 포함) 형식을 사용하여 적절한 폴더 경로에 로그를 업로드합니다.

2025년 2월 1일 UTC의 예제 로그: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### 처리 규칙 {#processing-rule}

- 지정된 **UTC 일** 동안 업로드된 로그는 **해당 UTC 일이 끝날 무렵**&#x200B;에 파이프라인에서 처리됩니다(매일 실행).
- **이전 날의 폴더**(채우기)에 업로드된 로그는 24시간 내에 **감지 및 처리**&#x200B;됩니다.

## 시나리오 {#scenarios}

### 시나리오 1: Splunk / Elasticsearch의 로그 — S3로 내보내기 및 업로드 {#scenario-splunk}

**목표**: 기존 가시성 플랫폼에서 로그를 가져와 S3 위치로 게재합니다.

- Splunk/Elastic 검색 이벤트에서 필수 필드를 추출합니다.
- 각 이벤트를 위의 스키마(JSON 라인)에 따라 하나의 JSON 오브젝트로 변환합니다.
- 결과 파일을 지정된 S3 버킷과 **현재 UTC 일** 경로에 업로드합니다. `…/byocdn-other/yyyy/mm/dd/`
- 로그는 UTC일 끝까지 자동으로 처리됩니다.

### 시나리오 2: Lambda / Azure 함수 — 형식 및 S3에 업로드 {#scenario-serverless}

**목표**: 서버리스 컴퓨팅을 사용하여 CDN 로그를 가져오고 수신한 후 정규화하여 S3 위치로 게재합니다.

- 이 함수는 고객의 소스(로그 저장소, 대기열, blob 스토리지 등)에서 로그를 가져옵니다.
- 이 함수는 필드를 예상 스키마에 매핑하고 **JSON 라인**&#x200B;을 방출합니다.
- 함수가 출력을 `…/byocdn-other/yyyy/mm/dd/`에 업로드합니다.
- 로그는 UTC일 끝까지 자동으로 처리됩니다.

## 빠른 체크리스트 {#checklist}

- **라인 당 하나의 JSON 오브젝트**(JSON 라인)
- 지정한 대로 **정확한 필드 맞춤법**
- 올바른 데이터 유형
- **time_to_first_byte**(밀리초)(정수)
- **byocdn-other** 아래의 해당 UTC 폴더 **yyyy/mm/dd/**&#x200B;에 업로드
