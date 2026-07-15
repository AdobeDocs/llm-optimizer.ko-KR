---
title: Google Analytics 통합
description: Google Analytics 4를 LLM Optimizer과 연결하여 참조 트래픽 대시보드에서 AI 기반 검색, 사이트 참여 및 비즈니스 결과를 측정하는 방법에 대해 알아봅니다.
feature: Referral Traffic
autotag-review: '2026-07-15T17:51:53.586Z'
TQID: 'https://experienceleague.adobe.com/SvWn3W6hpVsWNzfWdJFvPs94lwlKX4ufjjcXKM-6xIc'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: f5a6cbd1-8a9a-4c79-a6db-ba46537f516e
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 1169
ht-degree: 17%

---


# Google Analytics 통합

Google Analytics 4(GA4) 통합은 LLM Optimizer을 조직의 GA4 데이터와 연결하므로 ChatGPT, Gemini, Copilot, Claude 및 Perplexity와 같은 플랫폼에서 AI 기반 검색이 실제 웹 사이트 참여 및 비즈니스 성과로 변환되는 방식을 측정할 수 있습니다. GA4 속성에 연결한 후 LLM Optimizer은 GA4 특성이 지정된 참조 트래픽, 참여 및 전환 지표를 해당 소스로 가져와서 **비즈니스 영향** 탭 아래의 **참조 트래픽** 대시보드에 표시합니다.

>[!IMPORTANT]
>
>GA4 통합은 유료 LLM Optimizer 오퍼에 포함되어 있습니다. 무료 평가판을 사용하는 고객은 유료 오퍼로 업그레이드할 때까지 GA4에 연결할 수 없습니다.

## 시작하기에 앞서 {#before-you-begin}

연결을 완료하려면 다음이 필요합니다.

* 연결하려는 GA4 속성에서 **뷰어** 이상의 액세스 권한을 가진 Google 계정입니다. 속성 수준 액세스는 **관리 > 속성 액세스 관리**&#x200B;의 Google Analytics에서 관리됩니다.
* LLM Optimizer의 구성을 관리할 수 있는 권한입니다(그렇지 않으면 연결 단추가 표시되지만 비활성화됨).
* LLM Optimizer 원본에서 팝업을 허용하는 브라우저 — Google 로그인 단계가 새 탭에서 열립니다.

**not**&#x200B;은(는) Google Cloud 프로젝트를 만들거나 서비스 계정을 생성하거나 JSON 키를 업로드하거나 속성 ID를 입력해야 합니다. LLM Optimizer은 Google의 표준 OAuth 동의 화면을 통해 연결을 중개합니다.

## GA4를 참조 트래픽 대시보드에 연결 {#connect}

연결 흐름은 [참조 트래픽](/help/dashboards/referral-traffic.md) 대시보드에서 다음과 같이 시작됩니다.

1. LLM Optimizer에서 **참조 트래픽**&#x200B;을(를) 엽니다.

1. **비즈니스 영향** 탭을 엽니다.

   ![참조 트래픽 대시보드, 비즈니스 영향 탭](/help/dashboards/assets/ga4-integration-01-business-impact-tab.png)

1. **Analytics에 연결**&#x200B;을 선택합니다. LLM Optimizer에서 **고객 구성 > Analytics**(으)로 보냅니다. Analytics 공급자 선택기에서 **Google Analytics 연결**&#x200B;을 선택합니다.

   ![고객 구성, GA4가 있는 Analytics 탭 선택됨](/help/dashboards/assets/ga4-integration-02-analytics-ga4-picker.png)

1. **계정 연결**&#x200B;을 선택합니다. Google 로그인 화면에 새 브라우저 탭이 열립니다.

   ![GA4 연결용 Google 로그인](/help/dashboards/assets/ga4-integration-03-google-sign-in.png)

1. 연결하려는 GA4 속성에 액세스할 수 있는 Google 계정으로 로그인합니다. Google 메시지가 표시되면 `See and download your Google Analytics data` 권한(`analytics.readonly` 범위)을 승인하십시오.

