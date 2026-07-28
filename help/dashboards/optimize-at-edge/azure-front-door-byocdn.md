---
title: Optimize at Edge - Azure Front Door(BYOCDN)
description: LLM Optimizer에서 Optimize at Edge를 위해 Azure Front Door BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-07-15T17:40:54.797Z'
TQID: 'https://experienceleague.adobe.com/fe-kultqzWQdRdcUjzfNs21UpL6m5zcoAmaQyMMv5kk'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: d1956731-2adb-4bb7-8301-2b239254ac72id: e1b649f0-0a61-46e4-9082-64d5cb2576c6id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3aid: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2: id: d23587d6-14d6-4e3f-9ee1-cc18623832e1id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: ht
source-wordcount: 768
ht-degree: 100%

---


# Azure Front Door(BYOCDN)

이 구성은 에이전틱 트래픽(AI 봇 및 LLM 사용자 에이전트의 요청)을 Edge Optimize 백엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 기존과 동일하게 사용자의 원본 서버에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 헤더 `x-edgeoptimize-request-id`를 찾습니다.

Azure Front Door는 엣지에서 사용자 정의 코드를 실행하지 않습니다. Edge Optimize를 위한 전용 **원본 그룹**&#x200B;과 함께 **규칙 집합**&#x200B;을 사용하여 라우팅이 구성됩니다.장애 조치는 Azure Front Door의 우선 순위 기반 원본 그룹 상태 프로브에 의해 처리됩니다.

**사전 요구 사항**

Azure Front Door 라우팅 규칙을 설정하기 전에 다음을 확인하십시오.

