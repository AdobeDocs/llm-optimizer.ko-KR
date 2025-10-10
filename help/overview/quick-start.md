---
title: 빠른 시작
description: 이 문서는 빠른 시작 문서입니다.
source-git-commit: 5dbf794b87df92583daec83ab02063821ee7a412
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# 빠른 시작

LLM Optimizer를 시작하려면 온보딩 프로세스를 거쳐야 합니다. 그 후에는 LLM Optimizer의 대시보드 및 전체 기능에 액세스할 수 있습니다.

## 온보딩 개요

온보딩 프로세스는 도메인 온보딩으로 시작합니다. AEM Cloud 고객인지 여부에 따라 프로세스가 다릅니다. 프로세스를 완료한 후에는 CDN 로그 전달에 대한 정보를 제공하고 마지막으로 카테고리, 주제 및 프롬프트를 사용자 정의해야 합니다.

### 1단계: 도메인 온보드

### AEM 클라우드 고객

AEM Cloud 고객(Cloud Service/Managed Services/ Edge Delivery 서비스)에게는 [Experience Hub](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/experience-hub/experience-hub)의 제품 공지 카드를 통해 LLM Optimizer을 시도할 수 있는 옵션이 표시됩니다.

>[!NOTE]
>새로 추가된 프롬프트는 처리가 완료될 때까지 브랜드 유무에 표시되지 않습니다. AEM Cloud 고객(Cloud Service, Managed Services/ Edge Delivery Service)은 LLM Optimizer 무료 평가판을 사용할 수 있습니다. 200개 이상의 프롬프트를 사용하려면 별도의 라이센스 계약이 필요합니다. 액세스는 &quot;있는 그대로&quot; 및 &quot;사용 가능한 대로&quot; 제공되며 언제든지 Adobe에 의해 수정, 제한 또는 제거될 수 있습니다. 자세한 내용은 [계정 담당자]에게 문의하십시오.

![LLM Optimizer 평가판](/help/overview/assets/llm-trial.png)

**LLM Optimizer 시도** 단추를 클릭하면 [https://llmo.now](https://llmo.now)&#x200B;(으)로 리디렉션됩니다. 그런 다음 IMS를 통해 로그인해야 합니다. 로그인하면 도메인과 브랜드 이름을 제공하여 온보딩 프로세스를 시작합니다.

![LLM Optimizer 도메인](/help/overview/assets/domain.png)

>[!NOTE]
>제공한 도메인은 조직의 모든 사용자가 사용하게 되며 변경할 수 없습니다.

브랜드 유무 분석을 트리거하려면 카테고리, 주제 및 프롬프트를 제공해야 합니다.

![브랜드 유무 분석](/help/overview/assets/bp-analysis.png)

또한 트래픽 분석을 위해 CDN 로그 전달을 구성해야 합니다. LLM Optimizer은 기회를 식별하고 고객이 AI 가시성을 높이는 데 도움이 되는 처방적 권장 사항을 제공하기 위해 에이전트 및 레퍼러 트래픽의 브랜드 유무 데이터와 통찰력이 필요합니다.

### AEM 이외의 클라우드 고객

계약에 서명하면 LLM Optimizer에서 온보딩하려는 도메인과 함께 slackbot 명령을 통해 온보딩됩니다. 이 온보딩이 완료되면 [https://llmo.now](https://llmo.now) 을 통해 LLM Optimizer에 로그인할 수 있습니다.

### 2단계: 인사이트의 자동 사전 채우기

도메인이 온보딩되면 LLM Optimizer에서 자동으로 다음을 채웁니다.

* **범주** - 도메인과 관련된 광범위한 콘텐츠 영역입니다.
* **주제** - 도메인과 연결된 대량의 브랜드 이외의 키워드에 연결된 특정 테마입니다.
* **프롬프트** - 기준선 가시성을 제공하기 위한 쿼리(브랜드 및 비브랜드)입니다.

이렇게 하면 사용자 지정 구성 및 입력을 추가하기 전에 브랜드 가시성에 대한 초기 인사이트를 확인할 수 있습니다.

### 3단계: 범주, 주제 및 프롬프트 사용자 정의

[고객 구성 대시보드](/help/dashboards/customer-configuration.md)를 클릭하여 범주, 항목 및 프롬프트를 사용자 지정합니다.

![고객 구성 대시보드](/help/dashboards/assets/customer-config.png)

이 대시보드에서 다음을 수행할 수 있습니다.

* 비즈니스 우선 순위에 맞는 새 카테고리를 추가합니다.
* 추적해야 하는 사용자 정의 항목 또는 하위 항목을 입력합니다.
* 특정 쿼리에서 가시성을 모니터링하기 위한 프롬프트를 만듭니다.
* 모든 언급이 캡처되도록 언급 별칭을 정의합니다.
* 경쟁업체 별칭을 정의하여 경쟁업체를 정확하게 추적할 수 있습니다.

### 4단계: CDN 로그 전달에 대한 정보 제공

에이전트 트래픽 및 참조 트래픽 인사이트를 잠금 해제하려면 CDN 로그 전달에 대한 정보를 제공해야 합니다. 로그 전달을 구성하는 방법에 대한 자세한 내용은 각 특정 페이지를 참조하십시오.

* [무형성 트래픽](/help/dashboards/agentic-traffic.md)
* [참조 트래픽](/help/dashboards/referral-traffic.md#setup#cdn-setup)

### 5단계: 대시보드 탐색 및 작업 수행

CDN 로그 전달에 대한 정보를 제공하면 다음과 같은 작업을 수행할 수 있습니다.

* [브랜드 유무](/help/dashboards/brand-presence.md) 대시보드를 보고 가시성 점수를 보고 경쟁사와 비교하여 성과를 추적하십시오.
* [에이전트](/help/dashboards/agentic-traffic.md) 및 [참조 트래픽](/help/dashboards/referral-traffic.md) 대시보드를 살펴봅니다.
* [기회](/help/dashboards/opportunities.md)를 사용하여 콘텐츠 및 기술 개선 사항을 식별하십시오.
* 데이터를 내보내고 팀에 공동 작업하거나 동료가 제품을 사용하도록 초대합니다.

LLM 최적기의 기능을 완전히 이해하려면 사용 가능한 모든 [대시보드](/help/dashboards/dashboards-overview.md)를 살펴보세요.