1. Google은 계정이 액세스할 수 있는 GA4 속성이 나열된 LLM Optimizer으로 돌아갑니다. 연결 및 제출할 속성을 선택합니다.

1. LLM Optimizer 탭으로 돌아갑니다. Analytics 탭은 완료된 연결을 자동으로 감지하고 GA4 카드에 **연결됨** 상태가 표시됩니다.

### 연결 후 {#after-connect}

GA4가 LLM Optimizer에 연결되면 다음 상황이 발생합니다.

* LLM Optimizer가 **최근 4주** 및 **현재 주의 현재 시점**&#x200B;까지 데이터를 채웁니다.
* 데이터를 채운 후 **전일 전체 데이터**&#x200B;를 끌어와 **매일** 데이터를 업데이트합니다.

>[!NOTE]
>
>데이터 채우기 작업은 완료되는 데 몇 시간이 소요될 수 있습니다. 비즈니스 영향 대시보드는 데이터가 저장됨에 따라 점진적으로 채워지기 시작합니다. 채우기 실행 중에 사용자의 작업이 필요하지 않습니다.

다시 연결하는 경우(예: Google 계정 또는 GA4 속성을 전환하는 경우) 현재 달력 주만 다시 채워집니다. 이미 로드된 이전 주는 유지됩니다.

## 작동 방식 {#how-it-works}

### 연결 모델

통합에서는 Google의 표준 OAuth 2.0 사용자 위임 플로우를 사용합니다. LLM Optimizer은 선택한 GA4 속성에 범위가 지정된 새로 고침 토큰을 저장하며, 이 토큰을 사용하면 LLM Optimizer이 Google 계정에서 해지할 때까지 GA4 데이터 API를 대신(읽기 전용 액세스 권한 포함) 호출할 수 있습니다.

### LLM 트래픽 식별 방법

LLM Optimizer은 GA4 자체가 LLM 플랫폼에 기여하는 세션에 대해서만 GA4에 요청합니다. 현재 `sessionSourceMedium`이(가) `chatgpt`, `gemini.google.com`, `copilot.microsoft.com`, `claude` 또는 `perplexity` 중 하나와 일치하는 세션입니다. 지원되는 LLM 소스 목록은 Adobe에서 유지 관리되며 시간이 지남에 따라 확장될 수 있습니다.

### 수집되는 데이터 {#data-ingested}

각 일별 가져오기는 다음을 포함하는 집계된 보고서를 검색합니다.

**차원**

| GA4 차원 | 무엇을 나타냅니까 |
| --- | --- |
| `date` | 세션이 발생한 날짜입니다. |
| `landingPage` | 방문자가 사이트에서 본 첫 페이지입니다. |
| `countryId` | GA4의 IP 지리적 위치에 따라 결정된 방문자의 국가입니다. |
| `deviceCategory` | 모바일 / 데스크탑 / 태블릿. |
| `sessionSourceMedium` | GA4에 의한 LLM 소스/미디어. |

**지표**

| GA4 지표 | 무엇을 나타냅니까 |
| --- | --- |
| `sessions` | 버킷의 세션 수입니다. |
| `screenPageViews` | 버킷의 페이지 보기 수입니다. |
| `bounceRate` | 바운스된 세션의 일부입니다. |
| `totalPurchasers` | 고유한 구매자(전자 상거래가 GA4에서 구성된 경우). |
| `transactions` | 거래 수(전자 상거래가 구성된 경우). |
| `purchaseRevenue` | 구매 매출(USD). |
| `totalRevenue` | 총 수익(USD). |

### LLM Optimizer에서 이 데이터를 사용하는 방식

LLM Optimizer은 이 데이터를 사용하여 Business Impact 대시보드의 페이지 수준 성과, 소스 분류, 국가 및 장치 분할 및 시간 트렌드를 채웁니다. 모델을 교육하는 데 데이터를 사용하거나 테넌트 외부에서 데이터를 공유하지 않습니다.

