---
title: Edge에서 최적화 - Cloudflare(BYOCDN)
description: LLM Optimizer의 Edge에서 최적화를 위해 Cloudflare BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 1%

---


# Cloudflare(BYOCDN)

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

Cloudflare Worker 라우팅 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인에서 작업자가 활성화된 Cloudflare 계정입니다.
* Cloudflare에서 도메인의 DNS 설정에 액세스합니다.
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

{{retrieve-byocdn-api-key}}

**라우팅 작동 방식**

올바르게 구성된 경우 에이전트 사용자 에이전트에서 도메인(예: `www.example.com/page.html`)에 대한 요청이 Cloudflare Worker에 의해 이전되어 Edge Optimize 백엔드로 라우팅됩니다. 백엔드 요청에 필수 헤더가 포함됩니다.

**백 엔드 요청 테스트**

Edge 최적화 백엔드에 직접 요청하여 라우팅을 확인할 수 있습니다.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**필수 헤더**

Edge 최적화 백엔드에 대한 요청에 대해 다음 헤더를 설정해야 합니다.

| 헤더 | 설명 | 예 |
|--------|-------------|---------|
| `x-forwarded-host` | 요청의 원래 호스트입니다. 사이트 도메인을 식별하는 데 필요합니다. | `www.example.com` |
| `x-edgeoptimize-url` | 요청의 원래 URL 경로 및 쿼리 문자열입니다. | `/page.html` 또는 `/products?id=123` |
| `x-edgeoptimize-api-key` | Adobe에서 도메인에 대해 제공하는 API 키. | `your-api-key-here` |
| `x-edgeoptimize-config` | 캐시 키 구분을 위한 구성 문자열입니다. | `LLMCLIENT=TRUE;` |

**1단계: Cloudflare 작업자 만들기**

1. Cloudflare 대시보드에 로그인합니다.
2. 사이드바에서 **작업자 및 페이지**(으)로 이동합니다.
3. **응용 프로그램 만들기**&#x200B;를 클릭한 다음 **작업자 만들기**&#x200B;를 클릭합니다.
4. 작업자 이름을 지정합니다(예: `edge-optimize-router`).
5. 기본 코드로 작업자를 만들려면 **배포**&#x200B;를 클릭하십시오.

