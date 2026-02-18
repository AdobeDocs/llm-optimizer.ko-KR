---
title: Edge - Akamai(BYOCDN)에서 최적화
description: LLM Optimizer의 Edge에서 최적화를 위해 Akamai BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 26%

---


# Akamai(BYOCDN)

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

Akamai 속성 관리자 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인의 Akamai Property Manager에 액세스
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

{{retrieve-byocdn-api-key}}

**구성**

다음 Akamai Property Manager 규칙은 LLM 사용자 에이전트를 Edge Optimize로 라우팅합니다. 구성에는 다음 단계가 포함됩니다.

**1. 라우팅 기준 설정(사용자 에이전트 일치)**

다음 사용자 에이전트:image.png에 대한 라우팅 설정

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![라우팅 기준 설정](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. 원본 및 SSL 동작 설정**

원본을 `live.edgeoptimize.net`(으)로 설정하고 SAN을 `*.edgeoptimize.net`(으)로 일치

![원본 및 SSL 동작 설정](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. 캐시 키 변수 설정**

캐시 키 변수 `PMUSER_EDGE_OPTIMIZE_CACHE_KEY`을(를) `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`(으)로 설정

![캐시 키 변수 설정](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. 캐싱 규칙**

![캐싱 규칙](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. 수신 요청 헤더 수정**

다음 수신 요청 헤더를 설정합니다.
LLMO에서 검색한 API 키에 대한 `x-edgeoptimize-api-key`
`x-edgeoptimize-config` - `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` - `{{builtin.AK_URL}}`

![수신 요청 헤더 수정](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. 수신 응답 헤더 수정**

![수신 응답 헤더 수정](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. 캐시 ID 수정**

![캐시 ID 수정](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. 보내는 요청 헤더 수정**

`x-forwarded-host` 헤더를 `{{builtin.AK_HOST}}`(으)로 설정

![보내는 요청 헤더 수정](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. 사이트 장애 조치(Failover)**

![사이트 장애 조치(Failover)](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![장애 조치(Failover) 동작](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![장애 조치(Failover) 규칙](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

사이트 장애 조치(Failover)를 통해 Edge 최적화가 `4XX` 또는 `5XX` 오류를 반환하는 경우 요청이 기본 원본으로 다시 자동 라우팅되어 최종 사용자가 응답을 계속 받게 됩니다.

| 시나리오 | 비헤이비어 |
| --- | --- |
| Edge 최적화 반환: `2XX` | 최적화된 응답이 클라이언트에 제공됩니다. |
| Edge 최적화는 `4XX` 또는 `5XX` 반환 | 요청은 기본 원점으로 다시 라우팅됩니다. |

{{verify-setup-byocdn}}

{{return-to-overview}}
