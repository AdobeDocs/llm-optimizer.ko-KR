---
title: Optimize at Edge - AEM Cloud Service Managed CDN(Fastly)
description: LLM Optimizer에서 Optimize at Edge를 위해 AEM Cloud Service Managed CDN(Fastly)을 구성하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 184d6008c2579014c6ff453e8bfff4bb898f4b82
workflow-type: ht
source-wordcount: '836'
ht-degree: 100%

---


# AEM Cloud Service Managed CDN(Fastly)

이 구성은 에이전틱 트래픽(AI 봇 및 LLM 사용자 에이전트의 요청)을 Edge Optimize 백엔드 서비스(`live.edgeoptimize.net`)로 라우팅합니다. 사람 방문자와 SEO 봇은 기존과 동일하게 사용자의 원본 서버에서 계속 제공됩니다. 구성을 테스트하려면 설정이 완료된 후 응답에서 헤더 `x-edgeoptimize-request-id`를 확인합니다.

## 사전 요구 사항

이 기능에 액세스하려면:

- 유료 고객은 **Adobe LLM Optimizer 사용자** IMS 제품 프로필에 액세스할 수 있어야 합니다. 액세스 권한을 요청하려면 조직의 관리자에게 문의하십시오.
  ![제품 프로필에 사용자 추가](/help/assets/optimize-at-edge/cs-fastly-user-product-profiles.png)
- 체험판 고객은 **LLMO 관리자** IMS 그룹의 속해 있어야 합니다. 그룹이 존재하지 않는 경우 조직의 관리자가 그룹을 만들고 사용자를 추가할 수 있습니다.
  ![LLMO 관리자 IMS 그룹 만들기](/help/assets/optimize-at-edge/cs-fastly-create-ims-group.png)

>[!NOTE]
> 이 기능은 Safari 또는 시크릿/비공개 탐색 모드에서는 지원되지 않습니다.

## 라우팅 활성화 단계

에이전틱 트래픽을 Edge Optimize로 라우팅하려면 다음을 수행합니다.

1. LLM Optimizer에서 **고객 구성**&#x200B;을 열고  **CDN 구성** 탭을 선택합니다.

   ![고객 구성으로 이동](/help/assets/optimize-at-edge/cs-fastly-prereq-customer-config-nav.png)

2. **AI 에이전트에 최적화 배포** 섹션을 찾습니다. **활성화** 버튼을 클릭합니다.

   ![AI 에이전트에 최적화 배포 — 보류 중](/help/assets/optimize-at-edge/cs-fastly-enable-button.png)

3. 확인 대화 상자에서 **활성화**&#x200B;를 선택하여 라우팅을 활성화하도록 설정합니다. 오류가 나타나면 [문제 해결](#troubleshooting) 섹션을 참조하여 문제를 해결하십시오.

   ![최적화 엔진 확인 대화 상자 활성화](/help/assets/optimize-at-edge/cs-fastly-enable-dialog.png)

