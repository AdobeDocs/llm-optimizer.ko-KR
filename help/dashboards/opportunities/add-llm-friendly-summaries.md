---
title: LLM 친화적 요약 추가
description: LLM Optimizer이 AI 에이전트에 대한 간결한 요약 및 주요 포인트가 없는 트래픽 상위 페이지를 식별하는 방법과 Edge에서 최적화로 검토하고 배포하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-05-15T17:27:51.631Z'
TQID: 'https://experienceleague.adobe.com/QpBdx3B-qg41ZWtPU2R4CNq-POrSs31UIb0kms1H3GU'
product_v2: id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2: id: c0713b97-4af8-4c41-b742-5afcc6ced468
subfeature_v2: id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 793
ht-degree: 0%

---


# LLM 친화적 요약 추가

LLM 친화적 요약 추가 기회는 간결한 구조화된 요약이 부족한 트래픽이 많은 페이지를 식별하므로 AI 에이전트가 페이지의 주요 정보를 빠르게 이해하기가 더 어렵습니다. 기존 페이지 콘텐츠에 기반을 둔 명확한 요약 및 주요 사항을 소개합니다. 이를 통해 에이전트는 중요한 브랜드 주장을 보다 효율적으로 해석하고 캡처할 수 있으며, 콘텐츠가 AI 응답에 정확하게 포함될 가능성이 높아집니다.

영향을 받는 각 URL에 대해 AI가 생성한 제안을 검토한 다음 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 이를 배포할 수 있으므로 콘텐츠 관리 시스템(CMS) 변경 없이 에이전트 트래픽이 명확하고 훑어볼 수 있는 컨텍스트를 얻을 수 있습니다.

## 문제 해결 방법

수정 사항은 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 적용됩니다.

- 사전 렌더링된 HTML 스냅샷을 AI 에이전트에 제공합니다.
- 검색한 HTML의 요약 및/또는 주요 지점을 사용하여 페이지를 강화합니다.
- CDN 계층에서 작동합니다(CMS 변경 사항 없음).
- AI 전용 — 사람 방문자나 SEO 봇에 영향을 주지 않습니다.
- 몇 분 후에 배포되며 LLM Optimizer 인터페이스에서 **완전히 취소 가능**&#x200B;합니다.

## 작동 방식

LLM Optimizer은 페이지 또는 섹션 수준 **요약** 및 **주요 지점**&#x200B;이 AI 이해에 도움이 되는 트래픽이 많은 페이지를 식별합니다. 영향을 받는 URL은 **현재 제안** 탭의 **제안 있는 URL** 테이블에 표시되며 행을 확장하여 각 권장 사항을 검사할 수 있습니다.

![현재 제안에 대한 제안이 있는 URL, 페이지 및 섹션 요약 제안이 있는 확장된 행](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

**제안이 있는 URL** 표에는 요약이 에이전트 검색에 도움이 되는 페이지가 나열되어 있습니다. 제안은 **현재 제안**, **수정 제안** 및 **무시된 제안**&#x200B;으로 구성됩니다. 각 URL에 대해 다음 작업을 수행할 수 있습니다.

- 분석 및 제안된 요약 텍스트(및 포함된 경우 주요 사항)를 보려면 **행을 확장**&#x200B;하십시오.
- 에이전트 트래픽에 대한 이전 및 이후 비교를 **미리 보기**&#x200B;합니다.
- LLM Optimizer 외부의 영업 기회를 해결한 경우 **고정으로 표시**.
- 관련성이 없는 **제안 무시**&#x200B;개

확장된 각 항목에는 라이브 페이지에 연결된 페이지 수준 및 섹션 수준 요약 지침, **AI 생성** 복사, 편집 컨트롤 및 컨텍스트가 표시됩니다.

최적화 미리 보기를 열려면 **작업** 열에서 **미리 보기**&#x200B;를 클릭하십시오. 이 보고서는 현재 페이지에서 집계 트래픽을 찾는 모습과 최적화 후 보기(예: 제안된 배치에 맞게 삽입된 **요약** 및 **키 지점** 콘텐츠 삽입)를 비교합니다. 배포하기 전에 언제든지 해당 미리보기를 열거나 닫을 수 있습니다.

게시할 준비가 되면 확인란을 사용하여 요약 및 주요 라인 항목을 선택합니다. 바닥글은 선택한 항목의 수를 보여주며 **수정으로 표시**, **제안 무시** 및 **최적화 배포**&#x200B;를 제공합니다.

![바닥글에 요약 줄 항목을 선택하고 최적화를 배포하는 현재 제안](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

### 최적화 배포

Edge에 게시할 준비가 되면 **최적화 배포**&#x200B;를 클릭합니다. **Edge에 배포** 대화 상자에 선택한 URL 및 최적화 세부 정보가 나열됩니다. 목록을 검토한 다음 **배포** 또는 **취소**&#x200B;를 선택하십시오.

![Edge에 배포 대화 상자](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

배포에 성공하면 **배포 완료**&#x200B;에서 최적화 실행 횟수를 확인하고 AI 에이전트가 업데이트를 인덱싱하는 데 시간이 걸릴 수 있습니다. 대화 상자를 닫고 **수정 제안**&#x200B;을 열어 상태를 확인합니다.

![배포 완료 확인](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>최적화를 배포하려면 Edge 온보딩 프로세스에서 최적화해야 합니다. 아직 온보딩하지 않은 경우 **최적화 배포**&#x200B;를 클릭하면 온보딩 프로세스로 이동합니다. Edge에서 최적화 작동 방법, 지원되는 CDN 공급자 및 온보딩 프로세스에 대한 자세한 내용은 [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

### 수정된 제안 사항 및 라이브 보기

**수정된 제안**&#x200B;에서 배포된 URL은 상태 열에 **최적화됨**&#x200B;을(를) 표시합니다. 행을 확장하여 배포된 요약 사본과 지침을 검토합니다.

![최적화된 상태, 확장된 배포된 요약, 실시간 보기 및 세부 정보로 추천 탭](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

검증에 제공된 대로 **현재 페이지 콘텐츠**&#x200B;의 읽기 전용 보기를 열려면 행의 **실시간 보기**&#x200B;를 클릭하십시오(적용된 경우 **요약** 및 **키 포인트** 블록 포함). 분석에 **세부 정보**&#x200B;을(를) 사용합니다. 가장자리 변경 내용을 일괄적으로 되돌리려면 확인란을 사용하여 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 사용합니다.

![롤백 전에 대량 선택을 위한 확인란이 포함된 제안을 해결했습니다](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## 롤백

마음이 바뀌면 배포된 모든 최적화를 롤백할 수 있습니다. **수정 제안** 보기에서 되돌릴 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 클릭합니다.

**롤백** 대화 상자에는 롤백할 제안 사항이 나열되며 배포된 최적화가 되돌아갈 것이라는 짧은 경고가 표시됩니다. 목록을 확인한 다음 **롤백** 또는 **취소**&#x200B;를 클릭합니다.

되돌리기 제안을 나열하는 ![롤백 대화 상자](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

작업이 완료되면 **성공적으로 롤백됨** 요약이 나타납니다. 대시보드로 돌아가려면 닫으십시오.

![롤백 완료 — 롤백되었습니다](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

## 데모에서 사용해 보기

[Frescopa 데모](https://play.llmo.now/org/demo-org)에서 LLM 친화적인 요약 추가 워크플로우를 살펴보십시오.
