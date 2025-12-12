---
title: Edge에서 최적화
description: 작성 변경 작업 없이 CDN 에지에서 LLM Optimizer의 최적화를 제공하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 3c6f287b3c3787cee95f99b7031412f26692a88b
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---


# Edge에서 최적화

이 섹션 ...

## Edge에서 최적화란 무엇입니까?

Edge에서 최적화는 AI에게 친숙한 LLM 사용자 에이전트 변경 사항을 제공할 수 있는 LLM Optimizer의 에지 기반 배포 기능입니다. CDN 에지에서 최적화를 제공하기 때문에 컨텐츠 관리 시스템(CMS)의 작성 변경 사항이 필요하지 않습니다. 또한 에이전트 트래픽만 타겟팅하며 사람 사용자나 SEO 봇에는 영향을 주지 않습니다.

LLM Optimizer이 페이지 최적화 기회를 감지하면 사용자는 플랫폼 변경 없이 에지에서 직접 수정 사항을 배포할 수 있습니다.

이 기능은 현재 조기 액세스 중입니다.

## 고객이 관심을 가져야 하는 이유는 무엇입니까?

Edge에서 최적화는 복잡한 엔지니어링 노력이 필요한 기존의 수정 사항에 대한 보다 빠르고 효율적인 대안입니다. 고객이 1회 설정을 완료하면 웹 페이지에 변경 사항을 적용하는 데 플랫폼 변경 사항이나 긴 개발 주기가 필요하지 않습니다. 사용자는 개발자 참여 없이 몇 주가 아닌 몇 분 내에 향상된 기능을 게시할 수 있습니다. 이는 AI 에이전트용으로 웹 사이트를 최적화하는 위험이 적은 비코드 방법입니다.

### 주요 이점 및 가치 제안

* **AI 전용 게재:** 사람 방문자나 SEO 봇에 영향을 주지 않고 AI 에이전트에게만 최적화된 HTML을 제공합니다.
* **더 빠른 주기:** 게시 변경 사항을 몇 주가 아니라 몇 분 단위로 변경합니다. 플랫폼 변경이나 긴 엔지니어링 주기가 필요하지 않습니다.
* **위험이 적고 되돌리기 가능:** 페이지를 몇 분 안에 되돌릴 수 있는 한 번의 클릭으로 롤백 기능이 지원됩니다.
* **성능에 영향을 주지 않음:** Edge 기반 최적화 및 캐싱은 사이트 대기 시간에 영향을 주지 않습니다.
* **CDN 및 CMS에 관계없음:**&#x200B;은(는) CMS에 관계없이 모든 CDN 구성 및 프론트엔드 설정에서 작동합니다.

## 누가 사용해야 합니까?

Edge에서 최적화는 마케팅, SEO, 콘텐츠 및 디지털 전략 팀의 비즈니스 사용자를 위해 설계되었습니다. 이를 통해 비즈니스 사용자는 LLM Optimizer에서 기회 식별, 제안 사항 이해 및 수정 사항 간편한 배포와 같은 전체 여정을 완료할 수 있습니다. Edge에서 최적화를 사용하면 변경 사항을 미리 보고, 에지에서 신속하게 배포하고, 최적화가 라이브 상태인지 확인할 수 있습니다. LLM Optimizer 에코시스템에서 성능을 추적할 수 있습니다.

## Edge에서 최적화할 수 있는 영업 기회는 무엇입니까?

Edge에서 최적화를 통해 아젠틱 웹 경험을 개선할 수 있는 기회를 지원합니다. [기회](/help/dashboards/opportunities.md) 섹션에서 각 기회에 대해 자세히 알아보세요.

## 온보딩

LLM Optimizer에 온보딩하고 CDN 로그를 전달한 후 Edge에서 최적화 를 활성화할 수 있습니다.

Edge에서 최적화 를 활성화하려면 CDN 엔지니어가 초기 설정을 완료해야 합니다.

설정 요구 사항:

* API 키를 생성합니다.
* CDN에 Edge 라우팅 규칙에 최적화 를 추가합니다.
* 허용 목록에 추가하다 사용자 정의 경로 또는 전체 도메인
* LLM 사용자 에이전트의 사용자 정의 목록을 타겟에 추가합니다.
* robots.txt가 타깃팅할 사용자 에이전트를 차단하지 않도록 합니다.
* Edge에서 최적화 라우팅은 LLM Optimizer UI에 있는지 확인합니다.

