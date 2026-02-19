---
title: Edge에서 최적화 - AEM Cloud Service Managed CDN(Fastly)
description: LLM Optimizer의 Edge에서 최적화를 위해 AEM Cloud Service Managed CDN(Fastly)을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 12%

---


# AEM Cloud Service 관리 CDN(Fastly)

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

Cloud Manager 파이프라인을 통해 직접 라우팅을 구성하려는 경우 아래 단계를 따르십시오. 라우팅 구성은 [originSelector CDN 규칙](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors)을 사용하여 수행됩니다. 사전 요구 사항은 다음과 같습니다.

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

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

{{return-to-overview}}