* Azure Front Door 프로필에 액세스합니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키 단계는 [API 키 검색](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#production-api-key)을 참조하십시오.
* (선택 사항) 스테이징 라우팅을 테스트하려면 [스테이징 API 키](/help/dashboards/optimize-at-edge/retrieve-api-keys.md#staging-api-key-optional)를 참조하십시오.

## 1단계: Edge Optimize용 원본 그룹을 생성합니다.

Azure Front Door 프로필에는 이미 원본을 가리키는 기본 원본 그룹이 있습니다.Edge Optimize용 **새** 원본 그룹 만들기:

* **이름:** `edge-optimize-origin-group`
* **원본(우선 순위 기반의 장애 조치):**
  * **우선 순위 1** — `live.edgeoptimize.net`(원본 호스트 헤더: `live.edgeoptimize.net`)
  * **우선 순위 2** — 도메인 엔드포인트(예: `www.example.com`). 이는 장애 조치입니다. Edge Optimize가 비정상인 경우에는 요청이 도메인으로 라우팅되고, 이 도메인은 Azure Front Door에 다시 진입하고 기본 원본에서 서비스를 제공합니다.
* **상태 프로브:** **활성화됨**
  * 경로: `/health/<your-domain>`(예: `/health/www.example.com`)
  * 프로토콜: HTTPS
  * 간격: 225초
* **세션 선호도:** **비활성화됨**
* **인증서 제목 이름 유효성 검사:** **활성화됨**

![우선 순위 기반 원본 및 상태 프로브를 포함한 Edge Optimize 원본 그룹](/help/assets/optimize-at-edge/azure-front-door-origin-group.png)

>[!NOTE]
>
>`edge-optimize-origin-group` 원본 그룹은 포털에 **&#39;연결 해제됨&#39;** 경고를 표시합니다. 이는 예상되는 동작입니다. 경로가 직접 참조하는 것이 아니라 규칙 세트 경로 재정의를 통해 참조됩니다.

## 2단계: 경로 구성

기본 경로는 일반적으로 Azure Front Door 프로필로 만들어집니다. 규칙 세트(3단계)는 에이전틱 트래픽의 원본 그룹을 재정의하므로 Edge Optimize를 위한 별도의 경로가 필요하지 않습니다.

## 3단계: 규칙 세트 만들기

**규칙 세트** > **규칙 세트 추가**&#x200B;로 이동하여 이름을 `EORouting`으로 지정합니다. 다음 순서로 3개의 규칙을 추가합니다.

![헤더 제거 및 봇 라우팅 규칙을 표시하는 EORouting 규칙 집합](/help/assets/optimize-at-edge/azure-front-door-ruleset-routing.png)

### 규칙 1: StripIncomingEOHeaders01

스푸핑 방지를 위해 수신되는 Edge Optimize 헤더를 제거합니다. 조건 없음 — 모든 요청에 적용됩니다. 평가 중지: **꺼짐**.

**액션** — 각 항목에 대한 요청 헤더 삭제:

* `x-edgeoptimize-url`
* `x-edgeoptimize-config`
* `x-edgeoptimize-api-key`
* `x-edgeoptimize-fetcher-key`

### 규칙 2: EOGPTBotRootGET03

HTML 페이지 경로의 봇 요청을 Edge Optimize로 라우팅합니다. 평가 중지: **켜짐**.

**조건**(모두 일치해야 함):

* 요청 방법: **같음** `GET`
* 요청 경로: **RegEx**`(^$|^.*/$|(^|.*/)[^./]+$|^.*\.html$)`(사이트 루트, `/`로 끝나는 경로, 확장 없는 페이지 경로 및 `.html` 경로와 일치)
* 사용자-에이전트: `chatgpt-user`, `gptbot`, `oai-searchbot`, `adobeedgeoptimize-ai`, `perplexitybot`, `perplexity-user`, `claudebot`, `claude-user`, `claude-searchbot` **중 어느 것이든 포함합니다**. 문자열 변환을 **소문자로** 설정합니다.
* `x-edgeoptimize-monitor`: **포함하지 않음** `1`
* `x-edgeoptimize-request`: `failover`, `1` 중 **어느 것도 포함하지 않습니다**.

**액션**:

* 요청 헤더 덮어쓰기 `x-edgeoptimize-url` = `/{url_path}?{query_string}`
* 요청 헤더 덮어쓰기 `x-edgeoptimize-config` = `LLMCLIENT=TRUE;`
* 요청 헤더 덮어쓰기 `x-edgeoptimize-api-key` = `YOUR_API_KEY`
* 요청 헤더 덮어쓰기 `x-edgeoptimize-monitor` = `1`
* 경로 구성 재정의: 원본 그룹 → `edge-optimize-origin-group`, 전달 프로토콜 → 들어오는 요청 일치, 캐싱 → **비활성화됨**

### 규칙 3: HealthProbeRewrite03

Azure Front Door 상태 프로브 요청이 `/health/<domain>`가 아닌 `/`로 원본에 도달하도록 다시 작성합니다. 이를 통해 원본에 전용 상태 엔드포인트를 지정하지 않고도 Azure Front Door가 Edge Optimize 가용성을 모니터링하도록 할 수 있습니다.평가 중지: **켜짐**.

![상태 프로브 재작성 규칙](/help/assets/optimize-at-edge/azure-front-door-ruleset-healthprobe.png)

**조건**(모두 일치해야 함):

* 요청 URL 경로: **시작 문자** `/health/`
* `x-fd-healthprobe`: **포함** `1`

**액션**:

* URL 재작성 — 소스 패턴: `/health/`, 대상: `/`
* 응답 헤더 덮어쓰기 `custom-origin-health` = `routed`(진단 — 확인 후 제거할 수 있음)
* 요청 헤더 추가 `user-agent` = ` AdobeEdgeOptimize/1.0`(선행 공백 추가 — Azure Front Door가 값을 있는 그대로 추가)
* 경로 구성 재정의: 원본 그룹 → `default-origin-group`, 전달 프로토콜 → 들어오는 요청 일치, 캐싱 → **비활성화됨**

## 4단계: 규칙 세트를 경로와 연결

경로를 열고 하단의 **규칙** 섹션으로 스크롤한 다음 드롭다운에서 `EORouting` 규칙 세트를 선택합니다. 기존 규칙 세트가 있는 경우 **맨 위로 이동**&#x200B;을 사용하여 **#1**&#x200B;에서 `EORouting` 위치를 지정합니다.Optimize at Edge 규칙은 에이전틱 트래픽과 Edge Optimize 루프백 요청만 가로채므로 다른 모든 트래픽은 다른 규칙에 영향을 미치지 않고 통과합니다. 저장한 후 전파를 기다립니다(약 20분).

## 방화벽 규칙을 통해 Optimize at Edge 허용(선택 사항)

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

{{verify-routing-status-in-ui}}

{{return-to-overview}}
