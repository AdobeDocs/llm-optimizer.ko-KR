---
title: Edge에서 최적화
description: 작성 변경 작업 없이 CDN 에지에서 LLM Optimizer의 최적화를 제공하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 1f665bd14349c15d92f8274742606abcf9b02000
workflow-type: tm+mt
source-wordcount: '4708'
ht-degree: 1%

---


# Edge에서 최적화

이 페이지에서는 작성 변경 없이 CDN 에지에서 최적화를 제공하는 방법에 대한 자세한 개요를 제공합니다. 온보딩 프로세스, 사용 가능한 최적화 기회 및 에지에서 자동 최적화하는 방법을 다룹니다.

>[!NOTE]
>이 기능은 현재 조기 액세스 상태입니다. 조기 액세스 프로그램 [여기](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs)에 대해 자세히 알아볼 수 있습니다.

## Edge에서 최적화란 무엇입니까?

Edge에서 최적화는 AI에게 친숙한 LLM 사용자 에이전트 변경 사항을 제공하는 LLM Optimizer의 에지 기반 배포 기능입니다. 현재 컨텍스트에서 &quot;Edge&quot;는 최적화가 CDN 계층에서 적용됨을 의미합니다. CDN 계층에서 최적화를 제공하기 때문에, 원본 CMS이 변경되지 않은 상태로 유지되도록 컨텐츠 관리 시스템(CMS)의 작성 변경 사항이 필요하지 않습니다. 이러한 분리를 통해 기존 게시 워크플로우를 변경하지 않고 LLM 가시성을 향상시킬 수 있습니다. 에이전트 트래픽만 타겟팅하며 사람 사용자나 SEO 봇에는 영향을 주지 않습니다. LLM Optimizer이 페이지 최적화 기회를 감지하면 사용자가 CDN 에지에서 직접 수정 사항을 배포할 수 있습니다.

Edge에서 최적화는 복잡한 엔지니어링 노력이 필요한 기존의 수정 사항에 대한 보다 빠르고 효율적인 대안입니다. 위에서 언급했듯이 1회 설정을 완료한 후에는 플랫폼 변경 사항이나 변경 사항을 적용하는 데 긴 개발 주기가 필요하지 않습니다. 개발자 참여 없이 몇 분 만에 향상된 기능을 게시할 수 있습니다. AI 에이전트용으로 웹 사이트를 최적화하는 비코드 방법입니다.

Edge에서 최적화는 마케팅, SEO, 콘텐츠 및 디지털 전략 팀의 비즈니스 사용자를 위해 설계되었습니다. 이를 통해 비즈니스 사용자는 LLM Optimizer에서 기회 식별, 제안 사항 이해 및 수정 사항 간편한 배포와 같은 전체 여정을 완료할 수 있습니다. Edge에서 최적화를 사용하면 변경 사항을 미리 보고, CDN 에지에서 신속하게 배포하고, 최적화가 라이브 상태인지 확인할 수 있습니다. LLM Optimizer 에코시스템에서 성능을 추적할 수 있습니다.

### 주요 이점

* **AI 전용 게재:** 사람 방문자나 SEO 봇에 영향을 주지 않고 AI 에이전트에게만 최적화된 HTML을 제공합니다.
* **더 빠른 주기:** 몇 주가 아닌 몇 분 내에 변경 내용을 게시합니다. 플랫폼 변경이나 긴 엔지니어링 주기가 필요하지 않습니다.
* **복원 가능:** 페이지를 몇 분 안에 되돌릴 수 있는 원클릭 롤백 기능이 지원됩니다.
* **성능에 영향을 주지 않음:** Edge 기반 최적화 및 캐싱은 사이트 지연 시간에 영향을 주지 않습니다.
* **CDN 및 CMS 불가지론자:**&#x200B;은(는) 콘텐츠 관리 시스템에 관계없이 모든 CDN 구성 및 프론트엔드 설정에서 작동합니다.