### 수집되지 않은 항목

사용자 식별자(Google 클라이언트 ID, IP 주소, 장치 ID), 세션 수준 행, 이벤트 수준 행, 위에 나열된 차원 이외의 사용자 지정 차원 또는 지표 및 GA4 대상 또는 세그먼트 정의가 없습니다.

## 자주 묻는 질문 {#faq}

Q: 평가판 중에 GA4 통합을 사용할 수 있습니까?

아니요. 통합은 유료 LLM Optimizer 고객만 사용할 수 있습니다.

Q: Google Cloud 프로젝트 또는 서비스 계정을 만들어야 합니까?

아니요. 연결은 표준 Google 로그인입니다. LLM Optimizer은 Adobe 측에서 Google OAuth 클라이언트를 관리합니다. GA4 속성에서 뷰어 액세스 권한이 있는 Google 계정만 있으면 됩니다.

Q: 어떤 데이터가 수집 또는 저장됩니까?

LLM Optimizer은 원시 이벤트 수준 데이터가 아닌 조직에서 승인한 GA4 데이터 API의 집계된 지표와 함께 작동합니다.

Q: 데이터는 어떻게 수집됩니까?

조직은 LLM Optimizer에 선택한 속성에 대한 GA4 데이터 API를 쿼리하도록 권한을 부여합니다. LLM 소스에 정렬된 참조 트래픽은 해당 API를 통해 사용됩니다.

Q: 데이터가 얼마나 자주 업데이트됩니까?

데이터는 **매일** 업데이트 됩니다(데이터 채우기 작업 완료 후 전일 전체 데이터).

Q: 원시 이벤트 수준 데이터가 LLM Optimizer에 저장됩니까?

아니요. 트래픽 패턴 및 트렌드를 이해하는 데는 **집계된** 지표만 사용됩니다.

Q: 전체 URL, 쿼리 문자열 또는 페이지 콘텐츠가 저장됩니까?

랜딩 페이지 경로는 표준 보고서의 일부로 수집되며 쿼리 문자열 및 페이지 콘텐츠는 이 통합에 대해 수집되지 않습니다.

Q: 사용자 식별자(Google 클라이언트 ID, IP 주소, 장치 ID)가 저장됩니까?

아니요.

Q: 데이터가 얼마나 오래 보존됩니까?

현재 기준, 데이터는 무기한 저장됩니다.

Q: 데이터가 전송 중 및 유휴 상태에서 암호화됩니까?

현재 데이터는 전송 중에 암호화되며, 사용하지 않고 있습니다. 이는 향후 업데이트에서 변경될 수 있습니다.

Q: 내역 데이터가 채워집니까?

예. 설정이 성공적으로 완료되면 지난 4주 및 현재 주의 데이터가 채워집니다. [연결 후](#after-connect) 내용을 함께 참조하시기 바랍니다.

Q: 액세스 연결을 끊거나 취소할 수 있습니까?

예, 언제든지 가능합니다. LLM Optimizer의 GA4 카드에서 다른 계정 또는 속성에 다시 연결하거나 [https://myaccount.google.com/permissions](https://myaccount.google.com/permissions)에서 Google 계정에서 LLM Optimizer의 액세스를 완전히 취소할 수 있습니다. 액세스 취소는 새 데이터 가져오기를 중지합니다. 이전에 수집된 집계 데이터는 LLM Optimizer에 유지됩니다.

Q: 내 GA4 속성은 연결되어 있지만 비즈니스 영향은 비어 있습니다. 그 이유는 무엇입니까?

LLM Optimizer은 GA4 자체가 지원하는 LLM 소스/미디어에 기여하는 세션만 가져옵니다(현재: ChatGPT, Gemini, Copilot, Claude, Perplexity). GA4 속성이 표시된 시간 창에 이러한 소스의 참조 세션을 아직 기록하지 않은 경우 연결이 정상인 경우에도 대시보드가 비어 있습니다.
