---
title: Edge에서 최적화 - Fastly(BYOCDN)
description: LLM Optimizer의 Edge에서 최적화를 위해 Fastly BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 8cdd15413555057165f69ea4d5a15b243ab9098d
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 6%

---


# Fastly (BYOCDN)

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

Fastly VCL 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인의 Fastly에 액세스
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

{{retrieve-byocdn-api-key}}

**구성**

Fastly 서비스에 다음 3개의 VCL 코드 조각을 추가합니다. 이러한 스니펫은 Edge 최적화, 캐시 키 분리 및 기본 원본으로의 장애 조치(failover)에 대한 라우팅 에이전트 요청을 처리합니다.

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![VCL 스니펫 추가](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv 스니펫**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**vcl_hash 스니펫**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**vcl_deliver 스니펫**

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

**장애 조치**

`vcl_deliver` 코드 조각은 장애 조치(failover)를 자동으로 처리합니다. Edge 최적화가 `4XX` 또는 `5XX` 오류를 반환하는 경우 요청이 다시 시작되고 기본 원본으로 다시 라우팅되어 최종 사용자가 응답을 계속 받습니다. 장애 조치(failover) 응답에는 `x-edgeoptimize-fo: 1` 헤더가 포함됩니다.

| 시나리오 | 비헤이비어 |
| --- | --- |
| Edge 최적화 반환: `2XX` | 최적화된 응답이 클라이언트에 제공됩니다. |
| Edge 최적화는 `4XX` 또는 `5XX` 반환 | 요청이 다시 시작되고 기본 원본에서 제공됩니다. |
| 장애 조치(failover) 응답 | 헤더 `x-edgeoptimize-fo: 1`을(를) 포함합니다. |

{{verify-setup-byocdn}}

{{return-to-overview}}
