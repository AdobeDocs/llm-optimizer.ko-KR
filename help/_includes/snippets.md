---
source-git-commit: beae935e7a34f5bccbe21578fa9a928912958710
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---
# 스니펫

## 설정 확인 - Adobe Managed CDN {#verify-setup-adobe-aem-cs-cdn}

**설정 확인**

설정을 완료한 후 보트 트래픽이 Edge 최적화로 라우팅되고 사람 트래픽에 영향을 주지 않는지 확인하십시오.

**1. 보트 트래픽 테스트(최적화해야 함)**

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

라우팅이 활성화된 ![AI 트래픽 라우팅 상태](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

## 설정 확인 - BYOCDN {#verify-setup-byocdn}

**설정 확인**

설정을 완료한 후 보트 트래픽이 Edge 최적화로 라우팅되고 사람 트래픽에 영향을 주지 않는지 확인하십시오.

**1. 보트 트래픽 테스트(최적화해야 함)**

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

## API 키 검색 단계 {#retrieve-byocdn-api-key}

**API 키를 검색하는 단계:**

1. **고객 구성**(으)로 이동하고 **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. **최적화를 배포할 AI 트래픽 라우팅**&#x200B;에서 **AI 에이전트에 최적화 배포** 확인란을 선택하십시오.

   ![AI 에이전트에 최적화 적용](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. API 키를 복사하고 아래 라우팅 구성 단계를 진행합니다.

   ![API 키 복사](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >이 단계에서, 상태는 설정이 아직 완료되지 않았음을 나타내는 적색 십자가를 보여줄 수 있다. 예상된 결과입니다. 아래 라우팅 구성을 완료하고 AI 보트 트래픽이 흐르기 시작하면 상태가 라우팅이 성공적으로 활성화되었음을 확인하는 녹색 확인 표시로 업데이트됩니다.

또한 위의 단계에 대한 도움이 필요한 경우 Adobe 계정 팀이나 `llmo-at-edge@adobe.com`에 문의하십시오.

## 개요로 돌아가기 {#return-to-overview}

사용 가능한 기회, 자동 최적화 워크플로 및 FAQ를 포함하여 Edge에서 최적화에 대해 자세히 알아보려면 [Edge에서 최적화 개요](/help/dashboards/optimize-at-edge.md)로 돌아가십시오.
