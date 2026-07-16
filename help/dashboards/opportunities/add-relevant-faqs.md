---
title: 관련 FAQ 추가
description: LLM Optimizer가 AI 에이전트에 대한 구조화된 Q&A 콘텐츠가 부족한 트래픽이 많은 페이지를 식별하는 방법과 Optimize at Edge를 통해 AI 생성 FAQ를 검토하고 배포하는 방법에 대해 알아봅니다.
feature: Opportunities
autotag-review: '2026-07-15T16:47:24.291Z'
TQID: 'https://experienceleague.adobe.com/ObmJKEvR9-ovzugCtAsRkcUBemcsMw6cNwizkuKYPcc'
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
source-wordcount: 742
ht-degree: 100%

---


# 관련 FAQ 추가

관련 FAQ 추가 기회는 AI 에이전트가 응답을 생성할 때 종종 의존하는 구조화된 Q&amp;A 콘텐츠가 부족한 높은 트래픽 페이지를 식별합니다. 기존 페이지 자료에 기반을 둔 관련 **의도 정렬 FAQ** 콘텐츠를 소개합니다. 이렇게 하면 에이전트가 사용자 질문을 콘텐츠에 더 직접적으로 일치시킬 수 있습니다.

영향을 받는 각 URL에 대해 AI가 생성한 FAQ 제안을 검토한 다음 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 이를 배포하면 에이전틱 트래픽에서 콘텐츠 관리 시스템(CMS) 변경 없이 보다 명확한 Q&amp;A 컨텍스트를 받을 수 있습니다.

## 문제 해결 방법

수정 사항은 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md)를 사용하여 적용되며, 다음과 같습니다.

- 사전 렌더링된 HTML 스냅샷을 AI 에이전트에 제공합니다.
- 검색한 HTML의 FAQ 콘텐츠로 페이지를 강화합니다.
- CDN 계층에서 작동합니다(CMS 변경 사항 없음).
- AI 전용 - 사람 방문자나 SEO 봇에 영향을 주지 않습니다.
- 몇 분 후에 배포되며 LLM Optimizer 인터페이스에서 **완전히 취소 가능**&#x200B;합니다.

## 작동 방식

LLM Optimizer는 브랜드의 프롬프트 세트에 따라 Q&amp;A 콘텐츠가 누락되거나 두께가 얇은 트래픽이 많은 페이지를 식별합니다. 영향을 받는 URL은 **현재 제안** 탭의 **제안이 있는 URL** 테이블에 표시되며 행을 확장하여 각 권장 사항을 검사할 수 있습니다.

![현재 제안에 대한 제안이 있는 URL, FAQ 프롬프트 및 AI 생성 응답이 있는 확장된 행](/help/dashboards/opportunities/assets/add-relevant-faqs-expand.png)

**제안이 있는 URL** 테이블에는 AI 기반 검색에 도움이 되는 FAQ 페이지가 나열되어 있습니다. 제안은 **현재 제안**, **수정된 제안** 및 **무시된 제안**&#x200B;으로 구성됩니다. 각 URL에 대해 다음 작업을 수행할 수 있습니다.

- **행을 확장**&#x200B;하여 해당 페이지에 대해 제안된 FAQ 콘텐츠를 봅니다.
- 에이전틱 트래픽에 대한 이전 및 이후 비교를 **미리보기**&#x200B;합니다.
- LLM Optimizer 외부에서 기회를 해결한 경우 **수정됨으로 표시**&#x200B;됩니다.
- 관련성이 없는 제안을 **무시**&#x200B;합니다.

확장된 각 항목에는 페이지에 연결된 FAQ **프롬프트**, **AI 생성** 제안 답변, 간단한 **추론** 및 **소스**&#x200B;가 나열됩니다. 테이블에는 URL당 몇 개의 FAQ가 제안되는지 및 우선순위를 지정하는 데 도움이 되는 **에이전틱 트래픽(4주)**&#x200B;도 표시됩니다.

