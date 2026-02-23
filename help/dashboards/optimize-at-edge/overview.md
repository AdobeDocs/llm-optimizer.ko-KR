---
title: Optimize at Edge
description: CDN 에지에서 작성 변경 없이 LLM Optimizer로 최적화를 제공하는 방법에 대해 알아봅니다.
feature: Opportunities
source-git-commit: 547c38986da609a6cd42cb94402c811d6eb1f939
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 84%

---


# Optimize at Edge

이 페이지는 작성 변경 없이 CDN 에지에서 최적화를 제공하는 방법에 대한 자세한 개요를 제공합니다. 온보딩 프로세스, 사용 가능한 최적화 기회 및 에지에서 자동 최적화하는 방법을 다룹니다.

>[!NOTE]
>이 기능은 현재 얼리 액세스 상태입니다. 얼리 액세스 프로그램에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/ko/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs)에서 확인할 수 있습니다.

## Optimize at Edge란 무엇입니까?

Optimize at Edge는 LLM Optimizer의 에지 기반 배포 기능으로, LLM 사용자 에이전트에게 AI 친화적인 변경 사항을 제공합니다. 현재 컨텍스트에서 “Edge”는 최적화가 CDN 계층에서 적용됨을 의미합니다. CDN 계층에서 최적화를 제공하기 때문에 콘텐츠 관리 시스템(CMS)에서 작성 변경이 필요하지 않으므로 원본 CMS는 변경되지 않습니다. 이러한 분리를 통해 기존 게시 워크플로를 변경하지 않고 LLM 가시성을 향상시킬 수 있습니다. 에이전틱 트래픽만을 대상으로 하며, 사용자나 SEO 봇에는 영향을 미치지 않습니다. LLM Optimizer가 페이지 최적화 기회를 감지하면 사용자는 CDN 에지에 직접 수정 사항을 배포할 수 있습니다.

Optimize at Edge는 복잡한 엔지니어링 노력이 필요한 기존 수정 사항에 대한 더 빠르고 효율적인 대안입니다. 앞서 언급했듯이, 한 번의 설정을 완료하면 변경 사항을 적용하기 위해 플랫폼 변경이나 긴 개발 주기가 필요하지 않습니다. 개발자의 참여 없이 몇 분 만에 향상된 사항을 게시할 수 있습니다. AI 에이전트용으로 웹 사이트를 최적화하는 비코드 방법입니다.

Optimize at Edge는 마케팅, SEO, 콘텐츠 및 디지털 전략 팀의 비즈니스 사용자를 위해 설계되었습니다. 비즈니스 사용자는 기회 식별, 제안 이해, 수정 사항 간편 배포 등 LLM Optimizer의 전체 여정을 완료할 수 있습니다. Optimize at Edge를 사용하면 사용자는 변경 사항을 미리 보고 CDN 에지에 빠르게 배포하여 최적화가 실행 중인지 확인할 수 있습니다. 성능은 LLM Optimizer 생태계에서 추적할 수 있습니다.

### 주요 이점

* **AI 전용 게재:** AI 에이전트에게만 최적화된 HTML을 제공하며, 방문자나 SEO 봇에게 아무런 영향을 미치지 않습니다.
* **더 빠른 주기:** 변경 사항을 몇 주가 아닌 몇 분 안에 게시합니다. 플랫폼 변경이나 긴 엔지니어링 주기가 필요하지 않습니다.
* **복원 가능:** 몇 분 만에 페이지를 되돌릴 수 있는 원클릭 롤백 기능이 지원됩니다.
* **성능에 영향을 주지 않음:** Edge 기반 최적화 및 캐싱은 사이트 지연 시간에 영향을 주지 않습니다.
* **CDN 및 CMS 독립적:** 콘텐츠 관리 시스템에 관계없이 모든 CDN 구성 및 프론트엔드 설정에서 작동합니다.

### Optimize at Edge에서 어떤 기회가 지원됩니까?

