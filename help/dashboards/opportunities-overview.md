---
title: 최적화 기회
description: 기회 대시보드를 사용하여 브랜드 가시성을 높이기 위해 사이트를 개선할 수 있는 방법을 자동으로 감지하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-07-15T18:08:26.657Z'
TQID: 'https://experienceleague.adobe.com/nEVOXJiQZIqfs2Q-tpA3DeiBNwpZAjhMSyIVuNlACdM'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2:
  - id: bbfc1b77-44c5-4fe8-b65f-ec160fe0d021
  - id: a6256a78-8814-462c-9627-86699b39cee1
  - id: e0ec491f-fe51-42b6-801c-1c0dfcc0e64f
  - id: fe92ae96-fc87-4fea-96a0-adc06310d4f4
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 1225
ht-degree: 100%

---


# 최적화 기회

최적화 기회는 AI 검색에서 브랜드 가시성을 높이기 위해 사이트 및 외부 존재감을 개선할 수 있는 위치를 보여 주는 인사이트를 자동으로 감지합니다.

이러한 최적화에는 페이지 내 수정(구조화된 콘텐츠, 표준 또는 요약 추가), 기술 조정(AI 크롤러 차단 해제 또는 오류 해결), 권한 있는 서드파티 사이트의 콘텐츠에 영향을 주는 작업이 포함됩니다. 이러한 최적화 기회를 해결하면 브랜드가 정확하게 표현되고 생성형 응답에서 인용될 가능성이 높아집니다.

<!--![Optimization opportunities](/help/dashboards/assets/oport.png)-->

## 기회 대시보드

대시보드에 제시된 최적화 기회는 플레이어 격차, 트렌딩 주제 및 성과 데이터를 기반으로 우선순위를 정하고 목록으로 제시됩니다. 검색 필드를 사용하여 특정 기회를 검색할 수 있습니다. 또한 기회는 태그별로 그룹화되며, 태그를 직접 클릭하여 해당 태그 아래에 그룹화된 모든 기회를 표시할 수 있습니다.

**세부 정보**&#x200B;를 클릭하면 추가 정보와 추가 지침이 제공되는 별도의 창이 열립니다.

## 지원되는 기회

다음은 현재 지원되는 기회 테이블입니다.

