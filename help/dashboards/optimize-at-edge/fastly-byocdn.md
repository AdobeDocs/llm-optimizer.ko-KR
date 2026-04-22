---
title: Optimize at Edge - Fastly(BYOCDN)
description: LLM Optimizer의 Optimize at Edge를 위해 Fastly BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 13d2f4bbd1f9d3886f89f80df0e76093f2afdf13
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 95%

---


# Fastly(BYOCDN)

이 구성은 에이전틱 트래픽(AI 봇 및 LLM 사용자 에이전트의 요청)을 Edge Optimize 백엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 기존과 동일하게 사용자의 원본 서버에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 헤더 `x-edgeoptimize-request-id`를 찾습니다.

**사전 요구 사항**

Fastly VCL 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인에 대한 Fastly 액세스
* LLM Optimizer UI에서 검색한 Edge Optimize API 키 단계는 [API 키 검색](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key)을 참조하십시오.
* (선택 사항) 스테이징 라우팅을 테스트하려면 [스테이징 API 키](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional)를 참조하십시오.

**구성**

다음 세 가지 VCL 스니펫을 Fastly 서비스에 추가합니다. 이러한 스니펫은 Edge Optimize로의 라우팅 에이전틱 요청, 캐시 키 분리, 그리고 기본 원본으로의 장애 조치를 처리합니다.

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![VCL 스니펫 추가](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv 스니펫**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;
unset req.http.x-edgeoptimize-fetcher-key; # Optional (required only in case of WAF)

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.http.x-edgeoptimize-fetcher-key = "<YOUR FETCHER KEY>"; # Optional (required only in case of WAF)
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

**장애 조치(Failover)**

`vcl_deliver` 스니펫은 장애 조치를 자동으로 처리합니다. Edge Optimize가 `4XX` 또는 `5XX` 오류를 반환하는 경우 요청이 다시 시작되고 기본 원본으로 다시 라우팅되어 최종 사용자가 응답을 계속 수신합니다. 장애 조치(Failover) 응답에는 `x-edgeoptimize-fo: 1` 헤더가 포함됩니다.

| 시나리오 | 비헤이비어 |
| --- | --- |
| Edge Optimize는 `2XX`를 반환합니다. | 최적화된 응답을 클라이언트에 제공합니다. |
| Edge Optimize는 `4XX` 또는 `5XX`를 반환합니다. | 요청이 다시 시작되고 기본 원본에서 제공됩니다. |
| 장애 조치(Failover) 응답 | 헤더 `x-edgeoptimize-fo: 1`를 포함합니다. |

**방화벽 규칙을 통해 Edge에서 최적화 허용(선택 사항)**

{{waf-allowlist-setup}}

**설정 확인**

설정을 완료한 후 봇 트래픽이 Edge Optimize로 라우팅되고 있으며 사람 트래픽이 영향을 받지 않는지 확인합니다.

**1. 봇 트래픽 테스트(최적화해야 함)**

에이전틱 사용자 에이전트를 사용하여 AI 봇 요청을 시뮬레이션합니다.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

성공적인 응답에는 요청이 Edge Optimize를 통해 라우팅되었음을 확인하는 `x-edgeoptimize-request-id` 헤더가 포함됩니다.

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. 사람 트래픽 테스트(영향을 받지 않아야 함)**

일반 사람 브라우저 요청을 시뮬레이션합니다.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

응답에는 `x-edgeoptimize-request-id` 헤더가 **없어야** 합니다. 페이지 콘텐츠와 응답 시간은 Optimize at Edge를 활성화하기 전과 동일하게 유지되어야 합니다.

**3. 두 시나리오를 구분하는 방법**

| 헤더 | 봇 트래픽(최적화됨) | 사람 트래픽(영향을 받지 않음) |
|---|---|---|
| `x-edgeoptimize-request-id` | 있음 — 고유한 요청 ID가 포함되어 있습니다. | 없음 |
| `x-edgeoptimize-fo` | 장애 조치가 발생한 경우에만 표시됩니다(값: `1`). | 없음 |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
