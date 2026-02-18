---
title: Edge에서 최적화 - AEM Cloud Service Managed CDN(Fastly)
description: LLM Optimizer의 Edge에서 최적화를 위해 AEM Cloud Service Managed CDN(Fastly)을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 8cdd15413555057165f69ea4d5a15b243ab9098d
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 16%

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

{{verify-setup-adobe-aem-cs-cdn}}

{{return-to-overview}}
