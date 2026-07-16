---
title: 복잡한 콘텐츠 간소화
description: LLM Optimizer에서 AI 에이전트가 해석하기 어려운 밀도 높은 사본을 통해 트래픽이 많은 페이지를 식별하는 방법과 Optimize at Edge로 간소화된 텍스트를 검토하고 배포하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-07-15T18:04:55.581Z'
TQID: 'https://experienceleague.adobe.com/uMK9qeAGMNrtvR0TYbeg8SIOKlwKf4L5NIE9ZgsJaUw'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
subfeature_v2:
  - id: bbfc1b77-44c5-4fe8-b65f-ec160fe0d021
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 785
ht-degree: 100%

---


# 복잡한 콘텐츠 간소화

복잡한 콘텐츠 간소화 기회를 통해 AI 에이전트가 주요 정보를 해석하기 어렵게 만드는 밀도가 높거나 복잡한 텍스트가 있는 트래픽이 많은 페이지를 식별합니다. 원래 의미를 유지하면서 기존 사본의 더 명확하고 스캔하기 쉬운 버전을 소개합니다. 이는 에이전트가 중요한 정보를 보다 안정적으로 구문 분석, 요약 및 추출하는 데 도움이 됩니다.

영향을 받는 각 URL에 대해 **향상된 텍스트** 제안을 검토하고 **미리보기**&#x200B;와 비교한 다음 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md)로 배포하면 에이전틱 트래픽에서 콘텐츠 관리 시스템(CMS) 변경 없이 보다 명확한 HTML을 받을 수 있습니다.

## 문제 해결 방법

수정 사항은 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 적용되며, 다음과 같습니다.

- 사전 렌더링된 HTML 스냅샷을 AI 에이전트에 제공합니다.
- 복잡한 구문이 라이브 페이지에 정렬된 **향상된 텍스트**&#x200B;로 대체되거나 확대되도록 에이전트가 볼 수 있는 페이지를 업데이트합니다.
- CDN 계층에서 작동합니다(CMS 변경 사항 없음).
- AI 전용 - 사람 방문자나 SEO 봇에 영향을 주지 않습니다.
- 몇 분 후에 배포되며 LLM Optimizer 인터페이스에서 **완전히 취소 가능**&#x200B;합니다.

## 작동 방식

LLM Optimizer는 높은 에이전틱 트래픽을 수신하는 페이지와 콘텐츠 점수가 가독성 임계값 미만인 페이지를 식별한 다음 사본 재작성을 제안합니다. 각 페이지에 대해 다음 항목이 있습니다.

**향상된 텍스트** - 페이지에 이미 있는 내용에 기반을 둔 단순화된 콘텐츠입니다.
**미리보기** - 에이전틱 트래픽에 대한 이전 및 이후 비교입니다.

영향을 받는 URL은 **현재 제안** 탭의 **제안이 있는 URL** 테이블에 표시되며 행을 확장하여 각 권장 사항을 검사할 수 있습니다.

![현재 제안에 대한 제안이 있는 URL, 향상된 텍스트와 미리보기로 확장된 행](/help/dashboards/opportunities/assets/simplify-complex-content-expand.png)

**제안이 있는 URL** 테이블에는 단순화된 콘텐츠가 에이전틱 이해에 도움이 되는 페이지가 나열되어 있습니다. 제안은 **현재 제안**, **수정된 제안** 및 **무시된 제안**&#x200B;으로 구성됩니다. 각 URL에 대해 다음 작업을 수행할 수 있습니다.

- **행을 확장하여** 해당 페이지에 대한 **향상된 텍스트** 제안을 확인합니다.
- 에이전틱 트래픽에 대한 이전 및 이후 비교를 **미리보기**&#x200B;합니다.
- LLM Optimizer 외부에서 기회를 해결한 경우 **수정됨으로 표시**&#x200B;됩니다.
- 관련성이 없는 제안을 **무시**&#x200B;합니다.

**보기**&#x200B;에는 **현재 제안**, **수정된 제안**(배포된 경우 **최적화** 상태) 및 **무시된 제안**&#x200B;이 포함됩니다. **수정된 제안**&#x200B;에서 **실시간 보기**&#x200B;를 사용하여 실시간 배포를 확인하고 언제든지 롤백할 수 있습니다.

