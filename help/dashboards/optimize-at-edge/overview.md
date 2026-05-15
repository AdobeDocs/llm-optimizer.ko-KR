---
title: Optimize at Edge
description: CDN 에지에서 작성 변경 없이 LLM Optimizer로 최적화를 제공하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-05-15T17:55:41.072Z'
TQID: 'https://experienceleague.adobe.com/kMxoKtrfyzxIpLJP9nt-rq6GP37ICCNe4XienUKqDZE'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: a0b5a505-2fd7-4c3d-b61c-b557fb6f0558id: d1956731-2adb-4bb7-8301-2b239254ac72id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 3108
ht-degree: 66%

---


# Optimize at Edge

이 페이지는 작성 변경 없이 CDN 에지에서 최적화를 제공하는 방법에 대한 자세한 개요를 제공합니다. 온보딩 프로세스, 사용 가능한 최적화 기회 및 에지에서 자동 최적화하는 방법을 다룹니다.

## Optimize at Edge란 무엇입니까?

Optimize at Edge는 LLM Optimizer의 에지 기반 배포 기능으로, LLM 사용자 에이전트에게 AI 친화적인 변경 사항을 제공합니다. 현재 컨텍스트에서 “Edge”는 최적화가 CDN 계층에서 적용됨을 의미합니다. CDN 계층에서 최적화를 제공하기 때문에 콘텐츠 관리 시스템(CMS)에서 작성 변경이 필요하지 않으므로 원본 CMS는 변경되지 않습니다. 이러한 분리를 통해 기존 게시 워크플로를 변경하지 않고 LLM 가시성을 향상시킬 수 있습니다. 에이전틱 트래픽만을 대상으로 하며, 사용자나 SEO 봇에는 영향을 미치지 않습니다. LLM Optimizer가 페이지 최적화 기회를 감지하면 사용자는 CDN 에지에 직접 수정 사항을 배포할 수 있습니다.

Optimize at Edge는 복잡한 엔지니어링 노력이 필요한 기존 수정 사항에 대한 더 빠르고 효율적인 대안입니다. 앞서 언급했듯이, 한 번의 설정을 완료하면 변경 사항을 적용하기 위해 플랫폼 변경이나 긴 개발 주기가 필요하지 않습니다. 개발자의 참여 없이 몇 분 만에 향상된 사항을 게시할 수 있습니다. AI 에이전트용으로 웹 사이트를 최적화하는 비코드 방법입니다.

Optimize at Edge는 마케팅, SEO, 콘텐츠 및 디지털 전략 팀의 비즈니스 사용자를 위해 설계되었습니다. 비즈니스 사용자는 기회 식별, 제안 이해, 수정 사항 간편 배포 등 LLM Optimizer의 전체 여정을 완료할 수 있습니다. Optimize at Edge를 사용하면 사용자는 변경 사항을 미리 보고 CDN 에지에 빠르게 배포하여 최적화가 실행 중인지 확인할 수 있습니다. 성능은 LLM Optimizer 생태계에서 추적할 수 있습니다.

### 주요 이점

* **AI 전용 게재:** AI 에이전트에게만 최적화된 HTML을 제공하며, 방문자나 SEO 봇에게 아무런 영향을 미치지 않습니다.
* **더 빠른 주기:** 변경 사항을 몇 주가 아닌 몇 분 안에 게시합니다. 플랫폼 변경이나 긴 엔지니어링 주기가 필요하지 않습니다.
* **복원 가능:** 몇 분 만에 페이지를 되돌릴 수 있는 원클릭 롤백 기능이 지원됩니다.
* **성능에 영향을 주지 않음:** Edge 기반 최적화 및 캐싱은 사이트 지연 시간에 영향을 주지 않습니다.
* **CDN 및 CMS 독립적:** 콘텐츠 관리 시스템에 관계없이 모든 CDN 구성 및 프론트엔드 설정에서 작동합니다.

### Optimize at Edge에서 어떤 기회가 지원됩니까?

에이전틱 웹 경험을 향상시킬 수 있는 기회는 Optimize at Edge를 통해 지원됩니다. [기회 대시보드](/help/dashboards/opportunities-overview.md) 페이지와 현재 페이지의 기회 섹션에서 각 기회에 대해 자세히 알아봅니다.

## 온보딩

