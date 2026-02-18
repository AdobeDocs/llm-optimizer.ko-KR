---
title: LLM Optimizer 모범 사례
description: AI 검색에서 브랜드 가시성을 높이기 위한 LLM 최적화 모범 사례를 살펴보십시오. 콘텐츠 벤치마크 및 최적화에 대한 인사이트.
feature: Best Practices, Agentic Traffic, Brand Presence
source-git-commit: 31c36f9959993171de4bec384a361d38e6e01dad
workflow-type: ht
source-wordcount: '1718'
ht-degree: 100%

---


# LLM Optimizer 모범 사례

생성형 엔진 최적화(GEO) 또는 응답 엔진 최적화(AEO) 또는 AI 최적화(AIO)라고도 하는 LLM 최적화는 ChatGPT, Perplexity, Copilot, Gemini 및 기타 LLM 기반 어시스턴트를 통해 AI 생성 응답 내에서 브랜드와 콘텐츠를 보고 신뢰할 수 있으며 검색할 수 있도록 하는 방법입니다.

기존의 SEO가 1페이지 순위를 차지하는 데 도움이 되었다면 LLM 최적화는 응답 엔진 내에서 AI 인용과 가시성을 확보하는 데 도움이 됩니다. Adobe LLM Optimizer를 사용하면 응답 엔진 내부에서 브랜드의 가시성을 측정하고 향상시킬 수 있습니다.

이 문서에서는 Adobe LLM Optimizer를 사용하여 AI 기반 검색 환경에서 가시성과 영향력을 측정하고 향상시키는 모범 사례를 설명합니다.