확인란을 사용하여 배송할 URL 또는 줄 항목이 **향상된 텍스트**&#x200B;인 경우 선택한 다음 **기회 계획** 헤더에서 **수정됨으로 표시**, **제안 무시** 또는 **최적화 배포**&#x200B;를 사용합니다. 또한 데모 UI에는 선택 수 및 목록과 관련된 액션이 표시됩니다.

![계획 헤더에서 기회 계획, 현재 제안, 확장된 행 및 배포 최적화](/help/dashboards/opportunities/assets/simplify-complex-content-select.png)

### 최적화 배포

에지에 게시할 준비가 되면 **최적화 배포**&#x200B;를 클릭합니다. **Edge에 배포** 대화 상자에 선택한 URL 및 최적화 세부 정보가 나열됩니다. 목록을 검토한 다음 **배포** 또는 **취소**&#x200B;를 선택합니다.

![Edge에 배포 대화 상자](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-dialog.png)

배포에 성공하면 **배포 완료**&#x200B;에서 최적화 실행 횟수를 확인하고 AI 에이전트가 업데이트를 인덱싱하는 데 시간이 걸릴 수 있습니다. 대화 상자를 닫고 **수정된 제안**&#x200B;을 열어 상태를 확인합니다.

![배포 완료 확인](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-confirm.png)

>[!NOTE]
>
>최적화를 배포하려면 Optimize at Edge 온보딩 프로세스를 완료해야 합니다. 아직 온보딩하지 않은 경우 **최적화 배포**&#x200B;를 클릭하면 온보딩 프로세스로 이동합니다. Optimize at Edge 작동 방법, 지원되는 CDN 공급자 및 온보딩 프로세스에 대한 자세한 내용은 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

### 수정된 제안 및 실시간 보기

**수정된 제안**&#x200B;에서 배포된 URL은 상태 열에 **최적화됨**&#x200B;을 표시합니다. 행을 확장하여 배포된 **향상된 텍스트** 및 지침을 검토합니다.

![최적화된 상태, 확장된 간소화된 복사본, 실시간 보기 및 세부 정보가 있는 수정된 제안 탭](/help/dashboards/opportunities/assets/simplify-complex-content-fixed.png)

확인(적용되는 간소화된 경로 포함)에 제공된 대로 **현재 페이지 콘텐츠**&#x200B;의 읽기 전용 보기를 열려면 행에서 **실시간 보기**&#x200B;를 클릭합니다. 분석에 **세부 정보**&#x200B;를 사용합니다.

![실시간 보기 - 에이전트의 간소화된 텍스트를 포함하는 현재 페이지 콘텐츠](/help/dashboards/opportunities/assets/simplify-complex-content-view-live.png)

에지 변경 내용을 일괄적으로 되돌리려면 확인란을 사용하여 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 사용합니다.

![헤더에서 배포된 행, 최적화된 상태 및 롤백이 있는 수정된 제안](/help/dashboards/opportunities/assets/simplify-complex-content-rollback.png)

## 롤백

마음이 바뀌면 배포된 모든 최적화를 롤백할 수 있습니다. **수정된 제안** 보기에서 되돌릴 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 클릭합니다.

**롤백** 대화 상자에는 롤백할 제안 사항이 나열되며 배포된 최적화가 되돌아갈 것이라는 짧은 경고가 표시됩니다. 목록을 확인한 다음 **롤백** 또는 **취소**&#x200B;를 클릭합니다.

![되돌린 제안 사항을 나열한 롤백 대화 상자](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-dialog.png)

작업이 완료되면 **성공적으로 롤백됨** 요약이 나타납니다. 대시보드로 돌아가려면 닫습니다.

![롤백 완료 - 정상적으로 롤백되었습니다.](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-confirm.png)

## 데모에서 사용해 보기

[Frescopa 데모](https://play.llmo.now/org/demo-org)에서 복잡한 콘텐츠 간소화 워크플로를 살펴보십시오.
