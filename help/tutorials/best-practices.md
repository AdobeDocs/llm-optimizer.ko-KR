---
title: LLM Optimizer 우수 사례
description: AI 검색에서 브랜드 가시성을 높이기 위한 LLM 최적화 모범 사례를 살펴보십시오. 콘텐츠 벤치마킹 및 최적화에 대한 통찰력.
source-git-commit: 70d0b8c042cbdd87bab1c9ef3139af9c72a4a09d
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---


# 모범 사례

[초안]

LLM 최적화(GEO(Generative Engine Optimization) 또는 AEO(Answer Engine Optimization) 또는 AIO(AI Optimization)라고도 함)는 ChatGPT, Perplexity, Copilot, Gemini 및 기타 LLM 기반 도우미에 걸쳐 AI가 생성한 답변 내에서 브랜드와 콘텐츠를 보고 신뢰할 수 있으며 검색할 수 있도록 하는 방법입니다.

기존의 SEO가 1페이지 등급 획득에 도움이 되었다면, LLM 최적화는 답변 엔진 내에서 AI 인용과 가시성을 획득하는 데 도움이 됩니다. Adobe LLM Optimizer을 사용하면 응답 엔진 내에서 브랜드의 가시성을 측정하고 향상시킬 수 있습니다.

이 문서에서는 Adobe LLM Optimizer을 사용하여 AI 기반 검색 환경에서 가시성과 영향력을 측정하고 향상시키는 것과 관련된 모범 사례에 대해 설명합니다.

## LLM 브랜드 가시성 잠금 해제

LLM(대규모 언어 모델) 최적화는 AI 기반 환경에서 브랜드를 검색하고 참조하는 방법을 전환하고 있습니다. Adobe의 LLM Optimizer은 브랜드 가시성을 향상시키는 구조화된 접근 방식을 제공합니다.

LLM 가시성을 향상시키려면 다음 단계를 따르십시오.

1. **분석:** 브랜드가 LLM의 주요 고객 프롬프트에 어떻게 표시되는지 검토합니다.
2. **계획:** 집중 캠페인에 대해 유사한 의도를 가진 프롬프트 클러스터를 대상으로 합니다.
3. **동작:** 시간 경과에 따른 LLM 가시성의 변경 사항을 구현하고 모니터링합니다.
4. **조정:** 최적기의 실행 가능한 통찰력을 기반으로 전략을 구체화합니다.

<!--insert image-->

이러한 단계를 이해하고 활용하면 AI가 정보 발견의 중심이 되므로 브랜드의 연관성을 유지하는 데 도움이 될 수 있습니다.

## LLM과 SEO: 주요 차이점

좋은 LLM 전략은 좋은 SEO 전략 위에 구축됩니다. SEO 전략은 모든 LLM 최적화의 기본입니다. 현재 SEO 트래픽은 대부분의 웹 사이트에 대한 트래픽을 가장 많이 발생시키는 요소이므로 브랜드의 가시성 전략에 매우 중요합니다.

LLM에 대한 최적화는 몇 가지 주요 차이점 때문에 기존 SEO와 다르다는 것을 이해하는 것이 중요합니다.

* LLM은 인덱스가 아닌 토큰을 사용합니다. 결과는 인덱싱된 웹 페이지가 아닌 훈련된 데이터에서 생성되지만, LLM은 검색-증강 생성(RAG)을 통해 신속한 응답을 향상시키기 위해 검색 엔진을 사용합니다.
* RAG를 통한 실시간 정보: 검색 엔진은 실시간 데이터를 사용하는 반면 RAG를 통해 LLM은 최신 정보를 가져와 환각을 줄일 수 있습니다.
* 제한된 클라이언트측 JS 렌더링: 현재 LLM은 클라이언트측 JavaScript을 처리하지 않으므로 표시되는 콘텐츠에 영향을 줍니다.

이러한 기본적인 차이점 중 일부 때문에 LLM 전략에서는 다음 사항을 고려해야 합니다.

* 브랜드 언급은 LLM에 대한 링크보다 더 중요합니다. LLM은 백링크보다 콘텐츠 관련성 및 브랜드 존재의 우선 순위를 지정합니다. SEO와 달리 LLM은 링크를 사용하여 권한을 결정하지 않는다.
* 콘텐츠 신선도 문제: LLM은 최근에 업데이트된 콘텐츠의 우선 순위를 지정합니다. (검색 엔진도 시간에 민감한 쿼리에 대해 이를 우선 고려하지만, 다른 값에 더 많이 의존합니다.)
* 언급 및 인용의 형태로 벌어들이는 것(제3자)은 매우 중요하다.

## 전략 캠페인 계획

성공적인 LLM 최적화 캠페인을 구축하려면 다음이 필요합니다.

가치가 높은 주제 식별: 비즈니스 목표 및 고객 요구에 따라 신속한 의도를 파악합니다.
경쟁업체 언급 표시: 경쟁업체가 인용되는 프롬프트에 중점을 두어 브랜드 포함 기회를 나타냅니다.
의도별 그룹 프롬프트: 주제 및 검색 필드를 사용하여 벤치마킹 가시성을 위한 유사한 사용자 목표를 클러스터링합니다.
현실적인 브랜드 포함 평가: EEAT(경험, 전문 지식, 권한, 신뢰도) 및 YYYL(Your Money or Your Life) 표준과 같은 요소를 고려하여 브랜드를 신뢰할 수 있게 언급할 수 있는지 평가합니다.

