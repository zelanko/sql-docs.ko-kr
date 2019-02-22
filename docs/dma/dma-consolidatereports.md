---
title: 엔터프라이즈를 평가 하 고 통합 평가 보고서 (SQL Server) | Microsoft Docs
description: DMA를 사용 하 여 엔터프라이즈 평가 및 SQL Server를 업그레이드 또는 Azure SQL Database로 마이그레이션하기 전에 평가 보고서를 통합 하는 방법에 알아봅니다.
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 400876a2738c2ca791d3aee12da20c9af1db5b9f
ms.sourcegitcommit: 71913f80be0cb6f8d3af00c644ee53e3aafdcc44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56590348"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>엔터프라이즈 평가 및 DMA 사용 하 여 평가 보고서 통합

다음 단계별 지침을 통해 온-프레미스 SQL Server 또는 Azure Vm에서 실행 중인 SQL Server를 업그레이드 또는 Azure SQL Database로 마이그레이션에 대 한 성공적인 크기 조정 된 평가 수행 하려면 Data Migration Assistant를 사용 하 여 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- DMA가 시작 됩니다. 네트워크에 있는 도구 컴퓨터를 지정 합니다. 이 컴퓨터에 SQL Server 대상에 연결 되어 있는지 확인 합니다.
- 다운로드 및 설치:
    - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.6 이상.
    - [PowerShell](https://aka.ms/wmf5download) v5.0 이상.
    - [.NET framework](https://www.microsoft.com/download/details.aspx?id=30653) v4.5 이상.
    - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 이상.
    - [PowerBI desktop](https://docs.microsoft.com/power-bi/desktop-get-the-desktop)합니다.
    - [Azure PowerShell 모듈](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- 다운로드 및 추출 합니다.
    - 합니다 [DMA 보고서 Power BI 템플릿](https://msdnshared.blob.core.windows.net/media/2019/02/PowerBI-Reports1.zip)합니다.
    - 합니다 [LoadWarehouse 스크립트](https://msdnshared.blob.core.windows.net/media/2019/02/LoadWarehouse.zip)합니다.

## <a name="loading-the-powershell-modules"></a>PowerShell 모듈을 로드합니다.
PowerShell 모듈 디렉터리에 저장 하는 PowerShell 모듈을 사용 하기 전에 명시적으로 로드 하는 데 필요 없이 모듈 호출 할 수 있습니다.

모듈을 로드 하려면 다음 단계를 수행 합니다.
1. C:\Program Files\WindowsPowerShell\Modules 이동한 다음 라는 폴더를 만듭니다 **DataMigrationAssistant**합니다.
2. 엽니다는 [PowerShell 모듈](https://msdnshared.blob.core.windows.net/media/2019/02/PowerShell-Modules.zip), 사용자가 만든 폴더에 저장 합니다.

      ![PowerShell 모듈](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    다음 그림에 나와 있는 것 처럼 연결된 (psm1 파일을 포함 하는 각 폴더:

   ![PowerShell 모듈 psm1 파일](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > 폴더 및 포함 된 (psm1 파일 이름이 있어야 합니다.

   > [!IMPORTANT]
   > 모듈을 제대로 로드 되도록 WindowsPowerShell 디렉터리에 저장 하면 PowerShell 파일의 차단을 해제 해야 합니다. PowerShell 파일을 차단 해제를 마우스 오른쪽 단추로 클릭 파일을 선택 **속성**를 선택 합니다 **차단 해제** 텍스트 상자를 선택한 후 **확인**합니다.

   ![psm1 파일 속성](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    새 PowerShell 세션을 시작 하는 경우 PowerShell이이 모듈 자동 로드 이제 해야 합니다.

## <a name="create-inventory"></a> SQL Server의 인벤토리 생성
SQL Server를 평가 하기 위해 PowerShell 스크립트를 실행 하기 전에 평가 하려는 SQL Server의 인벤토리를 작성 해야 합니다.

이 인벤토리 두 가지 형식 중 하나일 수 있습니다.
- Excel CSV 파일
- SQL Server 테이블

### <a name="if-using-a-csv-file"></a>CSV 파일을 사용 하는 경우
데이터의 두 개의 열이 있는 csv 파일을 사용 하 여 데이터를 확인 **인스턴스 이름** 하 고 **데이터베이스 이름**, 열 머리글 행 없는 하 고 합니다.
 
 ![csv 파일 내용](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-sql-server-table"></a>SQL Server 테이블을 사용 하는 경우
라는 데이터베이스를 만듭니다 **EstateInventory** 테이블을 호출 하 고 **DatabaseInventory**합니다. 다음 4 개의 열이 없으면으로이 인벤토리 데이터를 포함 하는 테이블 임의 개수의 열을 포함할 수 있습니다.
- 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server 목차](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

이 데이터베이스를 도구 컴퓨터에 없는 경우 도구는 컴퓨터에이 SQL Server 인스턴스에 네트워크 연결 되어 있는지 확인 합니다.

CSV 파일을 통해 SQL Server 테이블을 사용 하는 이점은 인스턴스 제어 / 가져옵니다 쉽게 평가를 더 작은 청크로 구분 하는 평가 위한 픽업 데이터베이스 평가 플래그 열을 사용할 수 있는 경우  그런 다음 여러 평가 걸쳐 있을 수 있습니다 (참조 섹션에서이 문서의 뒷부분에서 평가 실행)는 여러 CSV 파일을 유지 관리 하는 것 보다 쉽습니다.

개체 및 복잡성에 수에 따라 평가 걸릴 수 있습니다는 매우 긴 시간 (시간 +), 관리 하기 쉬운 청크로 평가 구분 하는 것이 좋습니다 이므로 염두에 두어야 합니다.

## <a name="running-a-scaled-assessment"></a>크기 조정 된 평가 실행합니다.
Modules 디렉터리에 PowerShell 모듈을 로드 하 고 인벤토리를 만들, PowerShell을 열고 dmaDataCollector 함수를 실행 하 여 크기 조정 된 평가 실행 해야 합니다.
 
  ![dmaDataCollector 함수 목록](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

DmaDataCollector 함수와 연결 된 매개 변수를 다음과에서 같습니다.

|매개 변수  |Description |
|---------|---------|
|**getServerListFrom** | 인벤토리 합니다. 가능한 값은 **SqlServer** 하 고 **CSV**합니다.<br/>자세한 내용은 참조 하세요. [SQL Server의 인벤토리를 만들고](#create-inventory)합니다. |
|**serverName** | SQL Server 인스턴스 이름을 사용 하는 경우 인벤토리 **SqlServer** 에 **getServerListFrom** 매개 변수입니다. |
|**databaseName** | 인벤토리 테이블을 호스팅하는 데이터베이스입니다. |
|**AssessmentName** | DMA 평가의 이름입니다. |
|**TargetPlatform** | 수행 하려는 평가 대상 형식입니다.  가능한 값은 **AzureSQLDatabase**, **SQLServer2012**를 **SQLServer2014**하십시오 **SQLServer2016**,  **SQLServerLinux2017**하십시오 **SQLServerWindows2017**, 및 **ManagedSqlServer**합니다. |
|**AuthenticationMethod** | 평가 하려는 SQL Server 대상에 연결 하기 위한 인증 방법입니다. 가능한 값은 **이렇게 하면 SQLAuth** 하 고 **WindowsAuth**합니다. |
|**OutputLocation** | JSON을 저장 하는 평가 출력 파일 디렉터리입니다. 평가 중인 데이터베이스 수 및 데이터베이스 내에서 개체의 수에 따라 평가 시간이 아주 오래 걸릴 수 있습니다. 파일은 모든 평가 완료 후에 기록 됩니다. |

예기치 않은 오류가 있으면이 프로세스에서 시작 하는 명령 창 종료 됩니다.  실패 원인을 확인 하려면 오류 로그를 검토 합니다.
 
  ![오류 로그 위치](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>평가 JSON 파일 사용

평가 완료 되 면 준비가 이제 분석에 대 한 SQL Server로 데이터를 가져옵니다. 평가 JSON 파일에서 사용할 PowerShell을 열고 dmaProcessor 함수를 실행 합니다.
 
  ![dmaProcessor 함수 목록](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

DmaProcessor 함수와 연결 된 매개 변수를 다음과에서 같습니다.

|매개 변수  |Description |
|---------|---------|
|**processTo** | JSON 파일을 처리할 수 위치입니다. 가능한 값은 **SQLServer** 하 고 **AzureSQLDatabase**합니다. |
|**serverName** | 데이터를 처리할지 SQL Server 인스턴스.  지정 하는 경우 **AzureSQLDatabase** 에 대 한 합니다 **processTo** 매개 변수를 SQL Server 이름만 포함 (포함 되지 않습니다. database.windows.net). 메시지가 표시 됩니다 두 로그인에 대 한 Azure SQL 데이터베이스를 대상으로 할 때 첫 번째 Azure 테 넌 트 자격 증명 있고 두 번째는 Azure SQL Server에 대 한 관리자 로그인입니다. |
|**CreateDMAReporting** | JSON 파일을 처리 하는 것에 대 한 만들기 준비 데이터베이스입니다.  이미 지정한 데이터베이스가 하나에이 매개 변수를 설정 하는 경우 개체 만든 가져오기 하지 마세요.  이 매개 변수는 삭제 된 단일 개체를 다시 만드는 데 유용 합니다. |
|**CreateDataWarehouse** | Power BI 보고서에서 사용할 데이터 웨어하우스를 만듭니다. |
|**databaseName** | DMAReporting 데이터베이스의 이름입니다. |
|**warehouseName** | 데이터 웨어하우스 데이터베이스의 이름입니다. |
|**jsonDirectory** | JSON 평가 파일이 포함 된 디렉터리입니다.  디렉터리에 JSON 파일이 여러 개 있으면 해당 처리 중인 하나씩 있습니다. |

DmaProcessor 함수에는 단일 파일을 처리 하는 데 몇 초 걸립니다.

## <a name="loading-the-data-warehouse"></a>데이터 웨어하우스 로드
dmaProcessor에 평가 파일 처리 완료 후 보고서 데이터 표에 DMAReporting 데이터베이스로 데이터 로드 됩니다. 이 시점에서 데이터 웨어하우스 로드 해야 합니다.

1. 크기에 모든 누락 값을 채우는 LoadWarehouse 스크립트를 사용 합니다.

    스크립트는 DMAReporting 데이터베이스에서 보고서 데이터 테이블에서 데이터를 가져오는을 웨어하우스로 로드 합니다.  이 로드 프로세스 중에 오류가 경우 차원 테이블에서 누락 된 항목의 결과 가능성이 높습니다.

2. 데이터 웨어하우스를 로드 합니다.
 
      ![LoadWarehouse 콘텐츠 로드](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>사용자 데이터베이스 소유자를 설정 합니다.
필수 상태인 동안 보고서에서 가장 많은 가치를 얻을 것이 좋습니다 데이터베이스 소유자를 설정 하는 합니다 **dimDBOwner** 차원의 하 한 다음 업데이트 **DBOwnerKey** 에  **FactAssessment** 테이블입니다.  다음이 프로세스를 사용 하면 조각화 및 특정 데이터베이스 소유자를 기준으로 Power BI 보고서를 필터링 합니다.

또한 데이터베이스 소유자를 설정 하는 데에 대 한 기본적인 TSQL 문을 제공 LoadWarehouse 스크립트를 사용할 수 있습니다.

  ![LoadWarehouse 설정 소유자](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>DMA 보고서

1. Power BI Desktop에서 DMA 보고서 Power BI 템플릿을 엽니다.
2. 가리키는 서버 세부 정보를 입력 하 **DMAWarehouse** 데이터베이스를 선택한 후 **부하**합니다.

    > [!IMPORTANT]
    > 값을 그대로 사용 하려면 Enter를 누르지 마십시오.

      ![DMA 보고서 Power BI 템플릿 로드](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   보고서에서 데이터를 새로 고쳐 짐 후 합니다 **DMAWarehouse** 다음과 유사한 보고서를 사용 하 여 표시 하는 데이터베이스입니다.

   ![DMAWarehouse 보고서 보기](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > 예상 했던 데이터에 표시 되지 않는 경우에 활성 책갈피를 변경해 보세요.  자세한 내용은 참조는 다음 섹션에서 세부 정보입니다.

## <a name="working-with-dma-reports"></a>DMA 보고서 사용
DMA 보고서로 작업 하려면 기준으로 필터링 하려면 책갈피 및 슬라이서를 사용 합니다.
- 평가 형식 (Azure SQL DB, Azure SQL MI SQL 온-프레미스) 
- 인스턴스 이름
- 데이터베이스 이름
- 팀 이름

책갈피 및 필터 블레이드에 액세스 하려면 주 보고서 페이지의 필터 책갈피를 선택 합니다.

![DMA 보고서 책갈피 및 필터](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

이 통해 다음 블레이드:

![DMA 보고서 보기 블레이드](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

보고 컨텍스트 사이 전환 하려면 책갈피를 사용할 수 있습니다.
- Azure SQL DB 클라우드 평가
- Azure SQL MI 클라우드 평가
- 온-프레미스 평가

![DMA 보고서 뷰 책갈피](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

필터 블레이드, CTRL + 클릭 뒤로 단추를 숨기려면 합니다.

![DMA 보고서 뷰 뒤로 단추](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

필터를 다음 중 하나에 현재 적용 되는지 여부를 표시 하도록 보고서 페이지의 왼쪽 아래에 메시지가 같습니다.
* FactAssessment-InstanceName
* FactAssessment-DatabaseName
* dimDBOwner-DBOwner

![필터가 적용 된 프롬프트](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> Azure SQL Database 평가만 수행 하면 클라우드 보고서만 채워집니다. 반대로, 온-프레미스 평가만 수행 하면 온-프레미스 보고서만 채워집니다. 그러나 Azure와 온-프레미스 평가 수행 하 고 다음 두 평가 웨어하우스에 로드 전환할 수 있습니다 클라우드 보고서와 CTRL-클릭 하 여 온-프레미스 보고서 간에 연결 된 아이콘.

## <a name="reports-visuals"></a>보고서 시각적 개체
Power BI 보고서에 표시 된 세부 정보는 다음 섹션에 표시 됩니다.

### <a name="readiness-"></a>준비 %

  ![DMA 준비 백분율](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

이 시각적 개체 선택 컨텍스트를 기반으로 업데이트 됩니다 (모든 인스턴스, 데이터베이스 [의 배수로]).

### <a name="readiness-count"></a>준비 상태 수

  ![DMA 준비 개수](../dma/media//dma-consolidatereports/dma-readiness-count.png)

이 시각적 개체는 아직 마이그레이션할 준비가 되지 않은 데이터베이스의 수를 마이그레이션할 준비가 된 데이터베이스의 수를 보여 줍니다.

### <a name="readiness-bucket"></a>준비 버킷

  ![DMA 준비 버킷](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

이 시각적 개체의 다음 준비 버킷 데이터베이스에 대 한 분석을 보여 줍니다.
- 100% 준비
- 75 ~ 99% 준비
- 50-75% 준비
- 준비 안 됨

### <a name="issues-word-cloud"></a>문제 워드 클라우드
 
  ![DMA 문제 WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

이 시각적 개체에서 선택 항목 컨텍스트 내에서 현재 발생 하는 문제를 보여 줍니다. (모든 인스턴스, 데이터베이스 [의 배수로]). 클수록 단어가 나타납니다 큼 화면에서 해당 범주의 문제 수 있습니다. 단어 위에 마우스 포인터를 가져가면 해당 범주에서 발생 한 문제 수를 보여 줍니다.

### <a name="database-readiness"></a>데이터베이스 준비

  ![DMA 데이터베이스 준비 보고서](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

이 섹션에는 인스턴스 데이터베이스의 준비 상태를 보여주는 보고서의 기본 부분입니다. 이 보고서의 드릴 다운 계층 구조에 있습니다.
- InstanceDatabase
- ChangeCategory
- Title
- ObjectType
- ImpactedObjectName

 ![DMA 데이터베이스 준비 보고서 드릴 다운](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

이 보고서는 수정 계획 보고서를 만들기 위한 필터 점으로 역할도 합니다.

수정 계획 보고서를 드릴 하이 그래프에서 데이터 요소를 마우스 오른쪽 단추로 클릭을 가리킵니다 **드릴스루**를 선택한 후 **수정 계획**합니다.

이 작업의 현재 계층 구조 수준을 기반으로 드릴스루 옵션을 선택 하는 수정 계획 보고서를 필터링 합니다.

  ![DMA 데이터베이스 준비 보고서 필터링 드릴 다운](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![DMA 업데이트 관리 계획 보고서](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

필터를 사용 하 여 고유한 사용자 지정 수정 빌드할 계획에서 업데이트 관리 계획 보고서를 사용할 수도 있습니다는 **시각화 필터** 블레이드입니다.
 
  ![DMA 업데이트 관리 계획 보고서 필터 옵션](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>스크립트의 고 지 사항
*이 문서에서 제공 하는 샘플 스크립트는 Microsoft 표준 지원 프로그램 또는 서비스에서 지원 되지 않습니다. 모든 스크립트는 모든 종류의 보증도 없이 있는 그대로 제공 됩니다. Microsoft에서는 등 제한 되지 않고 모든 묵시적된 보증을 부인 상품성 또는 특정 목적에의 적합성 보증을 암시 합니다. 사용 하는 샘플 스크립트 및 설명서의 성능으로 인해 발생 하는 위험이와 책임입니다. 없는 이벤트에서 Microsoft, 작성자가, 또는 다른 생성, 프로덕션 환경 또는 스크립트의 배달에 참여 하는 모든 책임을 지지 모든 손해에 대해 전혀 (손해를 포함 한, 제한 없이 비즈니스 수익, 비즈니스 중단, 손실 손실에 대 한 비즈니스 정보 또는 기타 금전적 손실) Microsoft가 그와 같은 손해의 가능성을 사전에 알고 있던 경우에를 사용 하는 샘플 스크립트 또는 설명서를 사용할 수 없어 책임입니다.  다른 사이트/리포지토리/블로그에서 이러한 스크립트를 보고 하기 전에 권한을 검색 합니다.*
