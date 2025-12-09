---
title: 빠른 시작
description: Adobe LLM Optimizer 시작하기 - 브랜드를 온보딩하고, AI 가시성 통찰력을 잠금 해제하고, 대시보드를 탐색하여 검색 성능을 향상시키십시오.
feature: Quickstart, Onboarding
source-git-commit: 24183fbe2577bb9402f8b6aaaf1e46c75403383d
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---


# 빠른 시작

LLM Optimizer를 시작하려면 아래 제시된 단계에 설명된 대로 온보딩 프로세스를 완료해야 합니다. 프로세스를 완료하면 [LLM Optimizer의 대시보드](/help/dashboards/dashboards-overview.md) 및 기타 기능에 대한 전체 액세스 권한을 갖게 됩니다.

## 온보딩 개요

온보딩 프로세스는 도메인 온보딩으로 시작합니다. AEM Cloud 고객인지 여부에 따라 프로세스가 다릅니다. 프로세스를 완료한 후에는 CDN 로그 전달에 대한 정보를 제공하고 마지막으로 카테고리, 주제 및 프롬프트를 사용자 정의해야 합니다. 프로세스의 각 부분은 LLM Optimizer을 최대한 빨리 시작하는 방법에 대한 유용한 팁과 함께 아래에 자세히 설명되어 있습니다.

### Adobe LLM Optimizer의 공개 페이지 액세스 허용

정확한 컨텐츠 및 기술 권장 사항을 전달하려면 Adobe LLM Optimizer에서 공개 페이지에 액세스해야 합니다. 이는 보안 내부 크롤러(Spacecat/1.0 사용자 에이전트)를 통해 수행됩니다.

구성 요구 사항:

* 사이트의 robots.txt 파일 또는 보트 트래픽 규칙에 Spacecat/1.0 사용자 에이전트를 허용 목록에 추가하다 관리에 추가합니다
* 페이지가 도메인 또는 CDN 수준에서 차단되지 않았는지 확인합니다. 차단된 페이지는 인덱싱할 수 없어 최적화 작업과 그에 대한 인사이트를 생성할 수 없습니다.

대시보드에 컨텐츠 가시성이 낮게 나타나는 경우 크롤러가 도메인에 액세스할 수 있는지 확인하십시오. 제한된 액세스는 불완전한 색인화의 일반적인 원인입니다.

## 1단계: 도메인 온보드

### 구매하기 전에 시도

AEM Cloud(Cloud Service, Managed Services, Edge Delivery Service) 고객은 **구매 전에 시도** 오퍼를 사용할 수 있습니다. 최대 200개의 무료 프롬프트가 있는 LLM Optimizer 무료 평가판입니다. 200개 이상의 프롬프트를 사용하려면 별도의 라이센스 계약이 필요합니다. 액세스는 &quot;있는 그대로&quot; 및 &quot;사용 가능한 대로&quot; 제공되며 언제든지 Adobe에 의해 수정, 제한 또는 제거될 수 있습니다.

무료 버전에서는 사용할 수 없는 몇 가지 제품 기능이 있습니다.

* 평가판은 하나의 도메인으로 제한됩니다. 설치를 완료한 후에는 입력한 도메인을 변경할 수 없습니다.
* 최적화를 배포할 수 없습니다.

무료 평가판 버전을 활성화하고 도메인을 온보딩하는 방법에 대한 자세한 내용은 아래 섹션을 참조하십시오.

### AEM 클라우드 고객

AEM Cloud 고객인 경우 [Experience Hub](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/experience-hub/experience-hub)에서 제품 공지 카드를 사용하여 LLM Optimizer을 시도할 수 있습니다.

>[!NOTE]
>새로 추가된 프롬프트는 처리가 완료될 때까지 [브랜드 현재 상태 대시보드](/help/dashboards/brand-presence.md)에 표시되지 않습니다. AEM Cloud 고객은 LLM Optimizer의 무료 평가판을 사용할 수 있습니다. 200개 이상의 프롬프트를 사용하려면 별도의 라이센스 계약이 필요합니다. 액세스는 &quot;있는 그대로&quot; 및 &quot;사용 가능한 대로&quot; 제공되며 언제든지 Adobe에 의해 수정, 제한 또는 제거될 수 있습니다. 자세한 내용은 계정 담당자에게 문의하십시오.

![LLM Optimizer 평가판](/help/overview/assets/llm-trial.png)

