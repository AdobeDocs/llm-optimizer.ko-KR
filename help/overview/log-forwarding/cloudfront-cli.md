---
title: 로그 전달 - CloudFront(AWS CLI)
description: Adobe CLI를 사용하여 CloudFront CDN 로그를 AWS의 S3 버킷으로 전달하여 게재 설정 및 작업을 수행합니다.
feature: Agentic Traffic
source-git-commit: 0d51bbde954c399dc6595522fa70b576461f458a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 20%

---


# 로그 전달: CloudFront (AWS CLI) {#log-forwarding-cloudfront-cli}

이 페이지에서는 에이전트 트래픽 데이터 수집을 위해 CloudFront에서 Adobe의 S3 버킷으로 CDN 로그를 전달하는 방법에 대해 자세히 설명합니다. LLM Optimizer CDN 구성 페이지를 사용하여 LLM Optimizer에 온보딩합니다. 온보딩 프로세스가 완료되면 이 페이지에 제공된 단계에 따라 [2{3단계}에서 [AWS 명령줄 인터페이스](https://aws.amazon.com/cli/)를 사용하여 로그 전달을 구성합니다.](#step-2-cli)

>[!NOTE]
>
> 이 안내서에서는 [AWS 명령줄 인터페이스](https://aws.amazon.com/cli/)를 사용하여 로그 전달을 구성하는 방법을 설명합니다. **CloudFront UI**&#x200B;를 사용하여 로그 전달을 구성하려면 [로그 전달: CloudFront](/help/overview/log-forwarding/cloudfront.md)을(를) 참조하십시오.

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

## 2단계: AWS CLI를 사용하여 CDN 로그 전달 설정 {#step-2-cli}

AWS CLI를 사용하여 CDN 로그 전달을 다음과 같이 설정합니다.

### AWS CLI 자격 증명 구성

AWS CLI 자격 증명 MAC을 설정합니다. ~/.aws/credentials를 열고 아래에 변수 값을 입력합니다.

```text
[LLMO]
aws_access_key_id=<VALUE_OF_ACCESS_KEY_ID>
aws_secret_access_key=<VALUE_OF_SECRET_KEY>
aws_session_token=<ONLY_IF_USING_SECURITY_TOKEN_SERVICE> ## Optional
```

### 연결 테스트

아래 명령을 실행하여 연결을 테스트합니다.

```bash
aws sts get-caller-identity --profile LLMO
```

성공적인 출력의 예:

```bash
aws sts get-caller-identity --profile LLMO
{
    "UserId": "AxxxxxxxxxxxP:user",
    "Account": "012345678912",
    "Arn": "arn:aws:sts::012345678912:assumed-role/klam-master-role-BatlY3dnPVinQLC/user"
}
```

### 변수 초기화

`REPLACEME123@AdobeOrg`을(를) 조직 Adobe IMS 조직 ID로 바꾸고 아래 명령을 실행하십시오. 이 명령의 출력 ID를 `TRANSFORM_IMS_ID`(으)로 참조합니다.

```bash
echo "REPLACEME123@AdobeOrg" | sed 's/@AdobeOrg$//' | tr '[:upper:]' '[:lower:]'
```

아래 지침에 따라 `CUSTOMER`, `CDN_ID`, `ACCT1` 및 `TRANSFORM_IMS_ID`의 값을 입력한 다음 터미널에서 명령을 실행하십시오.

```bash
export PROFILE1=LLMO
export REGION1=us-east-1
export CUSTOMER=<CUSTOMER_NAME> ## No Space, user letters,numbers and dash
export CDN_ID=<YOUR_CLOUDFRONT_DISTRIBUTION_ID>
export ACCT1=<YOUR_AWS_ACCOUNT_NUMBER>
export DELIVERY_DEST_ARN=arn:aws:logs:us-east-1:640168421876:delivery-destination:cdn-logs-<TRANSFORM_IMS_ID>-ams  ## Replace TRANSFORM_IMS_ID with the output of the command above 
```

<!--Use the **Delivery destination ARN** and org values from the LLM Optimizer CDN configuration page if they differ from the pattern above.-->

### 게재 소스 만들기

3단계가 실행된 동일한 터미널에서 아래 명령을 실행합니다.

```bash
aws logs put-delivery-source --name llmo-cf-${CUSTOMER}-${CDN_ID} \
  --profile $PROFILE1 --region $REGION1 \
  --resource-arn arn:aws:cloudfront::${ACCT1}:distribution/${CDN_ID} \
  --log-type ACCESS_LOGS
```

>[!IMPORTANT]
>
>다음 오류가 발생하면 기존 게재 원본을 검색합니다. *PutDeliverySource 작업을 호출할 때 오류가 발생했습니다(ConflictException). 이 ResourceId는 이 계정의 다른 게재 Source에서 이미 사용되었습니다.*
>
>기존 게재 소스를 검색하려면 이 명령을 실행합니다.
>
>```bash
>aws logs describe-delivery-sources --region us-east-1 \
>--query "deliverySources[?contains(resourceArns[0], '<CDN DistributionID>')]"
>```
>
>다음 명령에서는 위의 명령 결과에서 게재 소스 이름을 사용합니다.

### 게재 구성 만들기

```bash
aws logs create-delivery \
  --profile "$PROFILE1" --region "$REGION1" \
  --delivery-source-name "llmo-cf-${CUSTOMER}-${CDN_ID}" \
  --delivery-destination-arn $DELIVERY_DEST_ARN \
  --s3-delivery-configuration '{"suffixPath":"/{yyyy}/{MM}/{dd}/{HH}"}' \
  --record-fields 'date' 'time' 'x-edge-location' 'cs-method' 'cs(Host)' 'cs-uri-stem' 'sc-status' 'cs(Referer)' 'cs(User-Agent)' 'time-to-first-byte' 'sc-content-type' 'x-host-header'
```

&lt;!—설명서 또는 제품 값이 변경되는 경우 LLM Optimizer CDN 구성 페이지에 표시되는 필드 목록 및 경로 접미사에 `--record-fields` 및 `--s3-delivery-configuration`을 맞춥니다.—>
