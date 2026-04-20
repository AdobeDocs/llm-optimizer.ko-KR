---
title: 액세스 제어
description: Adobe LLM Optimizer에서 제품 할당 사용자와 조직 사용자가 어떻게 다른지, UI에서 읽기 전용 사용자에게 표시되는 내용 및 관리자가 Adobe Admin Console에서 액세스 권한을 할당하는 방법을 알아보십시오.
feature: Customer Configuration
source-git-commit: 3b792a8ca7efd4b6d6764d2e83f9b0c103a56558
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 4%

---


# 액세스 제어

Adobe LLM Optimizer은 사용자 성향에 따라 기본 액세스 제어를 지원합니다. 이 기능은 **결제 고객**&#x200B;만 사용할 수 있으며 요청 시 사용할 수 있습니다. 체험판 고객은 사용할 수 없습니다.

>[!IMPORTANT]
>
>이 기능에 대한 액세스를 요청하려면 결제 고객이 Adobe 계정 관리자에게 문의해야 합니다.

## 제품이 할당한 사용자 {#product-assigned-users}

제품에 할당된 경우 다음 권한 외에 표준 조직 사용자와 동일한 기능이 제공됩니다.

* 프롬프트, 카테고리, 주제 및 관련 설정을 보려면 [고객 구성](/help/dashboards/customer-configuration.md)에서 쓰기 액세스 권한을 부여하십시오.
* [Edge에서 최적화](/help/dashboards/optimize-at-edge/overview.md)를 배포하고 제안을 최적화하고 관리합니다.
* Google Search Console 구성을 관리합니다.
* Edge 및 CDN 구성에서 최적화 관리.
* 새 사이트 온보딩

## 조직 사용자 {#organizational-users}

조직 사용자는 제품에 할당되지 않은 **표준 사용자입니다**. 조직 사용자의 경우 [LLM Optimizer 대시보드](/help/dashboards/dashboards-overview.md) 및 관련 보기에 대한 **읽기 전용** 액세스 권한이 있습니다. 다음 제한 사항이 적용됩니다.

### 고객 구성 {#customer-configuration-restrictions}

* **업로드 프롬프트**&#x200B;이(가) 비활성화되었습니다.
* 프롬프트, 카테고리, 주제 및 영역 관리 및 편집은 비활성화됩니다.

  ![읽기 전용 사용자에 대한 고객 구성 제한](/help/dashboards/assets/access-control-customer-configuration.png)

### CDN 구성 (고객 구성) {#cdn-configuration-restrictions}

* **온보드 CDN**&#x200B;이(가) 비활성화되었습니다(읽기 전용 사용자는 CDN 공급자를 추가할 수 없음).
* **CDN 삭제**&#x200B;이(가) 비활성화되었습니다(읽기 전용 사용자는 기존 CDN 구성을 제거할 수 없음).
* CDN 온보드 대화 상자의 **제출** 단추가 비활성화됩니다(읽기 전용 사용자가 CDN 설정을 완료할 수 없음).

  읽기 전용 사용자에 대한 ![CDN 구성 제한](/help/dashboards/assets/access-control-cdn-configuration.png)

### 브랜드 존재감 — 데이터 인사이트 {#brand-presence-restrictions}

* 항목 옆에 있는 **삭제** 단추가 숨겨져 있습니다(읽기 전용 사용자는 추적에서 항목을 제거할 수 없음).
* 프롬프트 옆에 있는 **삭제** 단추가 숨겨져 있습니다(읽기 전용 사용자는 추적에서 프롬프트를 제거할 수 없음).

  ![읽기 전용 사용자에 대해 숨겨진 브랜드 존재감 작업](/help/dashboards/assets/access-control-brand-presence.png)

### 에이전트 트래픽 기회(오류 페이지 기회) {#agentic-opportunities}

404, 403 및 503 오류 페이지와 같은 기회의 경우:

* **최적화 배포**&#x200B;가 숨겨져 있습니다.
* 배포 액세스 권한이 필요하다는 정보 경고가 표시됩니다.

  ![에이전트 트래픽 기회에 최적화를 배포합니다](/help/dashboards/assets/access-control-agentic-deploy.png)

### 기타 영업 기회 페이지 {#other-opportunities}

읽기 전용 동작은 다음과 같은 영업 기회 유형에도 적용됩니다.

* 목차
* 요약
* 가독성
* 사전 렌더링
* 제목
* FAQ
* 구조화된 데이터 누락
* 일반 패치 영업 기회

이 페이지의 경우:

* 사용자에게 배포 액세스 권한이 없는 경우 **배포 최적화**&#x200B;이(가) 숨겨집니다.
* 인라인 경고는 배포 액세스가 필요함을 설명합니다. 메시지는 다음과 유사합니다. *배포 액세스 필요 — 최적화를 배포하거나 제안을 관리할 수 있는 권한이 없습니다. 관리자에게 연락하여 액세스 권한을 요청하십시오.*
* 배포 작업이 있는 고정 하단 막대가 숨겨집니다.

  배포 액세스가 필요한 경우 ![인라인 경고](/help/dashboards/assets/access-control-deploy-alert.png)

  ![Edge에서 최적화 읽기 전용 사용자에 대해 숨겨진 작업 배포](/help/dashboards/assets/access-control-optimize-at-edge.png)

### Google 검색 콘솔 프롬프트 구성 {#gsc-restrictions}

* 관리 및 연결 작업이 비활성화되거나 숨겨집니다.
* 프롬프트를 추가하는 데 사용되는 작업 열은 숨겨집니다.

  ![Google 검색 콘솔 구성 제한](/help/dashboards/assets/access-control-gsc.png)

### 새 사이트 온보드 {#onboarding-restrictions}

* 액세스 제어가 없는 사용자는 새 사이트 온보딩을 사용할 수 없습니다.

  ![새 사이트 온보딩 사용 안 함](/help/dashboards/assets/access-control-onboarding.png)

## 제품을 사용자 또는 그룹에 할당 {#assign-product}

조직의 **시스템 관리자**&#x200B;가 [Adobe Admin Console](https://adminconsole.adobe.com/)을(를) 사용하여 Adobe LLM Optimizer을 사용자 또는 그룹에 할당할 수 있습니다.

1. 조직에 대한 관리 권한이 있는 계정으로 [Adobe Admin Console](https://adminconsole.adobe.com/)에 로그인합니다.
1. Adobe LLM Optimizer 제품 프로필(또는 조직의 동등한 제품 자격)을 제품이 할당한 기능을 받아야 하는 사용자 또는 그룹에 할당합니다.

자세한 단계는 [Admin Console에서 제품 관리](https://helpx.adobe.com/kr/enterprise/using/manage-products.html) 및 [사용자 그룹 관리](https://helpx.adobe.com/kr/enterprise/using/user-groups.html)를 참조하십시오.

>[!NOTE]
>
>Adobe Admin Console의 화면 흐름은 릴리스 간에 변경될 수 있습니다. 위의 옵션이 콘솔과 일치하지 않는 경우 Adobe Admin Console에서 제품 내 도움말 링크를 사용하거나 Adobe 계정 팀에 문의하십시오.