<!--You should reach out to either your Adobe account team or the FDE team to start the onboarding process. Your IT or CDN team is also required to complete the pre-requisites and setup process. Additionally, you can also contact `llmo-at-edge@adobe.com` for further onboarding assistance.-->

다음 단계를 따라 LLM Optimizer 계정에서 온보딩 프로세스를 시작합니다.

1. **고객 구성** 대시보드에서 **CDN 구성** 탭을 선택합니다.
1. **CDN 온보딩**을 클릭합니다.
   ![CDN 구성 탭](/help/overview/assets/cc-cdn.png)
1. AEM Cloud Service 관리 Fastly 고객의 경우, 라우팅 설정은 셀프서비스이며 LLM Optimizer UI에서 직접 완료할 수 있습니다. 다른 CDN 공급자를 사용하는 고객의 경우 IT/CDN 팀이 필요한 설정 및 사전 요구 사항을 완료해야 합니다. 추가 지침은 아래에 제공된 CDN 안내서 예시를 참조하십시오.

>[!NOTE]
>전체 온보딩 흐름을 다루는 아래의 단계별 안내서를 참조하십시오. 안내서를 통해 해결할 수 없는 문제의 경우 `llmo-at-edge@adobe.com`에 문의하십시오.

IT/CDN 팀에 대한 요구 사항:

* `*AdobeEdgeOptimize/1.0*` 사용자 에이전트를 사이트의 robots.txt 파일 또는 봇 트래픽 관리 규칙의 허용 목록에 추가합니다.
* 페이지가 도메인 또는 CDN 수준에서 차단되지 않았는지 확인합니다.
* CDN에서 Optimize at Edge 라우팅 규칙에 추가합니다.
* CDN에 WAF 또는 Bot Manager 규칙이 있는 경우 `*AdobeEdgeOptimize/1.0*` 사용자 에이전트를 허용 목록에 추가합니다. 추가 확인이 필요한 경우 `x-edgeoptimize-fetcher-key` 헤더를 구성합니다. 아래의 각 BYOCDN 안내서에는 해당 단계가 포함되어 있습니다.
* LLM Optimizer 인터페이스에서 Optimize at Edge 라우팅을 확인합니다.

다음 다이어그램은 Optimize at Edge를 사용한 BYOCDN 설정에서 요청이 전달되는 방식을 보여 줍니다.

![BYOCDN 요청 흐름](/help/assets/optimize-at-edge/byocdn-request-flow.png)

>[!IMPORTANT]
>라우팅은 외부 CDN(클라이언트에 가장 가까운 CDN)에서 구성해야 합니다. 여러 CDN이 있는 경우 라우팅은 외부 CDN에서만 수행할 수 있습니다.

설정 프로세스를 안내하려면 아래에서 CDN 공급자를 선택하고 해당 구성 안내서를 따르십시오. 이러한 예제는 실제 라이브 구성에 맞게 조정되어야 합니다. 먼저 저사양 환경에서 변경 사항을 적용하는 것을 권장합니다.

### CDN 구성 안내서

| CDN 공급자 | 유형 | 안내서 |
|---|---|---|
| AEM Cloud Service Managed CDN(Fastly) | Adobe 관리 | [설정 안내서 보기](/help/dashboards/optimize-at-edge/aemcs-managed-cdn.md) |
| Fastly(BYOCDN) | 자체 CDN 가져오기 | [설정 안내서 보기](/help/dashboards/optimize-at-edge/fastly-byocdn.md) |
| Akamai(BYOCDN) | 자체 CDN 가져오기 | [설정 안내서 보기](/help/dashboards/optimize-at-edge/akamai-byocdn.md) |
| Cloudflare(BYOCDN) | 자체 CDN 가져오기 | [설정 안내서 보기](/help/dashboards/optimize-at-edge/cloudflare-byocdn.md) |
| CloudFront(BYOCDN) | 자체 CDN 가져오기 | [설정 안내서 보기](/help/dashboards/optimize-at-edge/cloudfront-byocdn.md) |

>[!NOTE]
>
>CDN 공급자가 위에 나열되어 있지 않거나 LLM Optimizer UI에서 도메인이나 이메일을 찾을 수 없는 경우 `llmo-at-edge@adobe.com`에 연락하여 온보딩 지원을 받으십시오. 설정 구성이 완료되면 LLM Optimizer에서 Optimize at Edge 기회에 대한 제안을 배포할 수 있습니다.