최적화 미리보기를 열려면 행에서 **미리보기**&#x200B;를 클릭합니다. 에이전틱 트래픽에 대한 페이지의 현재 모습을 최적화 후 보기(예: 새 **FAQ** 블록)와 비교합니다.

![FAQ가 있는 현재 및 최적화 후 에이전트 보기를 비교하여 최적화 미리보기](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-01.png)

행 확인란을 사용하여 제공할 FAQ 제안을 선택합니다. 바닥글은 선택한 항목의 수를 보여 주며 **수정됨으로 표시**, **제안 무시** 및 **최적화 배포**&#x200B;를 제공합니다.

![배포 최적화가 있는 현재 제안에 대해 선택된 FAQ 제안](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-02.png)

### 최적화 배포

에지에 게시할 준비가 되면 **최적화 배포**&#x200B;를 클릭합니다. **Edge에 배포** 대화 상자에 푸시하려는 URL, 질문 및 답변이 나열됩니다. 목록을 검토한 다음 **배포** 또는 **취소**&#x200B;를 선택합니다.

![Edge에 배포 대화 상자](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-03.png)

배포에 성공하면 **배포 완료**&#x200B;에서 활성화된 최적화 수를 확인합니다. 대화 상자를 닫고 **수정된 제안**&#x200B;을 열어 상태를 확인합니다.

![배포 완료 확인](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-04.png)

>[!NOTE]
>
>최적화를 배포하려면 Optimize at Edge 온보딩 프로세스를 완료해야 합니다. 아직 온보딩하지 않은 경우 **최적화 배포**&#x200B;를 클릭하면 온보딩 프로세스로 이동합니다. Optimize at Edge 작동 방법, 지원되는 CDN 공급자 및 온보딩 프로세스에 대한 자세한 내용은 [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) 페이지를 참조하십시오.

### 수정된 제안 및 실시간 보기

**수정된 제안**&#x200B;에서 배포된 URL은 상태 열에 **최적화됨**&#x200B;을 표시합니다. 행을 확장하여 실시간 FAQ 콘텐츠를 검토하고, 분석을 위해 **세부 정보**&#x200B;를 사용하거나 **실시간 보기**&#x200B;를 클릭하여 확인을 위해 제공된 대로 **현재 페이지 콘텐츠**&#x200B;의 읽기 전용 보기를 엽니다(삽입된 **FAQ** 섹션 포함).

![최적화된 상태, 실시간 보기 및 롤백이 있는 수정된 제안](/help/dashboards/opportunities/assets/add-relevant-faqs-fixed.png)

**실시간 보기** 창은 해당 확인에 표시된 대로 페이지 구조 및 FAQ 복사본을 표시합니다.

![실시간 보기 - FAQ를 포함한 현재 페이지 콘텐츠입니다.](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-05.png)

## 롤백

마음이 바뀌면 배포된 모든 최적화를 롤백할 수 있습니다. **수정된 제안** 보기에서 되돌릴 최적화된 행을 선택한 다음 헤더에서 **롤백**&#x200B;을 클릭할 수 있습니다.

**롤백** 대화 상자에는 롤백할 제안 사항이 나열되며 배포된 최적화가 되돌아갈 것이라는 짧은 경고가 표시됩니다. 목록을 확인한 다음 **롤백** 또는 **취소**&#x200B;를 클릭합니다.

![되돌린 제안 사항을 나열한 롤백 대화 상자](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-07.png)

작업이 완료되면 **성공적으로 롤백됨** 요약이 나타납니다. 대시보드로 돌아가려면 닫습니다.

![롤백 완료 - 정상적으로 롤백되었습니다.](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-08.png)

## 데모에서 사용해 보기

[Frescopa 데모](https://play.llmo.now/org/demo-org)에서 관련 FAQ 추가 워크플로를 살펴보십시오.
