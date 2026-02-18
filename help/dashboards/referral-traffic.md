---
title: 참조 트래픽
description: 참조 트래픽 대시보드를 사용하여 외부 플랫폼, AI 인용 및 참조 링크에서 방문자가 사이트에 도달하는 방식을 알아봅니다.
feature: Referral Traffic
source-git-commit: e50c87e8e5a669526f3c10855c1629ce82b67aef
workflow-type: ht
source-wordcount: '605'
ht-degree: 100%

---


# 참조 트래픽

참조 트래픽은 외부 플랫폼, AI 인용 및 참조 링크에서 방문자가 사이트에 도달하는 방식을 보여 줍니다. 외부 웹 사이트 및 플랫폼에서 트래픽 소스, 참조 패턴 및 전환 지표를 추적하고 분석합니다. 이렇게 하면 가장 많은 트래픽이 발생하는 소스, 지역 및 페이지를 이해할 수 있습니다. <!--Data is sourced from the CDN logs, a privacy-preserving source that does not capture personal user data.--> 표시된 데이터를 세분화하는 데 도움이 되는 사용자 정의 가능 필터도 있습니다.

![참조 페이지](/help/dashboards/assets/referral-traffic.png)

이 페이지는 다음 사항을 자세히 설명합니다.

* [설정](#setup)
* [필터](#filters)
* [전체 참조 성능](#overall-performance)
* [상위 참조 URL](#top-referrals)
* [참조 트래픽 세부 정보](#traffic-details)

## 설정 {#setup}

처음 로그인하면 참조 트래픽 대시보드가 비어 있을 수 있습니다. 데이터를 보려면 **구성으로 이동**&#x200B;을 선택하여 [CDN 로그 전달](/help/dashboards/customer-configuration.md#cdn-configuration)을 구성해야 합니다.

![참조 설정](/help/dashboards/assets/referral-setup1.png)

<!--- 1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM-->

활성화되면 대시보드에 참조 트래픽 지표가 채워집니다.

## 필터 {#filters}

페이지 맨 위에서 필터를 적용하여 보기를 세분화할 수 있습니다. 선택한 필터는 대시보드에 있는 **모든** 섹션에 영향을 미칩니다. 다음을 사용자 정의할 수 있습니다.

* **날짜 범위** - 표시된 데이터의 시간대를 선택합니다. 예를 들어 지난 4주를 선택합니다. **주 사용자 정의** 옵션을 선택하여 기간을 사용자 정의할 수도 있습니다.
* **플랫폼** - Google, OpenAI 또는 소셜 미디어와 같은 특정 트래픽 소스를 선택합니다.
* **페이지 의도** - 사용자 의도로 참조 트래픽을 필터링합니다.
* **채널 소스** - 채널의 소스로 필터링합니다. 옵션에는 LLM, 획득, 유료 또는 혼합 참조 채널이 포함됩니다.
* **장치 유형** - 데스크탑, 모바일 또는 모든 장치 중 방문자의 장치 유형별로 트래픽을 분석합니다.
  **지역** - 다른 지역의 참조 패턴을 봅니다.

원하는 필터를 선택한 후 **필터 적용**&#x200B;을 클릭하여 대시보드에 선택 사항을 적용합니다.

## 전체 참조 성능 {#overall-performance}

대시보드는 다음과 같은 주요 지표를 표시하여 전체 참조 성능을 강조 표시합니다.

* **총 참조 트래픽** - 모든 소스에서 발생한 총 참조 트래픽입니다.
* **LLM의 참조 트래픽** - LLM의 총 참조 트래픽입니다.
* **동의율** - 동의 프롬프트를 수락하는 방문자의 비율입니다.
* **바운스 비율** - 참여 이벤트가 없는 참조 소스의 세션 비율입니다.

![참조 페이지](/help/dashboards/assets/referral-traffic.png)

위에 제시된 전반적인 성능 지표 외에도, 다양한 시장, 참조 소스 및 페이지 의도 카테고리 간의 트래픽 분포를 보여 주는 세 개의 추가 패널이 있습니다. <!-- the **Top Regions** panel breaks down traffic by geography. Meanwhile, the **Top Referral Sources** panel shows the platforms driving the most visits. Trend indicators for the metrics show how these values are changing over time compared to the previous period.-->

<!--## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site's most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)-->

## 참조 소스 세부 정보 및 URL 성능 분석 {#traffic-details}

참조 소스 세부 정보 및 URL 성능 분석 테이블은 트래픽 양과 품질을 모두 평가할 수 있습니다. 자세한 내용은 아래 각 탭을 클릭합니다.

![참조 트래픽 세부 정보](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB 참조 소스 세부 정보]

참조 소스 세부 정보 보기는 OpenAI, Microsoft, Google, Perplexity 등 다양한 플랫폼에서 들어오는 트래픽을 분류합니다. 방문 수, 바운스 비율, 채널 유형과 같은 주요 지표를 표시하여 어떤 AI 및 검색 소스가 사이트에 가장 많은 트래픽을 유도하는지 파악할 수 있습니다.

* **소스** - 참조 트래픽의 소스입니다.
* **방문 수** - 각 소스에 대한 총 방문 횟수입니다.
* **바운스 비율** - 참여 이벤트가 없는 참조 소스의 세션 비율입니다.
* **채널** - 소스에 대한 채널(획득, 유료 또는 둘 다)입니다.

>[!TAB URL 성능 분석]

URL 성능 분석 보기는 LLM 및 기타 소스의 참조 트래픽 양을 기준으로 최고 성능의 페이지를 순위 매깁니다. 트래픽, 바운스 비율, 동의율, 페이지 의도와 같은 지표를 강조 표시하여 AI 기반 추천에서 가장 많은 방문자를 끌어들이고 유지하는 페이지를 식별할 수 있습니다. 이 테이블에는 주제 바로 가기를 위한 검색 필드가 있습니다.

>[!ENDTABS]

두 테이블 모두에서 **내보내기** 옵션을 사용하여 table .csv를 다운로드하고 팀과 인사이트를 공유하거나 경영진 보고에 테이블을 포함할 수 있습니다. 또한 두 테이블 모두에 대해 **열 구성** 버튼을 클릭하여 표시되는 지표를 사용자 정의할 수 있습니다.
