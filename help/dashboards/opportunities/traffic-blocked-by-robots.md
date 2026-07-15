---
title: robots.txt로 차단된 트래픽
description: robots.txt 파일이 AI 에이전트의 콘텐츠 액세스를 차단할 때 LLM Optimizer가 감지하는 방법과 이를 수정하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-07-15T18:04:23.113Z'
TQID: 'https://experienceleague.adobe.com/rk82xEtvYBr47tTNzhC6ZbFw1Bim3Otr-D2ncBWPmwM'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
subfeature_v2: id: e0ec491f-fe51-42b6-801c-1c0dfcc0e64f
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 817
ht-degree: 100%

---


# robots.txt로 차단된 트래픽

내 `robots.txt` 파일이 사이트에 액세스할 수 있는 크롤러를 제어합니다. AI 에이전트가 일반 크롤러가 액세스할 수 있는 콘텐츠를 선택적으로 차단하면 해당 에이전트는 해당 콘텐츠를 색인화하거나 인용하여 AI 생성 응답에서 브랜드의 가시성을 직접적으로 저하시킵니다.

robots.txt로 차단된 트래픽 기회는 상위 페이지에 대해 `robots.txt` 파일을 분석하고 연결할 수 있는 콘텐츠에 AI 에이전트가 액세스하지 못하도록 하는 규칙을 식별합니다. 개별 `robots.txt` 행 수준에서 검색 결과를 보여 주기 때문에 전체 파일을 수동으로 감사하는 대신 특정 지시문을 검토하고 업데이트할 수 있습니다.

두 개의 주요 지표를 한눈에 보여 줍니다.

- **총 URL** - `robots.txt`에서 차단 규칙의 영향을 받는 URL의 수입니다.
- **차단된 에이전트** - 해당 URL에 액세스하지 못하도록 차단된 AI 에이전트 수입니다.

![robots.txt로 차단된 트래픽 대시보드](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-overview.png)

## 작동 방식

LLM Optimizer는 `robots.txt` 파일을 가져와 상위 페이지를 6개의 주요 AI 에이전트 사용자 에이전트와 비교합니다.

- ClaudeBot
- GPTBot
- OAI-SearchBot
- OAI-User
- PerplexityBot
- Perplexity-User

URL은 **와일드카드(`*`) 사용자 에이전트에 대해 허용되지만 특정 AI 에이전트에 허용되지 않을** 때만 플래그가 지정됩니다. 모든 크롤러가 동일하게 제한되는 포괄적인 차단은 보고되지 않습니다. 감사는 특히 GEO에 대해 가장 액션 가능한 검색 결과를 나타내는 선택적 AI 에이전트 제외를 타기팅합니다.

>[!NOTE]
>이 기회는 제안을 개발하거나 전달하는 데 AI를 사용하지 않습니다. 검색 결과는 전적으로 `robots.txt` 파일에 대한 직접 분석을 기반으로 합니다.

결과는 **robots.txt** 및 **에이전트에서 차단한 트래픽 세부 정보** 두 탭에 표시됩니다.

## robots.txt

이 탭에는 빨간색으로 강조 표시된 차단 지시문이 있는 전체 `robots.txt` 파일이 표시됩니다. 강조 표시된 각 행은 하나 이상의 AI 에이전트가 공개적으로 액세스할 수 있는 URL에 액세스하지 못하도록 선택적으로 차단하는 규칙을 나타냅니다.

![차단 지시문이 강조 표시된 robots.txt 보기](/help/dashboards/opportunities/assets/traffic-blocked-by-robots-robotstxt.png)

강조 표시된 지시문을 클릭하면 영향 및 제안된 수정 사항에 대한 자세한 정보가 표시됩니다.

## 에이전트에서 차단한 트래픽 세부 정보

이 탭에서는 AI 에이전트에서 구성한 차단된 트래픽에 대한 분류를 제공합니다. 차단된 각 에이전트에 대해 다음과 같이 표시됩니다.

