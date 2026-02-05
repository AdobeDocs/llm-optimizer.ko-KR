---
title: Edge에서 최적화
description: 작성 변경 작업 없이 CDN 에지에서 LLM Optimizer의 최적화를 제공하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: eb8bdf9144aebb85171a529a3cc25034be5b076e
workflow-type: tm+mt
source-wordcount: '2291'
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

* API 키를 생성합니다.
* CDN에 Edge 라우팅 규칙에 최적화 를 추가합니다.
* 허용 목록에 추가하다 사용자 정의 경로 또는 전체 도메인
* LLM 사용자 에이전트의 사용자 정의 목록을 타겟에 추가합니다.
* `robots.txt`이(가) 타깃팅할 사용자 에이전트를 차단하지 않는지 확인하십시오.
* LLM Optimizer 인터페이스에서 Edge 라우팅에서 최적화 를 확인합니다.

다음은 여러 CDN 설정에 대한 샘플 구성으로서, 설정 프로세스를 안내하는 예제입니다. 이러한 예제는 실제 라이브 구성에 맞게 조정되어야 합니다. 먼저 낮은 환경에서 변경 사항을 적용하는 것이 좋습니다.

>[!BEGINTABS]

>[!TAB Adobe 관리 CDN]

**Adobe 관리 CDN**

이 구성의 목적은 Optimizer 서비스(`live.edgeoptimize.net` 백 엔드)로 라우팅될 에이전트 사용자 에이전트를 사용하여 요청을 구성하는 것입니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾으십시오.

