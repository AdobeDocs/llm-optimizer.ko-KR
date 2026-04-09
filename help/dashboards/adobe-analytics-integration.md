---
title: Adobe Analytics 통합
description: Adobe Analytics를 LLM Optimizer과 연결하여 참조 트래픽 대시보드에서 AI 기반 검색, 사이트 참여 및 비즈니스 결과를 측정하는 방법에 대해 알아봅니다.
feature: Referral Traffic
source-git-commit: e7c9bc1d40267dc92608baa005f85f4be21cfda1
workflow-type: ht
source-wordcount: '879'
ht-degree: 100%

---


# Adobe Analytics 통합

Adobe Analytics 통합은 LLM Optimizer를 조직의 Adobe Analytics 데이터와 연결하므로 AI 기반 검색이 실제 웹 사이트 참여 및 비즈니스 성과로 해석되는 방식을 측정할 수 있습니다. 통합 프로세스가 완료되면 **비즈니스 영향** 탭 아래의 **참조 트래픽** 대시보드에서 데이터를 사용할 수 있습니다.

LLM Optimizer는 분석 데이터를 AI 가시성 인사이트와 연결하여 다음을 추적하는 데 도움이 됩니다.

* AI 참조 페이지에 대한 사용자 참여
* AI 검색 여정에 연결된 전환 신호
* GEO 최적화의 성능 영향

이 통합은 AI 가시성 측정과 비즈니스 성과 분석 간의 차이를 완화합니다. 이제 팀은 AI 응답에서 브랜드가 나타나는 위치뿐만 아니라 사용자가 도착한 후 어떤 일이 발생하는지 확인할 수 있습니다.

## 가용성 {#availability}

>[!IMPORTANT]
>
>Adobe Analytics 통합은 유료 LLM Optimizer 오퍼에 포함됩니다. 무료 체험판을 사용하는 고객은 유료 오퍼로 업그레이드할 때까지 Adobe Analytics에 연결할 수 없습니다.

## Adobe Analytics를 참조 트래픽 대시보드에 연결 {#connect}

연결 흐름은 [참조 트래픽](/help/dashboards/referral-traffic.md) 대시보드에서 다음과 같이 시작됩니다.

