---
title: Edge에서 최적화 - Apache HTTP 서버
description: LLM Optimizer의 Edge에서 최적화하기 위해 Apache HTTP Server(자체 호스팅 역방향 프록시) BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
source-git-commit: d7e723161836027dcdde931378f5d0f776a1ecfc
workflow-type: tm+mt
source-wordcount: 585
ht-degree: 32%

---


# Apache HTTP 서버

이 구성은 Apache HTTP Server가 원본(자체 호스팅 설정, **없이** AEM Dispatcher) 앞에서 역방향 프록시 역할을 하는 경우에 적용됩니다. 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 기존과 동일하게 사용자의 원본 서버에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 헤더 `x-edgeoptimize-request-id`를 찾습니다.

통합은 네이티브 Apache `Include` 파일 집합입니다. 배포할 코드나 작업자가 없습니다. 세 개의 파일을 다운로드하고 API 키를 설정한 다음 가상 호스트에 두 개의 `Include` 줄을 추가합니다.

**사전 요구 사항**

Apache 라우팅 규칙을 설정하기 전에 다음을 확인하십시오.

* `proxy`, `proxy_http`, `ssl`, `rewrite`, `headers`, `env` 및 `setenvif` 모듈이 활성화된 Apache HTTP Server 2.4 이상
* Apache 구성(사이트의 `<VirtualHost>`)에 액세스하고 Apache를 다시 로드하는 기능입니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키 단계는 [API 키 검색](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key)을 참조하십시오.
* (선택 사항) 스테이징 라우팅을 테스트하려면 [스테이징 API 키](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional)를 참조하십시오.

## 구성

**1. 구성 파일 다운로드**

다음 세 개의 Edge 최적화 포함 파일을 [Edge 코드 샘플 저장소에서 최적화](https://github.com/adobe/llmo-code-samples/tree/main/optimize-at-edge/apache)에서 다운로드하고 Apache 서버의 디렉터리(예: `conf/oae/`)에 배치합니다.

| 파일 | 목적 |
|------|---------|
| `oae-routing.conf` | AI 보트를 감지하고 Edge 최적화 헤더를 삽입하고 HTML 페이지 요청을 백엔드로 라우팅하며 캐시 격리 및 장애 조치를 설정합니다. |
| `oae-failover.conf` | Edge 최적화가 오류를 반환하는 경우 원래 요청을 원본에 대해 재생합니다. |
| `domains.conf` | 도메인당 Edge에서 최적화를 활성화하고 API 키를 보유합니다. |

`oae-routing.conf` 또는 `oae-failover.conf`을(를) 수정할 필요가 없습니다. 그대로 사용하십시오.

**2. 도메인을 사용하도록 설정하고 API 키(`domains.conf`)** 설정

`domains.conf`을(를) 편집하고 사용 중인 도메인당 한 줄을 추가합니다. 호스트를 도메인으로 바꾸고 `YOUR_API_KEY`을(를) LLM Optimizer UI의 키로 바꿉니다. 목록에 없는 도메인은 원본 경로를 변경하지 않았으므로 한 번에 하나의 도메인을 활성화할 수 있습니다.

```
SetEnvIfExpr "%{HTTP_HOST} =~ m#(?i)^(www\.)?example\.com(:\d+)?$#" OAE_DOMAIN_ENABLED=1 OAE_API_KEY=YOUR_API_KEY
```

**3. 가상 호스트**&#x200B;에 파일 포함

기존 `<VirtualHost *:443>`에 두 개의 `Include` 줄을 추가합니다. 라우팅 파일이 다시 작성되기 **전**, 규칙이 `ProxyPass`이고 장애 조치(failover) 파일은 **후**&#x200B;됩니다. 아래 예제에서 `#NEWLINE`이라고 표시된 줄은 Edge에서 최적화하기 위해 추가하는 유일한 줄입니다. 그 외 모든 항목(`ServerName`, `ProxyPass`, 나머지)은 변경되지 않은 기존 구성입니다.

```
Define OAE_CONF_DIR conf/oae                       #NEWLINE  directory holding the OAE include files

<VirtualHost *:443>
    ServerName www.example.com

    Include "${OAE_CONF_DIR}/oae-routing.conf"     #NEWLINE  OAE routing — BEFORE your Rewrite & ProxyPass rules

    # --- your existing rewrite rules and ProxyPass to origin ---
    ProxyPass        "/" "https://www.example.com/"
    ProxyPassReverse "/" "https://www.example.com/"

    Include "${OAE_CONF_DIR}/oae-failover.conf"    #NEWLINE  OAE failover — AFTER your ProxyPass rules
</VirtualHost>
```

**4. Apache** 다시 로드

구성을 확인하고 Apache를 다시 로드하여 변경 사항을 적용합니다.

>[!NOTE]
>
>봇에 최적화된 응답과 사람 응답은 자동으로 별도의 캐시 항목에 보관됩니다(라우팅 파일은 `Vary: x-edgeoptimize-config`을(를) 설정합니다). Apache에서 이미 `mod_cache`을(를) 사용하는 경우 Edge 최적화 헤더가 설정된 후에 캐시 조회가 실행되도록 `CacheQuickHandler Off`이(가) 있는지 확인하십시오.

## 방화벽 규칙을 통해 Edge에서 최적화 허용(선택 사항)

{{waf-allowlist-setup}}

## 설정 확인

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
| `x-edgeoptimize-request-id` | 있음 - 고유한 요청 ID가 포함되어 있습니다. | 없음 |
| `x-edgeoptimize-fo` | 장애 조치가 발생한 경우에만 표시됩니다(값: `1`). | 없음 |

{{verify-routing-status-in-ui}}

{{return-to-overview}}
