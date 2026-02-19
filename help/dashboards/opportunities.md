---
title: 최적화 기회
description: 기회 대시보드를 사용하여 브랜드 가시성을 높이기 위해 사이트를 개선할 수 있는 방법을 자동으로 감지하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 33196139fef1cebd47b15aa964df2bac366ea12a
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 100%

---


# 최적화 기회

최적화 기회는 AI 검색에서 브랜드 가시성을 높이기 위해 사이트 및 외부 존재감을 개선할 수 있는 위치를 보여 주는 인사이트를 자동으로 감지합니다.

이러한 최적화에는 페이지 내 수정(구조화된 콘텐츠, 표준 또는 요약 추가), 기술 조정(AI 크롤러 차단 해제 또는 오류 해결), 권한 있는 서드파티 사이트의 콘텐츠에 영향을 주는 작업이 포함됩니다. 이러한 최적화 기회를 해결하면 브랜드가 정확하게 표현되고 생성형 응답에서 인용될 가능성이 높아집니다.

![최적화 기회](/help/dashboards/assets/oport.png)

## 기회 대시보드

대시보드에 제시된 최적화 기회는 플레이어 격차, 트렌딩 주제 및 성과 데이터를 기반으로 우선순위를 정하고 목록으로 제시됩니다. 검색 필드를 사용하여 특정 기회를 검색할 수 있습니다. 또한 기회는 태그별로 그룹화되며, 태그를 직접 클릭하여 해당 태그 아래에 그룹화된 모든 기회를 표시할 수 있습니다.

**세부 정보**&#x200B;를 클릭하면 추가 정보와 추가 지침이 제공되는 별도의 창이 열립니다.

## 지원되는 기회

다음은 현재 지원되는 기회 테이블입니다.

| 기회 | 유형 | 식별된 문제 | 제안 사항 수정 |
|---------|----------|----------|----------|
| 긴 단락 요약 | 콘텐츠(온사이트) | 권장 길이 임계값을 초과하는 단락을 검색합니다. 영향을 받은 URL과 크기가 큰 텍스트 조각을 표시합니다. | 추상화를 만들거나 긴 텍스트를 더 짧게 훑어볼 수 있는 섹션으로 분할합니다. |
| 구조화된 콘텐츠 권장(FAQ) | 콘텐츠(온사이트) | FAQ 항목을 일치시키지 않고도 인기가 높은 프롬프트를 감지합니다. 관련 프롬프트, 카테고리 및 영향을 받은 URL을 표시합니다. | 일반적인 쿼리와 일치하도록 간결한 응답이 포함된 FAQ 스키마 블록을 추가합니다. |
| 차단된 에이전틱 트래픽 감지 | 기술 GEO | 알려진 AI 에이전트(예: GPTBot, PerplexityBot)에서 차단된 요청에 대한 CDN 로그를 분석합니다. 영향을 받는 URL 및 에이전트를 보고합니다. | 해당되는 경우 지원되는 AI 크롤러에 대한 액세스를 허용하도록 robots.txt 또는 서버 구성을 업데이트합니다. |
| 404s/403s/5xx 문제 감지 | 기술 GEO | CDN 로그에서 오류 응답을 모니터링합니다. 빈도, 영향을 받는 URL 및 예상 히트 손실을 보고합니다. | 깨진 링크를 수정하고, 권한을 업데이트하며, 서버측 문제를 해결하여 주요 콘텐츠가 200개의 응답을 반환하도록 합니다. |
| 복구 콘텐츠 가시성(얼리 액세스) | 기술 GEO | AI 에이전트에서 중요한 콘텐츠가 숨겨져 있는 페이지에 플래그를 지정합니다. 영향을 받는 URL 및 복구할 수 있는 예상 콘텐츠를 표시합니다. | 페이지를 사전 렌더링하여 JavaScript 실행 없이 AI 에이전트가 더 많은 콘텐츠를 사용할 수 있도록 합니다. |

## 자동 최적화 {#auto-optimization}

자동 최적화는 권장 최적화를 한 번의 클릭으로 배포할 수 있도록 하여 수작업의 번거로움과 가치 창출 시간을 줄여 줍니다. 최적화는 콘텐츠 소스 또는 CDN 에지에서 적용할 수 있습니다. Edge 기반 자동 최적화는 현재 선택한 기회에 대한 얼리 액세스에서 사용할 수 있습니다. 자세한 내용은 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

<!--### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.-->

### 추가 도구

[LLM 가시성 검사기](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc)는 웹 페이지 콘텐츠 LLM이 액세스할 수 있는 정확한 양과 숨겨진 항목을 확인할 수 있는 Chrome 확장 기능입니다. 무료 독립형 진단 도구로 설계되었으며, 제품 라이선스나 설정이 필요하지 않습니다. 한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가하고, AI 에이전트가 보는 항목과 인간 사용자가 보는 항목을 나란히 비교할 수 있습니다. 또한 LLM Optimizer를 사용하여 복구할 수 있는 콘텐츠 양을 예측합니다.

<!--| Detect Missing Hreflang | Content (Onsite)| Flags pages missing hreflang attributes. Provides affected URLs and expected coverage by language/region.| Implement hreflang tags to indicate correct localized versions. |
| Detect Missing Canonicals | Content (Onsite) | Scans for pages without canonical tags or with conflicting tags. Lists affected URLs and duplicates. | Add canonical tags pointing to the preferred version of each page. Ensure consistent usage across variants. |-->
