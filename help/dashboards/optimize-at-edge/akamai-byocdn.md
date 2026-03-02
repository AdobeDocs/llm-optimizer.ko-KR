---
title: Optimize at Edge - Akamai(BYOCDN)
description: LLM Optimizer의 Optimize at Edge를 위해 Akamai BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: ht
source-wordcount: '587'
ht-degree: 100%

---


# Akamai(BYOCDN)

이 구성은 에이전틱 트래픽(AI 봇 및 LLM 사용자 에이전트의 요청)을 Edge Optimize 백엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 기존과 동일하게 사용자의 원본 서버에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 헤더 `x-edgeoptimize-request-id`를 찾습니다.

**사전 요구 사항**

Akamai Property Manager 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인에 대한 Akamai Property Manager 액세스
* LLM Optimizer 온보딩 프로세스 완료
* LLM Optimizer로 CDN 로그 전달 완료
* LLM Optimizer UI에서 검색한 Edge Optimize API 키

{{retrieve-byocdn-api-key}}

**구성**

다음 Akamai Property Manager 규칙은 LLM 사용자 에이전트를 Edge Optimize로 라우팅합니다. 구성에는 다음 단계가 포함됩니다.

**1. 라우팅 기준 설정(사용자 에이전트 일치)**

다음 user-agents:image.png에 대한 라우팅을 설정합니다.

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

원본을 `live.edgeoptimize.net`으로 설정하고 SAN을 `*.edgeoptimize.net`으로 일치시킵니다.

![원본 및 SSL 동작 설정](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. 캐시 키 변수 설정**

캐시 키 변수 `PMUSER_EDGE_OPTIMIZE_CACHE_KEY`를 `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`로 설정합니다.

![캐시 키 변수 설정](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. 캐싱 규칙**

![캐싱 규칙](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. 수신 요청 헤더 수정**

다음 수신 요청 헤더를 설정합니다.
`x-edgeoptimize-api-key`를 LLMO에서 검색한 API 키로, `x-edgeoptimize-config`를 `LLMCLIENT=TRUE;`로, `x-edgeoptimize-url`을 `{{builtin.AK_URL}}`로 설정합니다.

![수신 요청 헤더 수정](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. 수신 응답 헤더 수정**

![수신 응답 헤더 수정](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. 캐시 ID 수정**

![캐시 ID 수정](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. 발신 요청 헤더 수정**

`x-forwarded-host` 헤더를 `{{builtin.AK_HOST}}`로 설정합니다.

![발신 요청 헤더 수정](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. 사이트 장애 조치(Failover)**

사이트 장애 조치(Failover) 구성에는 장애 조치 비헤이비어(기본 optimize-at-edge 라우팅 규칙 내에서 구성됨)과 별도의 장애 조치 테스트 헤더 규칙이 있습니다.

**9a. 사이트 장애 조치(Failover) 비헤이비어(기본 optimize-at-edge 라우팅 규칙 내)**

기본 라우팅 규칙 내에서 다음과 같이 사이트 장애 조치(Failover) 비헤이비어와 고급 XML 스니펫을 구성합니다.

![사이트 장애 조치(Failover)](/help/assets/optimize-at-edge/akamai-step9-failover.png)

고급 XML을 통해 값이 `fo`인 요청 헤더 `x-edgeoptimize-request`를 추가합니다.

```
<forward:availability.fail-action2>
<add-header>
<status>on</status>
<name>x-edgeoptimize-request</name>
<value>fo</value>
</add-header>
</forward:availability.fail-action2>
```

![장애 조치(Failover) 동작](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

**9b. 장애 조치(Failover) 테스트 헤더 규칙(형제 규칙)**

>[!IMPORTANT]
>
>라우팅 규칙의 **형제**(동일한 수준)로서 **EdgeOptimize 장애 조치(Failover) - 테스트 헤더** 규칙을 만듭니다. 이 규칙들은 중첩되지 **않습니다**. Akamai Property Manager 규칙 트리에서 계층은 다음과 같아야 합니다.
>
>```
>▼ Parent Rule
>   ▶ Optimize at Edge Routing     ← routing rule
>       EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>이렇게 하면 장애 조치 테스트 헤더 규칙이 하나의 라우팅 규칙뿐만 아니라 **모든** 라우팅 규칙에 대해 평가됩니다.

요청 헤더 `x-edgeoptimize-request` 값이 `fo`인 경우 발신 응답 헤더 `x-edgeoptimize-fo`를 `true`로 설정합니다.

![장애 조치(Failover) 규칙](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

사이트 장애 조치(Failover)는 Edge Optimize가 `4XX` 또는 `5XX` 오류를 반환하는 경우 요청이 자동으로 기본 원본으로 라우팅되어 최종 사용자가 응답을 계속 받게 됩니다.

| 시나리오 | 비헤이비어 |
| --- | --- |
| Edge Optimize는 `2XX`를 반환합니다. | 최적화된 응답을 클라이언트에 제공합니다. |
| Edge Optimize는 `4XX` 또는 `5XX`를 반환합니다. | 요청은 기본 원본으로 다시 라우팅됩니다. |

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

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**&#x200B;으로 이동하여 **CDN 구성** 탭을 선택합니다.

![라우팅이 활성화된 AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
