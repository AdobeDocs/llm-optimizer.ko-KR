---
title: 복잡한 콘텐츠 간소화
description: LLM Optimizer에서 AI 에이전트가 해석하기 어려운 고밀도 사본을 통해 트래픽이 많은 페이지를 식별하는 방법과 Edge에서 최적화로 간소화된 텍스트를 검토하고 배포하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-05-15T17:58:39.879Z'
TQID: 'https://experienceleague.adobe.com/wO3ZY-fEgOi7cD4dq0kCltk-YJSD431bkA6-9PW42Lo'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 564171851fdccee43afd233da143d66182464889
workflow-type: tm+mt
source-wordcount: 785
ht-degree: 1%

---


# 복잡한 콘텐츠 간소화

복잡한 콘텐츠 간소화 영업 기회를 통해 AI 에이전트가 주요 정보를 해석하기 어렵게 만드는 밀집되거나 복잡한 텍스트가 있는 트래픽이 많은 페이지를 식별할 수 있습니다. 기존 사본의 의미를 살리면서 보다 명확하고 스캔하기 쉬운 버전을 도입했습니다. 이렇게 하면 에이전트가 중요한 정보를 보다 안정적으로 구문 분석하고, 요약하고, 추출할 수 있습니다.

영향을 받는 각 URL에 대해 **향상된 텍스트** 제안을 검토하고 **미리 보기**&#x200B;와 비교한 다음 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)와(과) 함께 배포하면 에이전트 트래픽에서 CMS(콘텐츠 관리 시스템) 변경 없이 보다 명확한 HTML을 받을 수 있습니다.

## 문제 해결 방법

수정 사항은 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 적용됩니다.

- 사전 렌더링된 HTML 스냅샷을 AI 에이전트에 제공합니다.
- 복잡한 구문이 라이브 페이지에 정렬된 **향상된 텍스트**(으)로 대체되거나 확대되도록 에이전트 표시 페이지를 업데이트합니다.
- CDN 계층에서 작동합니다(CMS 변경 사항 없음).
- AI 전용 — 사람 방문자나 SEO 봇에 영향을 주지 않습니다.
- 몇 분 후에 배포되며 LLM Optimizer 인터페이스에서 **완전히 취소 가능**&#x200B;합니다.

## 작동 방식

LLM Optimizer은 높은 에이전트 트래픽을 수신하는 페이지와 콘텐츠 점수가 가독성 임계값 미만인 페이지를 식별한 다음 사본 재작성을 제안합니다. 각 페이지에 대해 다음 항목이 있습니다.

**향상된 텍스트** - 페이지에 이미 있는 내용에 기반을 둔 단순화된 콘텐츠입니다.
**미리 보기** - 에이전트 트래픽에 대한 비교 전후.

영향을 받는 URL은 **현재 제안** 탭의 **제안 있는 URL** 테이블에 표시되며 행을 확장하여 각 권장 사항을 검사할 수 있습니다.

현재 제안에 대한 제안이 있는 ![URL, 향상된 텍스트와 미리 보기로 확장된 행](/help/dashboards/opportunities/assets/simplify-complex-content-expand.png)

**제안 사항이 있는 URL** 표에는 단순화된 콘텐츠가 무의미한 이해에 도움이 되는 페이지가 나열되어 있습니다. 제안은 **현재 제안**, **수정 제안** 및 **무시된 제안**&#x200B;으로 구성됩니다. 각 URL에 대해 다음 작업을 수행할 수 있습니다.

- **행을 확장**&#x200B;하여 해당 페이지에 대한 **향상된 텍스트** 제안을 봅니다.
- 에이전트 트래픽에 대한 이전 및 이후 비교를 **미리 보기**&#x200B;합니다.
- LLM Optimizer 외부의 영업 기회를 해결한 경우 **고정으로 표시**.
- 관련성이 없는 **제안 무시**&#x200B;개

**보기**&#x200B;에는 **현재 제안**, **수정 제안**(배포된 경우 **최적화** 상태) 및 **무시된 제안**&#x200B;이 포함됩니다. **고정 제안**&#x200B;에서 **실시간 보기**&#x200B;를 사용하여 실시간 배포를 확인하고 언제든지 롤백할 수 있습니다.

