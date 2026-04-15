---
source-git-commit: e9309dc8f8d1d81b953483f17dcb424e46d5cd3b
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 20%

---
# 스니펫

## API 키 검색 단계 {#retrieve-byocdn-api-key}

**프로덕션 Edge 최적화 API 키를 검색하는 단계:**

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고  **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **AI 에이전트에 최적화 배포** 섹션을 찾습니다. **최적화 엔진 활성화** 확인란을 선택합니다.

   ![AI 에이전트에 최적화 배포 — 보류 중](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. 확인 대화 상자에서 **활성화**&#x200B;를 선택합니다.

   ![최적화 엔진 확인 대화 상자 활성화](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. **세부 정보 보기**&#x200B;를 선택합니다. **최적화 배포 세부 정보** 대화 상자에서 **프로덕션 API 키**&#x200B;을(를) 복사합니다(**필드 옆** 사용).

   ![배포 최적화 세부 정보의 프로덕션 API 키](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >대화 상자에서 설정이 완료되지 않았음을 보여줄 수 있습니다. 이는 라우팅을 확인할 때까지 발생합니다. IT 또는 CDN 팀이 구성을 완료할 수 있도록 API 키를 복사할 수 있습니다.

또한 위 단계에 대한 도움이 필요한 경우 Adobe 계정 팀 또는 `llmo-at-edge@adobe.com`에 문의하십시오.

## 선택 사항: 스테이징 호스트 이름에서 라우팅을 테스트합니다 {#retrieve-staging-edge-optimize-api-key}

**선택 사항: 스테이징 호스트 이름에서 라우팅을 테스트합니다**

프로덕션 라우팅을 활성화하기 전에 더 낮은 환경에서 라우팅을 확인하려는 경우 스테이징 호스트 이름을 구성할 수 있습니다.

**요구 사항**

* 스테이징 호스트 이름은 프로덕션과 동일한 **등록 가능한 도메인**&#x200B;에 있어야 합니다(예: 프로덕션이 `https://www.example.com`인 경우 `https://staging.example.com`).
* 사이트당 **one** 스테이징 도메인만. 저장되면 Adobe에 문의하지 않으면 변경할 수 없습니다.

**스테이징 API 키 가져오기**

1. **고객 구성**&#x200B;을 열고 **CDN 구성**&#x200B;을 선택합니다.
2. **AI 에이전트에 최적화 배포**&#x200B;에서 **단계 도메인 추가**(또는 스테이징 도메인이 이미 구성된 경우 **단계 도메인**)를 선택합니다.
3. `https://`을(를) 포함한 전체 스테이징 URL을 입력하고 **도메인 설정**&#x200B;을(를) 선택하십시오.
4. 확인 대화 상자에서 **스테이징** API 키를 복사합니다.

![스테이징 도메인 API 키](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

스테이징 API 키를 사용하여 스테이징 환경에 동일한 라우팅 규칙을 배포합니다.

**스테이징 보트 트래픽 테스트**

`https://staging.example.com/page.html`을 실제 스테이징 URL 및 경로로 바꿉니다. **성공:** 응답에 `x-edgeoptimize-request-id` 헤더가 포함되어 있습니다.

도움이 필요하면 `llmo-at-edge@adobe.com`에 문의하세요.

## LLM Optimizer에서 라우팅 상태 확인 {#verify-routing-status-in-ui}

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

![AI 에이전트에 최적화 배포 — 완료됨](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## 방화벽 규칙을 통해 Edge에서 최적화 허용(선택 사항) {#waf-allowlist-setup}

CDN에서 WAF 또는 보트 관리자를 사용하는 경우:

* Edge 서비스에서 최적화 서비스를 통해 원본 콘텐츠를 가져올 수 있도록 WAF 또는 봇 관리자에서 `*AdobeEdgeOptimize/1.0*` 사용자 에이전트를 최적화합니다.
* 방화벽에 사용자 에이전트 이외의 추가 확인이 필요한 경우 암호를 생성하고(예: `openssl rand -hex 32`):
   * 다른 `x-edgeoptimize-*` 헤더와 함께 라우팅 규칙에 암호가 포함된 `x-edgeoptimize-fetcher-key`을(를) 추가합니다.
   * `x-edgeoptimize-fetcher-key`이(가) 같은 암호와 일치하는 요청을 허용하도록 WAF 또는 보트 관리자 규칙을 추가합니다.
* Edge에서 최적화 는 이 헤더를 있는 그대로 전달합니다. — 전체 키 라이프사이클을 소유합니다.

## 개요로 돌아가기 {#return-to-overview}

사용 가능한 기회, 자동 최적화 워크플로 및 FAQ를 포함하여 Edge에서 최적화에 대해 자세히 알아보려면 [Edge에서 최적화 개요](/help/dashboards/optimize-at-edge/overview.md)로 돌아가십시오.
