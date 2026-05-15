---
title: 액세스 제어
description: Adobe LLM Optimizer에서 제품 할당 사용자와 조직 사용자가 어떻게 다른지, UI에서 읽기 전용 사용자에게 표시되는 내용, Adobe Admin Console에서 관리자가 액세스를 할당하는 방법에 대해 알아봅니다.
feature: Customer Configuration
autotag-review: '2026-05-15T17:26:43.837Z'
TQID: 'https://experienceleague.adobe.com/hJpQQpuHBRMdKT5oKA9z0Y8H3d3p6To-n2hWKrXgZsQ'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
subfeature_v2:
  - id: b704f6a0-b2fb-4df0-9177-9753751004f5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7a92587197cf6a9eec6b01bd4eaeeaf1194d3088
workflow-type: tm+mt
source-wordcount: 618
ht-degree: 100%

---


# 액세스 제어

Adobe LLM Optimizer는 사용자 페르소나에 따라 기본 액세스 제어를 지원합니다. 이 기능은 **유료 고객**&#x200B;에게만 제공되며 요청 시 활성화됩니다. 체험판 고객은 사용할 수 없습니다.

>[!IMPORTANT]
>
>이 기능에 대한 액세스를 요청하려면 유료 고객은 Adobe 계정 관리자에게 문의해야 합니다.

## 제품이 할당한 사용자 {#product-assigned-users}

제품에 할당되면 다음 권한 외에 표준 조직 사용자와 동일한 기능이 제공됩니다.

* 프롬프트, 카테고리, 주제 및 관련 설정을 보려면 [고객 구성](/help/dashboards/customer-configuration.md)에 접근 권한을 부여합니다.
* [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md)를 배포하고 제안을 최적화하고 관리합니다.
* Google Search Console 구성을 관리합니다.
* Optimize at Edge 및 CDN 구성을 관리합니다.
* 새 사이트를 온보딩합니다.

## 조직 사용자 {#organizational-users}

조직 사용자는 제품에 할당되지 **않은** 표준 사용자입니다. 조직 사용자의 경우 [LLM Optimizer 대시보드](/help/dashboards/dashboards-overview.md) 및 관련 보기에 대한 **읽기 전용** 액세스 권한이 있습니다. 다음 제한 사항이 적용됩니다.

### 고객 구성 {#customer-configuration-restrictions}

* **프롬프트 업로드**&#x200B;가 비활성화되었습니다.
* 프롬프트, 카테고리, 주제 및 지역 관리와 편집이 비활성화되었습니다.

  ![읽기 전용 사용자에 대한 고객 구성 제한](/help/dashboards/assets/access-control-customer-configuration.png)

### CDN 구성(고객 구성) {#cdn-configuration-restrictions}

* **CDN 온보딩**&#x200B;이 비활성화되었습니다(읽기 전용 사용자는 CDN 공급자를 추가할 수 없음).
* **CDN 삭제**&#x200B;가 비활성화되었습니다(읽기 전용 사용자는 기존 CDN 구성을 제거할 수 없음).
* CDN 온보딩 대화 상자의 **제출** 버튼이 비활성화되었습니다(읽기 전용 사용자는 CDN 설정을 완료할 수 없음).

  ![읽기 전용 사용자에 대한 CDN 구성 제한](/help/dashboards/assets/access-control-cdn-configuration.png)

### 브랜드 존재감 — 데이터 인사이트 {#brand-presence-restrictions}

* 항목 옆에 있는 **삭제** 버튼이 숨겨져 있습니다(읽기 전용 사용자는 추적에서 항목을 제거할 수 없음).
* 프롬프트 옆에 있는 **삭제** 버튼이 숨겨져 있습니다(읽기 전용 사용자는 추적에서 프롬프트를 제거할 수 없음).

  ![읽기 전용 사용자에 대해 숨겨진 브랜드 존재감 액션](/help/dashboards/assets/access-control-brand-presence.png)

### 에이전틱 트래픽 기회(오류 페이지 기회) {#agentic-opportunities}

404, 403 및 503 오류 페이지와 같은 기회의 경우:

* **최적화 배포**&#x200B;가 숨겨져 있습니다.
* 배포 액세스 권한이 필요하다는 정보 경고가 표시됩니다.

  ![에이전틱 트래픽 기회에 숨겨진 최적화 배포](/help/dashboards/assets/access-control-agentic-deploy.png)

### 기타 기회 페이지 {#other-opportunities}

읽기 전용 비헤이비어는 다음과 같은 기회 유형에도 적용됩니다.

* 목차
* 요약
* 가독성
* 사전 렌더링
* 제목
* FAQ
* 구조화된 데이터 누락
* 일반 패치 기회

이 페이지의 경우:

* **최적화 배포**&#x200B;는 사용자가 배포 액세스 권한이 없을 때 숨겨집니다.
* 배포 액세스 권한이 필요하다는 인라인 경고가 표시됩니다. 메시지는 다음과 유사합니다. *배포 액세스 필요 — 최적화를 배포하거나 제안을 관리할 권한이 없습니다. 액세스 권한을 요청하려면 관리자에게 문의하십시오.*
* 배포 액션이 있는 고정 하단 막대가 숨겨져 있습니다.

  ![배포 액세스 권한이 필요한 경우 인라인 경고](/help/dashboards/assets/access-control-deploy-alert.png)

  ![읽기 전용 사용자에 대한 Optimize at Edge 배포 액션](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Google Search Console 프롬프트 구성 {#gsc-restrictions}

* 관리 및 연결 액션이 비활성화되거나 숨겨져 있습니다.
* 프롬프트를 추가하는 데 사용되는 액션 열이 숨겨져 있습니다.

  ![Google Search Console 구성 제한](/help/dashboards/assets/access-control-gsc.png)

### 새 사이트 온보딩 {#onboarding-restrictions}

* 액세스 제어가 없는 사용자에게는 새 사이트 온보딩 기능이 비활성화됩니다.

  ![새 사이트 온보딩 비활성화](/help/dashboards/assets/access-control-onboarding.png)

## 제품을 사용자 또는 그룹에 할당 {#assign-product}

조직의 **시스템 관리자**&#x200B;가 [Adobe Admin Console](https://adminconsole.adobe.com/)을 사용하여 Adobe LLM Optimizer을 사용자 또는 그룹에 할당할 수 있습니다.

1. 조직에 대한 관리 권한이 있는 계정으로 [Adobe Admin Console](https://adminconsole.adobe.com/)에 로그인합니다.
1. 제품 할당 기능을 받아야 하는 사용자 또는 그룹에 Adobe LLM Optimizer 제품 프로필(또는 조직의 동등한 제품 권한)을 할당합니다.

자세한 단계는 [Admin Console에서 제품 관리](https://helpx.adobe.com/kr/enterprise/using/manage-products.html) 및 [사용자 그룹 관리](https://helpx.adobe.com/kr/enterprise/using/user-groups.html)를 참조하십시오.

>[!NOTE]
>
>Adobe Admin Console의 화면 흐름은 릴리스 간에 변경될 수 있습니다. 위의 옵션이 콘솔과 일치하지 않는 경우 Adobe Admin Console의 제품 내 도움말 링크를 사용하거나 Adobe 계정 팀에 문의하십시오.