에이전틱 웹 경험을 향상시킬 수 있는 기회는 Optimize at Edge를 통해 지원됩니다. [기회 대시보드](/help/dashboards/opportunities.md) 페이지와 현재 페이지의 기회 섹션에서 각 기회에 대해 자세히 알아봅니다.

## 온보딩

온보딩 프로세스를 시작하려면 Adobe 계정 팀 또는 FDE 팀에 문의해야 합니다. IT 또는 CDN 팀도 사전 요구 사항과 설정 프로세스를 완료해야 합니다. 또한 `llmo-at-edge@adobe.com`에 문의하여 추가 온보딩 지원을 받을 수도 있습니다.

Optimize at Edge에 온보딩하기 위한 전제 조건:

* LLM Optimizer에 대한 온보딩 프로세스를 완료합니다.
* CDN 로그에 대한 로그 전달 프로세스를 완료합니다.

IT/CDN 팀에 대한 요구 사항:
* 허용 목록에 추가하다 사이트의 txt 파일 또는 봇 트래픽 관리 규칙에 `*AdobeEdgeOptimize/1.0*` 사용자 에이전트를 robots에 추가합니다.
* 페이지가 도메인 또는 CDN 수준에서 차단되지 않았는지 확인합니다.
* CDN에서 Optimize at Edge 라우팅 규칙에 추가합니다.
* LLM Optimizer 인터페이스에서 Optimize at Edge 라우팅을 확인합니다.

설정 프로세스를 안내하려면 아래에서 CDN 공급자를 선택하고 해당 구성 안내서를 따르십시오. 이러한 예제는 실제 라이브 구성에 맞게 조정되어야 합니다. 먼저 저사양 환경에서 변경 사항을 적용하는 것을 권장합니다.

### CDN 구성 가이드

| CDN 공급자 | 유형 | 안내서 |
|---|---|---|
| AEM Cloud Service 관리 CDN(Fastly) | Adobe 관리 | [설치 가이드 보기](/help/dashboards/optimize-at-edge/aemcs-managed-cdn.md) |
| Fastly (BYOCDN) | 자체 CDN 가져오기 | [설치 가이드 보기](/help/dashboards/optimize-at-edge/fastly-byocdn.md) |
| Akamai(BYOCDN) | 자체 CDN 가져오기 | [설치 가이드 보기](/help/dashboards/optimize-at-edge/akamai-byocdn.md) |
| Cloudflare(BYOCDN) | 자체 CDN 가져오기 | [설치 가이드 보기](/help/dashboards/optimize-at-edge/cloudflare-byocdn.md) |
| CloudFront(BYOCDN) | 자체 CDN 가져오기 | [설치 가이드 보기](/help/dashboards/optimize-at-edge/cloudfront-byocdn.md) |

>[!NOTE]
>CDN 공급자가 위에 나열되어 있지 않거나 LLM Optimizer UI에서 도메인 또는 이메일을 찾을 수 없는 경우 `llmo-at-edge@adobe.com`에 연락하여 온보딩 지원을 받으십시오. 설정 구성이 완료되면 LLM Optimizer에서 Optimize at Edge 기회에 대한 제안을 배포할 수 있습니다.

위의 각 CDN 설정 안내서에는 에이전트 트래픽이 올바르게 라우팅되고 있으며 인간 트래픽에 영향을 주지 않는지 확인하는 자세한 확인 단계가 포함되어 있습니다.

## 기회

다음 테이블에는 에이전틱 웹 경험을 개선할 수 있는 기회가 제시되어 있으며, Optimize at Edge에서 지원됩니다.