Adobe은 대부분의 주요 CDN에 대한 샘플 구성 조각을 제공하여 설정 프로세스를 안내합니다. 지침에 포함된 코드 조각 예제는 실제 라이브 구성에 맞게 조정되어야 합니다. Adobe에서는 먼저 하위 환경에서 변경 사항을 구현할 것을 권장합니다.

>[!BEGINTABS]

>[!TAB AEM Cloud Service Managed CDN(Fastly)]

**Tokowaka BYOCDN - Adobe 관리 CDN**

originSelectors만 사용하여 Tokowaka 원본을 선택합니다.

다음 예제는 패턴 &quot;/es/*&quot; 또는 정확한 경로와 일치하는 특정 도메인에서 LLM 에이전트 요청을 라우팅합니다(html 페이지만 라우팅됨). 이 예제는 시작점을 제공하고 구성에 originSelectors 가 여러 개 있는 경우 이 예제를 먼저 배치하는 것이 좋습니다.

중요 참고 사항:

* Tokowaka 백엔드로 라우팅하기 전에 x-tokowaka-request를 확인해야 합니다. 이 헤더가 없는 요청만 Tokowaka 백엔드로 라우팅해야 합니다.
* 여러 규칙이 있는 경우 Tokowaka 백엔드로 라우팅되는 originSelector 규칙이 먼저 목록에 있어야 합니다.
* cdn.yaml을 배포하기 전에 TOKOWAKA_API_KEY 암호를 배포해야 합니다.

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Tokowaka backend
  originSelectors:
    rules:
      - name: route-to-tokowaka-backend
        when:
          allOf:
            - reqHeader: x-tokowaka-request
              exists: false # avoid loops when requests comes from Tokowaka
            - reqHeader: user-agent
              matches: "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: tokowaka-backend
          headers:
            x-tokowaka-api-key: "${{TOKOWAKA_API_KEY}}"
    origins:
      - name: tokowaka-backend
        domain: "edge.tokowaka.now"
```

>[!TAB Akamai(BYOCDN)]

**Tokowaka BYOCDN - Akamai**

```
{
    "name": "Project Tokowaka CDN Rule",
    "children": [
        {
            "name": "Connection settings",
            "children": [],
            "behaviors": [
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.health-detect.status>off</forward:availability.health-detect.status>\n<forward:availability>\n<max-reforwards>1</max-reforwards>\n<max-reconnects>1</max-reconnects>\n</forward:availability>\n<match:forward.server-type value=\"CUSTOMER_ORIGIN\">\n<network:http.read>%(PMUSER_HTTP_READ)</network:http.read>\n<network:http.first-byte-timeout>%(PMUSER_FIRST_BYTE_TIMEOUT)</network:http.first-byte-timeout>\n<network:http.connect-timeout>%(PMUSER_HTTP_CONNECT_TIMEOUT)</network:http.connect-timeout> \n</match:forward.server-type>"
                    },
                    "uuid": "4a8c027b-1b23-44a7-8e12-f8d07e453679",
                    "templateUuid": "41c77091-419f-43f2-9a84-0b406b050cc8"
                }
            ],
            "uuid": "4759571b-8036-4c16-9b60-d3aeb84958f1",
            "criteria": [],
            "criteriaMustSatisfy": "all"
        },
        {
            "name": "Site Failover Behavior",
            "children": [],
            "behaviors": [
                {
                    "name": "failAction",
                    "options": {
                        "actionType": "RECREATED_CO",
                        "contentCustomPath": false,
                        "contentHostname": "www.adobe.com",
                        "enabled": true
                    }
                },
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.fail-action2>\n<add-header>\n<status>on</status>\n<name>x-tokowaka-request</name>\n<value>fo</value>\n</add-header>\n</forward:availability.fail-action2>"
                    }
                }
            ],
            "uuid": "b3000c12-1ab8-49b1-a5d0-75e58bb18c9c",
            "criteria": [
                {
                    "name": "matchResponseCode",
                    "options": {
                        "lowerBound": 400,
                        "matchOperator": "IS_BETWEEN",
                        "upperBound": 599
                    }
                },
                {
                    "name": "originTimeout",
                    "options": {
                        "matchOperator": "ORIGIN_TIMED_OUT"
                    }
                }
            ],
            "criteriaMustSatisfy": "any",
            "comments": "If Tokowaka origin returns a 4xx or 5xx error (or times out), failover condition is to send the request back to Akamai and set the x-tokowaka-request header so we don't re-send the request to Tokowaka"
        }
    ],
    "behaviors": [
        {
            "name": "origin",
            "options": {
                "cacheKeyHostname": "ORIGIN_HOSTNAME",
                "compress": true,
                "customValidCnValues": [
                    "{{Origin Hostname}}",
                    "{{Forward Host Header}}",
                    "*.tokowaka.now"
                ],
                "enableTrueClientIp": true,
                "forwardHostHeader": "ORIGIN_HOSTNAME",
                "hostname": "edge.tokowaka.now",
                "httpPort": 80,
                "httpsPort": 443,
                "ipVersion": "IPV4",
                "minTlsVersion": "DYNAMIC",
                "originCertificate": "",
                "originCertsToHonor": "STANDARD_CERTIFICATE_AUTHORITIES",
                "originSni": true,
                "originType": "CUSTOMER",
                "ports": "",
                "standardCertificateAuthorities": [
                    "akamai-permissive",
                    "THIRD_PARTY_AMAZON"
                ],
                "tlsVersionTitle": "",
                "trueClientIpClientSetting": true,
                "trueClientIpHeader": "True-Client-IP",
                "verificationMode": "CUSTOM"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_LLMCLIENT",
                "variableValue": "TRUE"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "caseSensitive": false,
                "extractLocation": "CLIENT_REQUEST_HEADER",
                "globalSubstitution": false,
                "headerName": "Accept-Language ",
                "regex": "^([a-zA-Z]{2}).*",
                "replacement": "$1",
                "transform": "SUBSTITUTE",
                "valueSource": "EXTRACT",
                "variableName": "PMUSER_LANG"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_X_FORWARDED_HOST",
                "variableValue": "{{builtin.AK_HOST}}"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY",
                "variableValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}};X_FORWARDED_HOST={{user.PMUSER_X_FORWARDED_HOST}}"
            }
        },
        {
            "name": "caching",
            "options": {
                "behavior": "CACHE_CONTROL_AND_EXPIRES",
                "cacheControlDirectives": "",
                "defaultTtl": "1d",
                "enhancedRfcSupport": false,
                "honorMustRevalidate": false,
                "honorPrivate": false,
                "mustRevalidate": false
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-tokowaka-api-key",
                "newHeaderValue": "<your api-key here>",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-config",
                "newHeaderValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-url",
                "newHeaderValue": "{{builtin.AK_URL}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "cacheId",
            "options": {
                "rule": "INCLUDE_VARIABLE",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY"
            }
        },
        {
            "name": "modifyIncomingResponseHeader",
            "options": {
                "action": "DELETE",
                "customHeaderName": "Age",
                "standardDeleteHeaderName": "OTHER"
            }
        },
        {
            "name": "prefreshCache",
            "options": {
                "enabled": true,
                "prefreshval": 90
            }
        },
        {
            "name": "modifyOutgoingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-Forwarded-Host",
                "newHeaderValue": "{{builtin.AK_HOST}}",
                "standardModifyHeaderName": "OTHER"
            }
        }
    ],
    "criteria": [
        {
            "name": "userAgent",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "IS_ONE_OF",
                "matchWildcard": true,
                "values": [
                    "*Tokowaka-AI*",
                    "*ChatGPT-User*",
                    "*GPTBot*",
                    "*OAI-SearchBot*"
                ]
            }
        },
        {
            "name": "path",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "MATCHES_ONE_OF",
                "normalize": false,
                "values": [
                ]
            }
        },
        {
            "name": "requestHeader",
            "options": {
                "headerName": "x-tokowaka-request",
                "matchOperator": "DOES_NOT_EXIST",
                "matchWildcardName": false
            }
        },
        {
            "name": "matchVariable",
            "options": {
                "matchCaseSensitive": true,
                "matchOperator": "IS",
                "matchWildcard": false,
                "variableExpression": "FALSE",
                "variableName": "PMUSER_TOKOWAKA_DISABLE"
            }
        }
    ],
    "criteriaMustSatisfy": "all"
}
```

중요 고려 사항:

* Tokowaka 규칙은 사용자 에이전트 + 경로 + x-tokowaka-request (없는 경우) + TOKOWAKA_DISABLE 변수 (단일 변수 토글을 사용하여 전환 허용)를 기반으로 켜집니다.
* 규칙을 **수신 요청 헤더 수정** 규칙으로 설정하여 사용자 지정 헤더 설정
* Cache-ID 수정 메커니즘을 통해 사용자 정의 변수를 사용하여 Akamai의 캐시 키를 설정합니다. 단일 사용자 정의 변수만 허용되므로 cache_key에 대해 별도의 변수를 만들고 적절하게 설정합니다.
* 언어: &quot;regex&quot;를 사용하여 Accept-Language 헤더에서 추출: &quot;^([a-zA-Z]{2}).*&quot;
* 사용자 에이전트와 일치하는 항목 내에서 캐시 ID를 수정하면 URL로 콘텐츠를 삭제할 수 없습니다(FYI만 해당).
* 사이트 장애 조치(failover) 메커니즘: 사용자 에이전트 규칙에서 일치하면 Akamai는 상태 검사를 기반으로 한 장애 조치를 허용하지 않으며 요청당 원본 응답/연결만을 기반으로 합니다. 장애 조치(failover) 응답의 경우 **x-tokowaka-fo:true** resp 헤더를 설정합니다.
* SWR은 Akamai에서 지원되지 않습니다. 따라서 TTL 기반 캐싱만 제공됩니다. 따라서 원본 응답에서 Age 헤더를 제거하도록 Akamai에서 규칙을 구성하십시오. 그렇지 않으면 TTL 기반 캐싱이 작동하지 않습니다.
* Tokowaka 규칙이 규칙 계층 구조에서 맨 아래에 있는 규칙인지 확인합니다(다른 모든 규칙보다 우선함).

>[!TAB Fastly(BYOCDN)]

**Tokowaka BYOCDN - Fastly - VCL**

![가장 빠른 VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![VCL 코드 조각 추가](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv 코드 조각**

```
unset req.http.x-tokowaka-url;
unset req.http.x-tokowaka-config;
unset req.http.x-tokowaka-api-key;

if (!req.http.x-tokowaka-request
    && req.http.user-agent ~ "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-tokowaka-url = req.url; # required for identifying the original url
  set req.http.x-tokowaka-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-tokowaka-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_Tokowaka;
}
```

**vcl_hash 코드 조각**

```
if (req.http.x-tokowaka-config) {
  set req.hash += "tokowaka";
  set req.hash += req.http.x-tokowaka-config;
}
```

**vcl_deliver 코드 조각**

```
if (req.http.x-tokowaka-config && resp.status >= 400) {
  set req.http.x-tokowaka-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-tokowaka-config && req.http.x-tokowaka-request == "failover") {
  set resp.http.x-tokowaka-fo = "1";
}
```

>[!ENDTABS]


다른 CDN 공급자의 경우 llmo-at-edge@adobe.com에 연락하여 IT/CDN 팀의 온보딩을 지원하십시오.

<!--This should probably be included Opportunities dashboard content. Content also needs serious editing - lots of "customer needs"and business user" etc.-->

구성이 완료되면 비즈니스 사용자는 LLM Optimizer에서 Edge 기회에 최적화를 위한 제안을 배포할 수 있습니다.

## 기회

| 기회 | 유형 | 자동 식별 | 자동 제안 | 자동 최적화 |
|---------|----------|----------|----------|----------|
| 컨텐츠 가시성 복구 | 기술 지역 | AI 에이전트에서 중요한 콘텐츠를 숨기는 페이지를 감지합니다. 영향을 받는 URL 및 복구할 수 있는 예상 컨텐츠를 표시합니다. | AI 에이전트에 사용할 수 있는 콘텐츠를 강조 표시하고 해당 페이지에 대한 사전 렌더링을 활성화하는 것을 권장합니다. | 완전히 렌더링된 AI 친화적인 HTML 스냅샷을 이전에 숨긴 콘텐츠를 복구하는 에이전트 트래픽에 제공합니다. |
| AI에 대한 제목 최적화 | 콘텐츠 최적화 | 제목을 스캔하여 기계 가독성을 떨어뜨릴 수 있는 비어 있거나, 중복되거나, 누락되거나, 모호한 제목을 검색합니다. | 머리글 계층 구조 및 향상된 레이블을 제안하고 각 페이지에 대해 업데이트된 구조의 미리보기를 표시합니다. | AI 에이전트에 대해 향상된 제목 구조를 삽입하고, 시각적 디자인을 유지하면서 LLM에 대해 페이지를 보다 쉽게 이해할 수 있도록 합니다. |
| AI 친화적 요약 추가 | 콘텐츠 최적화 | 는 페이지 또는 섹션 수준에서 간결한 요약이 부족한 길거나 복잡한 페이지를 식별하여 AI가 빠르게 스캔하고 이해하는 것을 어렵게 합니다. | 주요 콘텐츠를 캡처하는 페이지 수준 및 섹션 수준에서 AI가 생성한 짧은 요약을 권장합니다. | 관련 HTML 섹션에 요약을 삽입하여 모델이 페이지 콘텐츠를 해석하고 설명하는 방식을 개선합니다. |
| 관련 FAQ 추가 | 콘텐츠 최적화 | FAQ의 이점을 얻을 수 있는 기존 페이지 콘텐츠의 의도 차이를 감지합니다. | 사용자 의도와 기존 주제에 맞게 AI가 생성한 FAQ 콘텐츠를 제안합니다. | HTML에 FAQ 콘텐츠를 삽입함으로써 페이지를 AI 기반 답변에서 더 많이 찾고 연관시킬 수 있습니다. |
| 복잡한 콘텐츠 간소화 | 콘텐츠 최적화 | AI 이해를 방해할 수 있는 복잡한 텍스트로 페이지에 플래그를 지정합니다. | AI가 생성한 간소화된 버전의 복잡한 테스트를 제공하면서도 원래 의미는 그대로 유지합니다. | 페이지의 복잡한 섹션을 재작성하여 AI 가독성을 개선합니다. |

### 컨텐츠 가시성 복구

이 영업 기회는 클라이언트측 렌더링으로 인해 AI 에이전트용 주요 콘텐츠가 숨겨져 있는 페이지에 플래그를 지정합니다. 식별된 각 페이지에 대해 AI 에이전트 보기에서 누락된 콘텐츠를 정확하게 보여 주고, 가시성 차이를 강조 표시하며, 숨겨진 콘텐츠를 복구하기 위해 변경 사항을 직접 적용할 수 있도록 합니다. Edge에서 최적화를 사용하여 이 영업 기회를 배포하면 사전 렌더링된 AI 최적화 버전의 페이지가 LLM 사용자 에이전트에게 제공되어 Javascript를 실행하지 않고도 전체 컨텍스트에 액세스할 수 있습니다.

**이 사전 렌더링 기능은 Edge에서 최적화를 사용하여 배포할 때 발생하는 모든 기회에 자동으로 적용됩니다.** 이렇게 하면 AI 에이전트에게 먼저 페이지가 완전히 표시됩니다. 추가 개선 사항은 사전 렌더링된 HTML 위에 적용됩니다.

#### 추가 도구

웹 페이지 사용 가능 여부 [Adobe LLM Optimizer: 웹 페이지를 사용할 수 있습니까?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome 확장을 사용하면 LLM이 액세스할 수 있는 웹 페이지 콘텐츠의 양과 숨겨진 항목을 정확하게 확인할 수 있습니다. 독립형 무료 진단 도구로 설계되어 제품 라이선스나 설정이 필요 없습니다.

한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가하고, AI 에이전트가 보는 항목과 사람 사용자가 보는 항목을 나란히 비교하며, LLM Optimizer을 사용하여 복구할 수 있는 콘텐츠 양을 예측할 수 있습니다. [AI가 웹 사이트를 읽을 수 있습니까?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension)을(를) 참조하십시오.

### LLM에 대한 제목 최적화

이 기회는 제목 구조가 비어 있거나, 중복되거나, 누락되거나 모호한 제목으로 인해 AI 에이전트가 페이지를 이해하기 어렵게 하는 페이지를 감지합니다. 영향을 받는 각 페이지에 대해 영업 기회는 하위 머리글을 표시하며 더 명확한 계층을 권장합니다. Edge에서 최적화를 사용하여 배포하면 개선된 제목이 에이전트 트래픽에 제공되는 HTML에 적용됩니다. 이렇게 하면 사람이 보는 레이아웃은 그대로 유지하면서 시스템 가독성을 개선하는 데 도움이 될 수 있습니다.

### LLM 친화적 요약 추가

이 영업 기회는 LLM이 페이지의 내용을 신속하게 이해할 수 있도록 간결한 요약의 이점을 얻을 수 있는 페이지를 식별합니다. 각 페이지에 대해 영업 기회는 요약이 가장 필요한 위치를 감지하고 페이지 수준 및/또는 섹션 수준에서 AI가 생성한 요약을 생성합니다. Edge에서 최적화를 사용하여 배포할 때 이러한 요약은 AI 에이전트가 검색하는 HTML에 삽입되므로 콘텐츠를 보다 정확하게 설명할 가능성이 향상됩니다.

### 관련 FAQ 추가

이 기회는 추가 Q&amp;A 콘텐츠가 AI 기반 검색에서 사용자 의도와 프롬프트에 보다 잘 부합할 수 있는 페이지에 플래그를 지정합니다. 각 페이지에 대해 페이지의 사용자 의도와 콘텐츠에 연결된 AI가 생성한 FAQ 블록을 제안합니다. Edge에서 최적화를 사용하면 이러한 FAQ가 HTML에 삽입되므로 페이지를 AI 친화적이고 AI 응답이 지침을 직접 반영할 가능성이 높아집니다.

### 복잡한 콘텐츠 간소화

이번 기회는 AI 이해도를 떨어뜨릴 수 있는 길고 복잡한 단락이 있는 페이지를 찾는다. 가독성 임계값을 초과하는 각 페이지에 대해 원래 의미를 유지하면서 보다 간단하고 훑어보기가 가능한 AI 생성 콘텐츠를 만듭니다. 에지에 배포되면 에이전트 트래픽에 전달되는 간소화된 콘텐츠를 통해 LLM이 콘텐츠를 보다 충실하게 해석하고 요약할 수 있습니다.

## 제안 사항

각 기회에 대해 에지에서 최적화를 미리 보고, 편집하고, 배포하고, 라이브 미리 보고, 롤백할 수 있습니다.

### 미리보기

미리보기를 통해 어떤 조치가 실행되기 전에 사용자에게 페이지에 대한 제안의 영향을 볼 수 있습니다. 현재 페이지와 제안을 적용한 후 예상되는 AI 최적화 버전 간의 병렬 차이가 나타납니다. 이 보기는 라이브 트래픽을 활성화하지만 안전한 격리된 미리보기 모드에서 작동하는 동일한 Edge 최적화 로직을 사용합니다. 이는 검토를 위한 읽기 전용 시뮬레이션이므로 라이브 트래픽에는 영향을 주지 않습니다.

![미리보기](/help/assets/optimize-at-edge/preview.png)

### 편집

편집 을 사용하면 자동 생성된 제안을 배포하기 전에 수정하거나 모두 다시 작성할 수 있습니다. 제안을 수동적으로 수락하는 대신 사용자는 루프 내에서 이 워크플로를 통해 모든 권한을 유지합니다. 이 보기에는 구조화된 편집기에 제안된 변경 사항이 표시되며, 이를 통해 사용자는 자신의 의도에 맞게 텍스트를 수정할 수 있습니다. 그런 다음 배포되면 편집된 버전이 AI 에이전트에 제공됩니다.

![편집](/help/assets/optimize-at-edge/edit.png)

### 배포

배포는 선택한 제안을 게시하여 에지에서 AI 에이전트에게 최적화된 경험을 제공할 수 있습니다. CDN이 완전히 라우팅되는 경우 도메인의 모든 페이지는 일반적으로 몇 분 안에 새로운 변경 사항을 따릅니다. 선택한 경로에 대해서만 라우팅이 구성된 경우 허용 목록에추가된 페이지만 최적화에 따라 활성화됩니다.

![배포](/help/assets/optimize-at-edge/deploy.png)

### 라이브 보기

라이브 보기를 통해 사용자는 최적화가 라이브인지 확인하고 에이전트 트래픽에 대해 예상대로 작동하는지 확인할 수 있습니다. 그렇지 않으면 보기가 제대로 액세스되지 않을 수 있습니다. 사용자는 고정 제안 아래에서 라이브 페이지를 볼 수 있으며, 이렇게 하면 페이지가 AI 에이전트에 표시된 대로 렌더링됩니다.

![실시간 보기](/help/assets/optimize-at-edge/view-live.png)

### 롤백

롤백은 이전에 배포한 최적화를 안전하게 되돌립니다. 페이지의 AI 전용 버전은 일반적으로 몇 분 내에 이전 상태로 반환되므로 사용자가 필요한 경우 최적화를 실험해 볼 수 있습니다.

![롤백](/help/assets/optimize-at-edge/rollback.png)

## 자주 묻는 질문

Q. Edge에서 어떤 종류의 LLM을 최적화로 타깃팅합니까?

고객이 온보딩 시 타겟팅할 사용자 에이전트 목록을 완전히 정의합니다.

Q. Edge에서 최적화의 &quot;Edge&quot;는 무엇을 의미합니까?

여기에서 &quot;Edge&quot;는 최적화가 CMS 내부가 아닌 CDN 계층에서 적용됨을 의미합니다.

Q. 이 최적화에 CDN이 필요한 이유는 무엇입니까?

CDN은 페이지의 최적화된 버전이 조합되어 AI 에이전트로 전달되는 곳입니다. CDN을 활용하여 원본 CMS이 변경되지 않도록 합니다. 이러한 분리를 통해 기존 게시 워크플로우를 변경하지 않고 LLM 가시성을 향상시킬 수 있습니다.

Q. Edge에서 최적화를 위해 온보딩되지 않은 경우 어떻게 됩니까?

필요한 설정을 완료하기 전에 **최적화 배포**&#x200B;를 클릭하면 사이트에 아무 것도 적용되지 않습니다. 대신 팝업 대화 상자가 나타나 팀에 문의하라는 메시지가 표시됩니다. llmo-at-edge@adobe.com 온보딩 지원. 온보딩이 완료될 때까지 감지된 영업 기회와 제안을 탐색할 수 있지만, 원클릭 배포 워크플로우는 비활성 상태로 유지됩니다.

질문: 소스에서 콘텐츠가 업데이트되면 어떻게 됩니까?

기본 소스 페이지가 변경되지 않는 한 캐시에서 최적화된 페이지 버전을 제공합니다. 그러나 소스가 변경되면 시스템이 자동으로 새로 고쳐져 AI 에이전트는 항상 최신 콘텐츠를 수신하게 됩니다. 사이트의 콘텐츠 업데이트가 해당 창 내에서 새로운 최적화를 트리거하도록 낮은 캐시 TTL을 분 단위로 사용하기 때문입니다. 모든 사이트에 맞는 범용 TTL이 없으므로 두 시스템이 동기화 상태를 유지하도록 캐시 무효화 규칙을 기반으로 이 TTL을 구성할 수 있습니다.

Q. Edge에서 Adobe EDS(Edge Delivery Service)를 사용하는 사이트에 대해서만 최적화됩니까?

아니요. Edge에서 최적화는 CDN에 종속되지 않으며 Adobe의 EDS 스택에 배포된 아키텍처뿐만 아니라 모든 프론트엔드 아키텍처와 작동합니다.

Q. Edge에서 최적화 사전 렌더링은 기존의 서버측 렌더링(SSR)과 어떻게 다릅니까?

이 둘은 서로 다른 문제를 해결하고 함께 일할 수 있다. 기존 SSR은 서버측 콘텐츠를 렌더링하지만 나중에 브라우저에서 로드되는 콘텐츠는 포함하지 않습니다. Edge에서 최적화 사전 렌더링은 JavaScript 및 클라이언트측 데이터가 로드된 후 페이지를 캡처하여 CDN 에지에서 완전히 조립된 버전을 생성합니다. SSR은 사용자 경험 개선에 중점을 두고 있으며, Edge에서 최적화는 LLM의 웹 경험을 개선합니다.


















