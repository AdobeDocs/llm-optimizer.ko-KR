---
title: 모범 사례 안내서
description: 문서 개요입니다. SEO 분석가 및 PR 및 커뮤니케이션 관리자 포함
source-git-commit: c5f99f6665ab44ca23cd4a41f9d4b3ccf2e4007e
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---


# 모범 사례

## LLM 브랜드 가시성 잠금 해제

LLM(대규모 언어 모델) 최적화는 AI 기반 환경에서 브랜드를 검색하고 참조하는 방법을 전환하고 있습니다. Adobe의 LLM Optimizer은 브랜드 가시성을 향상시키는 구조화된 접근 방식을 제공합니다.

다음 단계를 수행하면 LLM 가시성을 개선할 수 있습니다.

1. 분석: LLM에서 주요 고객 프롬프트에 브랜드가 표시되는 방식을 검토하십시오.
2. Planning: 집중 캠페인에 대해 유사한 의도를 갖는 프롬프트 클러스터를 타겟팅합니다.
3. 작업: 변경 사항을 구현하고 시간에 따른 LLM 가시성 변화를 모니터링합니다.
4. 적응: 최적기의 실행 가능한 통찰력을 기반으로 전략을 구체화합니다.
5. 이러한 단계를 이해하고 활용하면 AI가 정보 발견의 중심이 될 때 브랜드의 연관성을 유지하는 데 도움이 될 수 있습니다.

## LLM과 SEO: 주요 차이점

LLM에 대한 최적화는 기존 SEO와 근본적으로 다릅니다.

* LLM은 색인이 아닌 토큰을 사용합니다. 결과는 색인화된 웹 페이지가 아닌 훈련된 데이터에서 생성됩니다.
* 브랜드 언급은 링크보다 더 중요합니다. LLM은 백링크보다 콘텐츠 관련성 및 브랜드 존재의 우선 순위를 지정합니다.
* RAG를 통한 실시간 정보: Retrieval-Augmented Generation을 통해 LLM은 최신 정보를 가져올 수 있으므로 환각을 줄일 수 있습니다.
* 제한된 클라이언트측 JS 렌더링: 현재 LLM은 클라이언트측 JavaScript을 처리하지 않으므로 표시되는 콘텐츠에 영향을 줍니다.
* 링크 권한 속성 없음: SEO와 달리 LLM은 링크를 사용하여 권한을 결정하지 않습니다.
* 이러한 차이점을 인식하는 것은 효과적인 LLM 최적화에 중요합니다.


## 실행 가능한 최적화 단계

LLM Optimizer은 Opportunities 대시보드에서 최적화 기회를 제안합니다.

다음은 LLM에서 브랜드 가시성을 높이기 위한 몇 가지 실제 작업입니다.

* Wikipedia 페이지 업데이트: 회사 및 인용 페이지가 최신 상태이고 관련성이 있는지 확인합니다.
* LLM 액세스 활성화: robots.txt 및 CDN 설정을 모니터링하여 AI 봇이 차단되지 않도록 합니다.
* 콘텐츠 개선: 페이지 콘텐츠의 10~15%를 새로 고치고, 참조를 추가하고, 헤더(H1, H2, H3)로 구조를 개선합니다.
* FAQ 추가: 사용자 쿼리를 처리하기 위해 프롬프트 분석을 기반으로 관련 FAQ를 통합합니다.
* Reddit/Quora에서 브랜드 언급 늘리기: LLM 소스 인용이 있는 사용자 생성 콘텐츠 플랫폼에 기여합니다.

이러한 단계를 일관되게 수행하면 AI 기반 검색 결과에서 브랜드의 존재감이 크게 향상될 수 있습니다.


## 전략 캠페인 계획

성공적인 LLM 최적화 캠페인을 구축하려면 다음이 필요합니다.