확인란을 사용하여 배송할 URL 또는 줄 항목이 **개선된 텍스트**&#x200B;인 경우 선택한 다음 **영업 기회 계획** 헤더에서 **고정으로 표시**, **제안 무시** 또는 **최적화 배포**&#x200B;를 사용합니다. 또한 데모 UI에는 선택 카운트 및 목록과 관련된 작업이 표시됩니다.

![계획 헤더에서 영업 기회 계획, 현재 제안, 확장된 행 및 배포 최적화](/help/dashboards/opportunities/assets/simplify-complex-content-select.png)

### 최적화 배포

Edge에 게시할 준비가 되면 **최적화 배포**&#x200B;를 클릭합니다. **Edge에 배포** 대화 상자에 선택한 URL 및 최적화 세부 정보가 나열됩니다. 목록을 검토한 다음 **배포** 또는 **취소**&#x200B;를 선택하십시오.

![Edge에 배포 대화 상자](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-dialog.png)

배포에 성공하면 **배포 완료**&#x200B;에서 최적화 실행 횟수를 확인하고 AI 에이전트가 업데이트를 인덱싱하는 데 시간이 걸릴 수 있습니다. 대화 상자를 닫고 **수정 제안**&#x200B;을 열어 상태를 확인합니다.

![배포 완료 확인](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-confirm.png)

>[!NOTE]
>
>최적화를 배포하려면 Edge 온보딩 프로세스에서 최적화해야 합니다. 아직 온보딩하지 않은 경우 **최적화 배포**&#x200B;를 클릭하면 온보딩 프로세스로 이동합니다. Edge에서 최적화 작동 방법, 지원되는 CDN 공급자 및 온보딩 프로세스에 대한 자세한 내용은 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

### 수정된 제안 사항 및 라이브 보기

**수정된 제안**&#x200B;에서 배포된 URL은 상태 열에 **최적화됨**&#x200B;을(를) 표시합니다. 행을 확장하여 배포된 **향상된 텍스트** 및 지침을 검토합니다.

![최적화된 상태, 확장된 간소화된 복사본, 라이브 보기 및 세부 정보로 수정 제안 탭](/help/dashboards/opportunities/assets/simplify-complex-content-fixed.png)

확인(적용되는 간소화된 경로 포함)에 제공된 대로 **현재 페이지 콘텐츠**&#x200B;의 읽기 전용 보기를 열려면 행에서 **라이브 보기**&#x200B;를 클릭하십시오. 분석에 **세부 정보**&#x200B;을(를) 사용합니다.

![라이브 보기 — 에이전트의 간소화된 텍스트를 포함하는 현재 페이지 콘텐츠](/help/dashboards/opportunities/assets/simplify-complex-content-view-live.png)

가장자리 변경 내용을 일괄적으로 되돌리려면 확인란을 사용하여 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 사용합니다.

![헤더에서 배포된 행, 최적화된 상태 및 롤백을 사용한 수정 제안](/help/dashboards/opportunities/assets/simplify-complex-content-rollback.png)

## 롤백

마음이 바뀌면 배포된 모든 최적화를 롤백할 수 있습니다. **수정 제안** 보기에서 되돌릴 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 클릭합니다.

**롤백** 대화 상자에는 롤백할 제안 사항이 나열되며 배포된 최적화가 되돌아갈 것이라는 짧은 경고가 표시됩니다. 목록을 확인한 다음 **롤백** 또는 **취소**&#x200B;를 클릭합니다.

되돌리기 제안을 나열하는 ![롤백 대화 상자](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-dialog.png)

작업이 완료되면 **성공적으로 롤백됨** 요약이 나타납니다. 대시보드로 돌아가려면 닫으십시오.

![롤백 완료 — 롤백되었습니다](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-confirm.png)

## 데모에서 사용해 보기

[Frescopa 데모](https://play.llmo.now/org/demo-org)에서 복잡한 콘텐츠 간소화 워크플로를 살펴보십시오.