4. 확인 후 라우팅을 완료하는 데 몇 분 정도 소요됩니다.

   ![라우팅 진행 중](/help/assets/optimize-at-edge/cs-fastly-enable-button-clicked-routing-in-progress.png)

   5분 후 페이지를 다시 로드하여 라우팅이 완료되었는지 확인합니다. 라우팅이 구성되고 활성화되면 상태가 **완료됨**&#x200B;으로 업데이트되고 녹색 체크 표시가 표시되어 라우팅이 활성화되었음을 알려 줍니다. 추가적인 액션은 필요하지 않습니다.

   ![AI 에이전트에 최적화 배포 — 완료됨](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

   언제든지 라우팅을 비활성화하려면 **CDN 구성** 탭의 **AI 에이전트에 최적화 배포** 섹션으로 돌아가서 **비활성화**&#x200B;를 클릭합니다.

또한 위 단계에 대한 도움이 필요한 경우 Adobe 계정 팀 또는 `llmo-at-edge@adobe.com`에 문의하십시오.

## 문제 해결

라우팅을 활성화하거나 비활성화하는 동안 발생한 오류는 다음과 유사합니다.

![확인 대화 상자 오류](/help/assets/optimize-at-edge/cs-fastly-confirmation-dialog-error.png)

아래 목록을 사용하여 오류를 식별하고 지침을 따르십시오.

1. **사용자에게 LLMO 제품 액세스 권한 없음**

   **원인:** 사용자 계정에 Adobe IMS 프로필의 LLM Optimizer 제품 컨텍스트가 없습니다. 유료 고객이 CDN 라우팅을 구성하는 데 필요합니다.

   **추천:** 조직 관리자가 Adobe Admin Console에서 **Adobe LLM Optimizer 사용자** 제품 프로필을 할당했는지 확인하십시오.

2. **LLMO 관리자 그룹 구성원만 CDN 라우팅을 구성할 수 있음**

   **원인:** 계정이 **LLMO 관리자** IMS 그룹의 구성원이 아닙니다. 체험판 고객이 CDN 라우팅을 구성하는 데 필요합니다.

   **추천:** 조직 관리자가 Adobe Admin Console의 **LLMO 관리자** IMS 그룹에 추가되었는지 확인하십시오.

3. **요청한 CDN 유형 aem-cs-fastly가 이 도메인에 대해 감지된 CDN과 일치하지 않음**

   **원인:** 사이트에 대해 감지된 CDN 유형이 *AEM Cloud Service Managed CDN(Fastly)*&#x200B;이 아님을 나타냅니다.

   **추천:** 사이트가 AEM Cloud Service Managed CDN(Fastly)을 통해 제공되는지 확인하십시오.

4. **사이트 검색 중 오류**

   **원인:** 라우팅 설정 중에 LLM Optimizer에서 사이트에 연결할 수 없습니다. 이 문제는 사이트가 다운되었거나, 연결할 수 없거나, 요청 시간이 초과된 경우 발생할 수 있습니다.

   **추천:** 사이트에 공개적으로 액세스할 수 있고 올바른 응답을 반환하는지 확인한 후 다시 시도하십시오.

5. **사이트에서 라우팅 프로브에 대한 올바른 응답을 반환하지 않음**

   **원인:** 설정 시 조사할 때 사이트에서 예기치 않은 HTTP 상태(2xx 또는 301이 아님)를 반환했습니다.

   **추천:** 사이트에서 LLM Optimizer에 등록된 기본 URL에 대한 성공적인 응답(2xx)을 반환하고 있는지 확인한 후 다시 시도하십시오.

6. **업스트림 IMS 서비스에서 인증 실패**

   **원인:** 세션이 만료되었거나 라우팅 요청 중에 Adobe IMS로 인증하는 데 문제가 있을 수 있습니다.

   **추천:** LLM Optimizer에서 로그아웃했다가 다시 로그인한 다음 라우팅을 다시 활성화해 보십시오.

문제가 지속되면 Adobe 계정 팀이나 `llmo-at-edge@adobe.com`에 문의하십시오.

## (선택 사항) 설정 확인

라우팅 구성이 완료된 후, 선택적으로 AI 봇 트래픽이 Edge Optimize로 라우팅되고 있으며 사람 트래픽이 영향을 받지 않는지 확인할 수 있습니다.

1. **봇 트래픽 테스트(최적화해야 함)**

   에이전틱 사용자 에이전트를 사용하여 AI 봇 요청을 시뮬레이션합니다.

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: chatgpt-user"
   ```

   성공적인 응답에는 요청이 Edge Optimize를 통해 라우팅되었음을 확인하는 `x-edgeoptimize-request-id` 헤더가 포함됩니다.

   ```
   < HTTP/2 200
   < x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
   ```

2. **사람 트래픽 테스트(영향을 받지 않아야 함)**

   일반 사람 브라우저 요청을 시뮬레이션합니다.

   ```
   curl -svo /dev/null https://www.example.com/page.html \
     --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
   ```

   응답에는 `x-edgeoptimize-request-id` 헤더가 없어야 합니다. 페이지 콘텐츠와 응답 시간은 Optimize at Edge를 활성화하기 전과 동일하게 유지되어야 합니다.

3. **두 시나리오를 구분하는 방법**

   | 헤더 | 봇 트래픽(최적화됨) | 사람 트래픽(영향을 받지 않음) |
   |---|---|---|
   | `x-edgeoptimize-request-id` | 있음 — 고유한 요청 ID가 포함되어 있습니다. | 없음 |
   | `x-edgeoptimize-fo` | 장애 조치가 발생한 경우에만 표시됩니다(값: `1`). | 없음 |

4. **LLM Optimizer에서 라우팅 상태 확인**

   LLM Optimizer UI에서 라우팅을 확인할 수도 있습니다. **고객 구성**&#x200B;을 열고 **CDN 구성** 탭을 선택합니다. 라우팅이 활성화된 경우 **AI 에이전트에 최적화 배포** 섹션에 **완료됨**&#x200B;이 표시됩니다.

   ![AI 에이전트에 최적화 배포 — 완료됨](/help/assets/optimize-at-edge/cs-fastly-disable-button.png)

{{return-to-overview}}