가치가 높은 주제 식별: 비즈니스 목표 및 고객 요구에 따라 신속한 의도를 파악합니다.
경쟁업체 언급 표시: 경쟁업체가 인용되는 프롬프트에 중점을 두어 브랜드 포함 기회를 나타냅니다.
의도별 그룹 프롬프트: 주제 및 검색 필드를 사용하여 벤치마킹 가시성을 위한 유사한 사용자 목표를 클러스터링합니다.
현실적인 브랜드 포함 평가: EEAT(경험, 전문 지식, 권한, 신뢰도) 및 YYYL(Your Money or Your Life) 표준과 같은 요소를 고려하여 브랜드를 신뢰할 수 있게 언급할 수 있는지 평가합니다.

이 전략적 접근 방식은 LLM 가시성을 목표로 한 데이터 기반 개선 사항을 보장합니다.


이 보고서는 LLM(Large Language Models)에서 브랜드의 가시성이 시간에 따라 어떻게 변하는지를 이해하는 데 도움이 되도록 설계되었습니다. LLM이 생성한 응답에서 브랜드의 존재를 추적, 개선 및 측정하는 단계를 안내합니다.

LLM 가시성이란?
LLM 가시성은 ChatGPT나 다른 AI 모델과 같은 도구로 생성된 응답에 브랜드가 표시되는 빈도와 정도에 관한 것입니다. 다음에 따라 다릅니다.

언급: 답변에서 내 브랜드가 언급된 횟수.
인용: LLM이 질문에 답변하기 위해 콘텐츠나 소스를 사용하는 빈도.
감정: 브랜드에 대한 언급이 긍정적인지, 중립적인지 또는 부정적인지 여부.
위치: 응답에서 브랜드가 언급되는 위치(예: 첫 번째, 중간 또는 마지막).

이러한 모든 요소가 가시성 점수로 결합되므로 LLM 응답에서 브랜드의 존재감이 얼마나 강한지 알 수 있습니다.

<!--How to Track Visibility Changes
Here's how you can keep an eye on your brand's visibility in LLMs:
Step 1: Check Your Current Visibility

Use tools like Adobe LLM Optimizer to see how often your brand is mentioned in LLM responses.
Look at the prompts (questions) where your brand is mentioned and where it's missing.
Compare your visibility to your competitors to see how you stack up.

Step 2: Plan Your Strategy

Group similar prompts together based on what people are asking.
Focus on the prompts that are most important to your customers.
Check if your brand has a good chance of being mentioned for certain prompts. Make sure your content shows your expertise, trustworthiness, and authority.

Step 3: Improve Your Content

Update your website and other content to make it more relevant to the prompts you want to target.
Add FAQs to your pages that answer common questions people might ask.
Make sure your content is easy for LLMs to find and read. Fix any issues like blocked pages or problems with your website's code.

Step 4: Keep Improving

Use Adobe LLM Optimizer to track how your visibility changes over time.
If you notice competitors getting mentioned more often, adjust your strategy to stay ahead.
Keep updating your content to match what people are searching for and asking about.


Tools You Can Use
Here are some tools that can help you track and improve your visibility:

Adobe LLM Optimizer: This tool shows you how visible your brand is, what prompts you're mentioned in, and how you compare to competitors.
Google Search Console: Use this to find out what people are searching for and turn those searches into LLM prompts.
SEO Tools: Tools like Ahrefs or SEMrush can help you find keywords and questions people are asking online.
User-Generated Content Platforms: Platforms like Reddit, Quora, and Wikipedia are often used by LLMs to find information. Make sure your brand is visible there.


How to Measure Your Progress
To see how well your efforts are working, track these key metrics:

Mentions: How many times your brand is mentioned in LLM responses.
Citations: How often LLMs use your content or sources.
Sentiment: Are the mentions positive, neutral, or negative?
Position: Is your brand mentioned first, in the middle, or last in the response?
Visibility Score: This is a number that combines all the above metrics to show your overall visibility.


