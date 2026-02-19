---
title: Edge에서 최적화 - Fastly(BYOCDN)
description: LLM Optimizer의 Edge에서 최적화를 위해 Fastly BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 5%

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

**설정 확인**

설정을 완료한 후 보트 트래픽이 Edge 최적화로 라우팅되고 사람 트래픽에 영향을 주지 않는지 확인하십시오.

**1. 보트 트래픽 테스트(최적화해야 함)**

에이전트 사용자 에이전트를 사용하여 AI 보트 요청 시뮬레이션:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

성공적인 응답에는 `x-edgeoptimize-request-id` 헤더가 포함되어 있으므로 요청이 Edge 최적화를 통해 라우팅되었는지 확인합니다.

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. 사람 트래픽 테스트(영향을 받지 않아야 함)**

일반 사람 브라우저 요청 시뮬레이션:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

응답에는 `x-edgeoptimize-request-id` 헤더가 **없어야**&#x200B;합니다. 페이지 컨텐츠 및 응답 시간은 Edge에서 최적화를 활성화하기 전과 동일하게 유지되어야 합니다.

**3. 두 시나리오를 구분하는 방법**

| 헤더 | 보트 트래픽(최적화됨) | 사람 트래픽(영향을 받지 않음) |
|---|---|---|
| `x-edgeoptimize-request-id` | 있음 — 고유한 요청 ID가 포함되어 있습니다. | 없음 |
| `x-edgeoptimize-fo` | 장애 조치(failover)가 발생한 경우에만 표시됩니다(값: `1`). | 없음 |

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
