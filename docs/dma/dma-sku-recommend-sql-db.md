---
title: (Data Migration Assistant) 온-프레미스 데이터베이스에 대 한 올바른 Azure SQL 데이터베이스 SKU 확인 | Microsoft Docs
description: 온-프레미스 데이터베이스에 대 한 Azure SQL 데이터베이스 SKU 오른쪽을 확인 하려면 Data Migration Assistant를 사용 하는 방법 알아보기
ms.custom: ''
ms.date: 05/06/2019
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
ms.author: jtoland
ms.openlocfilehash: 7d87df240d4b83e53ef8f670609d2c896df7fe62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054676"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>온-프레미스 데이터베이스에 대 한 오른쪽 Azure SQL Database/관리 인스턴스 SKU를 식별 합니다.

클라우드로 데이터베이스 마이그레이션 데이터베이스에 대 한 최상의 Azure database 대상 및 SKU를 선택 하려고 할 때 특히 복잡할 수 있습니다. 목표 데이터베이스 마이그레이션 길잡이 (DMA)를 사용 하 여 데이터베이스 마이그레이션 환경을 사용자에 게 친숙 출력에서 다음 SKU 권장 사항을 제공 하 여 보다 편리 하 고 이러한 질문을 해결을 돕는 것입니다.

이 문서는 DMA의 Azure SQL 데이터베이스 SKU 권장 사항은 기능에 중점을 둡니다. Azure SQL Database에 여러 배포 옵션을 포함 합니다.

- 단일 데이터베이스
- 탄력적 풀
- 관리 되는 인스턴스

관리 되는 인스턴스에 데이터베이스를 호스팅하는 컴퓨터에서 수집 된 성능 카운터를 기반으로 한 SKU를 SKU 권장 기능을 사용 하면 모두 최소 권장 Azure SQL Database 단일 데이터베이스를 식별할 수 있습니다. 기능 관련 된 월별 예상된 비용 뿐만 아니라 계층, 계산 수준 및 최대 데이터 크기, 가격 책정 권장 사항을 제공 합니다. 또한 대량 프로 비전에 대 한 단일 데이터베이스 및 모든 권장 되는 데이터베이스에 대해 Azure에서 관리 되는 인스턴스 수를 제공합니다.

> [!NOTE]
> 이 기능은 현재 사용할 수만 통해 명령줄 인터페이스 (CLI)입니다.

Azure SQL 데이터베이스 SKU 권장 사항을 확인 하 고 해당 단일 데이터베이스 또는 DMA를 사용 하 여 Azure에서 관리 되는 인스턴스를 프로 비전 할 수 있도록 하는 지침은 다음과 같습니다.

## <a name="prerequisites"></a>사전 요구 사항