5. Real-Life Examples
Here are some examples of how you can improve your visibility:
Example 1: Fixing Website Issues
If LLMs can't access your website because of blocked pages or coding problems, they won't mention your brand. You can use Adobe LLM Optimizer to fix these issues and make sure your content is easy for LLMs to find.
Example 2: Updating Wikipedia
Since LLMs often use Wikipedia for information, make sure your company's page is accurate and up-to-date. You can also add your brand to other Wikipedia pages where it's relevant.
Example 3: Engaging on Reddit and Quora
LLMs use platforms like Reddit and Quora to find answers. You can join discussions and share helpful information about your brand to increase visibility.

6. Challenges You Might Face

Understanding Metrics: It can be tricky to figure out what visibility scores mean. Use tools like Adobe LLM Optimizer to get clear explanations.
Technical Problems: If your website has blocked pages or coding issues, LLMs might not be able to access your content.
Keeping Content Relevant: You'll need to make sure your content matches what people are asking about.


7. Tips for Success

Learn how to use Adobe LLM Optimizer to track your visibility and improve your content.
Make sure your website is easy for LLMs to access by fixing any technical issues.
Use data from search tools and user-generated content platforms to find out what people are asking about.
Keep updating your content to stay relevant and ahead of your competitors.


Conclusion
Improving your brand's visibility in LLMs is an ongoing process. By tracking your visibility, updating your content, and using the right tools, you can make sure your brand is mentioned more often and in a positive way. This report gives you the steps and tools you need to get started and succeed in LLM optimization.
What can I help with next?
Simplify the report further for a middle school audience.
Create a step-by-step LLM visibility improvement checklist.


Marketer's guide to Generative Engine Optimization (GEO)

Generative Engine Optimization (GEO), also called Answer Engine Optimization (AEO), is how you make your brand and content visible, trustworthy, and retrievable within AI-generated answers - across ChatGPT, Perplexity, Copilot, Gemini, and other LLM-driven assistants.

If traditional SEO helped you win page-one rankings, GEO helps you win AI citations and visibility inside answer engines. The Adobe LLM Optimizer lets you measure how your brand and content is visible inside those answer engines.

This article describes how to measure and enhance your visibility and influence in AI-driven search environments whether you're an SEO analyst/specialist, public relations (PR) or communication strategist, or a marketing manager.


<!-- brands enhance their visibility, accuracy, and influence in AI-driven search environments. It provides insights into brand presence in AI-generated answers, offers prescriptive content recommendations, and automates optimization fixes -->

<!-- Alva - don't forget to add to TOC -->

<!-- ## How GEO is changing your world

May remove this - Traditional SEO focuses on rankings in Google SERPs and GEO shifts focus to visibility within AI-generated answers and citation frequency.

Think about semantic visibility and retrieval relevance - not just keyword rankings. -->

GEO(Generative Engine Optimization)/AEO(Answer Engine Optimization)에 대한 SEO 분석가의 가이드

SEO 전문가/분석가로서 목표는 생성 AI 응답 내에서 검색 기능과 브랜드 콘텐츠 포함을 극대화하는 것입니다. 최적화된 페이지가 표시되고 인용되며 측정 가능한 트래픽 또는 참여를 유도합니다.

순위와 상위 10개 위치, 검색 엔진 결과 페이지(SERP) 결과 및 키워드 공유에 초점을 맞춥니다. 이제 생성 AI 시스템이 사용자 질문에 직접 답변하면서 가시성이 전환되고 있으므로 몇 가지 추가 지표를 확인해야 합니다. 사이트 **순위**&#x200B;뿐만 아니라 콘텐츠 **더 자주 검색**&#x200B;되고 있습니다.

SEO 분석가를 위한 상위 KPI

Adobe의 LLM Optimizer에서 상위 KPI를 도구에서 바로 사용할 수 있습니다.

