---
title: BYOCDN 로그 전달 개요
description: LLM Optimizer의 에이전틱 트래픽 데이터 수집을 위해 공급자에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법에 대해 알아봅니다.
feature: Agentic Traffic
autotag-review: '2026-07-15T18:07:52.453Z'
TQID: 'https://experienceleague.adobe.com/iN1Tm-7j2FTQ1UodWvCZpOSy0FnQEyMkBMZIL9z3t38'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
feature_v2:
  - id: d1956731-2adb-4bb7-8301-2b239254ac72
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
  - id: e0828736-236a-487b-a478-5a635455eadc
subfeature_v2:
  - id: d23587d6-14d6-4e3f-9ee1-cc18623832e1
  - id: dd952468-5202-43af-a365-6e0d2e67a703
  - id: e06fae5f-830b-4222-a469-b5e148d36465
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 2705cf26faea9c09817bbdcec4b4c531552df7ba
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 100%

---


# BYOCDN 로그 전달 개요 {#cdn-log-forwarding}

고객 관리 CDN(BYOCDN)에 대한 로그 전달은 LLM Optimizer가 에이전틱 트래픽 데이터를 수집하고 분석할 수 있도록 CDN 액세스 로그를 Adobe의 Amazon S3 버킷으로 전송하는 프로세스입니다. CDN 로그 전달이 없으면 [에이전틱 트래픽](/help/dashboards/agentic-traffic.md) 대시보드에 지표를 표시할 수 없습니다.

아래에 제공된 안내서는 동일한 2단계 워크플로를 따릅니다.

1. **LLM Optimizer에서 온보딩** — 필요한 S3 자격 증명과 경로 세부 정보를 생성하려면 [CDN 구성](/help/dashboards/customer-configuration.md) 페이지에서 CDN을 등록합니다.
2. **CDN 구성** — 이러한 세부 정보를 사용하여 CDN 공급자의 콘솔에서 로그 전달 작업을 만들거나 로그를 수동으로 업로드합니다. CloudFront의 경우 콘솔을 사용하거나 **AWS CLI**&#x200B;로만 게재 설정을 완료할 수 있습니다. [CloudFront(AWS CLI)](/help/overview/log-forwarding/cloudfront-cli.md)를 참조하십시오.

## CDN 공급자 {#cdn-providers}

CDN 공급자에 대해 해당 안내서를 따릅니다.

| CDN 공급자 | 안내서 |
|---|---|
| Akamai | [안내서 보기](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [안내서 보기](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront(콘솔) | [안내서 보기](/help/overview/log-forwarding/cloudfront.md) |
| CloudFront(AWS CLI) | [안내서 보기](/help/overview/log-forwarding/cloudfront-cli.md) |
| Fastly | [안내서 보기](/help/overview/log-forwarding/fastly.md) |
| Imperva | [안내서 보기](/help/overview/log-forwarding/imperva.md) |
| 기타(수동/지원되지 않는 CDN) | [안내서 보기](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>CDN 공급자가 위에 나열되지 않은 경우, 수동 업로드, 임시 스크립트 및 기본적으로 지원되지 않는 CDN을 다루는 **기타(수동/지원되지 않는 CDN)** 안내서를 사용하십시오.
