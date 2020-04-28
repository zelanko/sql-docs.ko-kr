---
title: 온-프레미스 데이터베이스에 적합 한 Azure SQL Database SKU 식별 (Data Migration Assistant) | Microsoft Docs
description: Data Migration Assistant를 사용 하 여 온-프레미스 데이터베이스에 적합 한 Azure SQL Database SKU를 식별 하는 방법을 알아봅니다.
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
ms.openlocfilehash: d6d329b97946d9d8042641653ed0167510a19b17
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72586732"
---
# <a name="identify-the-right-azure-sql-databasemanaged-instance-sku-for-your-on-premises-database"></a>온-프레미스 데이터베이스에 적합 한 Azure SQL Database/Managed Instance SKU 식별

데이터베이스를 클라우드로 마이그레이션하는 것은 특히 데이터베이스에 가장 적합 한 Azure 데이터베이스 대상과 SKU를 선택 하려고 할 때 복잡할 수 있습니다. DMA (데이터베이스 Migration Assistant)의 목표는 이러한 질문을 해결 하 고 사용자에 게 친숙 한 출력으로 이러한 SKU 권장 사항을 제공 하 여 데이터베이스 마이그레이션 환경을 더 쉽게 만드는 것입니다.

이 문서에서는 DMA의 Azure SQL Database SKU 권장 사항 기능에 대해 집중적으로 설명 합니다. Azure SQL Database에는 다음과 같은 몇 가지 배포 옵션이 있습니다.

- 단일 데이터베이스
- 탄력적 풀
- 관리되는 인스턴스

SKU 권장 사항 기능을 사용 하면 데이터베이스를 호스트 하는 컴퓨터에서 수집 된 성능 카운터를 기반으로 하는 최소 권장 Azure SQL Database 단일 데이터베이스 또는 관리 되는 인스턴스 SKU를 모두 식별할 수 있습니다. 이 기능은 가격 책정 계층, 계산 수준 및 최대 데이터 크기와 관련 된 권장 사항과 월별 예상 비용을 제공 합니다. 또한 모든 권장 데이터베이스에 대해 Azure에서 단일 데이터베이스 및 관리 되는 인스턴스를 대량 프로 비전 하는 기능을 제공 합니다.

> [!NOTE]
> 이 기능은 현재 CLI (명령줄 인터페이스)를 통해서만 사용할 수 있습니다.

다음은 Azure SQL Database SKU 권장 사항을 확인 하 고 DMA를 사용 하 여 Azure에서 해당 하는 단일 데이터베이스 또는 관리 되는 인스턴스를 프로 비전 하는 데 도움이 되는 지침입니다.

## <a name="prerequisites"></a>사전 요구 사항