<!-- * AI Visibility Tracking: You need to see when and how your pages are appearing in AI-generated answers. This includes **citations** and **mentions** and sentiment. See [Brand Presence dashboard](/help/dashboards/brand-presence.md)

* Agentic Traffic Measurement: You need to understand traffic coming from AI-driven referrals or summaries. See [Agentic Traffic dashboard](/help/dashboards/agentic-traffic.md)-->

<!-- Not sure llm optimizer has all these - remove those not relevant-->

쿼리-대답 매핑: AI가 콘텐츠를 사용하도록 유도하는 프롬프트 및 의도에 insight을 포함시켜야 합니다.

콘텐츠 검색 가능성 점수: 콘텐츠 구조, 스키마 및 의미 체계를 통해 LLM이 콘텐츠를 쉽게 &quot;이해&quot;할 수 있는지 알아야 합니다.

경쟁업체 AI 벤치마킹: AI 답변을 지배하는 경쟁사와 가시성을 확보하는 경쟁사를 확인해야 합니다.

코드 조각 속성 분석: AI가 사이트에서 가져오는 정확한 구문 또는 단락을 추적하려고 합니다.


생성 검색 결과에서 브랜드 및 콘텐츠 가시성
인용 및 속성 추적

웹 사이트의 성공 여부는 사람들이 브랜드, 제품 또는 전문 영역에 대한 질문을 할 때 AI 시스템이 콘텐츠를 얼마나 자주 찾고, 사용하고, 인용할 수 있는지에 따라 달라집니다.

### GEO 도구에서 필요한 것(예: Adobe LLM Optimizer)

* AI 가시성 추적: 페이지가 AI가 생성한 응답에 표시되는 시기와 방법을 확인해야 합니다.
* 에이전트 트래픽 측정: AI 기반 참조 또는 요약에서 오는 트래픽을 이해해야 합니다.

쿼리-대답 매핑: AI가 콘텐츠를 사용하도록 유도하는 프롬프트 및 의도에 insight을 포함시켜야 합니다.

콘텐츠 검색 가능성 점수: 콘텐츠 구조, 스키마 및 의미 체계를 통해 LLM이 콘텐츠를 쉽게 &quot;이해&quot;할 수 있는지 알아야 합니다.

경쟁업체 AI 벤치마킹: AI 답변을 지배하는 경쟁사와 가시성을 확보하는 경쟁사를 확인해야 합니다.

코드 조각 속성 분석: AI가 사이트에서 가져오는 정확한 구문 또는 단락을 추적하려고 합니다.


Adobe Analytics 통합: 이러한 GEO 신호를 기존 대시보드 및 KPI와 통합하려는 경우

### 이 문제가 귀하에게 중요한 이유

&#39;AI 음성 점유율&#39;을 측정해 포스트 키워드 세계에서 자신의 가치를 증명할 수 있다.

사용자가 검색 결과에서 AI 답변으로 이동할 때 전략을 미래에도 적용할 수 있습니다.

검색할 수 있을 뿐만 아니라 인용할 수 있는 콘텐츠를 구조화하여 SEO와 브랜드를 연결할 수 있습니다.

### 지역 KPI

AI 음성 공유(AI 답변에서의 가시성)

브랜드 인용 빈도

콘텐츠 검색 가능성 점수

AI 기반 클릭 또는 언급

구조화된 데이터 범위

## PR 및 통신 관리자의 GEO(Generative Engine Optimization)/AEO(Answer Engine Optimization) 안내서

홍보 및 커뮤니케이션 관리자로서 목표는 미디어 보도를 통제하고 언론인이 말하는 내용뿐만 아니라 AI 시스템이 말하는 내용도 관리하는 것입니다. 누군가가 AI 봇에게 브랜드·제품·CEO에 대해 질문하면 해당 모델은 보도자료, 위키백과, 리뷰, 서드파티 언급 등 웹 전반의 데이터를 종합하는 것이다.