* [LLM과 SEO: 주요 차이점](#key-differences)
* [전략 캠페인 계획 수립](#strategic-campaign-planning)
* [온사이트 최적화](#onsite-optimization---strengthening-your-owned-content)
* [오프사이트 최적화](#offsite-optimization---expanding-your-brand-footprint)
* [LLM 가시성 측정 및 변경 내용 추적](#measuring-llm-visibility-and-tracking-changes)
* [에이전틱 트래픽에 최적화하는 방법](#how-to-optimize-for-agentic-traffic)

## LLM과 SEO: 주요 차이점 {#key-differences}

강력한 SEO 기반은 LLM 최적화를 지원하지만 AI 생성 응답의 가시성을 보장하기 위해서는 새로운 전술이 필요합니다.

>[!NOTE]
>
>현재 SEO 트래픽은 대부분의 웹에 트래픽을 발생시키는 가장 큰 요인이므로 브랜드의 가시성 전략에 매우 중요합니다.


| SEO | LLM |
|---------|----------|
| 색인 기반 | *토큰 기반(훈련된 데이터) |
| 권한 문제 연결 | **브랜드 언급은 더 중요함 |
| JS 렌더링 지원됨 | 매우 제한된 클라이언트측 JS 렌더링 |
| 실시간 색인화 | ***신선도를 위한 검색 증강 생성(RAG) |

*LLM 결과는 색인된 페이지를 사용하지 않지만 LLM은 검색 엔진을 사용하여 검색 증강 생성(RAG)을 통해 프롬프트 응답을 향상시킵니다.

** LLM은 백링크보다 콘텐츠 관련성 및 브랜드 존재감의 우선순위를 지정합니다.

*** RAG는 환각을 줄입니다.

LLM 최적화에 대한 기타 고려 사항:

* 콘텐츠 신선도 문제: LLM은 최근에 업데이트된 콘텐츠의 우선순위를 지정합니다. (검색 엔진도 시간에 민감한 쿼리에 대해 이를 우선 고려하지만 다른 값에 더 많이 의존합니다.)
* 언급 및 인용의 형태로 얻는 것(서드파티)은 매우 중요합니다.

## 전략 캠페인 계획 수립

성공적인 LLM 최적화 캠페인 빌드에는 다음이 포함됩니다.

* 고객 의도에 맞게 높은 가치를 제공하는 주제를 식별합니다. 프롬프트 의도를 비즈니스 목표와 고객의 요구 사항에 맞춥니다.
* 경쟁 업체를 포함한 다른 브랜드에게 격차와 기회를 찾을 수 있도록 언급을 합니다. 다른 브랜드가 인용되는 프롬프트에 초점을 맞추어 브랜드 포함을 위한 기회를 나타냅니다.
* 주제 클러스터링을 사용하여 의도별 프롬프트 그룹화: 주제와 검색 필드를 사용하여 유사한 사용자 목표를 클러스터링하여 가시성을 벤치마크합니다.
* EEAT(경험, 전문성, 권한, 신뢰성) 및 YYYL(재정 또는 생활) 기준을 사용하여 브랜드 신뢰성을 평가합니다.

이 전략적 접근법은 LLM 가시성을 목표로 데이터 기반의 개선합니다.

### LLM 브랜드 가시성 잠금 해제

LLM의 가시성은 브랜드가 AI 생성 응답에 얼마나 자주, 얼마나 두드러지게 나타나는지에 달려 있습니다.

가시성을 향상시키려면 다음 절차를 따르십시오.

분석 > 계획 > 작업 > 조정

* **분석:** LLM 전반에 걸친 주요 고객 프롬프트에서 브랜드가 어떻게 나타나는지 검토합니다.
* **계획:** 집중적인 캠페인을 위해 유사한 의도를 가진 프롬프트 클러스터를 타기팅합니다.
* **동작:** 시간 경과에 따른 LLM 가시성 변화를 구현하고 모니터링합니다.
* **조정:** 최적화의 실행 가능한 인사이트를 바탕으로 전략을 구체화합니다.

<!--insert image-->

이러한 단계를 이해하고 활용하면 AI가 정보 발견의 중심이 되면서 브랜드가 관련성을 유지하는 데 도움이 될 수 있습니다.

## 온사이트 최적화 - 소유한 콘텐츠 강화

온사이트 최적화는 LLM 가시성을 위해 소유한 콘텐츠를 개선합니다. 이는 LLM이 브랜드를 인식하고 액세스하며 인용하는 방식을 개선하기 위해 자신의 웹 사이트와 디지털 속성에서 수행하는 액션입니다.

>[!TIP]
>
>LLM Optimizer는 [기회](/help/dashboards/opportunities.md) 대시보드에서 온사이트 및 오프사이트 최적화 기회를 제안합니다. 이러한 기회는 사이트에 따라 다릅니다. 이러한 제안 중 상당수는 LLM Optimizer를 사용하여 사이트에 직접 배포할 수 있습니다.

다음은 몇 가지 최적화 모범 사례입니다.

1. 기술 접근성 보장

   * robots.txt 및 CDN 설정을 검토하여 AI 에이전트가 사이트에 크롤링을 허용합니다.
   * URL 관리자를 사용하여 차단되거나 액세스할 수 없는 페이지를 식별합니다. [URL 관리자](/help/dashboards/url-inspector.md)를 참조하십시오.

2. 콘텐츠 새로 고침 및 구조

   * 페이지 콘텐츠의 10-15%를 정기적으로 업데이트합니다. LLM은 신선한 콘텐츠에 우선순위를 둡니다.
   * 권위 있는 소스에 인용과 참조를 추가합니다.
   * 더 나은 구문 분석을 위해 구조화된 헤더(H1, H2, H3)를 사용합니다.

3. FAQ 통합

   * 프롬프트 분석을 기반으로 자연어 FAQ를 추가합니다.
   * 대화 포맷으로 일반적인 사용자 질문을 해결합니다.

4. 모니터링 및 반복

   * [기회 대시보드](/help/dashboards/opportunities.md)를 사용하여 권장 사항을 식별하고 조치합니다.
   * 가시성 점수, 감정 및 인용 빈도를 추적합니다.
   * 다른 사람들의 활동(경쟁 업체 포함)과 프롬프트 트렌드에 따라 조정합니다.

## 오프사이트 최적화 - 브랜드 규모 확장

오프사이트 최적화는 LLM이 자주 언급을 하는 서드파티 콘텐츠 소스에 영향을 미쳐 AI 생성 응답에서 브랜드의 가시성을 개선하는 데 중점을 둡니다. 이는 LLM이 브랜드를 찾고 인용하는 방식에 영향을 미치기 위해 소유한 속성 외부에서 취하는 조치입니다.

>[!TIP]
>
>LLM Optimizer는 [기회](/help/dashboards/opportunities.md) 대시보드에서 온사이트 및 오프사이트 최적화 기회를 제안합니다. 이러한 기회는 사이트에 따라 다릅니다. 이러한 제안 중 상당수는 LLM Optimizer를 사용하여 사이트에 직접 배포할 수 있습니다.


주요 오프사이트 채널:

* Wikipedia: 페이지가 최신 상태이고 소스가 적절하며 완전히 작성되었는지 확인합니다.
* Reddit 및 Quora: 신뢰할 수 있고 유용한 기여 및 브랜드 언급을 통해 토론에 참여합니다.
* 제휴 문서 및 검토: 품질 좋은 콘텐츠를 위해 게시자와 공동 작업합니다.
* YouTube 및 소셜 미디어: 일반적인 질문에 응답하는 비디오 및 게시물을 만듭니다.
* 뉴스 및 PR: 평판 좋은 매장의 안전한 보도.

모범 사례:

* 오프사이트 공간 다변화
* Adobe LLM Optimizer을 사용하여 인용 여부를 모니터링합니다. [브랜드 존재감 대시보드](/help/dashboards/brand-presence.md)를 참조하십시오.
* 오래된 콘텐츠를 업데이트하고 새로운 포함 기회를 찾습니다.
* PR 및 소셜 팀과 조정합니다.
* 기여가 편향되지 않고 유익한지 확인합니다.

이러한 단계를 일관되게 실행하면 AI 기반 검색 결과에서 브랜드의 존재감을 크게 향상될 수 있습니다.

## LLM 가시성 측정 및 변경 내용 추적

브랜드가 AI 생성 응답에 어떻게 나타나는지 이해하는 것은 LLM을 최적화하는 데 필수적입니다. Adobe LLM Optimizer는 가시성을 측정하고 성능을 벤치마크하며 시간이 지남에 따라 개선 사항을 추적하는 구조화된 방법을 제공합니다.

다음 주요 지표를 추적합니다.

* **언급:** 브랜드가 응답에서 언급을 하는 빈도.
* **인용:** LLM에서 콘텐츠 또는 소스를 사용하여 질문에 응답하는 빈도.
* **감정:** 브랜드에 대한 언급이 긍정, 중립 또는 부정인지 여부.
* **위치:** 브랜드가 응답에서 언급되는 위치(예: 첫 번째, 중간 또는 마지막).

이러한 지표는 **가시성** 점수로 결합되므로 LLM 응답에서 브랜드의 존재감이 얼마나 강한지 알 수 있습니다. [브랜드 존재감](/help/dashboards/brand-presence.md) 보드를 참조하십시오.

### 추적 전략

다음은 진행 상황을 모니터링하기 위해 수행할 수 있는 단계입니다.

1. 현재 가시성을 벤치마크합니다.
   * 브랜드가 언급되고 인용되는 빈도와 위치, Adobe LLM Optimizer의 감정이 무엇인지 식별합니다. [브랜드 존재감](/help/dashboards/brand-presence.md) 대시보드를 참조하십시오.
   * 브랜드가 표시되는 프롬프트와 표시되지 않는 프롬프트를 분석합니다.
   * 경쟁 업체를 포함한 다른 브랜드와 가시성을 비교합니다([고객 구성 대시보드](/help/dashboards/customer-configuration.md)의 **다른 브랜드 추적**&#x200B;에서).
   * Reddit, Quora, Wikipedia와 같은 사용자 생성 플랫폼에서 가시성을 검토합니다. 플랫폼별 세그먼트(ChatGPT, Google AI 모드 등)
   * 에이전틱 트래픽을 모니터링하여 LLM이 방문하는 페이지를 파악합니다. 에이전틱 트래픽은 종종 홈 페이지로 이동하지 **않지만** 계층 구조상 낮은 다른 페이지로 이동합니다. [에이전틱 트래픽](/help/assets/overview/agentic-traffic-card.png) 대시보드를 참조하십시오.
1. 시간에 따른 변경 사항을 모니터링합니다.
   * 시간 필터를 사용하여 주간 및 월간 교대 근무를 추적합니다.
   * 가시성 점수가 급등하거나 하락하지 않도록 주의하십시오.
   * 브랜드 인식을 파악하기 위해 감정 트렌드를 분석합니다.
1. 가시성을 트래픽, 참여 및 전환과 상호 연관시킵니다.
   * 기여도 기능을 사용하여 가시성 향상을 트래픽, 참여 및 전환과 연결합니다. Adobe LLM Optimizer의 기여도 기능은 가시성 지표(언급, 인용, 감정)의 개선을 사이트 트래픽, 사용자 참여도, 전환과 같은 실제 비즈니스 결과와 연결할 수 있습니다. 이는 최적화 노력에 대한 ROI를 입증합니다.
   * 에이전틱 및 참조 트래픽의 변화를 추적하여 최적화 ROI를 검증합니다.
1. 콘텐츠 개선
   * LLM Optimizer의 [기회 대시보드](/help/dashboards/opportunities.md)를 사용하여 사이트를 식별하고 특히 권장되는 즉각적인 변경을 수행할 수 있습니다. [기회](/help/dashboards/opportunities.md)를 참조하십시오(그런 다음 결과 측정). 기회 섹션을 정기적으로 검토하고 제공된 권장 사항에 대해 조치를 취합니다.
   * 가시성이 떨어지는 페이지의 우선순위를 지정합니다.
   * 웹 사이트 및 기타 콘텐츠를 업데이트하여 타기팅하려는 프롬프트와 더 관련성을 높입니다.
   * 사람이 흔히 묻는 질문에 답하는 FAQ를 페이지에 추가합니다.
   * LLM이 콘텐츠를 쉽게 찾고 읽을 수 있도록 하십시오. 차단된 페이지나 웹 사이트 코드의 문제와 같은 문제를 수정합니다.
   * Wikipedia와 Reddit과 같은 플랫폼에 대한 기여가 편향되지 않고 비상업적이며 가치를 더합니다.
   * Adobe LLM Optimizer를 사용하여 시간이 지남에 따라 가시성이 어떻게 변하는지 추적합니다.
   * 경쟁 업체를 포함한 다른 브랜드들이 더 자주 언급되는 것을 발견하면 앞서가기 위해 전략을 조정합니다.
   * 사람들이 검색하고 묻는 내용에 맞게 콘텐츠를 계속 업데이트합니다.
1. 인사이트를 기반으로 [오프사이트](#offsite-optimization---expanding-your-brand-footprint) 및 [온사이트](#onsite-optimization---strengthening-your-owned-content) 전략을 조정합니다.

>[!NOTE]
>
>콘텐츠가 LLM에 표시되고 액세스 가능한지 확인합니다. Chrome 플러그인을 사용하여 AI 에이전트가 볼 수 있는 항목을 확인할 수 있습니다.

## 에이전틱 트래픽 이해

에이전틱 트래픽은 ChatGPT, Google의 AI mode/overviews, Copilot, Perplexity와 같은 AI 에이전트의 방문을 의미합니다. 이 에이전트들은 응답을 생성하기 위한 정보를 수집하기 위해 사이트를 탐색합니다.

에이전틱 트래픽은 클릭 없는 경험과 클릭 없는 가시성의 두 가지 방식으로 표시됩니다.

### 제로 클릭 경험

기존 검색에서 사용자는 웹 사이트를 클릭스루하여 콘텐츠를 사용합니다. 그러나 LLM을 사용하면 사용자가 사이트를 방문하지 않고도 채팅 인터페이스 또는 검색 엔진 결과 페이지에서 직접 완전한 응답을 얻을 수 있습니다. 이를 제로 클릭 경험이라고 합니다.

이것이 브랜드에 미치는 영향:

1. AI 어시스턴트가 콘텐츠를 요약하거나 인용할 수 있습니다.
2. 사용자는 링크를 클릭하지 않고도 필요한 정보를 얻을 수 있습니다.
3. 사이트의 가시성과 영향력은 트래픽과 분리됩니다.

따라서 분석 결과 방문 횟수가 적더라도 브랜드는 AI 생성 응답에서 여전히 높은 가시성과 영향력을 발휘할 수 있습니다.

### 클릭 없는 가시성

에이전틱 트래픽은 AI 봇이 사이트를 방문하여 교육이나 프롬프트에 응답하기 위한 정보를 수집하는 것을 의미합니다.

이 봇은 다음과 같은 작업을 수행합니다.

1. 페이지를 탐색하며 사실, 구조, 맥락을 추출합니다.
2. 해당 데이터를 사용하여 사용자의 응답을 생성합니다.
3. 사용자가 클릭하지 않더라도 브랜드나 콘텐츠를 인용할 수 있습니다.

이것이 중요한 이유:

* 콘텐츠는 간접적으로 사용자 결정을 내릴 수 있습니다.
* 기존 참여 지표 없이 구매 행동, 브랜드 인식 또는 신뢰에 영향을 미칠 수 있습니다.

에이전틱 트래픽을 추적하면 AI가 콘텐츠를 보고 사용하는 방식을 이해하는 데 도움이 됩니다.

### 에이전틱 트래픽에 최적화하는 방법

에이전틱 트래픽에 최적화하려면:

* robots.txt 및 CDN 설정을 검토하여 크롤링 가능성을 확인합니다.
* [URL 관리자](/help/dashboards/url-inspector.md)를 사용하여 URL 성능을 분석합니다.
* [에이전틱 트래픽 대시보드](/help/dashboards/agentic-traffic.md)에서 CDN 로그에 액세스하여 봇 동작을 추적합니다.
* 트래픽을 세분화하여 비즈니스 결과를 파악합니다. [카테고리, 주제 및 프롬프트에 대한 모범 사례](/help/overview/best-practices-topics-prompts.md)를 참조하십시오.

모니터링할 지표는 다음과 같습니다.

* URL당 에이전트 히트 수
* 봇 요청 성공률
* 페이지당 인용 빈도
* 브랜드 언급 감정 및 배치
* 시간에 따른 가시성 점수 트렌드

<!-- Add screenshot when available in demo environment>


<!-- Use the "Share of Voice" feature to see which competitors are dominating specific topics and adjust your strategy accordingly.-->

<!-- Purpose: Measure how much of the conversation your brand owns compared to competitors.
Insight:

This feature shows the percentage of visibility your brand has for specific topics compared to competitors.


Best Practice:

Use this insight to identify gaps in your visibility and focus on improving your presence in under-performing topics.-->

<!--6. Content Visibility

Purpose: Ensure LLMs can access and render your content.
Insight:

The dashboard compares what LLMs can see versus what is actually on your page.
It provides a percentage of content visibility, highlighting areas where LLMs may only see a small portion of your page due to client-side rendering issues.


Best Practice:

Use nametbd feature to render static HTML versions of your pages for LLM bots, ensuring full content visibility.
Address issues like blocked pages, robots.txt restrictions, and client-side rendering problems.-->



