---
title: (Data Migration Assistant) 온-프레미스 데이터베이스에 대 한 올바른 Azure SQL 데이터베이스 SKU 확인 | Microsoft Docs
description: 온-프레미스 데이터베이스에 대 한 Azure SQL 데이터베이스 SKU 오른쪽을 확인 하려면 Data Migration Assistant를 사용 하는 방법 알아보기
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 578e6ac47e84ad764cb050112eae768ff21444f3
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973829"
---
# <a name="identify-the-right-azure-sql-database-sku-for-your-on-premises-database"></a>온-프레미스 데이터베이스에 대 한 올바른 Azure SQL 데이터베이스 SKU 확인

클라우드로 데이터베이스를 마이그레이션하는 작업을 복잡 하 고 시간 소모적이 고 관련 된 다양 한 변수가 됩니다. 데이터베이스에 대 한 올바른 Azure 데이터베이스 대상 및 SKU를 선택 하는 것은 어려울 수 있습니다. 데이터베이스 마이그레이션 길잡이 (DMA)를 사용 하 여 이러한 목표는 이러한 질문을 해결 하려면 간단 하 고 효과적인 데이터베이스 마이그레이션 환경을 확인 합니다.

이 문서에서는 데이터베이스를 호스팅하는 컴퓨터에서 수집 된 성능 카운터에 따라 Azure SQL 데이터베이스 SKU를 권장 되는 최소를 식별할 수 있도록 DMA의 Azure SQL 데이터베이스 SKU 권장 사항 기능을에 주로 중점을 둡니다. 이 기능은 월별 예상된 비용 뿐만 아니라 계층, 계산 수준 및 최대 데이터 크기, 가격 책정에 관련 된 권장 사항을 제공 합니다. 또한 대량에서 Azure에 모든 데이터베이스를 프로 비전 하는 기능을 제공 합니다.

> [!NOTE] 
> 이 기능은 현재 사용할 수만 통해 명령줄 인터페이스 (CLI)입니다. DMA 사용자 인터페이스를 통해이 기능에 대 한 지원이 향후 릴리스에서 추가 됩니다.

다음 지침을 통해 Azure SQL 데이터베이스 SKU 권장 사항을 확인 하 고 Data Migration Assistant를 사용 하 여 azure에 연결된 된 데이터베이스를 프로 비전 합니다.

## <a name="prerequisites"></a>사전 요구 사항

Database Migration Assistant v4.0 다운로드 이상을 설치 합니다. 이미 있는 경우이 도구를 닫고 설치를 닫은 다음 다시 및 도구를 업그레이드 하 라는 메시지가 나타납니다.

## <a name="collect-performance-counters"></a>성능 카운터를 수집 합니다.

프로세스의 첫 번째 단계는 데이터베이스에 대 한 성능 카운터를 수집 하는 것입니다. 데이터베이스를 호스트 하는 컴퓨터에서 PowerShell 명령을 실행 하 여 성능 카운터를 수집할 수 있습니다. DMA이 PowerShell 파일의 복사본을 제공 하지만 컴퓨터에서 성능 카운터를 캡처하려면 사용자 고유의 메서드를 사용할 수도 있습니다.

개별적으로 각 데이터베이스에 대해이 작업을 수행할 필요가 없습니다. 컴퓨터에서 호스트 되는 모든 데이터베이스에 대 한 SKU를 권장 하는 컴퓨터에서 수집 된 성능 카운터를 사용할 수 있습니다.

> [!IMPORTANT]
> 이 명령은 실행 하는 컴퓨터에는 데이터베이스를 호스팅하는 컴퓨터에 관리자 권한이 필요 합니다.