이 새로운 AI 생태계에서 브랜드 스토리를 형성하고 보호하는 데 중점을 둡니다.

GEO Tool에서 필요한 기능

* AI 브랜드 모니터링: 주요 AI 시스템에서 브랜드, 경영진 및 제품을 설명하는 방법에 대한 가시성이 필요합니다.
* 감정 및 톤 추적: AI 응답이 원하는 음성 및 감정 톤을 반영하는지 여부를 평가하고자 합니다.
* Source 영향 매핑: AI 출력을 형성하는 데 가장 영향력 있는 미디어, 검토 사이트 및 서드파티 페이지를 알아야 합니다.
* 내러티브 정확도 점수 지정: 사실적 정확도를 확인하고 오래되거나 잘못된 데이터를 감지해야 합니다.
* 위기 감지 경고: AI 모델이 잘못된 표현을 확산시킬 때 즉시 알림을 받으려는 것입니다.
* 콘텐츠 유효성 검사 도구: 스키마, 위키백과 및 지식 그래프를 통해 올바르고 구조화된 신뢰할 수 있는 데이터를 에코시스템에 제공할 수 있습니다.

포커스 영역
포커스 영역    수행할 작업    중요한 이유
브랜드 내러티브 감사    AI가 브랜드를 설명하는 방법 확인    정확성 및 일관성 보장
영향 매핑    AI 답변을 도출하는 소스 식별    지원 및 수정 우선 순위 지정
사실적 관리    신뢰할 수 있는 소스에서 브랜드 데이터를 최신 상태로 유지    오래되거나 잘못된 정보 방지
감정 정렬    톤과 승인된 메시지 비교 측정    브랜드 평판 보호
위기 관리    AI 오판에 대한 경고 받기    신속한 응답 지원

브랜드는 더 이상 브랜드를 지배할 수 없습니다. 사이트를 읽을 수 있는 경우 상당히 얻을 수 있는 획득(타사) 콘텐츠가 필요합니다

<!-- Add table and also the PR and Comm manager mission and Marketing manager mission (see chatgpt and copilot-->

브랜드가 ai 검색에 나타나는 방식
하지만 그들은 추천을 받기도 합니다
다른 Adobe 제품은 필요하지 않습니다.

시장 점유율 획득

에이전트 트래픽이 항상 홈 페이지로 이동하는 것은 아닙니다.

규범적 권장 사항 - 구체적입니다. 승인된 최적화를 배포하고

사용 사례

분 22






<!-- Use the "Share of Voice" feature to see which competitors are dominating specific topics and adjust your strategy accordingly.-->

<!-- Purpose: Measure how much of the conversation your brand owns compared to competitors.
Insight:

This feature shows the percentage of visibility your brand has for specific topics compared to competitors.
For example, you can see how many mentions your brand has versus competitors like Canva or Microsoft for a topic like "design creation."


Best Practice:

Use this insight to identify gaps in your visibility and focus on improving your presence in underperforming topics.-->



<!--6. Content Visibility

Purpose: Ensure LLMs can access and render your content.
Insight:

The dashboard compares what LLMs can see versus what is actually on your page.
It provides a percentage of content visibility, highlighting areas where LLMs may only see a small portion of your page due to client-side rendering issues.


Best Practice:

Use the "LLM Optimizer on the Edge" feature to render static HTML versions of your pages for LLM bots, ensuring full content visibility.
Address issues like blocked pages, robots.txt restrictions, and client-side rendering problems.



7. Opportunities

Purpose: Identify actionable steps to improve visibility.
Insight:

The dashboard highlights opportunities for optimization, such as updating Wikipedia pages, contributing to Reddit or Quora threads, or improving page structure.
It provides specific recommendations, such as adding FAQs to pages or improving headers (H1, H2, H3).


Best Practice:

Review the opportunities section regularly and take action on the recommendations provided.
Ensure contributions to platforms like Wikipedia and Reddit are unbiased, non-commercial, and add value.-->