- 최신 버전 다운로드 및 설치 [DMA](https://aka.ms/get-dma)합니다. 이전 버전의 도구를 이미 있는 경우 연 DMA를 업그레이드 하 라는 메시지가 나타납니다.
- 컴퓨터에 있는지 확인 하십시오 [PowerShell 버전 5.1](https://www.microsoft.com/download/details.aspx?id=54616) 모든 스크립트를 실행 하는 데 필요한 나중 또는 합니다. PowerShell 버전을 컴퓨터에 설치 되어 findoug에 대 한 자세한 문서를 참조 [다운로드 하 여 Windows PowerShell 5.1 설치](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1)합니다.
- 컴퓨터에 Azure Powershell 모듈이 설치 되어 있는지 확인 합니다. 자세한 내용은 문서 참조 [Azure PowerShell 모듈을 설치](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0)합니다.
- 확인 하는 PowerShell 파일 **SkuRecommendationDataCollectionScript.ps1**, DMA 폴더에 설치 되는 성능 카운터를 수집 하는 데 필요한 합니다.
- 이 프로세스를 수행 하는 컴퓨터에 데이터베이스를 호스팅하는 컴퓨터에 관리자 권한이 있는지 확인 합니다.

## <a name="collect-performance-counters"></a>성능 카운터를 수집 합니다.

프로세스의 첫 번째 단계는 데이터베이스에 대 한 성능 카운터를 수집 하는 것입니다. 데이터베이스를 호스트 하는 컴퓨터에서 PowerShell 명령을 실행 하 여 성능 카운터를 수집할 수 있습니다. DMA이 PowerShell 파일의 복사본을 제공 하지만 컴퓨터에서 성능 카운터를 캡처하려면 사용자 고유의 메서드를 사용할 수도 있습니다.

개별적으로 각 데이터베이스에 대해이 작업을 수행할 필요가 없습니다. 컴퓨터에서 호스트 되는 모든 데이터베이스에 대 한 SKU를 권장 하는 컴퓨터에서 수집 된 성능 카운터를 사용할 수 있습니다.

1. DMA 폴더에서 SkuRecommendationDataCollectionScript.ps1 PowerShell 파일을 찾습니다. 이 파일은 성능 카운터를 수집 해야 합니다.

    ![DMA 폴더에 표시 된 PowerShell 파일](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 다음 인수를 사용 하 여 PowerShell 스크립트를 실행 합니다.
    - **ComputerName**: 데이터베이스를 호스트 하는 컴퓨터의 이름입니다.
    - **OutputFilePath**: 수집 된 카운터를 저장 하려면 출력 파일 경로입니다.
    - **CollectionTimeInSeconds**: 성능 카운터 데이터를 수집 하려는 동안 시간의 양입니다. 의미 있는 권장 사항을 가져오려면 40 분 이상에 대 한 성능 카운터를 캡처하십시오. 캡처를 오래 동안 더 정확 하 게 권장이 됩니다. 또한 보다 정확한 권장 사항을 사용 하도록 원하는 데이터베이스에 대 한 워크 로드를 실행 중인지 확인 합니다.
    - **DbConnectionString**: 성능 카운터 데이터를 수집 하는 컴퓨터의 호스트 된 master 데이터베이스를 가리키는 연결 문자열입니다.

    샘플 호출은 다음과 같습니다.

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    명령 실행 후 프로세스는 지정한 위치에 대 한 성능 카운터를 포함 한 파일을 출력 합니다. 단일 데이터베이스와 관리 되는 인스턴스 옵션에 대 한 SKU 권장 사항을 제공 하는 프로세스의 다음 부분에 대 한 입력으로이 파일을 사용할 수 있습니다.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>DMA CLI를 사용 하 여 SKU 권장 사항 가져오기

이 프로세스에 대 한 입력으로 만든 성능 카운터 출력 파일을 사용 합니다.

단일 데이터베이스 옵션의 경우 DMA는 가격 책정 계층, 계산 수준 및 각 데이터베이스에 대 한 최대 데이터 크기를 컴퓨터에 Azure SQL Database 단일 데이터베이스에 대 한 권장 사항을 제공 합니다. 여러 데이터베이스 컴퓨터에 있는 경우에 권장 하려는 데이터베이스를 지정할 수 있습니다. DMA는 또한 제공 월별 예상된 비용을 사용 하 여 각 데이터베이스에 대 한 합니다.

관리 되는 인스턴스에 대 한 권장 리프트 앤 시프트 시나리오를 지원 합니다. 결과적으로, DMA 가격 책정 계층, 계산 수준 및 데이터베이스 집합에 대 한 최대 데이터 크기를 컴퓨터에 Azure SQL Database 관리 되는 인스턴스에 대 한 권장 사항을 제공 합니다. 다시 컴퓨터에 여러 데이터베이스가 있는 경우 권장 사항을 사용 하도록 하려는 데이터베이스도 지정할 수 있습니다. DMA는 또한 제공 월별 예상된 비용을 사용 하 여 관리 되는 인스턴스에 대 한 합니다.

명령 프롬프트에서 SKU 권장 사항을 가져오려면 DMA CLI를 사용 하려면 다음 인수를 사용 하 여 dmacmd.exe를 실행 합니다.

- **/Action=SkuRecommendation**: SKU 평가 실행 하려면이 인수를 입력 합니다.
- **/SkuRecommendationInputDataFilePath**: 이전 섹션에서 수집 된 카운터 파일 경로입니다.
- **/SkuRecommendationTsvOutputResultsFilePath**: TSV 형식으로 결과 출력을 쓸 경로입니다.
- **/SkuRecommendationJsonOutputResultsFilePath**: JSON 형식으로 결과 출력을 쓸 경로입니다.
- **/SkuRecommendationHtmlResultsFilePath**: HTML 형식으로 결과 출력을 쓸 경로입니다.

또한 다음 인수 중 하나를 선택 합니다.

- 가격 새로 고침을 방지
  - **/SkuRecommendationPreventPriceRefresh**: 경우 True로 설정 하 고 가격 새로 고침이 발생 하는 것을 금지 기본 가격을 가정 합니다. 오프 라인 모드에서 실행 하는 경우 사용 합니다. 이 매개 변수를 사용 하지 않는 경우 지정된 된 지역에 따라 최신 가격을 보려면 아래 매개 변수를 지정 해야 합니다.
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
        - **AzureAuthenticationCertificateStoreLocation**: 인증서 저장소 위치 (예: "CurrentUser")로 설정 합니다.
        - **AzureAuthenticationCertificateThumbprint**: 인증서 지 문으로 설정 합니다.
      - 토큰 기반
        - **AzureAuthenticationToken**: 인증서 토큰을 설정 합니다.

> [!NOTE]
> 대화형 인증에 대 한 ClientId 및 TenantId를 가져오려면, 새 AAD 응용 프로그램을 구성 해야 합니다. 인증 및 문서에 이러한 자격 증명을 가져오기에 대 한 자세한 내용은 [Microsoft Azure 청구 API 코드 샘플: RateCard API](https://azure.microsoft.com/resources/samples/billing-python-ratecard-api/), 아래 지침에 따라 **1 단계: AAD 테 넌 트에 네이티브 클라이언트 응용 프로그램 구성**합니다.

마지막으로 권장 사항을 사용 하도록 하려는 데이터베이스를 지정 하 여 선택적 인수: 

- **/SkuRecommendationDatabasesToRecommend**: 목록 권장 사항을 제공 하는 데이터베이스입니다. 데이터베이스 이름은 대/소문자 구분 되며 (1) 해야 합니다. 입력된.csv에, 이중 따옴표로 묶을 수 (2) 각 및 (3)로 구분 이름 간에 단일 공백 (예: /SkuRecommendationDatabasesToRecommend "Database1" = "Database2" "Database3") . 입력된.csv 파일에 나오는 모든 사용자 데이터베이스에 대 한 권장 사항을 제공 되는 확인이 매개 변수를 생략 합니다.  

일부 샘플 호출은 다음과 같습니다.

**샘플 1: 기본 가격 권장 사항을 가져오는 중입니다. 오프 라인 모드에서 실행 하는 경우 또는 인증 자격 증명이 없는 경우 사용 합니다.**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**샘플 2: 지정된 된 영역 (예: "UKWest")에 대 한 최신 가격 권장 사항을 가져오는 중입니다.**

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

**샘플 3: 특정 데이터베이스에 대 한 권장 사항 (예: 가져오기 “TPCDS1G,EDW_3G,TPCDS10G”).**

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
/SkuRecommendationDatabasesToRecommend=“TPCDS1G” “EDW_3G” “TPCDS10G” 
/AzureAuthenticationInteractiveAuthentication=true 
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId> 
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
```

단일 데이터베이스 권장 사항에 대 한 TSV 출력 파일을 다음과 같이 표시 됩니다.

![DMA 폴더에 표시 된 PowerShell 단일 db 파일](../dma/media/dma-sku-recommend-single-db-recommendations.png)

관리 되는 인스턴스 권장 사항에 대 한 TSV 출력 파일을 다음과 같이 표시 됩니다.

![DMA 폴더에 표시 된 PowerShell 관리 되는 인스턴스 파일](../dma/media/dma-sku-recommend-mi-recommendations.png)

출력 파일의 각 열에 대 한 설명을 따릅니다.

- **DatabaseName** -데이터베이스의 이름입니다.
- **MetricType** -계층 인스턴스 권장 되는 Azure SQL Database 단일 데이터베이스/관리 합니다.
- **MetricValue** -SKU 인스턴스 권장 되는 Azure SQL Database 단일 데이터베이스/관리 합니다.
- **PricePerMonth** – 해당 SKU에 대 한 월별 예상된 가격입니다.
- **RegionName** – 해당 SKU에 대 한 지역 이름입니다. 
- **IsTierRecommended** -각 계층에 대 한 최소 SKU 권장 사항을 확인 합니다. 그런 다음 데이터베이스에 대 한 적합 한 계층을 결정 하는 추론 적용 합니다. 이 계층은 데이터베이스에 대 한 권장 반영 합니다. 
- **ExclusionReasons** -이 값은 계층에 권장 되는 경우 비어 있습니다. 권장 되지 않습니다는 각 계층에 대 한 선택 되지 않은 이유는 이유 제공 합니다.
- **AppliedRules** -적용 된 규칙의 약식 표기 합니다.

최종 권장된 계층 (즉, **MetricType**) 및 값 (즉, **MetricValue**)-여기서 찾을 수는 **IsTierRecommended** 최소 SKU를 반영 열이 TRUE- 온-프레미스 데이터베이스 비슷합니다 성공률을 사용 하 여 Azure에서 실행할 쿼리에 대 한 필요 합니다. 관리 되는 인스턴스에 대 한 현재 DMA 40vcore Sku에 자주 사용 하는 8vcore에 대 한 권장 사항에는 지원합니다. 예를 들어, 최소 권장 되는 SKU는 표준 계층 S4 경우 S3을 선택 하 고 아래 됩니다 쿼리 제한 시간 초과로 인해 또는 실행 되지 않습니다.

HTML 파일을 그래픽 형식으로이 정보를 포함 합니다. 최종 권장 구성 보기 및 프로세스의 다음 부분을 프로 비전의 친숙 한 방법을 제공 합니다. HTML 출력에 대 한 자세한 내용은 다음 섹션에 있는 경우

## <a name="provision-recommended-skus-to-azure"></a>Azure Sku를 권장 하는 프로 비전

몇 번의 클릭으로 프로 비전 대상 데이터베이스를 마이그레이션할 수 있는 Azure의 Sku에 식별 된 권장 사항을 사용할 수 있습니다. HTML 파일을 사용 하 여 Azure 구독;를 입력 합니다. 가격 책정 계층 선택, 수준 및 데이터베이스;에 대 한 최대 데이터 크기를 계산 합니다. 및 데이터베이스를 프로 비전 하는 스크립트를 생성 합니다. PowerShell을 사용 하 여이 스크립트를 실행할 수 있습니다.

단일 컴퓨터에서이 프로세스를 수행할 수 있습니다 또는 대규모 SKU 권장 사항을 확인 하려면 여러 컴퓨터에서 수행할 수 있습니다. DMA 현재 있도록 간단 하며 확장성 있는 환경을 명령줄 인터페이스를 통해 전체 프로세스를 지원 합니다.

에 프로 비전 정보를 입력 하 고 권장 사항에 대 한 변경, HTML 파일을 다음과 같이 업데이트 합니다.

**단일 데이터베이스 권장 사항에 대 한**

![Azure SQL DB SKU 권장 사항 화면](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. HTML 파일을 열고 다음 정보를 입력 합니다.
    - **구독 ID** -데이터베이스를 프로 비전 하려는 Azure 구독의 구독 ID입니다.
    - **리소스 그룹** -데이터베이스를 배포 하려는 리소스 그룹입니다. 존재 하는 리소스 그룹을 입력 합니다.
    - **지역** -데이터베이스를 프로 비전 하는 지역입니다. 구독 선택 영역을 지원 하는지 확인 합니다.
    - **서버 이름** -Azure SQL Database 서버는 배포 데이터베이스입니다. 존재 하지 않는 서버 이름을 입력 하면 만들어집니다.
    - **관리자 사용자 이름** -서버 관리자 사용자 이름입니다.
    - **관리자 암호** -서버 관리자 암호입니다. 암호는 8 자 이상이 고 길이 128 자 여야 합니다. 암호에는 다음 범주 중 세 개 문자가 있어야 합니다.-영어 대문자, 영어 소문자, 숫자 (0-9) 문자와 영숫자가 아닌 문자 (!, $, #, %, 등.). 암호를 사용할 수 없습니다 또는 사용자 이름에서 파트 (3 + 연속 문자).

2. 각 데이터베이스에 대 한 권장 사항을 검토 하 고 가격 책정 계층을 수정, 수준 및 필요에 따라 최대 데이터 크기를 계산 합니다. 현재 원하지 않는 프로 비전 된 모든 데이터베이스를 선택 취소 해야 합니다.

3. 선택 **프로 비전 스크립트 생성**, 스크립트를 저장 하 고 다음 PowerShell에서 실행 합니다.

    이 프로세스는 HTML 페이지에서 선택한 모든 데이터베이스를 만들어야 합니다.

**관리 되는 인스턴스 권장 사항에 대 한**

![Azure SQL MI SKU 권장 사항 화면](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. HTML 파일을 열고 다음 정보를 입력 합니다.
    - **구독 ID** -데이터베이스를 프로 비전 하려는 Azure 구독의 구독 ID입니다.
    - **리소스 그룹** -데이터베이스를 배포 하려는 리소스 그룹입니다. 존재 하는 리소스 그룹을 입력 합니다.
    - **지역** -데이터베이스를 프로 비전 하는 지역입니다. 구독 선택 영역을 지원 하는지 확인 합니다.
    - **인스턴스 이름을** – 인스턴스의 Azure SQL 관리 되는 인스턴스에 데이터베이스를 마이그레이션하려 합니다. 인스턴스 이름은 소문자, 숫자를 포함할 수 있습니다 및 '-'를 시작 하거나 끝날 수 없습니다 있지만 '-' 63 자입니다.
    - **관리자 사용자 이름 인스턴스** – 인스턴스 관리자 사용자 이름입니다. SQL 식별자를 및 없습니다 (예: 관리자, 관리자, sa, 루트, dbmanager, loginmanager 등), 일반적인 시스템 이름 또는 기본 제공 데이터베이스 사용자 또는 역할 (예: dbo, guest, public 등)-사용자의 로그인 이름에는 다음 요구 사항을 충족 하는지 확인 합니다. 사용자 이름에 공백, 유니코드 문자 또는 알파벳이 아닌 문자, 포함 되어 있지 않습니다 및 숫자나 기호를 사용 하 여 시작 되지 않습니다는 있는지 확인 합니다. 
    - **관리자 암호를 인스턴스** -인스턴스 관리자 암호입니다. 암호 길이 128 자 및 16 자 이상 이어야 합니다. 암호에는 다음 범주 중 세 개 문자가 있어야 합니다.-영어 대문자, 영어 소문자, 숫자 (0-9) 문자와 영숫자가 아닌 문자 (!, $, #, %, 등.). 암호를 사용할 수 없습니다 또는 사용자 이름에서 파트 (3 + 연속 문자).
    - **Vnet 이름** -VNet 이름은 관리 되는 인스턴스를 프로 비전 되어야 합니다. 기존 VNet 이름을 입력 합니다.
    - **서브넷 이름** -서브넷 이름은 관리 되는 인스턴스를 프로 비전 되어야 합니다. 기존 서브넷 이름을 입력 합니다.

2. 각 인스턴스에 대 한 권장 사항을 검토 하 고 가격 책정 계층을 수정, 수준 및 필요에 따라 최대 데이터 크기를 계산 합니다. 권장 사항을 현재 제한 40vcore sku 8vcore 중일 경우 여전히 원하는 경우 64vcore 및 80vcore Sku를 프로 비전 하는 옵션 현재 원하지 않는 프로 비전 하는 모든 인스턴스를 선택 취소 해야 합니다.

    이 프로세스는 HTML 페이지에서 선택한 모든 데이터베이스를 만들어야 합니다.

    > [!NOTE]
    > (특히 첫 번째 시간)에 대해 관리 되는 인스턴스 서브넷에 만들기를 완료 하는 데 몇 시간이 걸릴 수 있습니다. PowerShell을 통해 프로 비전 스크립트를 실행 한 후 Azure Portal에서 배포의 상태를 확인할 수 있습니다.

## <a name="next-step"></a>다음 단계

- CLI에서 DMA를 실행 하는 것에 대 한 명령의 전체 목록은, 문서를 참조 [실행 Data Migration Assistant 명령줄에서](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)합니다.
