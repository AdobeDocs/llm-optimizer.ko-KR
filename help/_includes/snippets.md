---
source-git-commit: da789100d814004687de2f46e18a295671dec4b8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 10%

---
# 스니펫

## API 키 검색 단계 {#retrieve-byocdn-api-key}

**프로덕션 Edge 최적화 API 키를 검색하는 단계:**

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **AI 에이전트에 최적화 배포** 섹션을 찾습니다. **최적화 엔진 사용** 확인란을 선택합니다.

   ![AI 에이전트에 최적화 배포 — 보류 중](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. 확인 대화 상자에서 **사용**&#x200B;을 선택합니다.

   ![최적화 엔진 확인 대화 상자 사용](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. **세부 정보 보기**&#x200B;를 선택합니다. **최적화 배포 세부 정보** 대화 상자에서 **프로덕션 API 키**&#x200B;을(를) 복사합니다(**필드 옆** 사용).

   ![배포 최적화 세부 정보의 프로덕션 API 키](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >대화 상자에서 설정이 완료되지 않았음을 보여줄 수 있습니다. 이는 라우팅을 확인할 때까지 발생합니다. IT 또는 CDN 팀이 구성을 완료할 수 있도록 API 키를 복사할 수 있습니다.

또한 위 단계에 대한 도움이 필요한 경우 Adobe 계정 팀 또는 `llmo-at-edge@adobe.com`에 문의하십시오.

## 스테이징 도메인 API 키(선택 사항) {#retrieve-staging-edge-optimize-api-key}

프로덕션 트래픽이 라우팅 규칙을 사용하기 전에 더 낮은 환경에서 Edge에서 최적화를 테스트하려면 스테이징 호스트 이름을 사용하십시오.

**사전 요구 사항**

* 스테이징 호스트 이름은 프로덕션 사이트와 **같은 등록 가능한 도메인**&#x200B;에 속해야 합니다(예: 프로덕션이 `https://www.example.com`인 경우 `https://staging.example.com`).
* 사이트에 대해 **one** 스테이징 도메인만 구성할 수 있습니다. 저장된 후에는 지원 없이 변경할 수 없습니다.

**단계**

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고 **CDN 구성** 탭을 선택합니다.

2. **AI 에이전트에 최적화 배포** 섹션에서 **단계 도메인 추가**(또는 스테이징 도메인이 이미 구성된 경우 **단계 도메인**)를 선택합니다.

3. **도메인 스테이징** 대화 상자에서 `https://`을(를) 포함한 전체 스테이징 URL을 입력하고 **도메인 설정**&#x200B;을(를) 선택합니다.

   ![단계 도메인 입력 대화 상자](/help/assets/optimize-at-edge/byocdn-staging-domain-input.png)

4. 다음 프롬프트에서 도메인을 확인합니다. 워크플로우가 완료되면 **도메인 스테이징** 대화 상자에 구성된 도메인과 해당 **API 키**&#x200B;가 표시됩니다. **복사**&#x200B;를 선택하여 스테이징 API 키를 복사합니다.

   ![스테이징 도메인 API 키](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

도움이 필요하면 `llmo-at-edge@adobe.com`에 문의하세요.

## LLM Optimizer에서 라우팅 상태 확인 {#verify-routing-status-in-ui}

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

![AI 에이전트에 최적화 배포 — 완료됨](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## 개요로 돌아가기 {#return-to-overview}

사용 가능한 기회, 자동 최적화 워크플로 및 FAQ를 포함하여 Edge에서 최적화에 대해 자세히 알아보려면 [Edge에서 최적화 개요](/help/dashboards/optimize-at-edge/overview.md)로 돌아가십시오.