- 최신 버전의 [DMA](https://aka.ms/get-dma)를 다운로드 하 여 설치 합니다. 이전 버전의 도구가 이미 있는 경우이를 열면 DMA를 업그레이드할지 묻는 메시지가 표시 됩니다.
- 모든 스크립트를 실행 하는 데 필요한 [PowerShell 버전 5.1](https://www.microsoft.com/download/details.aspx?id=54616) 이상이 컴퓨터에 있는지 확인 합니다. 컴퓨터에 설치 된 PowerShell 버전을 findoug 하는 방법에 대 한 자세한 내용은 [Windows powershell 5.1 다운로드 및 설치](https://docs.microsoft.com/skypeforbusiness/set-up-your-computer-for-windows-powershell/download-and-install-windows-powershell-5-1)문서를 참조 하세요.
- 컴퓨터에 Azure Powershell 모듈이 설치 되어 있는지 확인 합니다. 자세한 내용은 [Azure PowerShell 모듈 설치](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.8.0)문서를 참조 하세요.
- 성능 카운터를 수집 하는 데 필요한 PowerShell 파일 **SkuRecommendationDataCollectionScript**이 DMA 폴더에 설치 되어 있는지 확인 합니다.
- 이 프로세스를 수행할 컴퓨터에 데이터베이스를 호스트 하는 컴퓨터에 대 한 관리자 권한이 있는지 확인 합니다.

## <a name="collect-performance-counters"></a>성능 카운터를 수집 합니다.

이 프로세스의 첫 번째 단계는 데이터베이스에 대 한 성능 카운터를 수집 하는 것입니다. 데이터베이스를 호스트 하는 컴퓨터에서 PowerShell 명령을 실행 하 여 성능 카운터를 수집할 수 있습니다. DMA는이 PowerShell 파일의 복사본을 제공 하지만 사용자 고유의 메서드를 사용 하 여 컴퓨터에서 성능 카운터를 캡처할 수도 있습니다.

각 데이터베이스에 대해 개별적으로이 작업을 수행할 필요는 없습니다. 컴퓨터에서 수집 된 성능 카운터를 사용 하 여 컴퓨터에서 호스트 되는 모든 데이터베이스에 대 한 SKU를 권장할 수 있습니다.

1. DMA 폴더에서 PowerShell 파일 SkuRecommendationDataCollectionScript. p s 1을 찾습니다. 이 파일은 성능 카운터를 수집 하는 데 필요 합니다.

    ![DMA 폴더에 표시 되는 PowerShell 파일](../dma/media/dma-sku-recommend-data-collection-file.png)

2. 다음 인수를 사용 하 여 PowerShell 스크립트를 실행 합니다.
    - **ComputerName**: 데이터베이스를 호스트 하는 컴퓨터의 이름입니다.
    - **Outputfilepath**: 수집 된 카운터를 저장할 출력 파일 경로입니다.
    - **CollectionTimeInSeconds**: 성능 카운터 데이터를 수집 하려는 시간입니다. 의미 있는 권장 사항을 얻으려면 최소 40 분 동안 성능 카운터를 캡처 하세요. 캡처 기간이 길수록 권장 구성이 더 정확해 집니다. 또한 원하는 데이터베이스에 대 한 워크 로드가 실행 되 고 있는지 확인 하 여 더 정확한 권장 사항을 사용 하도록 합니다.
    - **Dbconnectionstring**: 성능 카운터 데이터를 수집 하는 컴퓨터에서 호스트 되는 마스터 데이터베이스를 가리키는 연결 문자열입니다.

    샘플 호출은 다음과 같습니다.

    ```
    .\SkuRecommendationDataCollectionScript.ps1
     -ComputerName Foobar1
     -OutputFilePath D:\counters2.csv
     -CollectionTimeInSeconds 2400
     -DbConnectionString "Server=localhost;Initial Catalog=master;Integrated Security=SSPI;"
    ```

    명령이 실행 되 면 프로세스에서 성능 카운터를 포함 하는 파일을 지정한 위치에 출력 합니다. 이 파일을 프로세스의 다음 부분에 대 한 입력으로 사용할 수 있으며,이는 단일 데이터베이스 및 관리 되는 인스턴스 옵션에 대 한 SKU 권장 사항을 제공 합니다.

## <a name="use-the-dma-cli-to-get-sku-recommendations"></a>DMA CLI를 사용 하 여 SKU 권장 사항 가져오기

이 프로세스에 대 한 입력으로 만든 성능 카운터 출력 파일을 사용 합니다.

단일 데이터베이스 옵션의 경우 DMA는 컴퓨터의 각 데이터베이스에 대 한 단일 데이터베이스 가격 책정 계층, 계산 수준 및 최대 데이터 크기 Azure SQL Database에 대 한 권장 사항을 제공 합니다. 컴퓨터에 데이터베이스가 여러 개 있는 경우 권장 구성에 사용할 데이터베이스를 지정할 수도 있습니다. 또한 DMA는 각 데이터베이스에 대해 예상 되는 월별 비용을 제공 합니다.

관리 되는 인스턴스의 경우 권장 사항은 리프트 앤 시프트 시나리오를 지원 합니다. 따라서 DMA는 컴퓨터의 데이터베이스 집합에 대 한 Azure SQL Database 관리 되는 인스턴스 가격 책정 계층, 계산 수준 및 최대 데이터 크기에 대 한 권장 사항을 제공 합니다. 컴퓨터에 데이터베이스가 여러 개 있는 경우 권장 구성을 원하는 데이터베이스를 지정할 수도 있습니다. 또한 DMA는 관리 되는 인스턴스에 대 한 월별 예상 비용을 제공 합니다.

DMA CLI를 사용 하 여 SKU 권장 사항을 가져오려면 명령 프롬프트에서 다음 인수를 사용 하 여 dmacmd .exe를 실행 합니다.

- **/Action = U권고안**: SKU 평가를 실행 하려면이 인수를 입력 합니다.
- **/SkuRecommendationInputDataFilePath**: 이전 섹션에서 수집 된 카운터 파일의 경로입니다.
- **/SkuRecommendationTsvOutputResultsFilePath**: 출력 결과를 쓸 경로는 TSV 형식입니다.
- **/SkuRecommendationJsonOutputResultsFilePath**: 출력 결과를 쓸 경로는 JSON 형식입니다.
- **/SkuRecommendationHtmlResultsFilePath**: 출력 결과를 HTML 형식으로 쓸 경로입니다.

또한 다음 인수 중 하나를 선택 합니다.

- 가격 새로 고침 방지
  - **/SkuRecommendationPreventPriceRefresh**: True로 설정 되 면 가격 새로 고침이 발생 하지 않도록 하 고 기본 가격을 가정 합니다. 오프 라인 모드에서 실행 하는 경우를 사용 합니다. 이 매개 변수를 사용 하지 않는 경우 지정 된 지역에 따라 최신 가격을 가져오려면 아래 매개 변수를 지정 해야 합니다.
- 최신 가격 얻기
  - **/SkuRecommendationCurrencyCode**: 가격 (예: "USD")을 표시 하는 통화입니다.
  - **/SkuRecommendationOfferName**: 제품 이름 (예: "Ms-azr-0017p-0003P"). 자세한 내용은 [Microsoft Azure 제품 세부 정보](https://azure.microsoft.com/support/legal/offer-details/) 페이지를 참조 하세요.
    - **/SkuRecommendationRegionName**: 영역 이름 (예: "WestUS").
    - **/SkuRecommendationSubscriptionId**: 구독 ID입니다.
    - **/Azureauthenticationtenantid**: 인증 테 넌 트입니다.
    - **/Azureauthenticationclientid**: 인증에 사용 되는 AAD 앱의 클라이언트 ID입니다.
    - 다음 인증 옵션 중 하나입니다.
      - Interactive (대화형)
        - **AzureAuthenticationInteractiveAuthentication**: 인증 팝업 창에 대해 true로 설정 합니다.
      - 인증서 기반
        - **AzureAuthenticationCertificateStoreLocation**: 인증서 저장소 위치 (예: "CurrentUser")로 설정 합니다.
        - **Azureauthenticationcertificatethumbprint**: 인증서 지 문으로 설정 합니다.
      - 토큰 기반
        - **Azureauthenticationtoken**: 인증서 토큰으로 설정 합니다.

> [!NOTE]
> 대화형 인증용 ClientId 및 TenantId를 가져오려면 새 AAD 응용 프로그램을 구성 해야 합니다. 인증 및 이러한 자격 증명 가져오기에 대 한 자세한 내용은 [Microsoft Azure 청구 Api 코드 샘플: RATECARD api](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)문서에서 **1 단계: AAD 테 넌 트의 네이티브 클라이언트 응용 프로그램 구성**에 있는 지침을 따르세요.

마지막으로, 권장 사항을 원하는 데이터베이스를 지정 하는 데 사용할 수 있는 선택적 인수가 있습니다. 

- **/SkuRecommendationDatabasesToRecommend**: 권장 사항을 만들 데이터베이스의 목록입니다. 데이터베이스 이름은 대/소문자를 구분 하며 (1) 입력 .csv에서 (1), (2) 각각 큰따옴표로 묶어야 하며 (3) 각 이름 사이에 단일 공백으로 구분 되어야 합니다 (예:/SkuRecommendationDatabasesToRecommend = "Database1" "Database2" "Database3"). 이 매개 변수를 생략 하면 입력 .csv 파일에서 식별 된 모든 사용자 데이터베이스에 대 한 권장 사항이 제공 됩니다.  

다음은 몇 가지 샘플 호출입니다.

**샘플 1: 기본 가격에 대 한 권장 사항을 가져옵니다. 오프 라인 모드에서 실행 하거나 인증 자격 증명이 없는 경우에 사용 합니다.**

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true
```

**샘플 2: 지정 된 지역 (예: "UKWest")에 대 한 최신 가격으로 권장 사항을 가져옵니다.**

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

**샘플 3: 특정 데이터베이스에 대 한 권장 사항 가져오기 (예: "TPCDS1G, EDW_3G, TPCDS10G").**

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

단일 데이터베이스 권장 사항에 대해 TSV 출력 파일은 다음과 같이 표시 됩니다.

![DMA 폴더에 표시 된 PowerShell 단일 db 파일](../dma/media/dma-sku-recommend-single-db-recommendations.png)

관리 되는 인스턴스 권장 사항에 대 한 TSV 출력 파일은 다음과 같습니다.

![DMA 폴더에 표시 된 PowerShell 관리 되는 인스턴스 파일](../dma/media/dma-sku-recommend-mi-recommendations.png)

출력 파일의 각 열에 대 한 설명은 다음과 같습니다.

- **DatabaseName** -데이터베이스의 이름입니다.
- **MetricType** -권장 Azure SQL Database 단일 데이터베이스/관리 되는 인스턴스 계층입니다.
- **MetricValue** -권장 Azure SQL Database 단일 데이터베이스/관리 되는 인스턴스 SKU입니다.
- **PricePerMonth** – 해당 SKU에 대 한 월별 예상 가격입니다.
- 영역 **이름** – 해당 SKU에 대 한 지역 이름입니다. 
- **IsTierRecommended** -각 계층에 대 한 최소 SKU 권장 사항을 만듭니다. 그런 다음 추론을 적용 하 여 데이터베이스에 적합 한 계층을 결정 합니다. 이는 데이터베이스에 권장 되는 계층을 반영 합니다. 
- **ExclusionReasons** -계층을 권장 하는 경우이 값은 비어 있습니다. 권장 되지 않는 각 계층에 대해 선택 하지 않은 이유를 제공 합니다.
- **AppliedRules** -적용 된 규칙에 대 한 간단한 표기법입니다.

최종 권장 계층 (즉, **MetricType**) 및 값 (예: **MetricValue**)- **IsTierRecommended** 열이 TRUE 인 경우 온-프레미스 데이터베이스와 유사한 성공률으로 Azure에서 실행 하는 데 필요한 최소 SKU를 반영 합니다. 관리 되는 인스턴스의 경우 현재 DMA는 가장 일반적으로 사용 되는 8vcore에서 40vcore Sku에 대 한 권장 사항을 지원 합니다. 예를 들어 표준 계층의 권장 되는 최소 SKU가 S4 인 경우 S3 또는 아래를 선택 하면 쿼리가 시간 초과 되거나 실행 되지 않습니다.

HTML 파일에는이 정보가 그래픽 형식으로 포함 되어 있습니다. 최종 권장 사항을 보고 프로세스의 다음 부분을 프로 비전 하는 사용자에 게 친숙 한 방법을 제공 합니다. HTML 출력에 대 한 자세한 내용은 다음 섹션에서 설명 합니다.

## <a name="provision-recommended-skus-to-azure"></a>권장 Sku를 Azure에 프로 비전

몇 번의 클릭 만으로 확인 된 권장 사항을 사용 하 여 Azure에서 대상 Sku를 프로 비전 할 수 있습니다 .이를 통해 데이터베이스를 마이그레이션할 수 있습니다. HTML 파일을 사용 하 여 Azure 구독을 입력할 수 있습니다. 데이터베이스에 대 한 가격 책정 계층, 계산 수준 및 최대 데이터 크기를 선택 합니다. 그리고 데이터베이스를 프로 비전 하는 스크립트를 생성 합니다. PowerShell을 사용 하 여이 스크립트를 실행할 수 있습니다.

단일 컴퓨터에서이 프로세스를 수행 하거나, 여러 컴퓨터에서이 프로세스를 수행 하 여 대규모 SKU 권장 사항을 확인할 수 있습니다. DMA는 현재 명령줄 인터페이스를 통해 전체 프로세스를 지원 함으로써 간단 하 고 확장 가능한 환경을 제공 합니다.

프로 비전 정보를 입력 하 고 권장 사항을 변경 하려면 HTML 파일을 다음과 같이 업데이트 합니다.

**단일 데이터베이스 권장 사항**

![Azure SQL DB SKU 권장 사항 화면](../dma/media/dma-sku-recommend-single-db-recommendations1.png)

1. HTML 파일을 열고 다음 정보를 입력 합니다.
    - **구독 id** -데이터베이스를 프로 비전 하려는 Azure 구독의 구독 id입니다.
    - **리소스 그룹** -데이터베이스를 배포 하려는 리소스 그룹입니다. 존재 하는 리소스 그룹을 입력 합니다.
    - **Region** -데이터베이스를 프로 비전 할 지역입니다. 구독에서 select 지역을 지원 하는지 확인 합니다.
    - **서버 이름** -데이터베이스를 배포 하려는 Azure SQL Database 서버입니다. 존재 하지 않는 서버 이름을 입력 하는 경우 생성 됩니다.
    - **관리자 사용자 이름** -서버 관리자 사용자 이름입니다.
    - **관리자 암호** -서버 관리자 암호입니다. 암호는 8 자 이상, 길이가 128 자이 하 여야 합니다. 암호에는 영어 대문자, 영어 소문자, 숫자(0-9) 및 영숫자가 아닌 문자(!, $, #, % 등) 범주 중 세 개에 해당하는 문자가 포함되어 있어야 합니다. 암호는 사용자 이름에서 전체 또는 일부 (3 + 연속 문자)를 포함할 수 없습니다.

2. 각 데이터베이스에 대 한 권장 사항을 검토 하 고 필요에 따라 가격 책정 계층, 계산 수준 및 최대 데이터 크기를 수정 합니다. 현재 프로 비전을 원하지 않는 데이터베이스는 선택 취소 해야 합니다.

3. **프로 비전 스크립트 생성**을 선택 하 고 스크립트를 저장 한 다음 PowerShell에서 실행 합니다.

    이 프로세스에서는 HTML 페이지에서 선택한 모든 데이터베이스를 만들어야 합니다.

**관리 되는 인스턴스 권장 사항**

![Azure SQL MI SKU 권장 사항 화면](../dma/media/dma-sku-recommend-mi-recommendations1.png)

1. HTML 파일을 열고 다음 정보를 입력 합니다.
    - **구독 id** -데이터베이스를 프로 비전 하려는 Azure 구독의 구독 id입니다.
    - **리소스 그룹** -데이터베이스를 배포 하려는 리소스 그룹입니다. 존재 하는 리소스 그룹을 입력 합니다.
    - **Region** -데이터베이스를 프로 비전 할 지역입니다. 구독에서 select 지역을 지원 하는지 확인 합니다.
    - **인스턴스 이름** – 데이터베이스를 마이그레이션하려는 Azure SQL Managed Instance 인스턴스입니다. 인스턴스 이름에는 소문자, 숫자 및 '-'만 포함 될 수 있지만 '-'로 시작 하거나 끝날 수 없으며, 63 자를 초과할 수 없습니다.
    - **인스턴스 관리자 사용자** 이름 – 인스턴스 관리자 사용자 이름입니다. 로그인 이름이 다음 요구 사항을 충족 하는지 확인 합니다. SQL 식별자는 일반적인 시스템 이름 (예: admin, administrator, sa, root, dbmanager, loginmanager 등) 이나 기본 제공 데이터베이스 사용자 또는 역할 (예: dbo, guest, public 등)이 아닙니다. 이름에 공백, 유니코드 문자 또는 알파벳이 아닌 문자가 포함 되지 않고 숫자 또는 기호로 시작 되지 않는지 확인 합니다. 
    - **인스턴스 관리자 암호** -인스턴스 관리자 암호입니다. 암호는 16 자 이상 이어야 하 고 길이가 128 자이 하 여야 합니다. 암호에는 영어 대문자, 영어 소문자, 숫자(0-9) 및 영숫자가 아닌 문자(!, $, #, % 등) 범주 중 세 개에 해당하는 문자가 포함되어 있어야 합니다. 암호는 사용자 이름에서 전체 또는 일부 (3 + 연속 문자)를 포함할 수 없습니다.
    - **Vnet 이름** – 관리 되는 인스턴스를 프로 비전 해야 하는 vnet 이름입니다. 기존 VNet 이름을 입력 합니다.
    - **서브넷 이름** – 관리 되는 인스턴스를 프로 비전 해야 하는 서브넷 이름입니다. 기존 서브넷 이름을 입력 합니다.

2. 각 인스턴스에 대 한 권장 사항을 검토 하 고 필요에 따라 가격 책정 계층, 계산 수준 및 최대 데이터 크기를 수정 합니다. 권장 사항은 현재 8vcore에서 40vcore Sku로 제한 되지만, 원하는 경우에는 여전히 64vcore 및 80vcore Sku를 프로 비전 할 수 있는 옵션이 있습니다. 현재 프로 비전을 원하지 않는 모든 인스턴스를 선택 취소 해야 합니다.

    이 프로세스에서는 HTML 페이지에서 선택한 모든 데이터베이스를 만들어야 합니다.

    > [!NOTE]
    > 서브넷에서 관리 되는 인스턴스를 만드는 작업을 완료 하는 데 몇 시간 정도 걸릴 수 있습니다. PowerShell을 통해 프로 비전 스크립트를 실행 한 후 Azure Portal에서 배포의 상태를 확인할 수 있습니다.

## <a name="next-step"></a>다음 단계

- CLI에서 DMA를 실행 하는 명령에 대 한 전체 목록은 [명령줄에서 Data Migration Assistant 실행](https://docs.microsoft.com/sql/dma/dma-commandline?view=sql-server-2017)문서를 참조 하세요.