이 전략적 접근 방식은 LLM 가시성을 목표로 한 데이터 기반 개선 사항을 보장합니다.


## 실행 가능한 최적화 단계

LLM Optimizer은 [기회](/help/dashboards/opportunities.md) 대시보드에서 최적화 기회를 제안합니다.

다음은 LLM에서 브랜드 가시성을 높이기 위해 고려해야 할 몇 가지 실제 작업입니다.

* Wikipedia 페이지 업데이트: 회사 및 인용 페이지가 최신 상태이고 관련성이 있는지 확인합니다.
* LLM 액세스 활성화: robots.txt 및 CDN 설정을 모니터링하여 AI 봇이 차단되지 않도록 합니다.
* 콘텐츠 개선: 페이지 콘텐츠의 10~15%를 새로 고치고, 참조를 추가하고, 헤더(H1, H2, H3)로 구조를 개선합니다.
* FAQ 추가: 사용자 쿼리를 처리하기 위해 프롬프트 분석을 기반으로 관련 FAQ를 통합합니다.
* Reddit/Quora에서 브랜드 언급 늘리기: LLM 소스 인용이 있는 사용자 생성 콘텐츠 플랫폼에 기여합니다. 트리거할 수 있는 대로 여기에 접근하는 방법에 주의하십시오.

이러한 단계를 일관되게 수행하면 AI 기반 검색 결과에서 브랜드의 존재감이 크게 향상될 수 있습니다.



## LLM 가시성이란 무엇입니까?

LLM 가시성은 ChatGPT나 다른 AI 모델과 같은 도구로 생성된 응답에 브랜드가 표시되는 빈도와 정도에 관한 것입니다.

## LLM 진행률을 측정하는 방법

웹 사이트의 가시성을 벤치마킹하고 노력이 얼마나 잘 작동하는지 확인하려면 다음 주요 지표를 추적하십시오.

* **언급:** 브랜드가 응답에서 몇 번이나 언급되었습니까?
* **인용:** LLM에서 콘텐츠 또는 소스를 사용하여 질문에 답변하는 빈도입니다.
* **감정:** 브랜드에 대한 언급이 긍정적인지, 중립적인지 또는 부정적인지 여부.
* **위치:** 브랜드가 응답에서 언급되는 위치(예: 첫 번째, 중간 또는 마지막).

이러한 모든 요소가 **가시성** 점수로 결합되므로 LLM 응답에서 브랜드의 존재감이 얼마나 강한지 알 수 있습니다.

## 가시성 변경 사항을 추적하는 방법

다음은 LLM에서 브랜드의 가시성을 주시할 수 있는 방법입니다.

1. 현재 가시성 확인
   * Adobe LLM Optimizer은 브랜드가 얼마나 자주 언급되고 인용되는지, LLM 응답에 감정이 무엇인지 보여 줍니다. 브랜드 유무 대시보드를 참조하십시오.
   * 브랜드가 언급되고 누락된 위치를 확인하는 메시지(질문)를 확인합니다.
   * 가시성을 경쟁사와 비교하여 누적 상태를 확인합니다.
   * LLM에서는 정보를 찾기 위해 종종 Reddit, Quora 및 Wikipedia와 같은 사용자 생성 플랫폼에서 어떻게 표시되는지 확인합니다.
   * 에이전트 트래픽에서 어떻게 표시되는지 확인하십시오. 에이전트 트래픽은 종종 홈 페이지로 이동하지 않습니다. 에이전트가 방문하는 페이지를 살펴볼 필요가 있습니다.
   * 콘텐츠가 LLM에 표시되고 액세스할 수 있는지 확인하십시오. Chrome 플러그인을 사용하여 AI 에이전트가 볼 수 있는 항목을 확인할 수 있습니다.

1. 전략 계획
   * 사람들이 묻는 말에 따라 유사한 프롬프트를 함께 그룹화합니다.
   * 고객에게 가장 중요한 프롬프트에 초점을 맞춥니다.
   * 특정 프롬프트에 대해 브랜드가 언급될 가능성이 높은지 확인하십시오.
   * 콘텐츠에 전문 지식, 신뢰성 및 권한(EEAT)이 표시되는지 확인하십시오.

1. 콘텐츠 개선
   * LLM Optimizer Opportunity 를 사용하여 사이트에 대해 특별히 권장되는 즉각적인 변경을 수행합니다. [기회](/help/dashboards/opportunities.md)를 참조하십시오(그런 다음 결과 측정). 기회 섹션을 정기적으로 검토하고 제공된 권장 사항에 대한 조치를 취하십시오.
   * 웹 사이트 및 기타 콘텐츠를 업데이트하여 타깃팅하려는 프롬프트에 더 연관성이 있게 만듭니다.
   * 사람들이 물을 수 있는 일반적인 질문에 답하는 FAQ를 페이지에 추가합니다.
   * LLM이 콘텐츠를 쉽게 찾고 읽을 수 있도록 하십시오. 차단된 페이지 또는 웹 사이트 코드 문제와 같은 문제를 수정합니다.
   * Wikipedia와 Reddit와 같은 플랫폼에 대한 기여는 편견 없고 비상업적이며 가치를 더합니다.
   * Adobe LLM Optimizer을 사용하여 시간이 지남에 따라 가시성이 어떻게 변하는지를 추적합니다.
   * 경쟁자들이 더 자주 언급되는 것을 발견한다면, 앞서가기 위해 전략을 조정하세요.
   * 사람들이 검색하고 묻는 내용에 맞게 콘텐츠를 계속 업데이트합니다.


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