1. [참조 트래픽](/help/dashboards/referral-traffic.md) 대시보드를 엽니다. 기본 보기는 **트래픽 인사이트**&#x200B;입니다.

   ![참조 트래픽 대시보드, 트래픽 분석 탭](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. **비즈니스 영향** 탭을 선택합니다. 연결된 분석 공급자가 없으면 **Analytics에 연결** 옵션과 함께 **비즈니스 영향을 보려면 연결** 배너가 표시됩니다.

   ![Analytics에 연결 옵션이 표시된 비즈니스 영향 탭](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. **Analytics에 연결**&#x200B;을 선택합니다. 이렇게 하면 **Analytics** 탭에서 [고객 구성](/help/dashboards/customer-configuration.md) 대시보드가 열립니다.

   ![고객 구성, Analytics 탭](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. **자격 증명**&#x200B;에서 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;를 입력한 다음 **확인 및 계속**&#x200B;을 선택합니다. 다음 사항을 참고하십시오.

   * **확인 및 계속**&#x200B;은 두 필드를 모두 채워야만 사용할 수 있습니다.
   * 확인이 완료되면 보고서 세트가 로드됩니다.
   * 필요한 보고서 세트에 액세스할 수 있는 [기술 계정](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)의 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;를 사용하십시오.

   ![Analytics 자격 증명과 확인 및 계속](/help/dashboards/assets/aa-integration-04-credentials.png)

1. **구성**&#x200B;에서 **보고서 세트**&#x200B;를 선택합니다.

   보고서 세트를 선택하면 LLM Optimizer는 해당 세트에 사용할 수 있는 **페이지 URL 차원** 옵션을 로드합니다.

   ![선택한 보고서 세트 및 차원 로드](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. **페이지 URL 차원**(세트별 차원 목록)을 선택한 다음 **저장 및 활성화**&#x200B;를 선택합니다.

   * **페이지 URL 차원**&#x200B;은 보고서 세트를 선택하고 차원을 로드할 때까지 비활성화 상태로 유지됩니다.
   * **저장 및 활성화**&#x200B;는 페이지 URL 차원을 선택한 후에만 사용할 수 있습니다.

   ![페이지 URL 차원과 저장 및 사용](/help/dashboards/assets/aa-integration-06-page-url-dimension.png)

1. 저장한 후 구성에 **연결됨** 상태가 표시됩니다. **참조 트래픽 대시보드로 이동**&#x200B;을 통해 참조 트래픽 대시보드로 돌아갈 수 있습니다. **비즈니스 영향** 탭의 **참조 트래픽**&#x200B;에서 상태는 **Adobe Analytics에 연결됨**&#x200B;으로 표시됩니다.

   ![구성 및 비즈니스 영향에서 Adobe Analytics에 연결됨](/help/dashboards/assets/aa-integration-07-connected.png)

### 연결 후 {#after-connect}

* LLM Optimizer가 **최근 4주** 및 **현재 주의 현재 시점**&#x200B;까지 데이터를 채웁니다.
* 데이터를 채운 후 **전일 전체 데이터**&#x200B;를 끌어와 **매일** 데이터를 업데이트합니다.

>[!NOTE]
>
>데이터 채우기 작업은 완료되는 데 몇 시간이 소요될 수 있습니다.

## 작동 방식 {#how-it-works}

### 구성

설정 중에 LLM Optimizer에서 Adobe Analytics 수집에 사용하는 보고서 세트와 페이지 차원을 정의합니다. 페이지 차원은 보고서 세트에 따라 표준 `variables/page` 매핑 또는 사용자 정의`eVar`가 될 수 있습니다.

### LLM 트래픽 식별 방법

LLM에서 시작된 트래픽은 Adobe Analytics [레퍼러 유형 — 대화형 AI 도구](https://experienceleague.adobe.com/ko/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools)를 사용하여 식별됩니다.

### 수집되는 데이터 {#data-ingested}

LLM Optimizer에서 수집하는 데이터는 다음과 같습니다.

**차원**

* 레퍼러 도메인
* 레퍼러 유형
* 국가
* 디바이스 유형
* 선택한 페이지 차원

**지표**

* 페이지 조회수
* 방문 횟수
* 방문자
* 시작
* 종료
* 바운스 수
* 단일 페이지 방문 횟수
* 체류 시간
* 장바구니
* 장바구니 추가
* 장바구니 제거 수
* 장바구니 보기 수
* 체크아웃
* 주문 수
* 수익
* 판매량

### LLM Optimizer에서 이 데이터를 사용하는 방식

이 데이터 세트는 다음에 대한 LLM Optimizer 인사이트를 강화합니다.

* 페이지 수준 LLM 트래픽 성능
* LLM 소스 간 레퍼러 성능
* 지역 및 디바이스 수준 트렌드
* 다운스트림 상거래 결과

## 자주 묻는 질문 {#faq}

Q: 체험판 사용 중에 Adobe Analytics 통합을 사용할 수 있습니까?

아니요. 통합은 유료 LLM Optimizer 고객만 사용할 수 있습니다.

Q: 어떤 데이터가 수집 또는 저장됩니까?

위의 [수집되는 데이터](#data-ingested) 장을 참조하십시오. LLM Optimizer는 원시 히트 수준 데이터가 아닌 조직에서 승인한 Adobe Analytics API의 집계된 지표와 함께 작동합니다.

Q: 데이터는 어떻게 수집됩니까?

조직은 LLM Optimizer에 Adobe Analytics API를 쿼리하도록 권한을 부여합니다. LLM 소스에 해당하는 참조 트래픽은 이러한 API를 통해 사용됩니다.

Q: 데이터가 얼마나 자주 업데이트됩니까?

데이터는 **매일** 업데이트 됩니다(데이터 채우기 작업 완료 후 전일 전체 데이터).

Q: 원시 히트 수준 데이터가 LLM Optimizer에 저장됩니까?

아니요. 트래픽 패턴 및 트렌드를 이해하는 데는 **집계된** 지표만 사용됩니다.

Q: 전체 URL, 쿼리 문자열 또는 페이지 콘텐츠가 저장됩니까?

선택한 페이지 차원에 사용되는 전체 URL은 수집될 수 있으며 통합을 위한 쿼리 문자열 및 페이지 콘텐츠는 수집되지 않습니다.

Q: 사용자 식별자(ECID, IP 주소, 쿠키 ID)가 저장됩니까?

아니요.

Q: 데이터가 얼마나 오래 보존됩니까?

보존 정책이 변경될 수 있다는 점에 유의하시기 바랍니다. 현재 기준, 데이터는 무기한 저장됩니다.

Q: 데이터가 전송 중 및 유휴 상태에서 암호화됩니까?

현재 기준, 데이터는 전송 중에 암호화되며 유휴 상태에서는 암호화되지 않습니다. 이는 향후 업데이트에서 변경될 수 있습니다.

Q: 내역 데이터가 채워집니까?

예. 설정이 성공적으로 완료되면 지난 4주 및 현재 주의 데이터가 채워집니다. [연결 후](#after-connect) 내용을 함께 참조하시기 바랍니다.
