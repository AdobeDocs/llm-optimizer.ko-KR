---
title: Optimize at Edge - AEM Cloud Service Managed CDN(Fastly)
description: LLM Optimizer에서 Optimize at Edge를 위해 AEM Cloud Service Managed CDN(Fastly)을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 0c7ccadbb40c8c119cb2a57cf8118708c33c4236
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 76%

---


# AEM Cloud Service Managed CDN(Fastly)

이 구성은 에이전틱 트래픽(AI 봇 및 LLM 사용자 에이전트의 요청)을 Edge Optimize 백엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 기존과 동일하게 사용자의 원본 서버에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 헤더 `x-edgeoptimize-request-id`를 찾습니다.

**사전 요구 사항**

에이전틱 트래픽을 Edge Optimize로 라우팅하려면 다음을 수행합니다.

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **AI 에이전트에 최적화 배포** 섹션을 찾습니다. **최적화 엔진 사용** 확인란을 선택합니다.

   ![AI 에이전트에 최적화 배포 — 보류 중](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. 확인 대화 상자에서 **사용**&#x200B;을 선택합니다. Adobe 팀이 사용자를 대신하여 라우팅 구성을 처리합니다.

   ![최적화 엔진 확인 대화 상자 사용](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

   라우팅을 구성하고 활성화하면 상태가 **완료됨**(으)로 업데이트되고 녹색 확인 표시가 표시되어 라우팅을 사용할 수 있음을 확인합니다. 추가적인 액션은 필요하지 않습니다.

   ![AI 에이전트에 최적화 배포 — 완료됨](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

또한 위 단계에 대한 도움이 필요한 경우 Adobe 계정 팀 또는 `llmo-at-edge@adobe.com`에 문의하십시오.

**Cloud Manager 파이프라인을 통한 셀프 서비스 라우팅**

Cloud Manager 파이프라인을 통해 직접 라우팅을 구성하려는 경우 아래 단계를 따르십시오. 라우팅 구성은 [originSelector CDN 규칙](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors)을 사용하여 수행됩니다. 사전 요구 사항은 다음과 같습니다.

* 라우팅할 도메인 결정
* 라우팅할 경로 결정
* 라우팅할 사용자 에이전트 결정(권장 정규 표현식)

규칙을 배포하려면 다음을 수행해야 합니다.

* [구성 파이프라인](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/operations/config-pipeline) 만들기
* 저장소에 `cdn.yaml` 구성 파일 커밋
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

**4. LLM Optimizer**&#x200B;에서 라우팅 상태 확인

LLM Optimizer UI에서 라우팅을 확인할 수도 있습니다. **고객 구성**&#x200B;을 열고 **CDN 구성** 탭을 선택합니다. 라우팅이 활성화된 경우 **AI 에이전트에 최적화 배포** 섹션에 **완료됨**&#x200B;이 표시됩니다.

![AI 에이전트에 최적화 배포 — 완료됨](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
