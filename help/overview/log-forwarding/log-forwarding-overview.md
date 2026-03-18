---
title: BYOCDN 로그 전달 개요
description: LLM Optimizer의 에이전트 트래픽 데이터 수집을 위해 공급자의 CDN 로그를 Adobe의 S3 버킷으로 전달하는 방법을 알아봅니다.
feature: Agentic Traffic
source-git-commit: a1ba7684ccef9baf3452cc158fc0d6a12aa7adb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 3%

---


# BYOCDN 로그 전달 개요 {#cdn-log-forwarding}

BYOCDN(고객 관리 CDN)에 대한 로그 전달은 Adobe이 agentic 트래픽 데이터를 수집하고 분석할 수 있도록 CDN 액세스 로그를 Amazon의 LLM Optimizer S3 버킷으로 전송하는 프로세스입니다. CDN 로그 전달이 없으면 [에이전트 트래픽](/help/dashboards/agentic-traffic.md) 대시보드에 지표를 표시할 수 없습니다.

아래에 제공된 안내서는 동일한 2단계 워크플로우를 따릅니다.

1. **LLM Optimizer에서 온보드** — 필요한 S3 자격 증명과 경로 세부 정보를 생성하려면 [CDN 구성](/help/dashboards/customer-configuration.md) 페이지에서 CDN을 등록하십시오.
2. **CDN 구성** — 이러한 세부 정보를 사용하여 CDN 공급자의 콘솔에서 로그 전달 작업을 만들거나 로그를 수동으로 업로드하십시오.

## CDN 공급자 {#cdn-providers}

CDN 공급자에 대해 해당 안내서를 따르십시오.

| CDN 공급자 | 안내서 |
|---|---|
| Akamai | [안내서 보기](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [안내서 보기](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront | [안내서 보기](/help/overview/log-forwarding/cloudfront.md) |
| Fastly | [안내서 보기](/help/overview/log-forwarding/fastly.md) |
| 임페르바 | [안내서 보기](/help/overview/log-forwarding/imperva.md) |
| 기타(수동/지원되지 않는 CDN) | [안내서 보기](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>CDN 공급자가 위에 나열되어 있지 않은 경우 수동 업로드, 임시 스크립트 및 기본적으로 지원되지 않는 CDN을 다루는 **기타(수동/지원되지 않는 CDN)** 안내서를 사용하십시오.