| 기회 | 유형 | 자동 식별 | 자동 제안 | 자동 최적화 |
|---------|----------|----------|----------|----------|
| 콘텐츠 가시성 복구 | 기술 GEO | AI 에이전트에서 중요한 콘텐츠가 숨겨져 있는 페이지를 감지합니다. 영향을 받는 URL 및 복구할 수 있는 예상 콘텐츠를 표시합니다. | AI 에이전트가 사용할 수 있는 콘텐츠를 강조하고 해당 페이지에 대한 사전 렌더링을 활성화할 것을 권장합니다. | 완전히 렌더링된 AI 친화적인 HTML 스냅샷을 에이전틱 트래픽에 제공하여 이전에 숨겨져 있던 콘텐츠를 복구합니다. |
| LLM 친화 요약 추가 | 콘텐츠 최적화 | 페이지나 섹션 수준에서 간결한 요약이 어려운 길거나 복잡한 페이지를 식별하여 AI가 빠르게 스캔하고 이해하기 어렵게 만듭니다. | 페이지 및 섹션 수준에서 주요 콘텐츠가 담긴 짧은 AI 생성 요약을 권장합니다. | 요약을 관련 HTML 섹션에 삽입하여 모델이 페이지 내용을 해석하고 설명하는 방식을 개선합니다. |
| 관련 FAQ 추가 | 콘텐츠 최적화 | FAQ의 혜택을 받을 수 있는 기존 페이지 콘텐츠의 의도 차이를 감지합니다. | 사용자 의도와 기존 주제에 맞춘 AI 생성 FAQ 콘텐츠를 제안합니다. | HTML에 FAQ 콘텐츠를 삽입하여 AI 기반 응답에서 페이지를 더 쉽게 발견하고 연관시킬 수 있습니다. |
| 복잡한 콘텐츠 간소화 | 콘텐츠 최적화 | AI 이해를 방해할 수 있는 복잡한 텍스트로 페이지에 플래그를 지정합니다. | AI가 생성한 복잡한 텍스트의 단순화된 버전을 제공하면서 원래의 의미를 유지합니다. | 페이지의 복잡한 섹션을 다시 작성하여 AI 가독성을 향상시킵니다. |

### 추가 도구

