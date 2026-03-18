---
title: 로그 전달 - 빠른
description: LLM Optimizer의 에이전트 트래픽 데이터 수집을 위해 CDN 로그를 Fastly에서 Adobe의 S3 버킷으로 전달하는 방법을 알아봅니다.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 4%

---


# 로그 전달: 빠르게 {#log-forwarding-fastly}

이 페이지에서는 에이전트 트래픽 데이터 수집을 위해 CDN 로그를 Fastly에서 Adobe의 S3 버킷으로 전달하는 방법을 설명합니다. LLM Optimizer CDN 구성 페이지를 사용하여 LLM Optimizer에 온보딩합니다. 온보딩 프로세스가 완료되면 이 페이지에 제공된 단계에 따라 Fastly 웹 콘솔에서 로그 전달을 구성합니다.

## 1단계: LLM Optimizer에서 온보드 {#step-1}

LLM Optimizer 페이지 [https://llmo.now/](https://llmo.now/)에서:

1. **구성**(으)로 이동합니다.

   ![구성 버튼](/help/overview/assets/log-forwarding/common/config-button.png)

1. **CDN 구성** 탭을 클릭합니다.

   ![CDN 구성 탭](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. **시작하기**&#x200B;를 클릭합니다.
1. **AI 트래픽 인사이트 활성화** 옆에 있는 **구성**&#x200B;을 클릭하세요.

   ![구성](/help/overview/assets/log-forwarding/common/configure.png)
1. **Fastly(BYOCDN)**&#x200B;을(를) 선택합니다.

   ![빠르게 선택](/help/overview/assets/log-forwarding/fastly/fastly-select.png)
1. **온보드**&#x200B;를 클릭합니다.

## 2단계: Fastly에서 S3 엔드포인트 만들기 {#step-2}

**Fastly Campaign 컨트롤 패널**&#x200B;에서 S3 끝점을 만들려면:

1. Fastly 대시보드에서 **CDN 서비스**(계산 서비스 아님)로 이동합니다.
1. **Amazon Web Services S3** 영역에서 **끝점 만들기**&#x200B;를 클릭합니다.
1. **Amazon S3 끝점 만들기** 필드를 채웁니다.

| 필드 | 설명 |
| --- | --- |
| **이름** | 사람이 인식할 수 있는 엔드포인트 이름. |
| **배치** | 기본값 |
| **로그 형식** | 아래의 **로그 형식 문자열** 섹션에 표시된 로그 형식 문자열을 사용하십시오. |
| **타임스탬프 형식** | `%Y-%m-%dT%H:%M:%S.000` |
| **버킷 이름** | LLM Optimizer 구성 페이지에서 **버킷 이름**&#x200B;을 복사합니다. ![버킷 이름](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **도메인** | LLM Optimizer 구성 페이지에서 **도메인 이름**&#x200B;을(를) 복사합니다. ![도메인 이름](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **액세스 메서드** | **사용자 자격 증명** |
| **사용자 자격 증명** | LLM Optimizer 구성 페이지에서 **액세스 키** 및 **암호 키**&#x200B;를 복사합니다. ![액세스 키](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **기간** | `300` |

**로그 형식 문자열:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>암호 관리자는 **암호 키** 필드에 Fastly 암호를 자동으로 입력할 수 있습니다. AWS 통합에 실패하는 경우 비밀 키를 수동으로 입력합니다.

위의 단계를 완료한 후 **고급 옵션**&#x200B;을 클릭하고 다음을 설정합니다.

| 필드 | 설명 |
| --- | --- |
| **경로** | LLM Optimizer 구성 페이지에서 **경로**&#x200B;을(를) 복사합니다. ![경로](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **로그 라인 형식 선택** | 비어 있음 |
| **압축** | Gzip |
| **중복 수준** | 표준 |
| **ACL** | 없음 |
| **서버측 암호화** | 없음 |
| **최대 바이트** | 0 |

고급 옵션을 설정한 후:

1. 끝점을 만들려면 **만들기**&#x200B;를 클릭합니다.
1. **활성화** 메뉴에서 **프로덕션에 활성화**&#x200B;를 선택하여 배포합니다.

>[!NOTE]
>
>Fastly는 로그를 S3에 지속적으로 스트리밍하며 S3 웹 사이트 및 API는 업로드가 완료된 후에만 파일을 사용할 수 있도록 합니다.

### 로그 항목 예 {#example}

다음은 Amazon S3로 데이터를 전송하기 위한 예제 형식 문자열입니다.

```json
{
  "timestamp": "2026-02-10T05:05:36+0000",
  "host": "example.com",
  "url": "/my/path",
  "request_method": "GET",
  "request_referer": "https://example.com/my/other/path",
  "request_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
  "response_status": 200,
  "response_content_type": "text/css; charset=utf-8",
  "client_country_code": "argentina",
  "time_to_first_byte": "0.138"
}
```
