---
title: Edge - CloudFront(BYOCDN)에서 최적화
description: LLM Optimizer의 Edge에서 최적화하기 위해 CloudFront BYOCDN을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 1253d0f0a58f6523699c52fbfab23028dc469c82
workflow-type: tm+mt
source-wordcount: '2228'
ht-degree: 1%

---


# CloudFront(BYOCDN)

이 구성은 에이전트 트래픽(AI 보트 및 LLM 사용자 에이전트의 요청)을 Edge 최적화 백 엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 평소처럼 원산지에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 `x-edgeoptimize-request-id` 헤더를 찾습니다.

**사전 요구 사항**

CloudFront 구성을 설정하기 전에 다음을 확인하십시오.

* 웹 사이트를 제공하는 기존 CloudFront 배포입니다.
* AWS IAM 권한은 Lambda 함수, IAM 역할, CloudFront 배포 및 캐시 정책을 만들 수 있습니다.
* LLM Optimizer 온보딩 프로세스를 완료했습니다.
* LLM Optimizer에 CDN 로그 전달을 완료했습니다.
* LLM Optimizer UI에서 검색한 Edge Optimize API 키.

{{retrieve-byocdn-api-key}}

**1단계: Edge 최적화 원본 만들기**

**탐색:** AWS 콘솔 > CloudFront > 배포 > [배포] > 원본 탭

1. **원본 만들기**&#x200B;를 클릭합니다.

2. 원본을 구성합니다.
   * **원본 도메인:** `live.edgeoptimize.net`
   * **이름:** `EdgeOptimize_Origin`

3. 다른 모든 필드는 기본값으로 둡니다.

4. 사용자 지정 헤더 추가:

   | 헤더 | 값 |
   |--------|-------|
   | `x-edgeoptimize-api-key` | API 키 |
   | `x-forwarded-host` | `www.example.com` |

   `www.example.com`을(를) 실제 웹 사이트 도메인으로 바꾸고 `Your API key`을(를) Adobe 담당자가 제공한 Edge Optimize API 키로 바꿉니다.

5. **원본 만들기**&#x200B;를 클릭합니다.

