---
title: 로그 전달 - CloudFront
description: LLM Optimizer의 에이전틱 트래픽 데이터 수집을 위해 CloudFront에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법에 대해 알아봅니다.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: ht
source-wordcount: '466'
ht-degree: 100%

---


# 로그 전달: CloudFront {#log-forwarding-cloudfront}

이 페이지에서는 에이전틱 트래픽 데이터 수집을 위해 CloudFront에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법을 설명합니다. LLM Optimizer CDN 구성 페이지를 사용하여 LLM Optimizer에 온보딩합니다. 온보딩 프로세스가 완료되면 이 페이지에 제공된 단계를 따라 CloudFront 대시보드 콘솔에서 로그 전달을 구성합니다.

## 1단계: LLM Optimizer에서 온보딩 {#step-1}

LLM Optimizer 페이지([https://llmo.now/](https://llmo.now/))로 이동합니다.

1. **고객 구성 대시보드**&#x200B;로 이동합니다.

   ![구성 버튼](/help/overview/assets/log-forwarding/common/config-button.png)

1. **CDN 구성** 탭을 클릭합니다.

   ![CDN 구성 탭](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. **시작하기**&#x200B;를 클릭합니다.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. **AI 트래픽 인사이트 활성화** 옆의 **구성**&#x200B;을 클릭합니다.

   ![구성](/help/overview/assets/log-forwarding/common/configure.png)

1. **AWS 계정** ID를 입력합니다.

   ![AWS 계정 ID](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

1. **CloudFront(BYOCDN)**&#x200B;를 선택합니다.

   ![CloudFront 선택](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. **온보딩**&#x200B;을 클릭합니다.

   ![온보딩 버튼](/help/overview/assets/log-forwarding/common/onboard-button.png)

## 2단계: 표준 로깅 활성화(CloudFront 콘솔) {#step-2}

표준 로깅을 활성화하려면 [AWS 관리 콘솔](https://aws.amazon.com/console/)에서 다음을 수행합니다.

1. [CloudFront 콘솔](https://console.aws.amazon.com/cloudfront/v4/home)에 액세스하고 [기존 배포를 업데이트](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure)합니다.

1. **로깅** 탭을 엽니다.

1. **추가**&#x200B;를 선택한 다음 로그를 수신할 서비스를 선택합니다(이 경우 **Amazon S3**).

1. **대상**&#x200B;에 대해 리소스를 선택하거나 만듭니다. **버킷 이름**&#x200B;을 입력합니다. LLM Optimizer CDN 구성 페이지에서 값을 복사할 수 있습니다.

   ![CloudFront 버킷 이름](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

1. **추가 설정**&#x200B;을 구성합니다.

   - **필드 선택** — 로그 파일 필드를 선택합니다. LLM Optimizer CDN 구성 페이지의 필수 필드를 참조하십시오.

     ![CloudFront 필드 선택](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **파티셔닝** — LLM Optimizer 구성 페이지에서 **경로 접미사**&#x200B;를 복사합니다.

     ![CloudFront 파티셔닝](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **출력 형식** — 형식은 JSON이어야 합니다.

     ![CloudFront 출력 형식](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

1. 배포를 업데이트하거나 만드는 단계를 완료합니다.

1. **로그** 페이지에서 배포 옆에 **활성화됨**&#x200B;이 표시되는지 확인합니다.

## 계정 간 게재를 위한 표준 로깅 활성화 {#cross-account}

**소스 계정**(CloudFront 배포 포함)이 **대상 계정**(LLM Optimizer CDN 구성 페이지에 표시된 S3 버킷)으로 액세스 로그를 보냅니다. 두 계정 모두에 올바른 권한이 있어야 합니다.

예를 들어 소스 계정 `111111111111`이 대상 계정 `222222222222`의 S3 버킷으로 로그를 보냅니다. [AWS 명령줄 인터페이스](https://aws.amazon.com/cli/)를 사용할 수 있습니다.

>[!NOTE]
>
>아래 명령에서 게재 대상 ARN 값(`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`)을 LLM Optimizer 구성 페이지의 **게재 대상 ARN** 값으로 바꿉니다.

![게재 대상 ARN](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

### 소스 계정 구성 {#source-account}

다음으로 소스 계정을 구성해야 합니다.

1. **게재 소스 만들기** - 이름 및 배포 ARN을 바꿉니다.

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

1. **게재 만들기** - 소스를 대상에 연결합니다. “대상 계정 구성” 단계에서 대상 ARN을 사용합니다.

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

1. **증명:**

   - **소스** 계정: CloudFront 콘솔 > 배포 > **로깅** 탭으로 이동합니다. **유형**&#x200B;에서 S3 계정 간 로그 게재가 표시됩니다.
   - **대상** 계정: S3 콘솔 > 버킷으로 이동합니다. 해당 폴더의 접두사(예: `MyLogPrefix`)와 로그가 표시됩니다.
