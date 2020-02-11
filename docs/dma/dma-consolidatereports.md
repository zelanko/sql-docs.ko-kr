---
title: Data Migration Assistant를 사용 하 여 엔터프라이즈 평가 및 평가 보고서 통합
description: SQL Server를 업그레이드 하거나 Azure SQL Database으로 마이그레이션하기 전에 DMA를 사용 하 여 엔터프라이즈를 평가 하 고 평가 보고서를 통합 하는 방법을 알아봅니다.
ms.date: 06/21/2019
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
ms.custom: seo-lt-2019
ms.openlocfilehash: ec8ededac012ccb2b3d4b62fc40d84132a6fb882
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056656"
---
# <a name="assess-an-enterprise-and-consolidate-assessment-reports-with-dma"></a>엔터프라이즈 평가 및 DMA에 평가 보고서 통합

다음 단계별 지침은 Data Migration Assistant를 사용 하 여 온-프레미스 SQL Server 또는 Azure Vm에서 실행 되는 SQL Server를 업그레이드 하거나 Azure SQL Database로 마이그레이션하기 위한 성공적으로 확장 된 평가를 수행 하는 데 도움이 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

- DMA가 시작 되는 네트워크의 도구 컴퓨터를 지정 합니다. 이 컴퓨터가 SQL Server 대상에 연결 되어 있는지 확인 합니다.
- 다운로드 및 설치:
  - [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v 3.6 이상
  - [PowerShell](https://aka.ms/wmf5download) v 5.0 이상
  - [.NET Framework](https://www.microsoft.com/download/details.aspx?id=30653) v 4.5 이상
  - [SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.0 이상.
  - [데스크톱을 Power BI](https://docs.microsoft.com/power-bi/desktop-get-the-desktop)합니다.
  - [Azure PowerShell 모듈](https://docs.microsoft.com/powershell/azure/install-az-ps?view=azps-1.0.0)
- 다운로드 및 추출:
  - [DMA 보고서 Power BI 템플릿입니다](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/2/PowerBI-Reports.zip).
  - [Loadwarehouse 스크립트](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/1/LoadWarehouse1.zip)입니다.

## <a name="loading-the-powershell-modules"></a>PowerShell 모듈 로드

Powershell 모듈을 PowerShell 모듈 디렉터리에 저장 하면 사용 하기 전에 명시적으로 로드할 필요 없이 모듈을 호출할 수 있습니다.

모듈을 로드 하려면 다음 단계를 수행 합니다.

1. C:\Program Files\WindowsPowerShell\Modules로 이동한 다음 **DataMigrationAssistant**라는 폴더를 만듭니다.
2. [PowerShell 모듈](https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/MicrosoftDataMigration/56/4/PowerShell-Modules2.zip)을 열고 만든 폴더에 저장 합니다.

      ![PowerShell 모듈](../dma/media//dma-consolidatereports/dma-powershell-modules.png)

    각 폴더에는 다음 그림에 표시 된 것 처럼 연결 된 .psm1 파일이 포함 되어 있습니다.

   ![PowerShell 모듈 .psm1 파일](../dma/media//dma-consolidatereports/dma-powershell-modules-psm1-files.png)

   > [!NOTE]
   > 폴더 및 폴더에 포함 된 .psm1 파일의 이름은 같아야 합니다.

   > [!IMPORTANT]
   > WindowsPowerShell 디렉터리에 저장 한 후 PowerShell 파일을 차단 해제 하 여 모듈이 올바르게 로드 되도록 할 수 있습니다. PowerShell 파일의 차단을 해제 하려면 파일을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **차단 해제** 텍스트 상자를 선택 하 고 **확인**을 선택 합니다.

   ![.psm1 파일 속성](../dma/media//dma-consolidatereports/dma-psm1-file-properties.png)

    이제 PowerShell은 새 PowerShell 세션이 시작 될 때 이러한 모듈을 자동으로 로드 해야 합니다.

## <a name="create-inventory"></a>SQL Server 인벤토리 만들기

PowerShell 스크립트를 실행 하 여 SQL Server를 평가 하기 전에 평가 하려는 SQL Server의 인벤토리를 작성 해야 합니다.

이 인벤토리는 다음 두 가지 형식 중 하나일 수 있습니다.

- Excel CSV 파일
- SQL Server 테이블

### <a name="if-using-a-csv-file"></a>CSV 파일을 사용 하는 경우

> [!IMPORTANT]
> 인벤토리 파일이 CSV (쉼표로 구분 된) 파일로 저장 되었는지 확인 합니다.
>
> 기본 인스턴스의 경우 인스턴스 이름을 MSSQLServer로 설정 합니다.


Csv 파일을 사용 하 여 데이터를 가져올 때 데이터 **인스턴스 이름** 및 **데이터베이스 이름**열이 두 개만 있고 열에 머리글 행이 없는 경우를 확인 합니다.

 ![csv 파일 콘텐츠](../dma/media//dma-consolidatereports/dma-csv-file-contents.png)

### <a name="if-using-a-sql-server-table"></a>SQL Server 테이블을 사용 하는 경우

> [!IMPORTANT]
> 기본 인스턴스의 경우 인스턴스 이름을 MSSQLServer로 설정 합니다.

**EstateInventory** 라는 데이터베이스와 **databaseinventory**라는 테이블을 만듭니다. 이 인벤토리 데이터를 포함 하는 테이블에는 다음 4 개의 열이 있는 한 많은 열이 있을 수 있습니다.

- ServerName
- InstanceName
- DatabaseName
- AssessmentFlag

![SQL Server 테이블 내용](../dma/media//dma-consolidatereports/dma-sql-server-table-contents.png)

이 데이터베이스가 tools 컴퓨터에 없으면 도구 컴퓨터에이 SQL Server 인스턴스에 대 한 네트워크 연결이 설정 되어 있는지 확인 합니다.

CSV 파일에 SQL Server 테이블을 사용 하면 평가 플래그 열을 사용 하 여 평가를 위해 선택 되는 인스턴스/데이터베이스를 제어할 수 있으므로 평가를 더 작은 청크로 쉽게 구분할 수 있습니다.  그런 다음 여러 개의 평가를 확장할 수 있습니다 (이 문서의 뒷부분에서 평가 실행에 대 한 섹션 참조) .이는 여러 CSV 파일을 유지 관리 하는 것 보다 더 쉽습니다.

개체 수와 복잡성에 따라 평가는 매우 긴 시간 (시간 +)을 사용할 수 있으므로 평가를 관리 하기 쉬운 청크로 분리 하는 것이 좋습니다.

## <a name="running-a-scaled-assessment"></a>크기 조정 된 평가 실행

모듈 디렉터리에 PowerShell 모듈을 로드 하 고 인벤토리를 만든 후 PowerShell을 열고 dmaDataCollector 함수를 실행 하 여 크기 조정 된 평가를 실행 해야 합니다.
 
  ![dmaDataCollector 함수 목록](../dma/media//dma-consolidatereports/dma-dmaDataCollector-function-listing.png)

DmaDataCollector 함수와 연결 된 매개 변수는 다음 표에 설명 되어 있습니다.

|매개 변수  |Description |
|---------|---------|
|**getServerListFrom** | 사용자의 인벤토리에 있습니다. 가능한 값은 **SqlServer** 및 **CSV**입니다.<br/>자세한 내용은 [SQL server 인벤토리 만들기](#create-inventory)를 참조 하세요. |
|**csvPath** | CSV 인벤토리 파일의 경로입니다.  **Getserverlistfrom** 이 **CSV**로 설정 된 경우에만 사용 됩니다. |
|**serverName** | **Getserverlistfrom** 매개 변수에서 **SqlServer** 를 사용 하는 경우 인벤토리의 SQL Server 인스턴스 이름입니다. |
|**databaseName** | 인벤토리 테이블을 호스트 하는 데이터베이스입니다. |
|**AssessmentName** | DMA 평가의 이름입니다. |
|**TargetPlatform** | 수행 하려는 평가 대상 유형입니다.  가능한 값은 **AzureSQLDatabase**, **SQLServer2012**, **SQLServer2014**, **Sqlserver2016-ssei-expr**, **SQLServerLinux2017**, **SQLServerWindows2017**및 **managedsqlserver**입니다. |
|**AuthenticationMethod** | 평가 하려는 SQL Server 대상에 연결 하기 위한 인증 방법입니다. 가능한 값은 **sqlauth** 및 **windowsauth**입니다. |
|**OutputLocation** | JSON 평가 출력 파일을 저장할 디렉터리입니다. 평가 되는 데이터베이스의 수와 데이터베이스 내의 개체 수에 따라 평가에 매우 긴 시간이 걸릴 수 있습니다. 모든 평가가 완료 된 후에 파일이 기록 됩니다. |

예기치 않은 오류가 발생 하는 경우이 프로세스에서 시작 하는 명령 창이 종료 됩니다.  오류 로그를 검토 하 여 실패 한 이유를 확인 합니다.
 
  ![오류 로그 위치](../dma/media//dma-consolidatereports/dma-error-log-file-location.png)

## <a name="consuming-the-assessment-json-file"></a>평가 JSON 파일 사용

평가가 완료 되 면 분석을 위해 데이터를 SQL Server으로 가져올 준비가 된 것입니다. 평가 JSON 파일을 사용 하려면 PowerShell을 열고 dmaProcessor 함수를 실행 합니다.
 
  ![dmaProcessor 함수 목록](../dma/media//dma-consolidatereports/dma-dmaProcessor-function-listing.png)

DmaProcessor 함수와 연결 된 매개 변수는 다음 표에 설명 되어 있습니다.

|매개 변수  |Description |
|---------|---------|
|**processTo** | JSON 파일을 처리 하는 위치입니다. 가능한 값은 **SQLServer** 및 **AzureSQLDatabase**입니다. |
|**serverName** | 데이터가 처리 될 SQL Server 인스턴스입니다.  **Processto** 매개 변수에 대해 **AzureSQLDatabase** 를 지정 하는 경우 SQL Server 이름만 포함 합니다 (database.windows.net는 포함 하지 않음). Azure SQL Database를 대상으로 지정 하는 경우 두 개의 로그인을 묻는 메시지가 표시 됩니다. 첫 번째는 Azure 테 넌 트 자격 증명 이며, 두 번째는 Azure SQL Server에 대 한 관리자 로그인입니다. |
|**CreateDMAReporting** | JSON 파일을 처리 하기 위해 만들 준비 데이터베이스입니다.  지정한 데이터베이스가 이미 존재 하 고이 매개 변수를 1로 설정 하면 개체가 생성 되지 않습니다.  이 매개 변수는 삭제 된 단일 개체를 다시 만드는 데 유용 합니다. |
|**CreateDataWarehouse** | Power BI 보고서에서 사용할 데이터 웨어하우스를 만듭니다. |
|**databaseName** | DMAReporting 데이터베이스의 이름입니다. |
|**warehouseName** | 데이터 웨어하우스 데이터베이스의 이름입니다. |
|**jsonDirectory** | JSON 평가 파일이 들어 있는 디렉터리입니다.  디렉터리에 여러 JSON 파일이 있는 경우 하나씩 처리 됩니다. |

DmaProcessor 함수는 단일 파일을 처리 하는 데 몇 초 밖에 걸리지 않습니다.

## <a name="loading-the-data-warehouse"></a>데이터 웨어하우스 로드

DmaProcessor 평가 파일의 처리를 완료 한 후에는 데이터가 ReportData 테이블의 DMAReporting 데이터베이스에 로드 됩니다. 이 시점에서 데이터 웨어하우스를 로드 해야 합니다.

1. LoadWarehouse 스크립트를 사용 하 여 차원에 누락 된 값을 채웁니다.

    이 스크립트는 DMAReporting 데이터베이스의 ReportData 테이블에서 데이터를 가져와 웨어하우스로 로드 합니다.  이 로드 프로세스 중에 오류가 발생 하는 경우 차원 테이블에 항목이 누락 될 수 있습니다.

2. 데이터 웨어하우스를 로드 합니다.
 
      ![LoadWarehouse 콘텐츠 로드 됨](../dma/media//dma-consolidatereports/dma-LoadWarehouse-loaded.png)

## <a name="set-your-database-owners"></a>데이터베이스 소유자 설정

필수는 아니지만 보고서에서 값을 최대한 얻으려면 **dimDBOwner** 차원에 데이터베이스 소유자를 설정한 다음 **FactAssessment** 테이블에서 **DBOwnerKey** 를 업데이트 하는 것이 좋습니다.  이 프로세스를 수행 하면 특정 데이터베이스 소유자에 따라 Power BI 보고서를 조각화 및 필터링 할 수 있습니다.

LoadWarehouse 스크립트를 사용 하 여 데이터베이스 소유자를 설정 하는 기본 TSQL 문을 제공할 수도 있습니다.

  ![LoadWarehouse 설정 소유자](../dma/media//dma-consolidatereports/dma-LoadWarehouse-set-owners.png)

## <a name="dma-reports"></a>DMA 보고서

1. Power BI Desktop에서 DMA 보고서 Power BI 템플릿을 엽니다.
2. **DMAWarehouse** 데이터베이스를 가리키는 서버 세부 정보를 입력 하 고 **로드**를 선택 합니다.

   ![DMA 보고서 Power BI 템플릿이 로드 됨](../dma/media//dma-consolidatereports/dma-reports-powerbi-template-loaded.png)

   보고서가 **DMAWarehouse** 데이터베이스에서 데이터를 새로 고친 후 다음과 비슷한 보고서를 제공 합니다.

   ![DMAWarehouse 보고서 뷰](../dma/media//dma-consolidatereports/dma-DMAWarehouse-report1.png)

   > [!TIP]
   > 예상한 데이터가 표시 되지 않는 경우 활성 책갈피를 변경해 보세요.  자세한 내용은 다음 섹션에서 세부 정보를 참조 하세요.

## <a name="working-with-dma-reports"></a>DMA 보고서 작업

DMA 보고서를 사용 하려면 다음과 같이 책갈피 및 슬라이서를 사용 하 여 필터링 합니다.

- 평가 유형 (Azure SQL DB, Azure SQL MI, SQL 온-프레미스) 
- 인스턴스 이름
- 데이터베이스 이름
- 팀 이름

책갈피 및 필터 블레이드에 액세스 하려면 주 보고서 페이지에서 필터 책갈피를 선택 합니다.

![DMA 보고서 책갈피 및 필터](../dma/media//dma-consolidatereports/dma-report-bookmarks-filters.png)

필터 책갈피를 선택 하면 다음 블레이드가 활성화 됩니다.

![DMA 보고서 뷰 블레이드](../dma/media//dma-consolidatereports/dma-report-views-blade.png)

다음과 같이 책갈피를 사용 하 여 보고 컨텍스트를 전환할 수 있습니다.

- Azure SQL DB 클라우드 평가
- Azure SQL MI 클라우드 평가
- 온-프레미스 평가

![DMA 보고서 뷰 책갈피](../dma/media//dma-consolidatereports/dma-report-bookmarks1.png)

필터 블레이드를 숨기려면 뒤로 단추를 CTRL + 클릭 합니다.

![DMA 보고서 뷰 뒤로 단추](../dma/media//dma-consolidatereports/dma-report-bookmarks-back.png)

보고서 페이지의 왼쪽 아래에는 필터가 다음 항목 중 하나에서 현재 적용 되는지 여부를 표시 하는 메시지가 표시 됩니다.

- FactAssessment – InstanceName
- FactAssessment – DatabaseName
- dimDBOwner-DBOwner

![필터 적용 프롬프트](../dma/media//dma-consolidatereports/dma-filter-applied-prompt.png)

> [!NOTE]
> Azure SQL Database 평가만 수행 하는 경우에는 클라우드 보고서만 채워집니다. 반대로 온-프레미스 평가만 수행 하는 경우 온-프레미스 보고서만 채워집니다. 그러나 Azure 및 온-프레미스 평가를 모두 수행 하 고 두 평가를 모두 웨어하우스로 로드 하는 경우에는 연결 된 아이콘을 CTRL + 클릭 하 여 클라우드 보고서와 온-프레미스 보고서 간을 전환할 수 있습니다.

## <a name="reports-visuals"></a>보고서 시각적 개체

Power BI 보고서에 표시 되는 세부 정보는 다음 섹션에 나와 있습니다.

### <a name="readiness-"></a>되었는지

  ![DMA 준비 비율](../dma/media//dma-consolidatereports/dma-readiness-percentage.png)

이 시각적 개체는 선택 컨텍스트 (모든 항목, 인스턴스, 데이터베이스 [의 배수])를 기준으로 업데이트 됩니다.

### <a name="readiness-count"></a>준비 수

  ![DMA 준비 수](../dma/media//dma-consolidatereports/dma-readiness-count.png)

이 시각적 개체는 마이그레이션할 준비가 되지 않은 데이터베이스 수를 마이그레이션할 준비가 된 데이터베이스의 수를 보여 줍니다.

### <a name="readiness-bucket"></a>준비 버킷

  ![DMA 준비 버킷](../dma/media//dma-consolidatereports/dma-readiness-bucket.png)

이 시각적 개체는 다음 준비 버킷에의 한 데이터베이스의 분석을 보여 줍니다.

- 100% 준비
- 75-99% 준비
- 50-75% 준비
- 준비 안 됨

### <a name="issues-word-cloud"></a>Word 클라우드 문제
 
  ![DMA 문제 WordCloud](../dma/media//dma-consolidatereports/dma-issues-word-cloud.png)

이 시각적 개체는 선택 컨텍스트 (모든 항목, 인스턴스, 데이터베이스 [의 배수]) 내에서 현재 발생 하 고 있는 문제를 보여 줍니다. 해당 단어가 화면에 표시 되 면 해당 범주의 문제 수가 커집니다. 마우스 포인터로 단어를 가리키면 해당 범주에서 발생 하는 문제 수가 표시 됩니다.

### <a name="database-readiness"></a>데이터베이스 준비

  ![DMA 데이터베이스 준비 보고서](../dma/media//dma-consolidatereports/dma-database-readiness-report.png)

이 섹션은 인스턴스 데이터베이스의 준비 상태를 보여 주는 보고서의 주요 부분입니다. 이 보고서의 드릴 다운 계층 구조는 다음과 같습니다.

- InstanceDatabase
- ChangeCategory
- 제목
- ObjectType
- ImpactedObjectName

 ![DMA 데이터베이스 준비 보고서 드릴 다운](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown.png)

이 보고서는 수정 계획 보고서를 만들기 위한 필터 지점으로도 사용 됩니다.

수정 계획 보고서를 자세히 살펴보려면이 그래프에서 데이터 요소를 마우스 오른쪽 단추로 클릭 하 고 **드릴스루**를 가리킨 다음 **수정 계획**을 선택 합니다.

이 태스크는 드릴스루 옵션을 선택한 시점에 따라 현재 계층 수준으로 수정 계획 보고서를 필터링 합니다.

  ![DMA 데이터베이스 준비 보고서 드릴 다운 필터링](../dma/media//dma-consolidatereports/dma-database-readiness-report-drilldown-filtered.png)

  ![DMA 수정 계획 보고서](../dma/media//dma-consolidatereports/dma-remediation-plan-report.png)

수정 계획 보고서를 자체적으로 사용 하 여 **시각화 필터** 블레이드의 필터를 사용 하 여 사용자 지정 수정 계획을 작성할 수도 있습니다.
 
  ![DMA 수정 계획 보고서 필터 옵션](../dma/media//dma-consolidatereports/dma-remediation-plan-report-filter-options.png)

### <a name="script-disclaimer"></a>스크립트 부인

*이 문서에 제공 된 샘플 스크립트는 Microsoft 표준 지원 프로그램 또는 서비스에서 지원 되지 않습니다. 모든 스크립트는 어떤 종류의 보증도 없이 있는 그대로 제공 됩니다. Microsoft는 상품성 또는 특정 목적에의 적합성에 대 한 묵시적 보증을 제한 없이 포함 하는 모든 묵시적 보증을 부인 합니다. 샘플 스크립트 및 설명서의 사용 또는 성능에서 발생 하는 전체 위험은 사용자에 게 남아 있습니다. Microsoft, 해당 작성자, 또는 스크립트의 생성, 프로덕션 또는 배달에 참여 하는 모든 사용자는 Microsoft가 이러한 손해에 대 한 문제를 해결 하는 경우에도 샘플 스크립트나 설명서를 사용할 수 없는 경우에도 발생 하는 제한 사항 (비즈니스 수익의 손실에 대 한 손해, 비즈니스 중단, 비즈니스 정보 손실, 기타 pecuniary 손실 등)에 대해 책임을 지지 않습니다.  다른 사이트/리포지토리/블로그에서 이러한 스크립트를 다시 게시 하기 전에 권한을 검색 합니다.*