```
curl -svo page.html https://frescopa.coffee/about-us --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

[originSelector CDN 규칙](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors)을 사용하여 라우팅 구성을 수행합니다. 전제 조건은 다음과 같습니다.

* 라우팅할 도메인 결정
* 라우팅할 경로 결정
* 라우팅할 사용자 에이전트 결정(권장 정규 표현식)

규칙을 배포하려면 다음을 수행해야 합니다.

* [구성 파이프라인 만들기](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/operations/config-pipeline)
* 저장소에 `cdn.yaml` 구성 파일을 커밋합니다.
* 구성 파이프라인 실행


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

설정을 테스트하려면 curl을 실행하고 다음을 기대해 보십시오.

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

>[!TAB Fastly(BYOCDN)]

**Edge BYOCDN 최적화 - Fastly - VCL**

![가장 빠른 VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![VCL 코드 조각 추가](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv 코드 조각**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=true"; # required for cache key
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

>[!TAB Akamai(BYOCDN)]

**Edge BYOCDN 최적화 - Akamai**

이 구성의 목적은 에이전트 사용자 에이전트의 요청을 Edge 최적화 서비스(`live.edgeoptimize.net` 백 엔드)로 라우팅하는 것입니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾으십시오.


**다음 Akamai Property Manager JSON 규칙은 LLM 사용자 에이전트를 Edge Optimize로 라우팅합니다.**

구성에는 다음 단계가 포함됩니다.

**1. 라우팅 조건 설정(사용자 에이전트 일치)**

![라우팅 조건 설정](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. 원본 및 SSL 동작 설정**

![원본 및 SSL 동작 설정](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. 캐시 키 변수 설정**

![캐시 키 변수 설정](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. 캐싱 규칙**

![캐싱 규칙](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. 수신 요청 헤더 수정**

![수신 요청 헤더 수정](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. 수신 응답 헤더 수정**

![수신 응답 헤더 수정](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. 캐시 ID 수정**

![캐시 ID 수정](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. 사이트 장애 조치(Failover)**

![사이트 장애 조치](/help/assets/optimize-at-edge/akamai-step8-failover.png)

![장애 조치(Failover) 동작](/help/assets/optimize-at-edge/akamai-step8-failover-behaviors.png)

![장애 조치(Failover) 규칙](/help/assets/optimize-at-edge/akamai-step8-failover-rules.png)

![동작 응답](/help/assets/optimize-at-edge/akamai-step8-behaviors-response.png)

설정을 테스트하려면 curl을 실행하고 다음을 기대해 보십시오.

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

>[!ENDTABS]

>[!NOTE]
>다른 CDN 공급자의 경우 `llmo-at-edge@adobe.com`에 연락하여 IT/CDN 팀의 온보딩을 지원하십시오. 설정 구성이 완료되면 LLM Optimizer에서 Edge 기회에 최적화를 위한 제안을 배포할 수 있습니다.

## 기회

다음 표에는 에이전트 웹 경험을 향상시킬 수 있는 기회와 Edge에서 최적화를 지원하는 옵션이 나와 있습니다.

| 기회 | 유형 | 자동 식별 | 자동 제안 | 자동 최적화 |
|---------|----------|----------|----------|----------|
| 콘텐츠 가시성 복구 | 기술 GEO | AI 에이전트에서 중요한 콘텐츠를 숨기는 페이지를 감지합니다. 영향을 받는 URL 및 복구할 수 있는 예상 컨텐츠를 표시합니다. | AI 에이전트에 사용할 수 있는 콘텐츠를 강조 표시하고 해당 페이지에 대한 사전 렌더링을 활성화하는 것을 권장합니다. | 완전히 렌더링된 AI 친화적인 HTML 스냅샷을 이전에 숨긴 콘텐츠를 복구하는 에이전트 트래픽에 제공합니다. |
| LLM에 대한 제목 최적화 | 콘텐츠 최적화 | 제목을 스캔하여 비어 있거나, 중복되거나, 누락되거나, 모호한 제목이 있으면 기계 가독성을 떨어뜨릴 수 있습니다. | 머리글 계층 구조 및 향상된 레이블을 제안하고 각 페이지에 대해 업데이트된 구조의 미리보기를 표시합니다. | AI 에이전트에 대한 향상된 제목 구조를 삽입하고 시각적 디자인을 유지하면서 LLM에 대해 페이지를 보다 읽기 쉽게 만듭니다. |
| LLM 친화적 요약 추가 | 콘텐츠 최적화 | 는 페이지 또는 섹션 수준에서 간결한 요약이 부족한 길거나 복잡한 페이지를 식별하여 AI가 빠르게 스캔하고 이해하는 것을 어렵게 합니다. | 는 주요 콘텐츠를 캡처하는 페이지 및 섹션 수준에서 AI가 생성한 짧은 요약을 권장합니다. | 관련 HTML 섹션에 요약을 삽입하여 모델이 페이지 콘텐츠를 해석하고 설명하는 방식을 개선합니다. |
| 관련 FAQ 추가 | 콘텐츠 최적화 | FAQ의 이점을 얻을 수 있는 기존 페이지 콘텐츠의 의도 차이를 감지합니다. | 사용자 의도와 기존 주제에 맞게 AI가 생성한 FAQ 콘텐츠를 제안합니다. | HTML에 FAQ 콘텐츠를 삽입함으로써 페이지를 AI 기반 답변에서 더 많이 찾고 연관시킬 수 있습니다. |
| 복잡한 콘텐츠 간소화 | 콘텐츠 최적화 | AI 이해를 방해할 수 있는 복잡한 텍스트로 페이지에 플래그를 지정합니다. | AI가 생성한 간소화된 버전의 복잡한 텍스트를 제공하면서도 원래 의미는 그대로 유지합니다. | 페이지의 복잡한 섹션을 재작성하여 AI 가독성을 개선합니다. |

### 추가 도구

[Adobe LLM Optimizer: 웹 페이지를 사용할 수 있습니까?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome 확장은 LLM이 액세스할 수 있는 웹 페이지 콘텐츠의 양과 숨겨진 항목을 보여 줍니다. 독립형 무료 진단 도구로 설계되어 제품 라이선스나 설정이 필요 없습니다.

한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가할 수 있습니다. AI 에이전트가 보는 내용과 사람 사용자가 보는 내용을 나란히 비교하고 LLM Optimizer을 사용하여 복구할 수 있는 콘텐츠의 양을 예측할 수 있습니다. [AI가 웹 사이트를 읽을 수 있습니까?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension)페이지입니다.

## 영업 기회 세부 정보

다음 섹션에서 Edge에서 최적화를 통해 지원되는 각 기회에 대한 추가 세부 정보를 볼 수 있습니다.

### 콘텐츠 가시성 복구

이 영업 기회는 클라이언트측 렌더링으로 인해 AI 에이전트용 주요 콘텐츠가 숨겨져 있는 페이지에 플래그를 지정합니다. 식별된 각 페이지에 대해 AI 에이전트 보기에서 누락된 콘텐츠를 정확하게 보여 주고, 가시성 차이를 강조 표시하며, 숨겨진 콘텐츠를 복구하기 위해 변경 사항을 직접 적용할 수 있도록 합니다. Edge에서 최적화를 사용하여 이 영업 기회를 배포하면 사전 렌더링된 AI 최적화 버전의 페이지가 LLM 사용자 에이전트에게 제공되어 Javascript를 실행하지 않고도 전체 컨텍스트에 액세스할 수 있습니다.
이렇게 하면 페이지가 AI 에이전트에게 처음으로 완전히 표시됩니다. 추가 개선 사항은 사전 렌더링된 HTML 위에 적용됩니다.

>[!IMPORTANT]
>이 사전 렌더링 기능은 Edge에서 최적화로 배포하면 아래에 제시된 모든 기회에 자동으로 적용되어 페이지가 AI 에이전트에게 완전히 표시되도록 합니다.

### LLM에 대한 제목 최적화

이 기회는 제목 구조가 비어 있거나, 중복되거나, 누락되거나 모호한 제목으로 인해 AI 에이전트가 페이지를 이해하기 어렵게 하는 페이지를 감지합니다. 영향을 받는 각 페이지에 대해 영업 기회는 하위 머리글을 표시하며 더 명확한 계층을 권장합니다. Edge에서 최적화를 사용하여 배포하면 개선된 제목이 에이전트 트래픽에 제공되는 HTML에 적용됩니다. 이렇게 하면 사람 대면 레이아웃을 그대로 유지하면서 기계를 가독할 수 있습니다.

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

기본 소스 페이지가 변경되지 않는 한 캐시에서 최적화된 페이지 버전을 제공합니다. 그러나 소스가 변경되면 시스템이 자동으로 새로 고쳐져 AI 에이전트는 항상 최신 콘텐츠를 수신하게 됩니다. 이는 낮은 캐시 TTL(Time to Live) 설정(분 단위)을 사용하여 사이트의 모든 콘텐츠 업데이트가 해당 창 내에서 새로운 최적화를 트리거하기 때문입니다. <!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

Q. Edge에서 Adobe EDS(Edge Delivery Service)를 사용하는 사이트에 대해서만 최적화됩니까?

아니요. Edge에서 최적화는 CDN과 관계없으며 Adobe의 EDS 스택에 배포된 아키텍처뿐만 아니라 모든 프론트엔드 아키텍처와 작동합니다.

Q. Edge에서 최적화 사전 렌더링은 기존의 서버측 렌더링(SSR)과 어떻게 다릅니까?

둘 다 서로 다른 문제를 해결하고 함께 일할 수 있다. 기존 SSR은 서버측 콘텐츠를 렌더링하지만 나중에 브라우저에서 로드되는 콘텐츠는 포함하지 않습니다. Edge에서 최적화 사전 렌더링은 JavaScript 및 클라이언트측 데이터가 로드된 후 페이지를 캡처하여 CDN 에지에서 완전히 조립된 버전을 생성합니다. SSR은 사용자 경험 개선에 중점을 두고 있으며, Edge에서 최적화는 LLM의 웹 경험을 개선합니다.