**LLM Optimizer 시도** 단추를 클릭하면 [https://llmo.now](https://llmo.now)&#x200B;(으)로 리디렉션됩니다. 그런 다음 IMS를 통해 로그인해야 합니다. 로그인하면 도메인과 브랜드 이름을 제공하여 온보딩 프로세스를 시작합니다.

![LLM Optimizer 도메인](/help/overview/assets/domain.png)

>[!NOTE]
>제공한 도메인은 조직의 모든 사용자가 사용하게 되며 변경할 수 없습니다.

온보딩 단계 중에 작은 범주, 주제 및 프롬프트 세트가 생성됩니다. 이러한 프롬프트에 대한 브랜드 현재 상태 분석은 사이트가 온보딩된 직후에 사용할 수 있습니다.

<!--![Brand Presence Analysis](/help/overview/assets/bp-analysis.png)-->

또한 트래픽 분석을 위해 [CDN 로그 전달](#step-4)을 구성해야 합니다. LLM Optimizer은 AI 가시성을 높이기 위해 에이전시 및 레퍼러 트래픽의 브랜드 유무 데이터와 통찰력을 통해 기회를 식별하고 처방적 권장 사항을 제공해야 합니다.

### AEM 이외의 클라우드 고객

비즈니스 계약이 완료되면 LLM Optimizer에서 온보딩하려는 도메인과 함께 온보딩됩니다. 이 온보딩이 완료되면 [https://llmo.now](https://llmo.now)을(를) 통해 LLM Optimizer에 로그인할 수 있습니다.

### 2단계: 범주, 주제 및 프롬프트 사용자 정의

사이트가 온보딩되면 온보딩 단계 중에 자동으로 생성된 작은 프롬프트 세트를 기반으로 브랜드 현재 상태 분석을 볼 수 있습니다. 앞으로 이동하여 브랜드에 대한 카테고리, 주제 및 프롬프트를 사용자 정의할 수 있습니다. 이 구성은 [고객 구성 대시보드](/help/dashboards/customer-configuration.md)에 만들어집니다.

![고객 구성 대시보드](/help/overview/assets/prompt-creation.png)

이 대시보드에서 다음을 수행할 수 있습니다.

* 비즈니스 우선 순위에 맞는 **새 범주**&#x200B;를 추가하십시오. 카테고리는 도메인과 관련된 광범위한 콘텐츠 영역일 수 있습니다.
* 추적할 **사용자 지정 항목** 또는 하위 항목을 입력하십시오. 주제는 도메인과 연결된 대량 비브랜드 키워드에 연결된 특정 테마일 수 있습니다.
* 특정 쿼리에서 가시성을 모니터링하려면 **프롬프트**&#x200B;를 만드십시오. 프롬프트는 기준 가시성을 제공하는 쿼리(브랜드 및 비브랜드)입니다. 제공한 범주 및 항목에 따라 제한된 수의 프롬프트만 자동으로 생성됩니다.
* 브랜드에 대한 모든 언급을 캡처하고 설명하도록 언급 **별칭**&#x200B;을(를) 정의합니다.
* 다른 브랜드를 정확하게 추적하려면 **다른 별칭**&#x200B;을 정의하세요.

>[!NOTE]
>LLM에 묻는 정확한 프롬프트는 LLM에 의해 공개되지 않으므로 공개적으로 사용할 수 없습니다.

>[!NOTE]
>
> 범주, 주제, 프롬프트를 설정하는 방법에 대한 자세한 내용은 [범주, 주제, 프롬프트 구성에 대한 모범 사례](/help/overview/best-practices-topics-prompts.md) 페이지를 참조하십시오.

### 3단계: 브랜드 유무 통찰력

도메인이 온보딩되면 온보딩 중에 자동으로 생성된 프롬프트를 기반으로 브랜드 현재 상태 보기에서 초기 인사이트를 보게 됩니다. 카테고리, 주제 및 프롬프트를 사용자 정의하면 LLM Optimizer에서 제공한 프롬프트에 대해 브랜드 존재 분석을 자동으로 트리거하고 24시간 후에 결과를 사용할 수 있습니다.

### 4단계: CDN 로그 전달에 대한 정보 제공 {#step-4}

에이전트 트래픽 및 참조 트래픽 인사이트를 잠금 해제하려면 CDN 로그 전달에 대한 정보를 제공해야 합니다. [CDN 구성](/help/dashboards/customer-configuration.md#cdn-configuration) 탭으로 이동한 다음 **CDN 온보드**&#x200B;를 클릭하여 **고객 구성 대시보드**&#x200B;에서 추가할 수 있습니다.

![고객 구성 CDN](/help/overview/assets/cc-cdn.png)

또는 위에서 설명한 대로 미리 추가된 CDN 공급자가 없는 경우 에이전트 및 참조 트래픽 대시보드에 처음 액세스할 때 CDN 로그 전달을 추가하라는 메시지가 표시됩니다. 자세한 내용은 다음을 참조하십시오.

* [무형성 트래픽](/help/dashboards/agentic-traffic.md#cdn-setup)
* [참조 트래픽](/help/dashboards/referral-traffic.md#setup#setup)

### 5단계: 대시보드 탐색 및 작업 수행

CDN 로그 전달에 대한 정보를 제공하면 다음과 같은 작업을 수행할 수 있습니다.

* [브랜드 유무](/help/dashboards/brand-presence.md) 대시보드를 보고 가시성 점수를 보고 다른 브랜드와 비교하여 성과를 추적하세요.
* CDN 로그 전달이 구성된 경우 [Agentic](/help/dashboards/agentic-traffic.md) 및 [참조 트래픽](/help/dashboards/referral-traffic.md) 대시보드를 살펴보십시오.
* [기회](/help/dashboards/opportunities.md)를 사용하여 콘텐츠 및 기술 개선 사항을 식별하십시오.
* 데이터를 내보내고 팀에 공동 작업하거나 동료가 제품을 사용하도록 초대합니다.

마지막으로 LLM Optimizer의 기능을 완전히 이해하려면 사용 가능한 모든 [대시보드](/help/dashboards/dashboards-overview.md)를 살펴봐야 합니다.