### Edge에서 최적화를 통해 지원되는 영업 기회는 무엇입니까?

Edge에서 최적화를 통해 아젠틱 웹 경험을 개선할 수 있는 기회를 지원합니다. [기회 대시보드](/help/dashboards/opportunities.md) 페이지와 현재 페이지의 기회 섹션 모두에서 각 기회에 대해 자세히 알아보세요.

## 온보딩

온보딩 프로세스를 시작하려면 Adobe 계정 팀 또는 FDE 팀에 연락해야 합니다. IT 또는 CDN 팀도 전제 조건 및 설정 프로세스를 완료해야 합니다. 또한 `llmo-at-edge@adobe.com`에 연락하여 추가 온보딩 지원을 받을 수도 있습니다.

Edge에서 최적화하기 위해 온보딩해야 하는 전제 조건:

* LLM Optimizer에 대한 온보딩 프로세스를 완료합니다.
* CDN 로그에 대한 로그 전달 프로세스를 완료합니다.

IT/CDN 팀에 대한 요구 사항:
* 허용 목록에 추가하다 사이트의 txt 파일 또는 봇 트래픽 관리 규칙에 `*AdobeEdgeOptimize/1.0*` 사용자 에이전트를 robots에 추가합니다.
* 페이지가 도메인 또는 CDN 수준에서 차단되지 않았는지 확인합니다.
* CDN에 Edge 라우팅 규칙에 최적화 를 추가합니다.
* LLM Optimizer 인터페이스에서 Edge 라우팅에서 최적화 를 확인합니다.

다음은 여러 CDN 설정에 대한 샘플 구성으로서, 설정 프로세스를 안내하는 예제입니다. 이러한 예제는 실제 라이브 구성에 맞게 조정되어야 합니다. 먼저 낮은 환경에서 변경 사항을 적용하는 것이 좋습니다.

>[!BEGINTABS]

>[!TAB AEM Cloud Service Managed CDN(Fastly)]

**Edge 최적화 - AEM Cloud Service Managed CDN(Fastly)**

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

에이전트 트래픽을 Edge으로 라우팅하려면 다음을 수행하십시오.

1. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **최적화를 배포할 AI 트래픽 라우팅**&#x200B;에서 **AI 에이전트에 최적화 배포** 확인란을 선택하십시오. Adobe 팀이 귀하를 대신하여 라우팅 구성을 처리합니다.

   ![AI 에이전트에 최적화 적용](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. 확인란을 활성화하면 설정 진행 중 상태가 표시됩니다. Adobe 팀이 라우팅 구성을 완료합니다.

   ![AI 트래픽 라우팅 설정 진행 중](/help/assets/optimize-at-edge/prereq-traffic-routing-progress.png)

   공정순서가 구성되고 활성화되면 상태가 업데이트되어 공정순서가 성공적으로 사용되었음을 나타내는 녹색 확인 표시가 나타납니다. 추가적인 작업은 필요하지 않습니다.

또한 위의 단계에 대한 도움이 필요한 경우 Adobe 계정 팀이나 `llmo-at-edge@adobe.com`에 문의하십시오.

**Cloud Manager 파이프라인을 통한 셀프 서비스 라우팅**

Cloud Manager 파이프라인을 통해 직접 라우팅을 구성하려는 경우 아래 단계를 따르십시오. [originSelector CDN 규칙](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors)을 사용하여 라우팅 구성을 수행합니다. 전제 조건은 다음과 같습니다.

* 라우팅할 도메인을 결정합니다.
* 라우팅할 경로를 결정합니다.
* 라우팅할 사용자 에이전트를 결정합니다(권장 정규 표현식).

규칙을 배포하려면 다음을 수행해야 합니다.

* [구성 파이프라인](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/operations/config-pipeline)을 만듭니다.
* 저장소에 `cdn.yaml` 구성 파일을 커밋합니다.
* 구성 파이프라인을 실행합니다.

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Edge Optimize backend
  originSelectors:
    rules:
      - name: route-to-edge-optimize-backend
        when:
          allOf:
            - reqHeader: x-edgeoptimize-request
              exists: false # avoid loops when requests comes from Edge Optimize
            - reqHeader: user-agent
              matches: "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: edge-optimize-backend
    origins:
      - name: edge-optimize-backend
        domain: "live.edgeoptimize.net"
```

**설정 확인**

설정을 테스트하려면 curl을 실행하고 다음을 기대해 보십시오.

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

>[!TAB Fastly(BYOCDN)]

**Edge 최적화 - Fastly(BYOCDN)**

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

Fastly VCL 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인의 Fastly에 액세스
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

**API 키를 검색하는 단계:**

1. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **최적화를 배포할 AI 트래픽 라우팅**&#x200B;에서 **AI 에이전트에 최적화 배포** 확인란을 선택하십시오.

   ![AI 에이전트에 최적화 적용](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. API 키를 복사하고 아래 라우팅 구성 단계를 진행합니다.

   ![API 키 복사](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >이 단계에서, 상태는 설정이 아직 완료되지 않았음을 나타내는 적색 십자가를 보여줄 수 있다. 예상된 결과입니다. 아래 라우팅 구성을 완료하고 AI 보트 트래픽이 흐르기 시작하면 상태가 라우팅이 성공적으로 활성화되었음을 확인하는 녹색 확인 표시로 업데이트됩니다.

또한 위의 단계에 대한 도움이 필요한 경우 Adobe 계정 팀이나 `llmo-at-edge@adobe.com`에 문의하십시오.

**구성**

Fastly 서비스에 다음 3개의 VCL 코드 조각을 추가합니다. 이러한 스니펫은 Edge 최적화, 캐시 키 분리 및 기본 원본으로의 장애 조치(failover)에 대한 라우팅 에이전트 요청을 처리합니다.

![가장 빠른 VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![VCL 코드 조각 추가](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv 코드 조각**

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

**vcl_hash 코드 조각**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**vcl_deliver 코드 조각**

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

설정을 테스트하려면 curl을 실행하고 다음을 기대해 보십시오.

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Akamai(BYOCDN)]

**Edge 최적화 - Akamai(BYOCDN)**

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

Akamai 속성 관리자 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인의 Akamai Property Manager에 액세스
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

**API 키를 검색하는 단계:**

1. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **최적화를 배포할 AI 트래픽 라우팅**&#x200B;에서 **AI 에이전트에 최적화 배포** 확인란을 선택하십시오.

   ![AI 에이전트에 최적화 적용](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. API 키를 복사하고 아래 라우팅 구성 단계를 진행합니다.

   ![API 키 복사](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >이 단계에서, 상태는 설정이 아직 완료되지 않았음을 나타내는 적색 십자가를 보여줄 수 있다. 예상된 결과입니다. 아래 라우팅 구성을 완료하고 AI 보트 트래픽이 흐르기 시작하면 상태가 라우팅이 성공적으로 활성화되었음을 확인하는 녹색 확인 표시로 업데이트됩니다.

또한 위의 단계에 대한 도움이 필요한 경우 Adobe 계정 팀이나 `llmo-at-edge@adobe.com`에 문의하십시오.

**구성**

다음 Akamai Property Manager 규칙은 LLM 사용자 에이전트를 Edge Optimize로 라우팅합니다. 구성에는 다음 단계가 포함됩니다.

**1. 라우팅 조건 설정(사용자 에이전트 일치)**

다음 사용자 에이전트에 대한 라우팅을 설정합니다.

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![라우팅 조건 설정](/help/assets/optimize-at-edge/akamai-step1-routing.png)

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

![사이트 장애 조치](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![장애 조치(Failover) 동작](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![장애 조치(Failover) 규칙](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

사이트 장애 조치(Failover)를 통해 Edge 최적화가 `4XX` 또는 `5XX` 오류를 반환하는 경우 요청이 기본 원본으로 다시 자동 라우팅되어 최종 사용자가 응답을 계속 받게 됩니다.

| 시나리오 | 비헤이비어 |
| --- | --- |
| Edge 최적화 반환: `2XX` | 최적화된 응답이 클라이언트에 제공됩니다. |
| Edge 최적화는 `4XX` 또는 `5XX` 반환 | 요청은 기본 원점으로 다시 라우팅됩니다. |

**설정 확인**

설정을 테스트하려면 curl을 실행하고 다음을 기대해 보십시오.

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB Cloudflare(BYOCDN)]

**Edge 최적화 - Cloudflare(BYOCDN)**

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

Cloudflare Worker 라우팅 규칙을 설정하기 전에 다음을 확인하십시오.

* 도메인에서 작업자가 활성화된 Cloudflare 계정입니다.
* Cloudflare에서 도메인의 DNS 설정에 액세스합니다.
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

**API 키를 검색하는 단계:**

1. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **최적화를 배포할 AI 트래픽 라우팅**&#x200B;에서 **AI 에이전트에 최적화 배포** 확인란을 선택하십시오.

   ![AI 에이전트에 최적화 적용](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. API 키를 복사하고 아래 라우팅 구성 단계를 진행합니다.

   ![API 키 복사](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >이 단계에서, 상태는 설정이 아직 완료되지 않았음을 나타내는 적색 십자가를 보여줄 수 있다. 예상된 결과입니다. 아래 라우팅 구성을 완료하고 AI 보트 트래픽이 흐르기 시작하면 상태가 라우팅이 성공적으로 활성화되었음을 확인하는 녹색 확인 표시로 업데이트됩니다.

또한 위의 단계에 대한 도움이 필요한 경우 Adobe 계정 팀이나 `llmo-at-edge@adobe.com`에 문의하십시오.

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

**5단계: 설정 확인**

배포 후 에이전트 사용자 에이전트를 사용하여 요청하여 구성을 테스트합니다.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

성공적인 응답에는 `x-edgeoptimize-request-id` 헤더가 포함됩니다.

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

또한 일반 트래픽이 계속 작동하는지 확인할 수 있습니다.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0"
```

이 요청은 `x-edgeoptimize-request-id` 헤더 없이 원본에서 제공해야 합니다.

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

>[!ENDTABS]

>[!NOTE]
>다른 CDN 공급자의 경우 `llmo-at-edge@adobe.com`에 연락하여 IT/CDN 팀의 온보딩을 지원하십시오. 설정 구성이 완료되면 LLM Optimizer에서 Edge 기회에 최적화를 위한 제안을 배포할 수 있습니다.

## 기회

다음 표에는 에이전트 웹 경험을 향상시킬 수 있는 기회와 Edge에서 최적화를 지원하는 옵션이 나와 있습니다.

| 기회 | 유형 | 자동 식별 | 자동 제안 | 자동 최적화 |
|---------|----------|----------|----------|----------|
| 콘텐츠 가시성 복구 | 기술 GEO | AI 에이전트에서 중요한 콘텐츠를 숨기는 페이지를 감지합니다. 영향을 받는 URL 및 복구할 수 있는 예상 컨텐츠를 표시합니다. | AI 에이전트에 사용할 수 있는 콘텐츠를 강조 표시하고 해당 페이지에 대한 사전 렌더링을 활성화하는 것을 권장합니다. | 완전히 렌더링된 AI 친화적인 HTML 스냅샷을 이전에 숨긴 콘텐츠를 복구하는 에이전트 트래픽에 제공합니다. |
| LLM 친화적 요약 추가 | 콘텐츠 최적화 | 는 페이지 또는 섹션 수준에서 간결한 요약이 부족한 길거나 복잡한 페이지를 식별하여 AI가 빠르게 스캔하고 이해하는 것을 어렵게 합니다. | 는 주요 콘텐츠를 캡처하는 페이지 및 섹션 수준에서 AI가 생성한 짧은 요약을 권장합니다. | 관련 HTML 섹션에 요약을 삽입하여 모델이 페이지 콘텐츠를 해석하고 설명하는 방식을 개선합니다. |
| 관련 FAQ 추가 | 콘텐츠 최적화 | FAQ의 이점을 얻을 수 있는 기존 페이지 콘텐츠의 의도 차이를 감지합니다. | 사용자 의도와 기존 주제에 맞게 AI가 생성한 FAQ 콘텐츠를 제안합니다. | HTML에 FAQ 콘텐츠를 삽입함으로써 페이지를 AI 기반 답변에서 더 많이 찾고 연관시킬 수 있습니다. |
| 복잡한 콘텐츠 간소화 | 콘텐츠 최적화 | AI 이해를 방해할 수 있는 복잡한 텍스트로 페이지에 플래그를 지정합니다. | AI가 생성한 간소화된 버전의 복잡한 텍스트를 제공하면서도 원래 의미는 그대로 유지합니다. | 페이지의 복잡한 섹션을 재작성하여 AI 가독성을 개선합니다. |

### 추가 도구

[Adobe LLM Optimizer: 웹 페이지를 사용할 수 있습니까?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome 확장은 LLM이 액세스할 수 있는 웹 페이지 콘텐츠의 양과 숨겨진 항목을 보여 줍니다. 독립형 무료 진단 도구로 설계되어 제품 라이선스나 설정이 필요 없습니다.

한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가할 수 있습니다. AI 에이전트가 보는 내용과 사람 사용자가 보는 내용을 나란히 비교하고 LLM Optimizer을 사용하여 복구할 수 있는 콘텐츠의 양을 예측할 수 있습니다. [AI가 웹 사이트를 읽을 수 있습니까?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) 페이지 를 참조하십시오.

## 영업 기회 세부 정보

다음 섹션에서 Edge에서 최적화를 통해 지원되는 각 기회에 대한 추가 세부 정보를 볼 수 있습니다.

### 콘텐츠 가시성 복구

이 영업 기회는 클라이언트측 렌더링으로 인해 AI 에이전트용 주요 콘텐츠가 숨겨져 있는 페이지에 플래그를 지정합니다. 식별된 각 페이지에 대해 AI 에이전트 보기에서 누락된 콘텐츠를 정확하게 보여 주고, 가시성 차이를 강조 표시하며, 숨겨진 콘텐츠를 복구하기 위해 변경 사항을 직접 적용할 수 있도록 합니다. Edge에서 최적화를 사용하여 이 영업 기회를 배포하면 사전 렌더링된 AI 최적화 버전의 페이지가 LLM 사용자 에이전트에게 제공되어 Javascript를 실행하지 않고도 전체 컨텍스트에 액세스할 수 있습니다.
이렇게 하면 페이지가 AI 에이전트에게 처음으로 완전히 표시됩니다. 추가 개선 사항은 사전 렌더링된 HTML 위에 적용됩니다.

>[!IMPORTANT]
>이 사전 렌더링 기능은 Edge에서 최적화로 배포하면 아래에 제시된 모든 기회에 자동으로 적용되어 페이지가 AI 에이전트에게 완전히 표시되도록 합니다.

### LLM 친화적 요약 추가

이 기회는 LLM이 페이지 콘텐츠의 내용을 신속하게 이해할 수 있도록 간결한 요약의 이점을 얻을 수 있는 페이지를 식별합니다. 각 페이지에 대해 영업 기회는 요약이 가장 필요한 위치를 감지하고 페이지 수준 또는 섹션 수준에서 AI가 생성한 요약을 생성합니다. Edge에서 최적화를 사용하여 배포할 때 이러한 요약은 AI 에이전트가 검색하는 HTML에 삽입되므로 콘텐츠를 보다 정확하게 설명할 가능성이 향상됩니다.

### 관련 FAQ 추가

이 기회는 추가 Q&amp;A 콘텐츠가 AI 기반 검색의 사용자 의도와 프롬프트에 더 잘 부합할 수 있는 페이지에 플래그를 지정합니다. 각 페이지에 대해 페이지의 사용자 의도와 콘텐츠에 연결된 AI가 생성한 FAQ 블록을 제안합니다. Edge에서 최적화를 사용하면 이러한 FAQ가 HTML에 삽입되므로 페이지를 AI 친화적이고 AI 응답이 지침을 직접 반영할 가능성이 높아집니다.

### 복잡한 콘텐츠 간소화

이번 기회는 AI 이해도를 떨어뜨릴 수 있는 길고 복잡한 단락이 있는 페이지를 찾는다. 가독성 임계값을 초과하는 각 페이지에 대해 원래 의미를 유지하면서 보다 간단하고 스캔하기 쉬운 AI 생성 콘텐츠를 만듭니다. 에지에 배포되면 에이전트 트래픽에 전달되는 간소화된 콘텐츠를 통해 LLM이 콘텐츠를 보다 충실하게 해석하고 요약할 수 있습니다.

## Edge에서 자동 최적화

각 영업 기회에 대해 에지에서 최적화를 미리 보고, 편집하고, 배포하고, 라이브를 보고, 롤백할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### 미리보기

**미리 보기**&#x200B;를 사용하면 제안이 실행되기 전에 제안의 영향을 확인할 수 있습니다. 현재 페이지와 제안을 적용한 후 예상되는 AI 최적화 버전 간의 병렬 차이가 나타납니다. 이 보기는 라이브 트래픽을 향상시키는 Edge에서 동일한 최적화 로직을 사용하지만 격리된 미리보기 모드에서 사용됩니다. 이는 검토를 위한 읽기 전용 시뮬레이션이므로 라이브 트래픽에는 영향을 주지 않습니다.

![미리보기](/help/assets/optimize-at-edge/preview.png)

### 편집

**편집**&#x200B;을(를) 사용하면 자동 생성된 제안을 배포하기 전에 수정하거나 모두 다시 작성할 수 있습니다. 제안을 수락하는 대신 편집 워크플로를 통해 모든 권한을 유지합니다. 이 보기에는 원래 의도와 더 잘 일치하도록 텍스트를 수정할 수 있는 구조화된 편집기에 제안된 변경 사항이 표시됩니다. 그런 다음 배포되면 편집된 버전이 AI 에이전트에 제공됩니다.

![편집](/help/assets/optimize-at-edge/edit.png)

### 배포

**배포**&#x200B;에서는 선택한 제안을 게시하므로 Edge에서 AI 에이전트에게 최적화된 경험을 제공할 수 있습니다. CDN이 완전히 라우팅되는 경우 도메인의 모든 페이지는 일반적으로 몇 분 안에 새로운 변경 사항을 반영합니다. 선택한 경로에 대해서만 라우팅이 구성된 경우 허용 목록에추가된 페이지만 최적화에 따라 활성화됩니다.

![배포](/help/assets/optimize-at-edge/deploy.png)

### 라이브 보기

**실시간 보기**&#x200B;를 통해 최적화가 실시간 상태이고 에이전트 트래픽에 대해 예상대로 작동하는지 확인할 수 있습니다. 그렇지 않으면 액세스하기 어려운 보기입니다. AI 에이전트에 표시된 대로 페이지를 렌더링하는 고정 제안 아래에서 라이브 페이지를 볼 수 있습니다.

![실시간 보기](/help/assets/optimize-at-edge/view-live.png)

### 롤백

롤백은 이전에 배포한 최적화를 안전하게 되돌립니다. 페이지의 AI 전용 버전은 일반적으로 몇 분 내에 이전 상태로 반환되므로 필요한 경우 최적화를 실험해 보는 것이 안전합니다.

![롤백](/help/assets/optimize-at-edge/rollback.png)

## 자주 묻는 질문

Q. Edge에서 어떤 종류의 LLM을 최적화로 타깃팅합니까?

온보딩 프로세스 중에 타깃팅할 사용자 에이전트 목록을 사용자가 정의합니다.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

Q. Edge에서 최적화를 위해 온보딩되지 않은 경우 어떻게 됩니까?

필요한 설정을 완료하기 전에 **최적화 배포**&#x200B;를 클릭하면 사이트에 아무 것도 적용되지 않습니다. 대신 팝업 대화 상자가 나타나 온보딩 지원을 위해 `llmo-at-edge@adobe.com`에 있는 팀에 문의하라는 메시지가 표시됩니다. 온보딩이 완료될 때까지 감지된 영업 기회와 제안을 탐색할 수 있지만, 원클릭 배포 워크플로우는 비활성 상태로 유지됩니다.

질문: 소스에서 콘텐츠가 업데이트되면 어떻게 됩니까?

기본 소스 페이지가 변경되지 않는 한 캐시에서 최적화된 페이지 버전을 제공합니다. 그러나 소스가 **콘텐츠 가시성 복구**&#x200B;에 대해 변경되면 시스템이 자동으로 새로 고침되므로 AI 에이전트는 항상 최신 콘텐츠를 수신합니다. 이는 낮은 캐시 TTL(Time to Live) 설정(분 단위)을 사용하여 사이트의 모든 콘텐츠 업데이트가 해당 창 내에서 새로운 최적화를 트리거하기 때문입니다. **LLM 친화적 요약 추가**&#x200B;와 같은 콘텐츠 기회에 대해 LLM Optimizer은 소스 페이지에서 변경 사항을 모니터링합니다. 변경 사항이 감지되면 최적화를 일시 중지하고 사람이 검토할 수 있도록 플래그를 지정하여 에이전트가 표시하는 페이지와 사람이 표시하는 페이지 사이의 콘텐츠 드리프트를 방지합니다.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

Q. Edge에서 Adobe EDS(Edge Delivery Service)를 사용하는 사이트에 대해서만 최적화됩니까?

아니요. Edge에서 최적화는 CDN과 관계없으며 Adobe의 EDS 스택에 배포된 아키텍처뿐만 아니라 모든 프론트엔드 아키텍처와 작동합니다.

Q. Edge에서 최적화 사전 렌더링은 기존의 서버측 렌더링(SSR)과 어떻게 다릅니까?

둘 다 서로 다른 문제를 해결하고 함께 일할 수 있다. 기존 SSR은 서버측 콘텐츠를 렌더링하지만 나중에 브라우저에서 로드되는 콘텐츠는 포함하지 않습니다. Edge에서 최적화 사전 렌더링은 JavaScript 및 클라이언트측 데이터가 로드된 후 페이지를 캡처하여 CDN 에지에서 완전히 조립된 버전을 생성합니다. SSR은 사용자 경험 개선에 중점을 두고 있으며, Edge에서 최적화는 LLM의 웹 경험을 개선합니다.

Q. 모든 URL이 아닌 일부 URL에 대해 최적화를 배포할 경우 어떻게 됩니까?

명시적으로 최적화하는 URL만 수정됩니다. 기회가 배포된 URL의 경우 AI 에이전트는 최적화된 버전을 받습니다. 배포된 기회가 없는 URL의 경우, 당사 서비스는 변경 사항을 적용하거나 최적화 캐시 레이어에 저장하지 않고 원본 페이지를 그대로 프록시합니다. 이렇게 하면 사이트의 나머지 부분에 영향을 주지 않고 최적화를 선택적으로 배포할 수 있습니다.