| 기회 | 유형 | 식별된 문제 | 제안 사항 수정 |
|---------|----------|----------|----------|
| [LLM 친화 요약 추가](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | 콘텐츠(온사이트) | 페이지 또는 섹션 수준에서 간결한 요약과 구조화된 핵심 사항이 부족하여 AI 에이전트가 브랜드 클레임을 스캔하고 해석하기 어려운 트래픽이 많은 페이지를 식별합니다. 영향을 받는 URL과 요약이 권장되는 위치를 표시합니다. | AI에서 생성된 요약과 기존 콘텐츠에 기반한 핵심 사항을 검토한 다음 에이전트가 더 명확하고 스캔 가능한 컨텍스트를 받을 수 있도록 Optimize at Edge를 통해 CDN 에지에 배포합니다. |
| [관련 FAQ 추가](/help/dashboards/opportunities/add-relevant-faqs.md) | 콘텐츠(온사이트) | 프롬프트 세트에 맞는 구조화된 Q&amp;A 콘텐츠가 부족한 트래픽이 많은 페이지를 식별하여 AI 에이전트가 사용자 질문에 페이지에 더 쉽게 매칭할 수 있도록 합니다. 영향을 받는 URL과 FAQ가 권장되는 위치를 표시합니다. | 기존 페이지 자료에 기반한 AI 생성 의도 정렬 FAQ 콘텐츠를 검토한 다음 에이전트가 더 명확한 Q&amp;A 컨텍스트를 받을 수 있도록 Optimize at Edge를 통해 CDN 에지에 배포합니다. |
| [멀티미디어 트랜스크립트 요약 추가](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | 콘텐츠(온사이트) | AI 에이전트가 해당 콘텐츠를 사용하기 어렵게 만드는 컴퓨터에서 읽을 수 있는 트랜스크립트나 요약이 없는 비디오나 다른 미디어에 주요 정보가 임베드된 페이지를 식별합니다. 영향을 받는 URL 및 권장 텍스트를 표시합니다. | 미디어와 페이지에 기반한 AI 생성 트랜스크립트 요약을 검토한 다음 에이전트가 컴퓨터에서 읽을 수 있는 텍스트(예: 관련 비디오 근처)를 받을 수 있도록 Optimize at Edge를 사용하여 CDN 에지에 배포합니다. |
| [robots.txt로 차단된 트래픽](/help/dashboards/opportunities/traffic-blocked-by-robots.md) | 기술 GEO | robots.txt 파일을 분석하여 공개적으로 액세스할 수 있는 콘텐츠에서 AI 에이전트를 선택적으로 차단하는 규칙을 찾습니다. 영향을 받는 URL 및 차단된 에이전트를 보고합니다. | 해당되는 경우 지원되는 AI 크롤러에 대한 액세스를 허용하도록 robots.txt 파일을 업데이트합니다. |
| [에이전틱 트래픽 오류](/help/dashboards/opportunities/agentic-traffic-errors.md) | 기술 GEO | AI 에이전트에 반환된 404, 403 및 5xx 오류 응답에 대한 CDN 로그를 모니터링합니다. 영향을 받는 URL 및 손실된 총 히트 수를 보고합니다. | 깨진 링크를 수정하고, 권한을 업데이트하며, 서버측 문제를 해결하여 주요 콘텐츠가 200개의 응답을 반환하도록 합니다. |
| [복잡한 콘텐츠 간소화](/help/dashboards/opportunities/simplify-complex-content.md) | 콘텐츠(온사이트) | 밀도가 높거나 복잡한 복사본이 가독성 임계값 이하에 위치하여 AI 에이전트가 주요 정보를 해석하기 어렵게 만드는 트래픽이 많은 페이지를 식별합니다. 영향을 받는 URL과 간소화된 텍스트가 권장되는 위치를 표시합니다. | 기존 페이지 콘텐츠에 기반한 AI가 생성한 향상된 텍스트를 검토한 다음 에이전트가 더 명확하고 스캔하기 쉬운 지문을 받을 수 있도록 Optimize at Edge를 사용하여 CDN 에지에 배포합니다. |
| [콘텐츠 가시성 복구](/help/dashboards/opportunities/recover-content-visibility.md) | 기술 GEO | AI 에이전트에서 중요한 콘텐츠가 숨겨져 있는 페이지에 플래그를 지정합니다. 영향을 받는 URL 및 복구할 수 있는 예상 콘텐츠를 표시합니다. | CDN 계층에서 Optimize at Edge를 사용하여 페이지를 사전 렌더링하면 JavaScript 실행 없이도 AI 에이전트가 더 많은 콘텐츠를 이용할 수 있습니다. |
| [목차 추가](/help/dashboards/opportunities/add-table-of-contents.md) | 기술 GEO | AI 에이전트가 콘텐츠를 구문 분석하고 사용자 쿼리에 매핑하기 어렵게 만드는 명확한 구조적 조직이나 탐색 머리글이 없는 페이지를 감지합니다. 영향을 받는 URL과 구조화된 목차가 권장되는 위치를 표시합니다. | 페이지의 기본 섹션을 반영하는 앵커 연결 머리글이 있는 제안된 구조의 목차를 검토한 다음 Optimize at Edge를 사용하여 CDN 에지에 배포하여 목차가 HTML에 삽입되도록 함으로써 모델이 관련 섹션을 보다 쉽게 추출하고 매핑하고 인용할 수 있도록 페이지 구조를 개선합니다. |
| [Wikipedia 분석](/help/dashboards/opportunities/wikipedia-analysis.md) | 오프사이트 | 참조, 섹션, 콘텐츠 길이, 이미지 및 정보 상자 완성도 전반에 걸쳐 업계 경쟁업체와 비교하여 회사의 Wikipedia 페이지를 분석합니다. 페이지가 업계 벤치마크보다 낮은 특정 간격을 파악합니다. | 참조 추가, 정보 상자 강화, 섹션 확장 및 문서 품질 개선을 포함하여 Wikipedia의 존재를 개선하기 위해 AI가 생성한 전략적 권장 사항을 검토합니다. |
| [YouTube 감정 분석(Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | 오프사이트, 소셜 및 커뮤니티 | 브랜드 언급, 감정, 언급 점유율 및 반복 주제에 대한 브랜드 존재감 프롬프트 세트에 인용된 YouTube 비디오를 분석합니다. YouTube 비디오가 프롬프트 세트에 대한 인용으로 검색될 때만 표시됩니다. | 제안된 액션 및 이를 구현하는 팀을 포함하여 YouTube 콘텐츠 전반에서 브랜드 인식을 개선하기 위해 우선순위가 지정된 권장 사항을 검토합니다. |
| [Reddit 감정 분석(Beta)](/help/dashboards/opportunities/reddit-sentiment-analysis.md) | 오프사이트, 소셜 및 커뮤니티 | 브랜드 언급, 감정, 언급 점유율 및 반복 주제에 대한 브랜드 존재감 프롬프트 세트에 인용된 Reddit 스레드를 분석합니다. Reddit 스레드가 프롬프트 세트의 인용으로 검색되는 경우에만 나타납니다. | 제안된 액션 및 이를 구현하는 팀을 포함하여 Reddit 콘텐츠 전반에서 브랜드 인식을 개선하기 위해 우선순위가 지정된 권장 사항을 검토합니다. |
| [인용된 감정 분석(Beta)](/help/dashboards/opportunities/cited-sentiment-analysis.md) | 오프사이트, 소셜 및 커뮤니티 | 브랜드 언급, 감정, 언급 점유율 및 반복 주제에 대해 설정된 브랜드 존재감 프롬프트에 대해 감지된 상위 인용 URL을 분석합니다. | 브랜드에 대한 프롬프트에 응답할 때 AI 시스템이 가장 많이 인용하는 페이지에서 브랜드 인식을 개선하기 위해 우선순위가 지정된 권장 사항을 검토합니다. |
| [제품 카탈로그 강화(Beta)](/help/dashboards/opportunities/enrich-product-catalog.md) | 콘텐츠(온사이트), Adobe Commerce | LLM이 해석하기에 이름이나 설명이 너무 일반적이거나, 기술적으로 밀도가 높거나, 모호한 Commerce 카탈로그 제품을 식별합니다. 평가된 PDP, 에이전틱 트래픽 컨텍스트 및 AI가 생성한 내러티브 보강을 표시합니다. | 제안된 제품 이름 및 설명을 검토하고 편집한 다음 최적화를 배포하여 업데이트를 Adobe Commerce 카탈로그에 직접 게시합니다(수정된 제안에서 롤백 포함). |
| [제품 세부 정보 페이지 보강](/help/dashboards/opportunities/enrich-product-detail-pages.md) | 테크니컬 GEO, Adobe Commerce | Adobe Commerce 상점의 경우, 전체 카탈로그 데이터를 AI 에이전트가 각 제품 세부 정보 페이지에서 액세스할 수 있는 데이터와 비교합니다. 즉, 에이전틱 트래픽별로 우선순위가 지정된 에이전트가 표시하는 HTML에서 변형, 사양, 속성 및 관련 카탈로그 필드가 누락된 PDP를 표시합니다. | 에이전트 보기에서 누락된 복구 가능한 카탈로그 정보와 LLM 기반 제품 검색이 중요한 이유를 강조 표시합니다. Optimize at Edge를 사용하여 배포하면 완전히 사전 렌더링된 AI 친화적인 HTML 스냅샷을 CDN 에지의 에이전틱 트래픽에 제공하므로 에이전트는 CMS 또는 카탈로그 변경 없이 카탈로그에서 풍부한 제품 컨텍스트를 받습니다. |

## 자동 최적화 {#auto-optimization}

자동 최적화는 권장 최적화를 한 번의 클릭으로 배포할 수 있도록 하여 수작업의 번거로움과 가치 창출 시간을 줄여 줍니다. 최적화는 콘텐츠 소스 또는 CDN 에지에서 적용할 수 있습니다. Edge 기반 자동 최적화는 현재 선택한 기회에 대한 얼리 액세스에서 사용할 수 있습니다. 자세한 내용은 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

<!--
### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.
-->

### 추가 도구

[LLM 가시성 검사기](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc)는 웹 페이지 콘텐츠 LLM이 액세스할 수 있는 정확한 양과 숨겨진 항목을 확인할 수 있는 Chrome 확장 기능입니다. 무료 독립형 진단 도구로 설계되었으며, 제품 라이선스나 설정이 필요하지 않습니다. 한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가하고, AI 에이전트가 보는 항목과 인간 사용자가 보는 항목을 나란히 비교할 수 있습니다. 또한 LLM Optimizer를 사용하여 복구할 수 있는 콘텐츠 양을 예측합니다.

<!--
| Detect Missing Hreflang | Content (Onsite)| Flags pages missing hreflang attributes. Provides affected URLs and expected coverage by language/region.| Implement hreflang tags to indicate correct localized versions. |
| Detect Missing Canonicals | Content (Onsite) | Scans for pages without canonical tags or with conflicting tags. Lists affected URLs and duplicates. | Add canonical tags pointing to the preferred version of each page. Ensure consistent usage across variants. |
-->
