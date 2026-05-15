---
title: 제품 세부 사항 페이지 강화
description: LLM Optimizer이 AI 에이전트에서 카탈로그 데이터가 숨겨진 제품 페이지를 식별하는 방법과 Adobe Commerce에서 제공하는 에지 기반 최적화 및 제품 카탈로그 인사이트를 사용하여 해당 가시성을 복구하는 방법을 알아봅니다.
feature: Opportunities
autotag-review: '2026-05-15T17:46:41.487Z'
TQID: 'https://experienceleague.adobe.com/l4hTGNNg1NW40ceI00P41KZBSGcqmr-t1RWM-NXtRV4'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 1210
ht-degree: 0%

---


# 제품 세부 사항 페이지 강화

AI 에이전트는 완전히 이해할 수 있는 제품만 추천할 수 있습니다. 대부분의 상점에서 제품 페이지는 사람 쇼핑객을 위해 설계되었습니다. 따라서 이러한 제품은 JavaScript 렌더링 탭, 확장 가능한 패널, 쇼핑 마법사, 대화형 모델 및 표면 제품 변형, 사양 및 기능에 대한 링크를 사용합니다. AI 에이전트는 제품 세부 사항 페이지의 깊이를 분석하지 않습니다. 즉, 사람 방문자가 AI 기반 검색을 지원하는 LLM 웹 크롤러는 이 풍부한 제품 데이터를 완전히 볼 수 있더라도 볼 수 없습니다.

제품 세부 사항 페이지 강화 영업 기회는 Adobe Commerce 카탈로그에서 이 가시성 차이가 존재하는 제품 페이지를 식별합니다. Adobe Commerce 카탈로그를 기반으로 AI 에이전트가 상점 전면에서 액세스할 수 있는 내용과 카탈로그에서 사용 가능한 전체 제품 데이터를 비교하고 AI 에이전트 보기에서 누락된 모든 속성, 변형 및 제품 특성의 깊이를 표시합니다.

다음 주요 지표를 한눈에 볼 수 있습니다.

- **제품 페이지** — 카탈로그 데이터 표시 간격이 있는 식별된 모든 제품 세부 정보 페이지의 목록입니다.
- **에이전트 트래픽** — 콘텐츠를 검색, 검색 또는 참여하기 위해 사용자를 대신하여 동작하는 자율 AI 에이전트(예: LLM 기반 도우미 또는 봇)에 의해 시작 및 구동되는 사이트에서의 총 방문 횟수 및 상호 작용 수입니다.

![제품 세부 정보 페이지 대시보드 강화](/help/dashboards/opportunities/assets/enrich-product-detail-pages-overview.png)

