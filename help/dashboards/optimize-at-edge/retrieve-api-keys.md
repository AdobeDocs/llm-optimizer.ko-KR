---
title: API 키 검색
description: LLM Optimizer에서 프로덕션 및 스테이징 Edge Optimize API 키를 가져오는 방법.
feature: Opportunities
autotag-review: '2026-07-15T18:05:12.505Z'
TQID: 'https://experienceleague.adobe.com/X3vIzxrlaqJ5Mx3K8rOpX2QqgGyxT6p8qfdLzTWC1gQ'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 100%

---


# API 키 검색

CDN을 구성하기 전에 LLM Optimizer UI에서 Edge Optimize API 키를 검색합니다. 라이브 트래픽에는 **프로덕션** API 키가 필요합니다. 선택적으로, 스테이징 호스트 이름에서 라우팅을 먼저 테스트하기 위해 **스테이징** API 키를 검색할 수도 있습니다.

## 프로덕션 API 키

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고  **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **AI 에이전트에 최적화 배포** 섹션을 찾습니다. **최적화 엔진 활성화** 확인란을 선택합니다.

   ![AI 에이전트에 최적화 배포 — 보류 중](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. 확인 대화 상자에서 **활성화**&#x200B;를 선택합니다.

   ![최적화 엔진 확인 대화 상자 활성화](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png)

4. **세부 정보 보기**&#x200B;를 선택합니다. **최적화 배포 세부 정보** 대화 상자에서 **프로덕션 API 키**&#x200B;를 복사합니다(필드 옆에 **복사** 사용).

   ![최적화 배포 세부 정보의 프로덕션 API 키](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png)

   >[!NOTE]
   >대화 상자에 설정이 완료되지 않았음이 표시될 수 있습니다. 라우팅을 확인할 때까지 발생합니다. IT 또는 CDN 팀이 구성을 완료할 수 있도록 API 키를 복사할 수 있습니다.

위 단계에 대한 도움이 필요한 경우 Adobe 계정 팀 또는 `llmo-at-edge@adobe.com`에 문의하십시오.

## 스테이징 API 키(선택 사항)

프로덕션 라우팅을 활성화하기 전에 하위 환경에서 라우팅을 검증하려면 스테이징 호스트 이름을 구성할 수 있습니다.

**요구 사항**

* 스테이징 호스트 이름은 프로덕션과 **동일한 등록 가능한 도메인**&#x200B;에 있어야 합니다(예: 프로덕션이 `https://www.example.com`인 경우 `https://staging.example.com`).
* 사이트당 **하나의** 스테이징 도메인. 저장된 후에는 Adobe에 연락하지 않고는 변경할 수 없습니다.

**단계**

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고  **CDN 구성** 탭을 선택합니다.
2. **AI 에이전트에 최적화 배포**&#x200B;에서 **스테이지 도메인 추가**(또는 **스테이지 도메인**&#x200B;이 이미 구성된 경우 단계 도메인 추가)를 선택합니다.
3. `https://`를 포함한 전체 스테이징 URL을 입력하고 **도메인 설정**&#x200B;을 선택합니다.
4. 확인 대화 상자에서 **스테이징** API 키를 복사합니다.

   ![스테이징 도메인 API 키](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

스테이징 API 키를 사용하여 스테이징 환경에 동일한 라우팅 규칙을 배포합니다.

도움이 필요하면 `llmo-at-edge@adobe.com`에 문의하십시오.

## 다음 단계

API 키를 검색한 후 [CDN 설정 안내서](/help/dashboards/optimize-at-edge/overview.md#cdn-configuration-guides)로 돌아가 라우팅을 구성합니다.