위의 각 CDN 설정 안내서는 에이전틱 트래픽이 올바르게 라우팅되고 있으며 사람 트래픽이 영향을 받지 않는지 확인하기 위한 자세한 검증 단계가 포함되어 있습니다.

## 기회

다음 테이블에는 에이전틱 웹 경험을 개선할 수 있는 기회가 제시되어 있으며, Optimize at Edge에서 지원됩니다.

| 기회 | 유형 | 자동 식별 | 자동 제안 | 자동 최적화 |
|---------|----------|----------|----------|----------|
| [콘텐츠 가시성 복구](/help/dashboards/opportunities/recover-content-visibility.md) | 기술 GEO | AI 에이전트에서 중요한 콘텐츠가 숨겨져 있는 페이지를 감지합니다. 영향을 받는 URL 및 복구할 수 있는 예상 콘텐츠를 표시합니다. | AI 에이전트가 사용할 수 있는 콘텐츠를 강조하고 해당 페이지에 대한 사전 렌더링을 활성화할 것을 권장합니다. | 완전히 렌더링된 AI 친화적인 HTML 스냅샷을 에이전틱 트래픽에 제공하여 이전에 숨겨져 있던 콘텐츠를 복구합니다. |
| [제품 세부 정보 페이지 보강](/help/dashboards/opportunities/enrich-product-detail-pages.md) | 기술 GEO | Adobe Commerce 스토어프론트의 경우, 전체 카탈로그 데이터를 AI 에이전트가 각 제품 세부 정보 페이지에서 액세스할 수 있는 데이터와 비교합니다. 즉, 에이전트 트래픽별로 우선 순위가 지정된 에이전트가 표시하는 HTML에서 변형, 사양, 속성 및 관련 카탈로그 필드가 누락된 PDP를 표시합니다. | 에이전트 보기에서 누락된 복구 가능한 카탈로그 정보와 LLM 기반 제품 검색에 중요한 이유를 소개합니다. | 완전히 사전 렌더링된 AI 친화적인 HTML 스냅샷을 CDN 에지의 에이전트 트래픽에 제공하여 에이전트가 CMS 또는 카탈로그 변경 없이 카탈로그에서 풍부한 제품 컨텍스트를 받습니다. |
| [LLM 친화적 요약 추가](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | 콘텐츠 최적화 | 는 페이지 또는 섹션 수준에서 간결한 요약과 구조화된 키 포인트가 부족한 트래픽 상위 페이지를 식별하여 AI 에이전트가 스캔하고 해석하기 어렵게 합니다. | 는 기존 콘텐츠에 기반을 둔 짧고 AI가 생성한 요약 및 키 포인트를 권장합니다. | 관련 HTML 섹션에 요약 및 주요 사항을 삽입하여 모델이 페이지 콘텐츠를 해석하고 설명하는 방식을 개선합니다. |
| [관련 FAQ 추가](/help/dashboards/opportunities/add-relevant-faqs.md) | 콘텐츠 최적화 | 는 프롬프트 세트에 맞는 구조화된 Q&amp;A 콘텐츠가 부족한 트래픽이 많은 페이지를 식별하여 AI 에이전트가 사용자 질문에 페이지에 더 쉽게 매칭할 수 있도록 합니다. | 사용자 의도와 기존 페이지 주제에 맞게 AI가 생성한 FAQ 콘텐츠를 제안합니다. | HTML에 FAQ 콘텐츠를 삽입하여 AI 기반 응답에서 페이지를 더 쉽게 발견하고 연관시킬 수 있습니다. |
| [복잡한 콘텐츠 단순화](/help/dashboards/opportunities/simplify-complex-content.md) | 콘텐츠 최적화 | AI 이해를 방해할 수 있는 복잡한 텍스트로 페이지에 플래그를 지정합니다. | AI가 생성한 복잡한 텍스트의 단순화된 버전을 제공하면서 원래의 의미를 유지합니다. | 페이지의 복잡한 섹션을 다시 작성하여 AI 가독성을 향상시킵니다. |
| [목차 추가](/help/dashboards/opportunities/add-table-of-contents.md) | 기술 GEO | 명확한 구조 구성 또는 탐색 제목이 없는 페이지를 탐지하여 AI 에이전트가 콘텐츠를 구문 분석하고 사용자 쿼리에 매핑하기 어렵게 합니다. | 페이지의 기본 섹션을 반영하는 앵커와 연결된 머리글이 있는 구조화된 목차를 제안합니다. | HTML에 목차를 도입해 AI 모델이 관련 섹션을 보다 쉽게 추출, 매핑, 인용할 수 있도록 페이지 구조를 개선했다. |
| [멀티미디어 성적 증명서 요약 추가](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | 콘텐츠 최적화 | 컴퓨터에서 읽을 수 있는 대본이나 요약이 없는, 주요 정보가 비디오나 다른 미디어에 포함된 페이지를 식별하여 AI 에이전트가 해당 콘텐츠를 사용하기 어렵게 만듭니다. 영향을 받는 URL 및 권장 텍스트를 표시합니다. | 미디어와 페이지에 기반을 둔 AI 생성 대본 요약을 권장합니다. | 대본 요약을 HTML에 삽입하면 에이전트 트래픽에서 기계가 읽을 수 있는 텍스트(예: 관련 비디오 근처)를 받게 됩니다. |

### 추가 도구

[AI 콘텐츠 가시성 검사기](https://chromewebstore.google.com/detail/ai-content-visibility-che/jbjngahjjdgonbeinjlepfamjdmdcbcc) 브라우저 확장 프로그램은 LLM이 웹 페이지 콘텐츠 중 액세스할 수 있는 부분과 숨겨져 있는 부분을 보여 줍니다. 무료 독립형 진단 도구로 설계되었으며, 제품 라이선스나 설정이 필요하지 않습니다.

한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가할 수 있습니다. AI 에이전트가 보는 내용과 사용자가 보는 내용을 나란히 비교하고 LLM Optimizer을 사용하여 복구할 수 있는 콘텐츠의 양을 예측할 수 있습니다. 자세한 내용은 [AI가 웹 사이트를 읽을 수 있습니까?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) 페이지를 참조하십시오.

## 기회 세부 정보

다음 섹션에서는 Optimize at Edge에서 지원되는 각 기회에 대한 추가 세부 정보를 확인할 수 있습니다.

### 콘텐츠 가시성 복구

이 기회는 클라이언트측 렌더링으로 인해 AI 에이전트용 주요 콘텐츠가 숨겨져 있는 페이지를 표시합니다. 식별된 각 페이지마다 AI 에이전트 보기에서 누락된 콘텐츠가 정확히 표시되고, 가시성 격차를 강조 표시하며, 숨겨진 콘텐츠를 복구하기 위해 변경 사항을 직접 적용할 수 있습니다. 이 기회를 Optimize at Edge와 함께 배포하면 사전 렌더링된 AI 최적화 버전의 페이지가 LLM 사용자 에이전트에게 제공되므로 Javascript를 실행하지 않고도 전체 컨텍스트에 액세스할 수 있습니다.
이렇게 하면 AI 에이전트가 페이지를 먼저 완전히 볼 수 있습니다. 사전 렌더링된 HTML 위에 추가 개선 사항이 적용됩니다.

>[!IMPORTANT]
>이 사전 렌더링 기능은 Optimize at Edge와 함께 배포하면 아래에 제시된 모든 기회에 자동으로 적용되어 AI 에이전트가 페이지를 완전히 볼 수 있도록 합니다.

대시보드 연습, 배포 단계 및 FAQ는 [콘텐츠 가시성 복구](/help/dashboards/opportunities/recover-content-visibility.md)를 참조하십시오.

### 제품 세부 사항 페이지 강화

이 영업 기회는 구매자가 대화형 상점 경험을 통해 전체 제품 컨텍스트를 확인하지만 AI 에이전트에게는 약식 HTML 스냅샷만 받는 Adobe Commerce 제품 세부 정보 페이지를 타깃팅합니다. 카탈로그 에이전트는 신뢰할 수 있는 Commerce 카탈로그를 에이전트가 표시하는 PDP와 비교하고 모든 의미 있는 간격(예: 정적 HTML에 표시되지 않는 변형 또는 사양)을 나열하며, 카탈로그 레코드나 사람 UI를 변경하지 않고 LLM 웹 크롤러에 대한 패리티를 복원하는 봇 전용 에지 응답을 배포할 수 있도록 합니다.

대시보드 연습, 배포 단계 및 FAQ는 [제품 세부 정보 페이지 강화](/help/dashboards/opportunities/enrich-product-detail-pages.md)를 참조하십시오.

### LLM 친화 요약 추가

이 기회는 LLM이 페이지의 클레임을 신속하게 이해할 수 있도록 간결한 요약과 구조화된 주요 사항의 이점을 얻을 수 있는 트래픽이 많은 페이지를 식별합니다. 각 페이지에 대해 요약이 가장 필요한 위치를 감지하고 기존 콘텐츠에 기반을 둔 페이지 또는 섹션 수준에서 AI가 생성한 요약(및 관련 있는 경우 주요 포인트)을 제안합니다. Edge에서 최적화를 사용하여 배포하면 해당 콘텐츠가 AI 에이전트가 검색하는 HTML에 삽입되므로 브랜드가 AI 답변에 표시되는 정확도가 향상됩니다.

이 영업 기회에 대한 자세한 내용은 [LLM 친화적 요약 추가](/help/dashboards/opportunities/add-llm-friendly-summaries.md)를 참조하십시오.

### 관련 FAQ 추가

이 기회는 추가 Q&amp;A 콘텐츠가 AI 기반 검색에서 사용자 의도와 프롬프트에 보다 잘 부합할 수 있는 높은 트래픽 페이지에 플래그를 지정합니다. 각 페이지에 대해 프롬프트 세트와 페이지의 콘텐츠에 연결된 AI가 생성한 FAQ 블록을 제안합니다. Edge에서 최적화를 사용하면 이러한 FAQ가 HTML에 삽입되므로 페이지를 AI 친화적이고 AI 응답이 지침을 직접 반영할 가능성이 높아집니다.

대시보드 연습, 배포 단계 및 FAQ에 대해서는 [관련 FAQ 추가](/help/dashboards/opportunities/add-relevant-faqs.md)를 참조하십시오.

### 복잡한 콘텐츠 간소화

이 기회는 AI 이해를 줄일 수 있는 길고 복잡한 단락이 있는 페이지를 찾습니다. 가독성 임계값을 초과하는 각 페이지마다 원래 의미를 유지하면서 더 간단하고 스캔하기 쉬운 AI 생성 콘텐츠를 생성합니다. 에지에 배포되면 에이전틱 트래픽에 전달되는 간소화된 콘텐츠는 LLM이 콘텐츠를 보다 충실하게 해석하고 요약할 수 있습니다.

대시보드 연습, 배포 단계 및 FAQ에 대해서는 [복잡한 콘텐츠 단순화](/help/dashboards/opportunities/simplify-complex-content.md)를 참조하십시오.

### 목차 추가

이 기회는 제목과 섹션 구조가 명확하지 않거나 누락되었기 때문에 AI 에이전트가 탐색하기 어려운 페이지를 감지합니다. 영향을 받는 각 페이지에 대해 앵커 연결 항목이 기본 섹션에 정렬된 구조화된 목차를 제안합니다. Edge에서 최적화를 사용하여 를 배포할 때 해당 목차는 HTML에 삽입되므로 모델이 사용자 쿼리를 페이지의 오른쪽 부분에 보다 안정적으로 매핑하고 이를 인용할 수 있습니다.

대시보드 연습, 배포 단계 및 조기 액세스 지침은 [목차 추가](/help/dashboards/opportunities/add-table-of-contents.md)를 참조하십시오.

### 멀티미디어 트랜스크립트 요약 추가

이 기회는 AI 에이전트가 읽을 수 있는 트랜스크립트나 텍스트 요약 없이 중요한 정보가 비디오 재생 내부에만 존재하는 페이지를 타깃팅합니다. 각 페이지에 대해 AI가 생성한 녹취록과 매체의 주요 사항에 대한 간략한 요약을 추천한다. Edge에서 최적화를 사용하면 이러한 요약이 기계가 읽을 수 있는 텍스트로 HTML에 추가되므로 에이전트는 사람 방문자가 비디오를 보고 얻은 것과 동일한 내용을 사용할 수 있습니다.

대시보드 연습, 배포 단계 및 FAQ는 [멀티미디어 성적 증명서 요약 추가](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md)를 참조하십시오.

## 자동 Optimize at Edge

각 기회마다 에지에서 최적화를 미리 보고, 편집하고, 배포하고, 라이브를 보고, 롤백할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### 미리보기

**미리보기**&#x200B;를 사용하면 제안이 실행되기 전에 그 영향을 확인할 수 있습니다. 제안을 적용한 후 예상되는 현재 페이지와 AI 최적화 버전 간의 병렬 차이가 나타납니다. 이 보기는 라이브 트래픽을 향상시키는 Edge에서 동일한 최적화 로직을 사용하지만 독립적인 미리보기 모드에서 작동합니다. 이는 검토를 위한 읽기 전용 시뮬레이션이기 때문에 라이브 트래픽에는 영향을 미치지 않습니다.

![미리보기](/help/assets/optimize-at-edge/preview.png)

### 편집

**편집**&#x200B;을 사용하면 자동 생성된 제안을 배포하기 전에 완전히 수정하거나 다시 작성할 수 있습니다. 제안을 수락하는 대신 편집 워크플로를 통해 완전히 제어합니다. 이 보기는 구조화된 편집기에서 제안된 변경 사항을 표시하여 원래 의도와 더 잘 일치하도록 텍스트를 수정할 수 있습니다. 편집된 버전은 배포된 후 AI 에이전트에게 제공됩니다.

![편집](/help/assets/optimize-at-edge/edit.png)

### 배포

**배포**&#x200B;는 선택된 제안을 게시하여 에지에서 최적화된 경험을 AI 에이전트에게 제공할 수 있도록 합니다. CDN이 완전히 라우팅되면 도메인의 모든 페이지는 일반적으로 몇 분 안에 새로운 변경 사항과 함께 활성화됩니다. 라우팅이 선택된 경로에만 설정된 경우, 허용 목록에 추가된 페이지만 최적화와 함께 활성화됩니다.

![배포](/help/assets/optimize-at-edge/deploy.png)

### 라이브 보기

**라이브 보기**&#x200B;를 통해 최적화가 에이전틱 트래픽에 대해 예상대로 작동하는지 확인할 수 있으며, 그렇지 않으면 액세스하기 어려운 보기입니다. AI 에이전트에 표시된 대로 페이지를 렌더링하는 고정 제안 아래에서 라이브 페이지를 볼 수 있습니다.

![라이브 보기](/help/assets/optimize-at-edge/view-live.png)

### 롤백

롤백은 이전에 배포된 최적화를 안전하게 되돌립니다. AI 전용 버전의 페이지는 일반적으로 몇 분 안에 이전 상태로 돌아가므로 필요할 때 최적화 실험을 안전하게 할 수 있습니다.

![롤백](/help/assets/optimize-at-edge/rollback.png)

## 추가 리소스

Edge에서 최적화 기능에 대한 자세한 내용은 다음 재생 목록 [LLM Optimizer — Edge에서 최적화](https://www.youtube.com/playlist?list=PLzbVcr6JHocVSMWBCaCw4xxjQ_VFVvFh0)를 참조하십시오.

## 자주 묻는 질문

Q: 체험판 고객이 Edge에서 최적화를 시도할 수 있습니까?

예. 체험판 고객은 하나의 최적화 기회에 액세스하여 이를 최대 10페이지에 배포할 수 있습니다. 기본적으로 이 기회는 AI 에이전트가 페이지 콘텐츠의 전체 버전에 액세스할 수 있는 콘텐츠 가시성 복구입니다.

질문. Optimize at Edge는 어떤 종류의 LLM을 목표로 합니까?

타기팅할 사용자 에이전트 목록은 온보딩 프로세스 중에 사용자가 정의합니다.

<!--
Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.
-->

질문. 아직 Optimize at Edge에 온보딩되지 않았으면 어떻게 됩니까?

필요한 설정을 완료하기 전에 **최적화 배포**&#x200B;를 클릭하면 사이트에 아무것도 적용되지 않습니다. 대신 팝업 대화 상자가 나타나 `llmo-at-edge@adobe.com`의 팀에 문의하여 온보딩 지원을 받으라는 메시지가 표시됩니다. 온보딩이 완료될 때까지 감지된 기회와 제안을 계속 탐색할 수 있지만 원클릭 배포 워크플로는 비활성 상태로 유지됩니다.

Q: 콘텐츠가 소스에서 업데이트되면 어떻게 됩니까?

기본 소스 페이지가 변경되지 않는 한 캐시에서 최적화된 버전의 페이지를 제공합니다. 그러나 **콘텐츠 가시성 복구**&#x200B;를 위해 소스가 변경되면 시스템이 자동으로 새로 고침되므로 AI 에이전트는 항상 최신 콘텐츠를 수신합니다. 이는 사이트의 모든 콘텐츠 업데이트가 해당 창 내에서 새로운 최적화를 트리거하도록 낮은 캐시 TTL(Time to Live) 설정(분 단위)을 사용하기 때문입니다. **LLM 친화 요약 추가**와 같은 콘텐츠 기회를 위해 LLM Optimizer는 소스 페이지에서 변경 사항을 모니터링합니다. 변경 사항이 감지되면 에이전트가 볼 수 있는 페이지와 사람이 볼 수 있는 페이지 간의 콘텐츠 이동을 방지하기 위해 최적화를 일시 중지하고 사람이 검토할 수 있도록 플래그를 지정합니다.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

질문. Optimize at Edge는 Adobe Edge Delivery Service(EDS)를 사용하는 사이트에만 적용됩니까?

아니요. Optimize at Edge는 CDN에 구애받지 않으며 Adobe의 EDS Stack에 배포된 아키텍처뿐만 아니라 모든 프론트엔드 아키텍처에서 작동합니다.

질문. Optimize at Edge 사전 렌더링 기존 서버측 렌더링(SSR)과 어떻게 다릅니까?

둘 다 서로 다른 문제를 해결하고 함께 일할 수 있습니다. 기존 SSR은 서버측 콘텐츠를 렌더링하지만 나중에 브라우저에 로드된 콘텐츠는 포함하지 않습니다. Optimize at Edge 사전 렌더링은 JavaScript와 클라이언트측 데이터가 로드된 후 페이지를 캡처하여 CDN 에지에서 완전히 조립된 버전을 생성합니다. SSR은 사용자 경험을 개선하는 데 중점을 두고 있으며, Optimize at Edge는 LLM의 웹 경험을 개선합니다.

Q. 복구 콘텐츠 가시성(즉, 사전 렌더링)가 클로킹 상태입니까? 다른 버전의 페이지가 AI 에이전트에 제공되는 것 같습니다.

아니요. 사전 렌더링은 AI 에이전트가 사람 방문자와 SEO 봇이 이미 본 것과 동일한 콘텐츠를 볼 수 있도록 합니다. 많은 사이트가 JavaScript을 사용하여 의미 있는 콘텐츠를 로드하지만 일반적인 AI 에이전트는 이 콘텐츠를 실행하지 않으므로 에이전트는 페이지의 많은 부분을 놓칠 수 있습니다. 사전 렌더링은 전체 텍스트를 캡처하는 정적 스냅샷을 생성하여 에이전트가 사람 및 검색 엔진과 동일한 정보를 받습니다. LLM에 대한 **컨텐츠 패리티를 복원**&#x200B;합니다. 실제 컨텐츠를 추가하거나 변경하지 않습니다.

Q. 새 사본이 에이전트에게 제공되는 페이지에 표시되는 LLM 친화적 요약 추가 와 같은 다른 콘텐츠 기회는 어떻게 됩니까? 저거 클로킹 하는 거야?

아니요. Edge에서 최적화해도 사람 사용자와 SEO 웹 크롤러가 액세스할 수 없는 정보는 포함되지 않습니다. 이 서비스는 페이지에 이미 존재하는 콘텐츠를 재편성하거나 요약해 AI 에이전트가 보다 쉽게 해석할 수 있도록 한다. 누군가가 AI 답변에서 사이트에 대한 링크를 따라가도 라이브 페이지에서 동일한 기본 정보를 찾을 수 있습니다.

Q. 모든 URL이 아닌 일부 URL에 대한 최적화를 배포하면 어떻게 됩니까?

명시적으로 최적화된 URL만 수정됩니다. 배포된 기회가 있는 URL의 경우, AI 에이전트는 최적화된 버전을 받습니다. 배포된 기회가 없는 URL의 경우, 당사 서비스는 변경 사항을 적용하거나 최적화 캐시 레이어에 저장하지 않고 원본 페이지를 그대로 프록시합니다. 이렇게 하면 나머지 사이트에 영향을 미치지 않고 최적화를 선택적으로 배포할 수 있습니다.