![Cloudfront 원본 만들기](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

**2단계: 뷰어 요청 함수 만들기**

**탐색:** AWS 콘솔 > CloudFront > 함수

1. **함수 만들기**&#x200B;를 클릭합니다.

2. 다음을 구성하십시오.
   * **이름:** `edgeoptimize-routing`
   * **런타임:** `cloudfront-js-2.0`

3. 기본 코드를 [viewer-request.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/cloudfront-function/viewer-request.js)의 코드로 바꿉니다.

   게시하기 전에 코드에서 다음 값을 사용자 지정합니다.

   * `YOUR_DEFAULT_ORIGIN` — 기존 기본 원본 이름으로 대체합니다( CloudFront > 배포 > [배포] > 원본 탭에 있음).
   * `TARGETED_PATHS` — 모든 HTML 페이지를 대상으로 지정하려면 `null`(으)로 설정하거나 특정 경로의 배열(예: `['/', '/products', '/about']`)로 설정합니다.

4. **변경 내용 저장** > **함수 게시**&#x200B;를 클릭합니다.

![Cloudfront 함수 만들기](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


**3단계: 캐시 정책 구성**

**탐색:** AWS 콘솔 > CloudFront > 배포 > [배포] > 동작

현재 동작에 연결된 캐시 정책을 확인합니다. 동작을 클릭하여 **편집**&#x200B;을 클릭하고 **캐시 키 및 원본 요청** 섹션을 보고 시나리오를 식별하세요.

* **시나리오 A(기존):** 선택한 **기존 캐시 설정**&#x200B;이라는 라디오 단추가 표시됩니다. 정책 이름 드롭다운이 없습니다. 대신 인라인 TTL 및 헤더 설정이 표시됩니다.
* **시나리오 B(사용자 지정 정책):** 사용자 또는 팀이 만든 정책 이름(AWS 제공 정책이 아님)으로 선택한 **캐시 정책**&#x200B;이 표시됩니다.
* **시나리오 C(관리 정책):** `CachingOptimized`, `CachingDisabled` 또는 `CachingOptimizedForUncompressedObjects`과(와) 같이 AWS에서 제공한 이름으로 선택한 **캐시 정책**&#x200B;이(가) 있습니다. 이러한 정책은 편집할 수 없습니다.

**시나리오 A: 레거시 캐시 설정**

동작이 레거시 캐시 설정을 사용하는 경우:

1. **캐시 키 및 원본 요청**&#x200B;에서 **레거시 캐시 설정**&#x200B;이 선택됩니다.

2. **Headers** 허용 목록에 `x-edgeoptimize-config` 및 `x-edgeoptimize-url` 추가:

   * 드롭다운에서 **다음 헤더 포함**&#x200B;을 선택합니다.
   * `x-edgeoptimize-config` 및 `x-edgeoptimize-url`을(를) 추가합니다.
     ![Cloudfront 캐시 레거시](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   헤더 드롭다운에서 이미 **모두**&#x200B;을(를) 선택한 경우 이 단계를 건너뜁니다. 모든 헤더가 자동으로 원본으로 전달됩니다.

3. **개체 캐싱** 설정을 확인하십시오.

   * **사용자 지정**(으)로 설정하는 경우 **최소 TTL**&#x200B;을(를) `0`(으)로 설정하는 것이 좋습니다. 그러나 현재 최소 TTL이 이미 매우 짧은 경우 변경할 필요가 없습니다.
   * **원본 캐시 헤더 사용**(으)로 설정된 경우 변경할 필요가 없습니다.

4. **변경 내용 저장**&#x200B;을 클릭합니다.

**시나리오 B: 사용자 지정 캐시 정책을 사용하는 비레거시**

동작이 이미 사용자 지정 캐시 정책(AWS 관리 정책이 아닌 사용자가 만든 정책)을 사용하는 경우:

**탐색:** AWS 콘솔 > CloudFront > 정책 > 캐시

1. 기존 정책을 클릭합니다.

2. **편집**&#x200B;을 클릭합니다.

3. **최소 TTL**&#x200B;을(를) `0`(으)로 설정하는 것이 좋습니다. 그러나 현재 최소 TTL이 이미 매우 짧은 경우 변경할 필요가 없습니다.
   ![캐시 정책 TTL 설정](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. **캐시 키 설정** > **헤더**&#x200B;에서 기존 포함과 함께 `x-edgeoptimize-config` 및 `x-edgeoptimize-url`을(를) 추가합니다.
   ![캐시 정책 헤더](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. **변경 내용 저장**&#x200B;을 클릭합니다.

**시나리오 C: 관리되는(AWS) 캐시 정책이 있는 비레거시**

동작이 AWS 관리 캐시 정책(예: `CachingOptimized`)을 사용하는 경우 편집할 수 없습니다. 기존 관리 정책 설정을 복제하고 맨 위에 Edge 최적화 헤더를 추가하는 새 사용자 지정 캐시 정책을 만들어야 합니다.

**1부: 현재 관리되는 캐시 정책 설정을 적어 두십시오**

**탐색:** AWS 콘솔 > CloudFront > 정책 > 캐시

1. 현재 동작에 연결된 관리되는 캐시 정책을 찾아 클릭합니다(예: `CachingOptimized`).

2. 기존 설정을 모두 기록합니다.
   * 최소 TTL, 최대 TTL, 기본 TTL
   * 캐시 키에 포함된 헤더
   * 캐시 키에 포함된 쿠키
   * 캐시 키에 포함된 쿼리 문자열
   * 압축 지원(Gzip, Brotli)

**파트2: 동일한 설정 + Edge 최적화 구성을 사용하여 새 사용자 지정 캐시 정책 만들기**

**탐색:** AWS 콘솔 > CloudFront > 정책 > 캐시

1. **캐시 정책 만들기**&#x200B;를 클릭합니다.

2. **이름:** `edgeoptimize-cache`

   ![캐시 정책 이름](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. 1부에 언급된 모든 설정을 다음과 같이 수정하여 복제합니다.

   * **최소 TTL**&#x200B;을(를) `0`(으)로 설정하는 것이 좋습니다. 그러나 현재 최소 TTL이 이미 매우 짧은 경우 변경할 필요가 없습니다.

   ![캐시 정책 TTL 설정](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * **캐시 키 설정** > **헤더**&#x200B;에서 관리 정책에 있는 모든 내용을 포함하고 `x-edgeoptimize-config` 및 `x-edgeoptimize-url`을(를) 추가합니다.

   ![캐시 정책 헤더](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. **만들기**&#x200B;를 클릭합니다.

5. 동작으로 돌아가서 새로 만든 정책을 연결합니다.

   **탐색:** AWS 콘솔 > CloudFront > 배포 > [배포] > 동작

   1. 비헤이비어를 편집합니다.
   2. **캐시 키 및 원본 요청**&#x200B;에서 **캐시 정책**&#x200B;을 선택합니다.
   3. 드롭다운에서 `edgeoptimize-cache`을(를) 선택합니다.
   4. **변경 내용 저장**&#x200B;을 클릭합니다.

**4단계: Lambda@Edge 함수 만들기(원본 요청 및 응답)**

>[!IMPORTANT]
>Lambda@Edge 함수 **은(는) `us-east-1`(버지니아 북부) 지역**&#x200B;에서 만들어야 합니다. AWS 요구 사항입니다. 함수가 `us-east-1`에서 만들어지더라도 AWS은 이 함수를 전 세계의 모든 CloudFront 엣지 로케이션에 자동으로 복제하므로 뷰어에 가장 가까운 엣지 로케이션에서 실행됩니다. 계속하기 전에 AWS 콘솔에서 `us-east-1` 지역에 있는지 확인하십시오.

**Lambda 함수 만들기**

**탐색:** AWS 콘솔 > 람다

1. **함수 만들기**&#x200B;를 클릭합니다.

2. **처음부터 작성자**&#x200B;를 선택하십시오.

3. 다음을 구성하십시오.
   * **함수 이름:** `edgeoptimize-origin`
   * 다른 모든 필드는 기본값으로 둡니다.

4. **함수 만들기**&#x200B;를 클릭합니다.

5. 코드 편집기에서 기본 코드를 [origin-request-response.js](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/origin-request-response.js)의 코드로 바꿉니다.

6. 코드를 저장하려면 **배포**&#x200B;를 클릭하세요.

7. **구성** > **권한**(예: `edgeoptimize-origin-role-xxxxx`)에 표시된 **실행 역할 이름**&#x200B;을 참고하십시오. 다음 단계에서 이 작업이 필요합니다.

**실행 역할의 트러스트 정책을 업데이트합니다**

자동으로 만든 역할은 `lambda.amazonaws.com`만 신뢰합니다. Lambda@Edge의 경우 `edgelambda.amazonaws.com`도 추가해야 합니다.

**탐색:** AWS 콘솔 > IAM > 역할 > [이전 단계의 역할] > 트러스트 관계 탭

1. **트러스트 정책 편집**&#x200B;을 클릭합니다.

2. 정책을 [trust-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/trust-policy.json)의 콘텐츠로 바꾸십시오.

3. **정책 업데이트**&#x200B;를 클릭합니다.

>[!WARNING]
>Lambda@Edge의 `edgelambda.amazonaws.com` 서비스 주체는 **필수**&#x200B;입니다. 이 기능이 없으면 CloudFront가 엣지 로케이션에서 함수를 호출할 수 없습니다.

**CloudWatch 로그 권한 정책 수정**

자동 생성된 역할에는 Lambda@Edge에 대한 잘못된 지역 및 로그 그룹 이름이 있는 일반 Lambda에 대해 구성된 `AWSLambdaBasicExecutionRole` 정책이 있습니다. 업데이트해야 합니다.

**탐색:** AWS 콘솔 > IAM > 역할 > [사용자 역할] > 권한 탭 > 연결된 정책 이름(예: `AWSLambdaBasicExecutionRole-xxxx`) 클릭

1. **편집**&#x200B;을 클릭합니다.

2. 정책을 [cloudwatch-policy.json](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/cloudwatch-policy.json)의 콘텐츠로 바꿉니다.

   JSON에서 `ACCOUNT_ID`을(를) 실제 AWS 계정 ID(AWS 콘솔의 오른쪽 상단 모서리에 있음)로 바꾸고, `FUNCTION_NAME`을(를) Lambda 함수 이름(예: `edgeoptimize-origin`)으로 바꿉니다.

3. **변경 내용 저장**&#x200B;을 클릭합니다.

>[!WARNING]
>ARN의 영역은 `*`이어야 합니다. Lambda@Edge은 뷰어에 가장 가까운 에지 위치에서 실행되므로 로그가 에지 위치의 영역(예: `ap-south-1`, `eu-west-1`)에 있는 CloudWatch에 기록되며, 반드시 `us-east-1`일 필요는 없습니다. 로그 그룹에서 지역 접두사가 있는 이름 `/aws/lambda/us-east-1.FUNCTION_NAME`을(를) 사용합니다. 여기서 `us-east-1`은(는) 항상 함수의 홈 영역입니다.

**버전 게시**

1. 함수 페이지에서 **작업**(오른쪽 상단) > **새 버전 게시**&#x200B;를 클릭합니다.

2. 설명을 추가합니다.

3. **게시**&#x200B;를 클릭합니다.
   ![Lambda 게시](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. **함수 ARN**&#x200B;을(를) 복사하거나 메모하십시오. 다음 단계에서 이 작업이 필요합니다.
   ![람다 ARN](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

**5단계: 함수 및 캐시 정책을 동작과 연결**

**탐색:** AWS 콘솔 > CloudFront > 배포 > [배포] > 동작

1. 비헤이비어를 편집합니다.

2. 3단계(시나리오 C)에서 새 캐시 정책을 만든 경우 **캐시 정책**&#x200B;을(를) `edgeoptimize-cache`(으)로 설정하십시오.
   ![캐시 정책](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. **함수 연결**&#x200B;에서 다음을 구성하십시오.

   * **뷰어 요청:** `edgeoptimize-routing`
   * **원본 요청:** 버전 관리 함수 ARN 4단계(**버전 게시**)
   * **원본 응답:** 버전 관리 함수 ARN 4단계(**버전 게시**)

   ![함수 연결 구성](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. **변경 내용 저장**&#x200B;을 클릭합니다.

**6단계: 구성 테스트**

**1. 보트 트래픽 테스트(최적화해야 함)**

에이전트 보트 사용자 에이전트를 사용하여 요청을 보냅니다. **첫 번째 요청**&#x200B;에서 Edge 최적화는 페이지를 처리하고 캐시하는 동안 프록시화된(최적화되지 않은) 응답을 반환할 수 있습니다. 응답의 `x-edgeoptimize-proxy: 1` 헤더로 식별할 수 있습니다.

에이전트 사용자 에이전트를 사용하여 AI 보트 요청 시뮬레이션:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

성공적인 응답에는 `x-edgeoptimize-request-id` 헤더가 포함되어 있으므로 요청이 Edge 최적화를 통해 라우팅되었는지 확인합니다.

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. 사람 트래픽 테스트(영향을 받지 않아야 함)**

일반 사람 브라우저 요청 시뮬레이션:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

응답에는 `x-edgeoptimize-request-id` 헤더가 **없어야**&#x200B;합니다. 페이지 컨텐츠 및 응답 시간은 Edge에서 최적화를 활성화하기 전과 동일하게 유지되어야 합니다.

**3. 두 시나리오를 구분하는 방법**

| 헤더 | 보트 트래픽(최적화됨) | 사람 트래픽(영향을 받지 않음) |
|---|---|---|
| `x-edgeoptimize-request-id` | 있음 — 고유한 요청 ID가 포함되어 있습니다. | 없음 |
| `x-edgeoptimize-fo` | 장애 조치(failover)가 발생한 경우에만 표시됩니다(값: `1`). | 없음 |

LLM Optimizer UI에서 트래픽 라우팅 상태를 확인할 수도 있습니다. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

**4. 로그가 올바르게 흐르고 있는지 확인하십시오**

위의 테스트 요청을 실행한 후 CloudFront 함수와 Lambda@Edge 함수 모두에 대해 로그가 기록되고 있는지 확인하십시오.

*CloudFront 함수 로그(`edgeoptimize-routing`)*

**탐색:** AWS 콘솔 > CloudWatch > 로그 그룹(`us-east-1` 또는 CloudFront 배포가 구성된 지역)

1. 이름이 `/aws/cloudfront/function/edgeoptimize-routing`인 로그 그룹을 찾습니다.
2. 최신 로그 스트림을 엽니다.
3. 에이전트 요청의 경우 다음과 같은 항목이 표시됩니다.
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. 에이전시가 아닌 요청의 경우 다음을 볼 수 있습니다.
   * `Routing to Default origin for userAgent: ...`

또한 **AWS 콘솔 > CloudFront > 함수 > edgeoptimize-routing**&#x200B;에서 **지표** 탭을 확인하여 호출 카운트 및 오류율을 볼 수 있습니다.

*Lambda@Edge 로그(`edgeoptimize-origin`)*

>[!IMPORTANT]
>Lambda@Edge 로그는 `us-east-1`이(가) 아닌 요청을 제공한 **에지 위치**&#x200B;의 CloudWatch에 기록됩니다. curl 명령을 실행한 위치와 가장 가까운 AWS 영역에서 CloudWatch를 확인합니다.

**탐색:** AWS 콘솔 > CloudWatch > 로그 그룹(올바른 지역에 있는지 확인)

1. 이름이 `/aws/lambda/us-east-1.edgeoptimize-origin`인 로그 그룹을 찾습니다.
2. 최신 로그 스트림을 엽니다.
3. 에이전트 요청의 경우 다음과 같은 항목이 표시됩니다.
   * `Calling Edge Optimize Origin for agentic requests` — 기본 경로
   * `Calling Default Origin in case of failover for agentic requests` — 장애 조치(failover) 경로
   * `Failover Triggered for agentic requests` — 원본-응답 장애 조치(failover) 감지

로그 그룹이 없으면 4단계에서 IAM 권한이 올바르게 업데이트되었는지 확인합니다. 근처에 있는 다른 AWS 지역도 확인하십시오. 요청을 제공한 에지 위치가 예상과 다를 수 있습니다.

**문제 해결**

| 문제 | 가능한 원인 | 솔루션 |
|-------|----------------|----------|
| 에이전트 요청에 대한 응답으로 `x-edgeoptimize-request-id`이(가) 없음 | 원본 그룹이 Edge 최적화로 라우팅되지 않음 | `YOUR_DEFAULT_ORIGIN`이(가) CloudFront 함수 코드에서 올바르게 대체되었는지 확인하십시오(2단계). |
| 에이전트 요청에 대한 403 오류 | API 키가 잘못되었거나 누락 | Edge 원본 사용자 지정 헤더 최적화(1단계)에서 `x-edgeoptimize-api-key` 헤더 값을 확인하십시오. |
| Lambda@Edge에 대한 CloudWatch 로그를 찾을 수 없습니다. | 잘못된 IAM 권한 | CloudWatch 로그 권한 정책이 업데이트되었는지 확인합니다(4단계). 참고: Lambda@Edge 로그는 요청을 제공한 에지 영역에 표시되지만 `us-east-1`일 필요는 없습니다. |
| 캐시가 `cache-control: no-store`을(를) 준수하지 않음 | 최소 TTL이 너무 높을 수 있습니다. | 캐시 정책에서 최소 TTL을 `0`(으)로 설정합니다(3단계). 최소 TTL이 이미 매우 짧은 경우 문제가 될 수 있습니다. |
| 설정 후 중단된 일반(에이전트 아님) 트래픽 | 캐시 정책 구성 오류 | 새 캐시 정책을 만든 경우(시나리오 C) 원래 관리 정책에서 모든 설정을 복제했는지 확인하십시오. |

**Edge에서 최적화 비활성화 및 다시 활성화**

Lambda@Edge 함수(`edgeoptimize-origin`)는 CloudFront 동작의 원본 요청 및 원본 응답 이벤트와 연결되어 있습니다. 이 서비스는 사람과 아젠틱을 막론하고 해당 비헤이비어를 통과하는 모든 요청에 인라인으로 실행되기 때문에 Lambda@Edge 작동 중단은 아젠틱 요청뿐만 아니라 모든 라이브 트래픽에 영향을 미칩니다. Lambda@Edge 중단을 감지하면 함수 연결을 즉시 제거하여 일반 트래픽 흐름을 기본 원본으로 복원합니다.

**Lambda@Edge 중단을 감지하는 방법**

* **AWS 서비스 상태 대시보드** — [AWS 서비스 상태 대시보드](https://health.aws.amazon.com/health/status)에서 **Amazon CloudFront** 또는 **AWS Lambda**&#x200B;에 영향을 주는 활성 인시던트에 대해 확인하십시오. 여기에 보고된 전역 또는 지역 중단은 문제가 구성이 아닌 AWS 인프라 측에 있는지 확인하는 가장 빠른 방법입니다.
* **Lambda@Edge 오류** — **AWS 콘솔 > CloudFront > 모니터링 > [내 배포]**&#x200B;로 이동합니다. **Lambda@Edge 오류** 탭을 열고 **실행 오류** 그래프에서 실행 오류를 확인합니다. 이 값이 높으면 Lambda@Edge 이 다운될 수 있습니다.

**Lambda@Edge 함수 분리**

**탐색:** AWS 콘솔 > CloudFront > 배포 > [배포] > 동작

1. 동작을 클릭하여 **편집**&#x200B;을 클릭하세요.

2. **함수 연결** 섹션까지 아래로 스크롤합니다.

3. 다음 연결을 **연결 없음**(으)로 설정합니다.

   | 이벤트 | 다음으로 변경 |
   |---|---|
   | 뷰어 요청 | 연결 없음 |
   | 원본 요청 | 연결 없음 |
   | 원본 응답 | 연결 없음 |

   ![함수 연결 구성](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. **변경 내용 저장**&#x200B;을 클릭합니다.

5. CloudFront 배포가 배포를 완료할 때까지 기다립니다. **배포**&#x200B;에서 마지막 수정 날짜로 상태가 변경되며, 일반적으로 몇 분 이내에 수정됩니다.

배포되면 모든 트래픽이 기본 원본으로 바로 이동합니다. 구성이 삭제되지 않으므로 Lambda 함수와 해당 연결은 언제든지 복원할 수 있습니다.

**Lambda@Edge 함수를 다시 연결합니다**

**탐색:** AWS 콘솔 > CloudFront > 배포 > [배포] > 동작

1. 동작을 클릭하여 **편집**&#x200B;을 클릭하세요.

2. **함수 연결** 섹션까지 아래로 스크롤합니다.

3. 연결 복원:

   | 이벤트 | 다음으로 설정 |
   |---|---|
   | 뷰어 요청 | `edgeoptimize-routing`(CloudFront 함수) |
   | 원본 요청 | 4단계의 버전 관리 Lambda ARN |
   | 원본 응답 | 4단계의 버전 관리 Lambda ARN |

   4단계(**버전 게시**)에서 기록한 버전 있는 **함수 ARN**&#x200B;을(를) 사용하십시오.

   ![함수 연결 구성](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. **변경 내용 저장**&#x200B;을 클릭합니다.

5. 배포가 배포를 완료할 때까지 기다린 다음 에이전트 요청이 6단계에서 설명한 대로 `x-edgeoptimize-request-id` 헤더를 반환하는지 확인합니다.

{{return-to-overview}}
