---
source-git-commit: b13f91d144d4899198891c4dcd841de8cfbb2355
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 14%

---
# 스니펫

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