1. 성능 카운터를 수집 하는 데 필요한 PowerShell 파일 DMA 폴더에 설치 되어 있는지 확인 합니다.

    ![DMA 폴더에 표시 된 PowerShell 파일](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 다음 인수를 사용 하 여 PowerShell 스크립트를 실행 합니다.
    - **ComputerName**: 데이터베이스를 호스트 하는 컴퓨터의 이름입니다.
    - **OutputFilePath**: 수집 된 카운터를 저장 하려면 출력 파일 경로입니다.
    - **CollectionTimeInSeconds**: 성능 카운터 데이터를 수집 하려는 동안 시간의 양입니다.
      의미 있는 권장 사항을 가져오려면 40 분 이상에 대 한 성능 카운터를 캡처하십시오. 캡처를 오래 동안 더 정확 하 게 권장이 됩니다.
    - **DbConnectionString**: 성능 카운터 데이터를 수집 하는 컴퓨터의 호스트 된 master 데이터베이스를 가리키는 연결 문자열입니다.
     
    샘플 호출은 다음과 같습니다.

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```
    
    명령 실행 후 프로세스는 지정한 위치에서 성능 카운터를 사용 하 여 파일을 출력 합니다. 이 파일은 다음 섹션에서 SKU 권장 명령에 대 한 입력으로 사용할 수 있습니다.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>DMA CLI를 사용 하 여 SKU 권장 사항 가져오기

이 단계에 대 한 입력으로 이전 단계에서 성능 카운터 출력 파일을 사용 합니다. DMA 하면와 Azure SQL Database에 대 한 권장 가격 책정 계층, 계산 수준 및 각 데이터베이스에 대 한 최대 데이터 크기를 컴퓨터에 있습니다. DMA는 또한 제공 월별 예상된 비용을 사용 하 여 각 데이터베이스에 대 한 합니다.

다음 인수를 사용 하 여는 dmacmd.exe를 실행 합니다.

- **/Action=SkuRecommendation**: SKU 평가 실행 하려면이 인수를 입력 합니다.
- **/SkuRecommendationInputDataFilePath**: 이전 섹션에서 수집 된 카운터 파일 경로입니다.
- **/SkuRecommendationTsvOutputResultsFilePath**: TSV 형식으로 결과 출력을 쓸 경로입니다.
- **/SkuRecommendationJsonOutputResultsFilePath**: JSON 형식으로 결과 출력을 쓸 경로입니다.
- **/SkuRecommendationHtmlResultsFilePath**: HTML 형식으로 결과 출력을 쓸 경로입니다.

또한 다음 인수 중 하나를 선택 해야 합니다.
- 가격 새로 고침을 방지
    - **/SkuRecommendationPreventPriceRefresh**: 발생 가격 새로 고침을 방지합니다. 오프 라인 모드에서 실행 하는 경우 사용 합니다.
- 최신 가격 가져오기 
    - **/SkuRecommendationCurrencyCode**: (예: 가격을 표시 하는 통화 "USD")입니다.
    - **/SkuRecommendationOfferName**: 제품 이름 (예: "MS-AZR-0003P"). 자세한 내용은 참조는 [Microsoft Azure 제품 세부 정보](https://azure.microsoft.com/support/legal/offer-details/) 페이지입니다.
    - **/SkuRecommendationRegionName**: 지역 이름 (예: "미국 서 부")입니다.
    - **/SkuRecommendationSubscriptionId**: 구독 ID입니다.
    - **/AzureAuthenticationTenantId**: Authentication 테 넌 트가 있습니다.
    - **/AzureAuthenticationClientId**: 인증에 사용 되는 AAD 앱의 클라이언트 ID입니다.
    - 다음 인증 옵션 중 하나입니다.
        - 대화형
            - **AzureAuthenticationInteractiveAuthentication**: 인증 팝업 창에 대 한 true로 설정 합니다.
        - 인증서 기반
            - **AzureAuthenticationCertificateStoreLocation**: (예: 인증서 저장소 위치를 설정 "CurrentUser")입니다.
            - **AzureAuthenticationCertificateThumbprint**: 인증서 지 문으로 설정 합니다.
        - 토큰 기반
            - **AzureAuthenticationToken**: 인증서 토큰을 설정 합니다.

일부 샘플 호출은 다음과 같습니다.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationInteractiveAuthentication=true
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

TSV 출력 파일에는 다음 그림에 표시 된 열 포함 됩니다.

   ![DMA 폴더에 표시 된 PowerShell 파일](../dma/media/dma-tsv-file-column.png)

각 열에 대 한 설명을 따릅니다.

- **DatabaseName** -데이터베이스의 이름입니다.
- **MetricName** -메트릭을 실행 된 여부.
- **MetricType** -Azure SQL Database 권장 계층입니다.
- **MetricValue** -Azure SQL Database SKU를 권장 합니다.
- **SQLMiEquivalentCores** -Azure SQL Database Managed Instance에 대 한 이동 하려는 경우 코어 수에 대 한이 값을 사용할 수 있습니다.
- **IsTierRecommended** -각 계층에 대 한 최소 SKU 권장 사항을 확인 합니다. 그런 다음 데이터베이스에 대 한 적합 한 계층을 결정 하는 추론 적용 합니다. 
- **ExclusionReasons** -이 값은 계층에 권장 되는 경우 비어 있습니다. 권장 되지 않습니다는 각 계층에 대 한 선택 되지 않은 이유는 이유 제공 합니다.
- **AppliedRules** -적용 된 규칙의 약식 표기 합니다.

권장된 값은 온-프레미스 데이터베이스 비슷합니다 성공률을 사용 하 여 Azure에서 실행 하 여 쿼리 하는 데 필요한 최소 SKU입니다. 예를 들어, 최소 권장 되는 SKU는 표준 계층 S4 경우 S3을 선택 하 고 아래 됩니다 쿼리 제한 시간 초과로 인해 또는 실행 되지 않습니다.

HTML 파일을 그래픽 형식으로이 정보를 포함 합니다. Azure 구독 정보를 입력, 가격 책정 계층 선택, 데이터베이스에 대 한 수준 및 최대 데이터 크기를 계산 및 데이터베이스를 프로 비전 하는 스크립트를 생성 하는 HTML 파일을 사용할 수 있습니다. PowerShell을 사용 하 여이 스크립트를 실행할 수 있습니다.

## <a name="provision-your-databases-to-azure"></a>Azure에 데이터베이스를 프로 비전
몇 번의 클릭으로 데이터베이스를 마이그레이션할 수 있는 Azure에서 프로 비전 대상 데이터베이스에 이전 단계에서 권장 사항을 사용할 수 있습니다. 작업도 가능 변경 권장 사항에 다음과 같은 HTML 파일을 업데이트 하 여 합니다.

1. HTML 파일을 열고 다음 정보를 입력 합니다.
    - **구독 ID** -데이터베이스를 프로 비전 하려는 Azure 구독의 구독 ID입니다.
    - **지역** -데이터베이스를 프로 비전 하는 지역입니다. 구독 선택 영역을 지원 하는지 확인 합니다.
    - **리소스 그룹** -데이터베이스를 배포 하려는 리소스 그룹입니다. 존재 하는 리소스 그룹을 입력 합니다.
    - **서버 이름** -Azure SQL Database 서버는 배포 데이터베이스입니다. 존재 하지 않는 서버 이름을 입력 하면 만들어집니다.
    - **관리자 사용자 이름 \ 암호** -서버 관리자 사용자 이름 및 암호입니다.

2. 각 데이터베이스에 대 한 권장 사항을 검토 하 고 가격 책정 계층을 수정, 수준 및 필요에 따라 최대 데이터 크기를 계산 합니다. 현재 원하지 않는 프로 비전 된 모든 데이터베이스를 선택 취소 해야 합니다.

3. 선택 **프로 비전 스크립트 생성**, 스크립트를 저장 하 고 다음 PowerShell에서 실행 합니다.

    이 프로세스는 HTML 페이지에서 선택한 모든 데이터베이스를 만들어야 합니다.

이 프로세스는 단일 컴퓨터에서 모든 단계를 수행할 수 또는 대규모 SKU 권장 사항을 확인 하려면 여러 컴퓨터에서 수행할 수 있습니다. DMA는 명령줄 인터페이스를 통해 이러한 모든 단계를 지원 하 여 간단 하며 확장성 있는 환경이 있습니다. 마찬가지로 DMA 사용자 인터페이스를 통해이 기능에 대 한 지원이이 올해 후반 제공 됩니다.

## <a name="next-steps"></a>다음 단계
- 최신 버전을 다운로드 [Data Migration Assistant](https://aka.ms/get-dma)합니다.
- 문서를 참조 하세요 [실행 Data Migration Assistant 명령줄에서](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017) CLI에서 DMA를 실행 하는 것에 대 한 명령의 전체 목록은 합니다.