![Cloudflare Workers 대시보드](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**2단계: 작업자 코드 추가**

작업자를 만든 후 **코드 편집**&#x200B;을 클릭하고 기본 코드를 다음으로 바꿉니다.

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

작업자를 게시하려면 **저장 및 배포**&#x200B;를 클릭하십시오.

![Cloudflare Worker 코드 편집기](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**3단계: 환경 변수 구성**

환경 변수는 API 키와 같은 민감한 구성을 안전하게 저장합니다.

1. 작업자 설정에서 **설정** > **변수**(으)로 이동합니다.
2. **환경 변수**&#x200B;에서 **변수 추가**&#x200B;를 클릭합니다.
3. 다음 변수를 추가합니다.

   | 변수 이름 | 설명 | 필수 |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | Adobe 제공 Edge Optimize API 키. | 예 |
   | `EDGE_OPTIMIZE_TARGET_HOST` | Edge 최적화 요청의 대상 호스트(`x-forwarded-host` 헤더로 전송됨)와 장애 조치(failover)의 원본 도메인입니다. 프로토콜 없이 도메인만 사용해야 합니다(예: `https://www.example.com`이(가) 아닌 `www.example.com`). | 예 |

4. API 키를 안전하게 저장하려면 **암호화**&#x200B;를 클릭합니다.
5. **저장 및 배포**&#x200B;를 클릭합니다.

![Cloudflare 환경 변수](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**4단계: 도메인에 대한 경로 추가**

도메인에서 작업자를 활성화하려면 다음을 수행합니다.

1. 작업자의 **설정** > **트리거**(으)로 이동합니다.
2. **경로**&#x200B;에서 **경로 추가**&#x200B;를 클릭합니다.
3. 도메인 패턴(예: `www.example.com/*` 또는 `example.com/*`)을 입력하십시오.
4. 드롭다운에서 영역을 선택합니다.
5. **저장**&#x200B;을 클릭합니다.

또는 영역 수준에서 경로를 구성할 수 있습니다.

1. Cloudflare에서 도메인 탐색
2. **작업자 경로**(으)로 이동합니다.
3. **경로 추가**&#x200B;를 클릭하고 패턴과 작업자를 지정하십시오.

![Cloudflare Worker 경로](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**장애 조치(failover) 동작 확인**

Edge 최적화를 사용할 수 없거나 오류를 반환하는 경우 작업자가 자동으로 원점으로 장애 조치(failover)합니다. 장애 조치(failover) 응답에는 `x-edgeoptimize-fo` 헤더가 포함됩니다.

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

Cloudflare Workers 로그에서 페일오버 이벤트를 모니터링하여 문제를 해결할 수 있습니다.

**작업자 논리 이해**

Cloudflare Worker는 다음과 같은 논리를 구현합니다.

1. **사용자 에이전트 검색:** 들어오는 요청의 사용자 에이전트가 정의된 에이전트 봇과 일치하는지 확인합니다(대/소문자 구분 안 함).

2. **경로 타깃팅:** 선택적으로 타깃팅된 경로를 기반으로 요청을 필터링합니다. 기본적으로 모든 HTML 페이지(`/`, 확장 없음 또는 `.html`(으)로 끝나는 URL)는 라우팅됩니다. `TARGETED_PATHS` 배열을 사용하여 특정 경로를 지정할 수 있습니다.

3. **루프 보호:** `x-edgeoptimize-request` 헤더에서 무한 루프를 방지합니다. Edge 최적화에서 원본을 다시 요청하면 이 헤더가 `"1"`(으)로 설정되고, 작업자는 요청을 다시 Edge 최적화로 라우팅하지 않고 통과시킵니다.

4. **헤더 보안:** Edge Optimize 헤더를 설정하기 전에 작업자가 수신 요청에서 기존 `x-edgeoptimize-*` 헤더를 제거하여 헤더 삽입 공격을 방지합니다.

5. **헤더 매핑:** 작업자가 Edge 최적화에 필요한 헤더를 설정합니다.
   * `x-forwarded-host` - 원래 사이트 도메인을 식별합니다.
   * `x-edgeoptimize-url` - 원래 요청 경로와 쿼리 문자열을 유지합니다.
   * `x-edgeoptimize-api-key` - Edge 최적화로 요청을 인증합니다.
   * `x-edgeoptimize-config` - 캐시 키 구성을 제공합니다.

6. **장애 조치(Failover) 논리:** Edge 최적화가 오류 상태 코드(4XX 클라이언트 오류 또는 5XX 서버 오류)를 반환하거나 네트워크 오류로 인해 요청이 실패하는 경우 작업자는 `EDGE_OPTIMIZE_TARGET_HOST`을(를) 사용하여 자동으로 원본으로 장애 조치합니다. 장애 조치(failover) 응답에는 장애 조치가 발생했음을 나타내는 `x-edgeoptimize-fo: 1` 헤더가 포함됩니다.

7. **리디렉션 처리:** `redirect: "manual"` 옵션을 사용하면 작업자가 리디렉션 응답을 팔로우하지 않고 Edge 최적화의 리디렉션 응답을 클라이언트에 전달할 수 있습니다.

**구성 사용자 지정**

코드의 맨 위에서 구성 상수를 수정하여 작업자 동작을 사용자 정의할 수 있습니다.

**에이전트 보트 목록**

사용자 에이전트를 추가하거나 제거하려면 `AGENTIC_BOTS` 배열을 수정하십시오.

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**타깃팅된 경로**

기본적으로 모든 HTML 페이지는 Edge 최적화로 라우팅됩니다. 특정 경로로 라우팅을 제한하려면 `TARGETED_PATHS` 배열을 수정하십시오.

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**장애 조치(failover) 구성**

기본적으로 작업자는 Edge 최적화에서 4XX 또는 5XX 오류가 발생하면 장애 조치됩니다. 다음 동작을 사용자 지정합니다.

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**중요 고려 사항**

* **장애 조치(failover) 동작:** Edge 최적화가 오류(4XX 또는 5XX 상태 코드)를 반환하거나 네트워크 오류로 인해 요청이 실패하는 경우 작업자가 자동으로 원본에 장애 조치됩니다. 장애 조치(failover)에서 `EDGE_OPTIMIZE_TARGET_HOST`을(를) 원본 도메인으로 사용합니다(Fastly의 `F_Default_Origin` 또는 CloudFront의 `Default_Origin`과(와) 유사). 장애 조치(failover) 응답에는 모니터링 및 디버깅에 사용할 수 있는 `x-edgeoptimize-fo: 1` 헤더가 포함됩니다.

* **캐싱:** Cloudflare는 기본적으로 URL을 기반으로 응답을 캐시합니다. 에이전트 트래픽은 사람 트래픽과 다른 콘텐츠를 수신하므로 캐시 구성이 이를 처리하는지 확인하십시오. 캐시 API 또는 캐시 헤더를 사용하여 캐시된 콘텐츠를 구분하는 것이 좋습니다. `x-edgeoptimize-config` 헤더가 캐시 키에 포함되어야 합니다.

* **속도 제한:** Edge을 모니터링하여 사용을 최적화하고 필요한 경우 에이전트 트래픽에 대한 속도 제한을 구현하는 것이 좋습니다.

* **테스트:** 프로덕션에 배포하기 전에 항상 스테이징 환경에서 구성을 테스트하십시오. 무의미한 트래픽과 사람 트래픽이 모두 예상대로 작동하는지 확인합니다. Edge 최적화 오류를 시뮬레이션하여 장애 조치(failover) 동작을 테스트합니다.

* **로깅:** Cloudflare Workers 로깅을 사용하여 요청을 모니터링하고 문제를 해결합니다. 실시간 로그를 보려면 **작업자** > **작업자** > **로그**(으)로 이동합니다. 작업자는 디버깅을 위해 페일오버 이벤트를 기록합니다.

**문제 해결**

| 문제 | 가능한 원인 | 솔루션 |
|-------|----------------|----------|
| 응답 중인 `x-edgeoptimize-request-id` 헤더 없음 | 작업자 경로가 일치하지 않거나 사용자 에이전트가 에이전트 보트 목록에 없습니다. | 경로 패턴이 요청 URL과 일치하는지 확인합니다. 사용자 에이전트가 `AGENTIC_BOTS` 배열에 있는지 확인하십시오. |
| Edge 최적화에서 401 또는 403 오류 | API 키가 잘못되었거나 누락되었습니다. | `EDGE_OPTIMIZE_API_KEY`이(가) 환경 변수에 올바르게 설정되어 있는지 확인하십시오. Adobe에 문의하여 API 키가 활성 상태인지 확인하십시오. |
| 무한 리디렉션 또는 루프 | 루프 보호 헤더가 올바르게 설정되거나 검사되지 않습니다. | `x-edgeoptimize-request` 헤더 검사가 제대로 되어 있는지 확인하십시오. |
| 영향을 받는 사람 트래픽 | 작업자 라우팅 논리가 너무 광범위합니다. | 사용자 에이전트 일치 논리가 올바르고 대/소문자를 구분하지 않는지 확인합니다. `TARGETED_PATHS`이(가) 올바르게 구성되어 있는지 확인하십시오. |
| 느린 응답 시간 | Edge 최적화 백엔드에 대한 네트워크 대기 시간. | 이는 첫 번째 요청에 대해 예상되며, 후속 요청은 Edge 최적화에 캐시됩니다. |
| 응답의 `x-edgeoptimize-fo: 1` 헤더 | Edge 최적화에서 오류를 반환했으며 원본으로 페일오버가 발생했습니다. | Cloudflare Workers 로그에서 특정 오류 코드를 확인합니다. Adobe을 사용하여 Edge 서비스 상태 최적화 를 확인합니다. |
| 장애 조치(failover)가 작동하지 않음 | 장애 조치(failover) 플래그가 비활성화되어 있거나 장애 조치(failover) 논리에 오류가 있습니다. | `FAILOVER_ON_4XX` 및 `FAILOVER_ON_5XX`이(가) `true`(으)로 설정되어 있는지 확인하십시오. 작업자 로그에서 오류 메시지를 확인하십시오. |
| 특정 경로가 최적화되지 않음 | 경로가 타겟팅된 경로 또는 HTML 페이지 패턴과 일치하지 않습니다. | 경로가 `TARGETED_PATHS`에 있고(지정된 경우) HTML 페이지 정규 표현식 패턴과 일치하는지 확인하십시오. |
| 잘못된 호스트로 인해 요청 실패 | `EDGE_OPTIMIZE_TARGET_HOST`에 프로토콜(예: `https://`)이 포함되어 있습니다. | 프로토콜 없이 도메인 이름만 사용합니다(예: `https://example.com`이(가) 아닌 `example.com`). |
| 장애 조치(failover) 중 530 오류 | Cloudflare가 원본에 연결할 수 없거나 장애 조치(failover) 요청에 잘못된 헤더가 있습니다. | 장애 조치(failover) 기능이 Edge 최적화 헤더를 제거하는지 확인합니다. 원본을 액세스할 수 있고 DNS가 올바르게 구성되어 있는지 확인하십시오. |

{{verify-setup-byocdn}}

{{return-to-overview}}