- **문제 설명** - 차단되는 에이전트와 중요한 이유에 대한 설명입니다.
- **해결 방법** - `robots.txt` 파일을 열고 영향을 받는 각 URL 옆에 나열된 특정 행 번호를 검토하는 지침입니다.
- 차단된 각 페이지의 **라인**, **순위** 및 **URL**&#x200B;이 있는 영향을 받는 URL 테이블입니다.

각 에이전트(예: OAI-User, GPTBot, OAI-SearchBot)에는 에이전트당 블록을 처리할 수 있도록 자체 하위 탭이 있습니다.

## 수정 방법

차단된 에이전트 검색 결과를 해결하려면 `robots.txt` 파일을 열고 에이전트에서 차단한 트래픽 세부 정보 탭에서 영향을 받는 각 URL 옆에 표시된 행 번호를 찾습니다. 관련 AI 에이전트에 대한 불허 지시문을 업데이트하거나 제거하여 영향을 받는 URL에 대한 액세스를 허용합니다.

예를 들어 특정 페이지에서 GPTBot의 차단을 해제하려면 지시문을 제거하거나 업데이트합니다.

```
User-agent: GPTBot
Disallow: /blog/cold-brewing-101
```

`robots.txt` 파일이 업데이트되고 다시 게시되면 LLM Optimizer가 다음 감사 실행에서 변경 사항을 감지하고 제안을 해결된 것으로 표시합니다.

## 데모에서 사용해 보기

Frescopa 데모 환경을 사용하여 robots.txt로 차단된 트래픽 기회 액션을 참조하십시오.

[Frescopa 데모에서 robots.txt로 차단된 트래픽 보기](https://play.llmo.now/org/demo-org/opportunities/blocked-urls-llm-agents)

## 자주 묻는 질문

**GEO에 AI 에이전트 차단이 중요한 이유는 무엇입니까?**

생성형 엔진 최적화를 사용하려면 AI 크롤러가 사이트 콘텐츠에 액세스하고 콘텐츠를 색인화할 수 있어야 합니다. AI 에이전트를 차단하면 AI가 생성한 응답에 페이지가 표시되지 않아 인용, 브랜드 언급 및 전체 AI 가시성이 줄어듭니다. 트래픽이 많은 페이지를 차단한 것 하나로도 AI 기반 브랜드 노출의 상당한 손실을 나타낼 수 있습니다.

**포괄적인 차단과 선택적 차단의 차이점은 무엇입니까?**

포괄적 차단은 일반 웹 크롤러를 포함한 모든 크롤러가 페이지에서 제한되는 것을 의미합니다. 선택적 차단은 일반 크롤러는 페이지에 액세스할 수 있지만 특정 AI 에이전트는 액세스할 수 없음을 의미합니다. 이 기회는 AI 에이전트를 공개된 콘텐츠에서 의도적 또는 우발적으로 제외하는 것을 의미하기 때문에 선택적 차단에만 플래그를 지정하며, 이는 가장 액션 가능한 검색 결과입니다.

**LLM Optimizer에서 확인하는 AI 에이전트는 무엇입니까?**

LLM Optimizer는 ClaudeBot, GPTBot, OAI-SearchBot, OAI-User, PerplexityBot 및 Perplexity-User에 대해 확인합니다.

**특정 AI 에이전트를 의도적으로 차단하려면 어떻게 해야 합니까?**

플래그가 지정된 각 지시문을 검토하고 의도적으로 블록을 유지하도록 선택할 수 있습니다. 무시된 제안은 감사 실행 동안 유지되며 `robots.txt` 파일이 변경되고 규칙이 다시 나타나지 않는 한 다시 표시되지 않습니다.

**LLM Optimizer는 시간이 지남에 따라 내 robots.txt의 변경 사항을 어떻게 추적합니까?**

LLM Optimizer는 해싱을 사용하여 실행 동안 `robots.txt` 콘텐츠를 추적합니다. 이전에 해결된 차단 규칙이 다시 나타나면(예: `robots.txt` 업데이트 후) 새 제안으로 다시 표시됩니다.

**상위 페이지는 어떻게 결정됩니까?**

페이지는 가장 트래픽이 많은 SEO 페이지, CDN 로그에서 상위 AI 에이전트 방문 URL 및 사이트 구성에 지정된 사용자 정의 URL의 조합에서 가져온 것입니다.