[Adobe LLM Optimizer: 웹 페이지가 인용 가능합니까?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome 확장 기능은 LLM이 액세스할 수 있는 웹 페이지 콘텐츠의 양과 숨겨진 항목을 보여 줍니다. 무료 독립형 진단 도구로 설계되었으며, 제품 라이선스나 설정이 필요하지 않습니다.

한 번의 클릭으로 모든 사이트의 시스템 가독성을 평가할 수 있습니다. AI 에이전트가 보는 내용과 사용자가 보는 내용을 나란히 비교하고 LLM Optimizer을 사용하여 복구할 수 있는 콘텐츠의 양을 예측할 수 있습니다. 자세한 내용은 [AI가 웹 사이트를 읽을 수 있습니까?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) 페이지를 참조하십시오.

## 기회 세부 정보

다음 섹션에서는 Optimize at Edge에서 지원되는 각 기회에 대한 추가 세부 정보를 확인할 수 있습니다.

### 콘텐츠 가시성 복구

이 기회는 클라이언트측 렌더링으로 인해 AI 에이전트용 주요 콘텐츠가 숨겨져 있는 페이지를 표시합니다. 식별된 각 페이지마다 AI 에이전트 보기에서 누락된 콘텐츠가 정확히 표시되고, 가시성 격차를 강조 표시하며, 숨겨진 콘텐츠를 복구하기 위해 변경 사항을 직접 적용할 수 있습니다. 이 기회를 Optimize at Edge와 함께 배포하면 사전 렌더링된 AI 최적화 버전의 페이지가 LLM 사용자 에이전트에게 제공되므로 Javascript를 실행하지 않고도 전체 컨텍스트에 액세스할 수 있습니다.
이렇게 하면 AI 에이전트가 페이지를 먼저 완전히 볼 수 있습니다. 사전 렌더링된 HTML 위에 추가 개선 사항이 적용됩니다.

>[!IMPORTANT]
>이 사전 렌더링 기능은 Optimize at Edge와 함께 배포하면 아래에 제시된 모든 기회에 자동으로 적용되어 AI 에이전트가 페이지를 완전히 볼 수 있도록 합니다.

### LLM 친화 요약 추가

이 기회는 간결한 요약을 통해 혜택을 받을 수 있는 페이지를 식별하여 LLM이 페이지 내용을 빠르게 이해할 수 있습니다. 각 페이지마다 기회는 요약이 가장 필요한 위치를 감지하고 페이지 수준 또는 섹션 수준에서 AI 생성 요약을 생성합니다. Optimize at Edge를 사용하여 배포하면 이러한 요약이 AI 에이전트가 검색하는 HTML에 삽입되어 콘텐츠가 보다 정확하게 설명될 가능성이 높아집니다.

### 관련 FAQ 추가

이 기회는 추가 Q&amp;A 콘텐츠가 사용자 의도와 AI 기반 검색의 프롬프트에 더 잘 부합할 수 있는 페이지에 플래그를 지정합니다. 각 페이지마다 사용자 의도 및 페이지의 콘텐츠와 연계된 AI 생성 FAQ 블록을 제안합니다. Optimize at Edge를 사용하면 이러한 FAQ가 HTML에 삽입되어 페이지에 AI 친화적이며, AI 응답이 직접적으로 지침을 반영할 가능성이 높아집니다.

### 복잡한 콘텐츠 간소화

이 기회는 AI 이해를 줄일 수 있는 길고 복잡한 단락이 있는 페이지를 찾습니다. 가독성 임계값을 초과하는 각 페이지마다 원래 의미를 유지하면서 더 간단하고 스캔하기 쉬운 AI 생성 콘텐츠를 생성합니다. 에지에 배포되면 에이전틱 트래픽에 전달되는 간소화된 콘텐츠는 LLM이 콘텐츠를 보다 충실하게 해석하고 요약할 수 있습니다.

## 자동 Optimize at Edge

각 기회마다 에지에서 최적화를 미리 보고, 편집하고, 배포하고, 라이브를 보고, 롤백할 수 있습니다.

>[!VIDEO](https://video.tv.adobe.com/v/3477991/?captions=kor&learn=on&enablevpops)

### 미리보기

**미리보기**&#x200B;를 사용하면 제안이 실행되기 전에 그 영향을 확인할 수 있습니다. 제안을 적용한 후 예상되는 현재 페이지와 AI 최적화 버전 간의 병렬 차이가 나타납니다. 이 보기는 라이브 트래픽을 향상시키는 Edge에서 동일한 최적화 로직을 사용하지만 독립적인 미리보기 모드에서 작동합니다. 이는 검토를 위한 읽기 전용 시뮬레이션이기 때문에 라이브 트래픽에는 영향을 미치지 않습니다.

![미리보기](/help/assets/optimize-at-edge/preview.png)

### 편집

**편집**&#x200B;을 사용하면 자동 생성된 제안을 배포하기 전에 완전히 수정하거나 다시 작성할 수 있습니다. 제안을 수락하는 대신 편집 워크플로를 통해 완전히 제어합니다. 이 보기는 구조화된 편집기에서 제안된 변경 사항을 표시하여 원래 의도와 더 잘 일치하도록 텍스트를 수정할 수 있습니다. 편집된 버전은 배포된 후 AI 에이전트에게 제공됩니다.

![편집](/help/assets/optimize-at-edge/edit.png)

### 배포

**배포**&#x200B;는 선택된 제안을 게시하여 에지에서 최적화된 경험을 AI 에이전트에게 제공할 수 있도록 합니다. CDN이 완전히 라우팅되면 도메인의 모든 페이지는 일반적으로 몇 분 안에 새로운 변경 사항과 함께 활성화됩니다. 라우팅이 선택된 경로에만 설정된 경우, 허용 목록에 추가된 페이지만 최적화와 함께 활성화됩니다.

![배포](/help/assets/optimize-at-edge/deploy.png)

### 라이브 보기

**라이브 보기**&#x200B;를 통해 최적화가 에이전틱 트래픽에 대해 예상대로 작동하는지 확인할 수 있으며, 그렇지 않으면 액세스하기 어려운 보기입니다. AI 에이전트에 표시된 대로 페이지를 렌더링하는 고정 제안 아래에서 라이브 페이지를 볼 수 있습니다.

![라이브 보기](/help/assets/optimize-at-edge/view-live.png)

### 롤백

롤백은 이전에 배포된 최적화를 안전하게 되돌립니다. AI 전용 버전의 페이지는 일반적으로 몇 분 안에 이전 상태로 돌아가므로 필요할 때 최적화 실험을 안전하게 할 수 있습니다.

![롤백](/help/assets/optimize-at-edge/rollback.png)

## 자주 묻는 질문

질문. Optimize at Edge는 어떤 종류의 LLM을 목표로 합니까?

타기팅할 사용자 에이전트 목록은 온보딩 프로세스 중에 사용자가 정의합니다.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

질문. 아직 Optimize at Edge에 온보딩되지 않았으면 어떻게 됩니까?

필요한 설정을 완료하기 전에 **최적화 배포**&#x200B;를 클릭하면 사이트에 아무것도 적용되지 않습니다. 대신 팝업 대화 상자가 나타나 `llmo-at-edge@adobe.com`의 팀에 문의하여 온보딩 지원을 받으라는 메시지가 표시됩니다. 온보딩이 완료될 때까지 감지된 기회와 제안을 계속 탐색할 수 있지만 원클릭 배포 워크플로는 비활성 상태로 유지됩니다.

질문: 콘텐츠가 소스에서 업데이트되면 어떻게 됩니까?

기본 소스 페이지가 변경되지 않는 한 캐시에서 최적화된 페이지 버전을 제공합니다. 그러나 소스가 **콘텐츠 가시성 복구**&#x200B;에 대해 변경되면 시스템이 자동으로 새로 고침되므로 AI 에이전트는 항상 최신 콘텐츠를 수신합니다. 이는 낮은 캐시 TTL(Time to Live) 설정(분 단위)을 사용하여 사이트의 모든 콘텐츠 업데이트가 해당 창 내에서 새로운 최적화를 트리거하기 때문입니다. **LLM 친화적 요약 추가**&#x200B;와 같은 콘텐츠 기회에 대해 LLM Optimizer은 소스 페이지에서 변경 사항을 모니터링합니다. 변경 사항이 감지되면 최적화를 일시 중지하고 사람이 검토할 수 있도록 플래그를 지정하여 에이전트가 표시하는 페이지와 사람이 표시하는 페이지 사이의 콘텐츠 드리프트를 방지합니다.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

질문. Optimize at Edge는 Adobe Edge Delivery Service(EDS)를 사용하는 사이트에만 적용됩니까?

아니요. Optimize at Edge는 CDN에 구애받지 않으며 Adobe의 EDS Stack에 배포된 아키텍처뿐만 아니라 모든 프론트엔드 아키텍처에서 작동합니다.

질문. Optimize at Edge 사전 렌더링 기존 서버측 렌더링(SSR)과 어떻게 다릅니까?

둘 다 서로 다른 문제를 해결하고 함께 일할 수 있습니다. 기존 SSR은 서버측 콘텐츠를 렌더링하지만 나중에 브라우저에 로드된 콘텐츠는 포함하지 않습니다. Optimize at Edge 사전 렌더링은 JavaScript와 클라이언트측 데이터가 로드된 후 페이지를 캡처하여 CDN 에지에서 완전히 조립된 버전을 생성합니다. SSR은 사용자 경험을 개선하는 데 중점을 두고 있으며, Optimize at Edge는 LLM의 웹 경험을 개선합니다.

Q. 모든 URL이 아닌 일부 URL에 대해 최적화를 배포할 경우 어떻게 됩니까?

명시적으로 최적화하는 URL만 수정됩니다. 기회가 배포된 URL의 경우 AI 에이전트는 최적화된 버전을 받습니다. 배포된 기회가 없는 URL의 경우, 당사 서비스는 변경 사항을 적용하거나 최적화 캐시 레이어에 저장하지 않고 원본 페이지를 그대로 프록시합니다. 이렇게 하면 사이트의 나머지 부분에 영향을 주지 않고 최적화를 선택적으로 배포할 수 있습니다.