[Edge에서 최적화](https://experienceleague.adobe.com/ko/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge)를 사용하여 이 기회를 최적화할 수 있습니다. 최적화는 인간 방문자에게 영향을 주지 않고 AI 에이전트에게만 제공되며(보트 전용 제공), CDN 계층에 적용되므로 CMS 또는 카탈로그 변경이 필요하지 않으며, 개발자 참여 없이도 몇 분 안에 적용할 수 있으므로 대규모 제품 카탈로그의 빠르고 위험도가 낮은 배포 경로가 됩니다.

## 작동 방식

Adobe Commerce 카탈로그 에이전트는 변형, 더 깊은 제품 관계, 속성, 패싯, 카테고리 메타데이터 및 모든 제품 특성을 포함한 전체 제품 카탈로그 데이터를 읽습니다. 그런 다음 해당 상점 PDP에서 AI 에이전트가 실제로 액세스할 수 있는 것과 데이터를 비교합니다. 카탈로그 데이터가 AI 웹 크롤러에서 숨겨져 있는 페이지는 주요 트래픽 볼륨에 따라 우선 순위가 지정된 **제안이 있는 URL** 테이블에 표시됩니다.

영향을 받는 각 제품 페이지에 대해 LLM Optimizer은 다음을 제공합니다.

- **AI 분석 미리 보기** — 제품 변형, 크기 옵션, 재질 사양 및 호환성 세부 정보 등 복구 가능한 데이터 포인트 목록을 포함하여 AI 에이전트 보기에서 누락된 카탈로그 정보와 LLM 기반 제품 검색에 중요한 이유에 대한 전체 목록입니다.

이 수정 사항은 CDN 계층에서 LLM 사용자 에이전트에게 완전히 사전 렌더링된 AI 친화적인 Edge 스냅숏을 제공하는 Adobe의 에지 기반 배포 기능인 [Optimize at HTML](https://experienceleague.adobe.com/ko/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge)을(를) 사용하여 적용됩니다. 이렇게 하면 Commerce 카탈로그나 사람이 볼 수 있는 상점 UI를 조작하지 않고도 이전에 숨겨진 모든 카탈로그 데이터(제품 변형, 기술 사양 및 기능 세부 사항 포함)를 복구할 수 있습니다.

제안 테이블이 있는 ![URL](/help/dashboards/opportunities/assets/enrich-product-detail-pages-suggestions.png)

## 제안 사항이 있는 URL

**제안이 있는 URL** 테이블에는 최적화의 이점을 얻을 수 있는 식별된 모든 제품 페이지가 나열됩니다. 각 제품 URL에 대해 다음 작업을 수행할 수 있습니다.

- 누락된 카탈로그 정보와 AI 기반 검색 기능에 중요한 이유를 포함하여 AI 분석을 보려면 **미리 보기**&#x200B;를 참조하십시오.
- 최적화가 배포되고 확인되면 **고정으로 표시**
- 머천다이징 전략과 관련이 없는 **제안 무시**

제안은 다음 세 가지 보기로 구성됩니다. **현재 제안**, **수정 제안** 및 **무시된 제안**. 제안이 배포되면 상태가 **최적화됨**&#x200B;이고 작업이 **라이브 보기**&#x200B;인 수정 제안으로 이동하여 데이터 보강이 에이전트 트래픽에 대해 라이브되는지 확인합니다. 언제든지 수정된 제안을 롤백할 수 있습니다.

## 최적화 배포

제안을 검토하고 최적화할 제품 페이지를 선택했으면 **최적화 배포**&#x200B;를 클릭하여 CDN 에지에서 데이터 강화를 게시합니다. **Edge에 배포** 확인 대화 상자에 선택한 제품 URL, 최적화 유형 및 적용 중인 데이터 보강이 표시됩니다. 배포 후 성공적으로 최적화된 제품 페이지를 확인하는 화면이 표시됩니다.

최적화는 CDN 에지 계층을 통해 AI 사용자 에이전트에만 전달됩니다. 사람 방문자는 PDP 디자인, 페이지 성능 또는 브랜드 경험을 변경하지 않고 이전과 동일하게 기존 상점 경험을 계속 볼 수 있습니다.

>[!NOTE]
>
>최적화를 배포하려면 (1) LLM Optimizer을 Adobe Commerce에 연결하고 (2) Edge 온보딩 프로세스에서 최적화해야 합니다.

Commerce 인스턴스가 아직 LLM Optimizer에 연결되어 있지 않은 경우 강화 기능이 적용되기 전에 연결 설정으로 이동됩니다.

아직 온보딩하지 않은 경우 **최적화 배포**&#x200B;를 클릭하면 온보딩 프로세스로 이동합니다. Edge에서 최적화 작동 방법, 지원되는 CDN 공급자 및 온보딩 프로세스에 대한 자세한 내용은 [Edge에서 최적화](https://experienceleague.adobe.com/ko/docs/llm-optimizer/using/resources/optimize-at-edge/overview#what-is-optimize-at-edge) 페이지를 참조하십시오.

![Edge에 배포 대화 상자](/help/dashboards/opportunities/assets/enrich-product-detail-pages-deploy.png)

## 데모에서 사용해 보기

Frescopa 데모 환경을 사용하여 제품 세부 사항 페이지 강화 영업 기회를 참조하십시오.

[Frescopa 데모에서 제품 세부 사항 페이지 보기](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## 자주 묻는 질문

**AI 에이전트에서 제품 카탈로그 데이터를 숨기는 이유는 무엇입니까?**

Commerce 상점들은 사람 쇼핑객들을 위해 지어졌습니다. 제품 특성, 변형, 크기 옵션, 재질 세부 사항 및 기타 기술 사양은 종종 탭, 축소 가능한 패널, 팝업 양식, 링크 및 쇼핑 마법사와 같은 JavaScript 기반 상호 작용을 통해 표면화됩니다. AI 에이전트는 제품 세부 사항 페이지의 깊이를 구문 분석하지 않으므로, 이 모든 데이터는 제품 카탈로그에 완전히 있어도 LLM 웹 크롤러에게 표시되지 않습니다. 그 결과 AI 에이전트가 실제 사용 가능한 제품 정보의 극히 일부를 기반으로 제품 추천을 하게 된다.

**이 최적화는 어떤 유형의 제품 데이터를 복구합니까?**

카탈로그 에이전트는 Adobe Commerce 카탈로그에서 현재 AI 에이전트용 상점에서 액세스할 수 없는 모든 제품 정보를 복구합니다. 여기에는 제품 문자, 관계, 변형(크기, 색상, 구성), 기술 사양 및 속성, 호환성 세부 정보, 카테고리 메타데이터 및 Facet 값이 포함됩니다.

**이 최적화가 사람 방문자, SEO 보트 또는 상점 성능에 영향을 줍니까?**

아니요. Edge에서 최적화 는 AI 사용자 에이전트만 타겟팅합니다. 사람 방문자와 SEO 봇은 경험, 페이지 로드 성능 또는 상점 디자인을 변경하지 않고 이전과 동일하게 원본 제품 페이지를 받습니다.

**Commerce 카탈로그, CMS을 변경하거나 개발자를 참여시켜야 합니까?**

아니요. 최적화는 CDN 에지 계층에서 적용되며, Adobe Commerce 카탈로그를 변경하거나 코드 배포 및 개발자 참여를 변경할 필요가 없습니다. Edge에서 최적화하기 위해 온보딩하면 LLM Optimizer 인터페이스에서 직접 몇 분 안에 강화를 배포하고 롤백할 수 있습니다.

**배포 후 제품 데이터가 변경되면 어떻게 됩니까?**

제품 세부 사항 페이지 강화 기회를 위해 LLM Optimizer은 낮은 캐시 TTL 설정을 사용하므로 Commerce 카탈로그의 모든 제품 업데이트가 몇 분 내에 새로 고침을 트리거합니다. AI 에이전트는 항상 사용 가능한 최신 제품 데이터를 받습니다.
