---
title: 멀티미디어 트랜스크립트 요약 추가
description: LLM Optimizer이 컴퓨터에서 읽을 수 있는 텍스트 없이 비디오에 주요 정보가 포함된 페이지를 식별하는 방법과 Edge에서 최적화로 AI가 생성한 대본 요약을 검토하고 배포하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 36a6836f86b6d31cc4bf4682e881bd127edf66e4
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# 멀티미디어 트랜스크립트 요약 추가

>[!NOTE]
>
> **조기 액세스** — 멀티미디어 성적 증명서 요약 추가는 조기 액세스에서 사용할 수 있습니다. 기능이 향상되면 가용성, 자격 요건 및 워크플로의 일부가 변경될 수 있습니다. 액세스에 대한 질문이 있는 경우 Adobe 계정 팀에 문의하십시오.

멀티미디어 트랜스크립트 추가 요약 기회는 AI 에이전트가 읽을 수 있는 트랜스크립트나 짧은 텍스트 요약이 없는 중요한 정보가 비디오나 다른 미디어에 있는 페이지를 식별합니다. 미디어와 주변 페이지 컨텍스트에 기반을 둔 **AI 생성 대본 요약**&#x200B;을 소개합니다. 멀티미디어 콘텐츠를 AI 에이전트가 이해할 수 있도록 만들어 놓치는 주요 브랜드 정보를 복구하는 데 도움이 됩니다.

영향을 받는 각 URL에 대해 제안된 **콘텐츠 패치**, **구현** 세부 정보(예: 대상 CSS 선택기 및 작업) 및 **합리적**&#x200B;을 검토한 다음 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 배포하면 에이전트 트래픽에서 콘텐츠 관리 시스템(CMS) 변경 필요 없이 보강된 HTML을 받을 수 있습니다.

## 문제 해결 방법

수정 사항은 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 적용됩니다.

- 사전 렌더링된 HTML 스냅샷을 AI 에이전트에 제공합니다.
- 검색한 HTML의 트랜스크립트 요약 텍스트로 페이지를 강화합니다(예: 관련 인라인 비디오 근처).
- CDN 계층에서 작동합니다(CMS 변경 사항 없음).
- AI 전용 — 사람 방문자나 SEO 봇에 영향을 주지 않습니다.
- 몇 분 후에 배포되며 LLM Optimizer 인터페이스에서 **완전히 취소 가능**&#x200B;합니다.

## 작동 방식

LLM Optimizer은 구성 및 페이지 구조를 기반으로 임베디드 미디어에 대해 기계가 읽을 수 있는 텍스트가 누락된 높은 트래픽 페이지에 플래그를 지정합니다. 영향을 받는 URL은 **현재 제안** 탭의 **제안이 있는 URL** 테이블에 나타나며, 행을 확장하여 각 **콘텐츠 패치**&#x200B;를 검사하고, 적용 방법과 권장 이유를 살펴볼 수 있습니다.

각 페이지에 대해 다음 항목이 있습니다.

**멀티미디어 요약** - 비디오 콘텐츠에서 파생된 구조화된 요약입니다.
**미리 보기** - 페이지 비교 전과 후.

![현재 제안에 대한 제안 사항이 있는 URL, 콘텐츠 패치가 있는 확장된 행, 구현 세부 정보 및 이유](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-expand.png)

**제안 URL** 표에는 대본 또는 요약 텍스트가 대소문자 검색에 도움이 되는 페이지가 나열되어 있습니다. 제안은 **현재 제안**, **수정 제안** 및 **무시된 제안**&#x200B;으로 구성됩니다. 각 URL에 대해 다음 작업을 수행할 수 있습니다.

- **행을 확장**&#x200B;하여 **콘텐츠 패치** 텍스트, **구현** 세부 정보(계획된 DOM 작업 및 CSS 선택기 포함) 및 변경 **이유**&#x200B;를 확인합니다.
- 에이전트 트래픽에 대한 이전 및 이후 비교를 **미리 보기**&#x200B;합니다.
- LLM Optimizer 외부의 영업 기회를 해결한 경우 **고정으로 표시**.
- 관련성이 없는 **제안 무시**&#x200B;개

지원되면(연필 컨트롤) 행에서 패치 텍스트를 편집한 다음 행 확인란을 사용하여 배포할 항목을 선택할 수 있습니다. 바닥글은 선택한 항목의 수를 보여주며 **수정으로 표시**, **제안 무시** 및 **최적화 배포**&#x200B;를 제공합니다.

### 최적화 배포

Edge에 게시할 준비가 되면 **최적화 배포**&#x200B;를 클릭합니다. **Edge에 배포** 대화 상자에 실행하려는 URL, 선택기 및 작업이 나열됩니다. 목록을 검토한 다음 **배포** 또는 **취소**&#x200B;를 선택하십시오.

![멀티미디어 성적 증명서 요약 콘텐츠 패치를 위한 Edge에 배포 대화 상자](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-dialog.png)

배포에 성공하면 **배포 완료**&#x200B;에서 활성화된 최적화 수를 확인합니다. 대화 상자를 닫고 **수정 제안**&#x200B;을 열어 상태를 확인합니다.

![배포 완료 확인](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-confirm.png)

>[!NOTE]
>
> 최적화를 배포하려면 Edge 온보딩 프로세스에서 최적화해야 합니다. 아직 온보딩하지 않은 경우 **최적화 배포**&#x200B;를 클릭하면 온보딩 프로세스로 이동합니다. Edge에서 최적화 작동 방법, 지원되는 CDN 공급자 및 온보딩 프로세스에 대한 자세한 내용은 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

### 수정된 제안 사항 및 라이브 보기

**수정된 제안**&#x200B;에서 배포된 URL은 상태 열에 **최적화됨**&#x200B;을(를) 표시합니다. 행을 확장하여 라이브 **콘텐츠 패치**, **구현** 세부 정보 및 **이유** 를 검토합니다. 또한 분석에 대해 **세부 정보**&#x200B;를 사용하거나 가능한 경우 **실시간 보기**&#x200B;를 사용하여 에이전트 트래픽이 수신하는 항목을 확인할 수 있습니다.

![최적화된 상태, 확장된 콘텐츠 패치 및 롤백을 사용하여 제안을 해결했습니다](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-fixed.png)

일괄 롤백하려면 확인란을 사용하여 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 사용합니다.

![롤백 전에 선택한 행이 있는 수정 제안](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-select-in-fixed.png)

## 롤백

마음이 바뀌면 배포된 최적화를 롤백할 수 있습니다. **수정 제안**&#x200B;에서 되돌릴 행을 선택한 다음 **롤백**&#x200B;을 클릭합니다.

**롤백** 대화 상자에는 롤백될 제안 사항이 나열되며 배포된 최적화가 에이전트 트래픽의 라이브 경로에서 제거된다는 경고가 표시됩니다. 확인한 다음 **롤백** 또는 **취소**&#x200B;를 클릭합니다.

되돌리기 제안을 나열하는 ![롤백 대화 상자](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-dialog.png)

작업이 완료되면 **성공적으로 롤백됨** 요약이 나타납니다. 대시보드로 돌아가려면 닫으십시오.

![롤백 완료 — 롤백되었습니다](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-confirm.png)

## 데모에서 사용해 보기

[Frescopa 데모](https://play.llmo.now/org/demo-org)에서 멀티미디어 트랜스크립트 요약 추가 워크플로우를 살펴보십시오.
