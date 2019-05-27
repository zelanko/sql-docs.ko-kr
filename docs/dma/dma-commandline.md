---
title: Data Migration Assistant (SQL Server) 명령줄에서 실행 | Microsoft Docs
description: 마이그레이션에 대 한 SQL Server 데이터베이스를 평가 하기 위해 명령줄에서 Data Migration Assistant를 실행 하는 방법 알아보기
ms.custom: ''
ms.date: 05/06/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: ccb2b0b6a60bfc2df94f2cc09b087a22b22ce7ab
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105844"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>명령줄에서 Data Migration Assistant 실행

Data Migration Assistant 설치 버전 2.1 이상에서 시기, dmacmd.exe에도 설치 됩니다 *\% ProgramFiles %\\Microsoft Data Migration Assistant\\* 합니다. Dmacmd.exe를 사용 하 여 무인된 모드에서 데이터베이스를 평가 및 JSON 또는 CSV 파일로 결과 출력 합니다. 이 메서드는 여러 데이터베이스 또는 대규모 데이터베이스를 평가할 때 특히 유용 합니다. 

> [!NOTE]
> Dmacmd.exe 실행 중인 평가 지원합니다. 이 이번에는 마이그레이션이 지원 되지 않습니다.

## <a name="assessments-using-the-command-line-interface-cli"></a>명령줄 인터페이스 (CLI)를 사용 하 여 평가

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|인수  |Description  | 필수 (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Dmacmd.exe 도움말 텍스트를 사용 하는 방법        | N
|`/AssessmentName`     |   평가 프로젝트의 이름   | Y
|`/AssessmentDatabases`     | 연결 문자열의 공백으로 구분 된 목록입니다. 데이터베이스 이름 (초기 카탈로그)은 대/소문자 구분 합니다. | Y
|`/AssessmentSourcePlatform`     | 평가 위해 원본 플랫폼: <br>평가 대 한 지원 되는 값: SqlOnPrem, RdsSqlServer (기본값) <br>대상 준비 상태 평가 대 한 지원 되는 값: SqlOnPrem, (기본값) 이면 RdsSqlServer Cassandra (미리 보기)   | N
|`/AssessmentTargetPlatform`     | 평가 위해 대상 플랫폼:  <br> 평가 대 한 지원 되는 값: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, SqlServer2016, SqlServerLinux2017 및 SqlServerWindows2017 (기본값)  <br> 대상 준비 상태 평가 대 한 지원 되는 값: (기본값) 이면 ManagedSqlServer CosmosDB (미리 보기)   | N
|`/AssessmentEvaluateFeatureParity`  | 기능 패리티 규칙을 실행 합니다. 기능 패리티 평가 대상 플랫폼 AzureSqlDatabase RdsSqlServer 소스 플랫폼을 사용 하는 경우 지원 되지 않습니다.  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 호환성 규칙을 실행  | Y <br> AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendations 이어서 필요 합니다.
|`/AssessmentEvaluateRecommendations`     | 기능 권장 사항 실행        | Y <br> (AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendations 필요)
|`/AssessmentOverwriteResult`     | 결과 파일 덮어쓰기    | N
|`/AssessmentResultJson`     | JSON 결과 파일에 전체 경로     | Y <br> (AssessmentResultJson 또는 AssessmentResultCsv 필요)
|`/AssessmentResultCsv`    | CSV 결과 파일에 전체 경로   | Y <br> (AssessmentResultJson 또는 AssessmentResultCsv 필요)
|`/Action`    | SkuRecommendation를 사용 하 여 SKU 권장 사항 가져오기를 AssessTargetReadiness를 사용 하 여 대상 준비 상태 평가 수행 합니다.   | N
|`/SourceConnections`    | 연결 문자열의 공백으로 구분 기호로 분리 된 목록입니다. 데이터베이스 이름 (초기 카탈로그) 선택 사항입니다. 데이터베이스 이름을 제공 하지, 모든 데이터베이스 원본에 평가 됩니다.   | Y <br> (작업 'AssessTargetReadiness' 인 경우 필수)
|`/TargetReadinessConfiguration`    | 전체 경로 이름, 원본 연결 및 결과 파일에 대 한 값을 설명 하는 XML 파일입니다.   | Y <br> (TargetReadinessConfiguration 또는 SourceConnections 필요)
|`/FeatureDiscoveryReportJson`    | 기능 검색 보고서 JSON 경로입니다. 이 파일을 생성 하는 경우 다음 사용할 수 원본에 연결 하지 않고 대상 준비 상태 평가 다시 실행 합니다. | N
|`/ImportFeatureDiscoveryReportJson`    | 이전에 만든 기능 검색 JSON 보고서에 대 한 경로입니다. 원본 연결 대신이 파일이 사용 됩니다.   | N

## <a name="examples-of-assessments-using-the-cli"></a>CLI를 사용 하 여 평가의 예

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Windows 인증 및 실행 호환성 규칙을 사용 하 여 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**SQL Server 인증 및 실행 기능 권장 사항을 사용 하 여 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**SQL Server 2012를 대상 플랫폼에 대 한 단일 데이터베이스 평가.json 및.csv 파일로 결과 저장**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**대상 플랫폼이 SQL Azure 데이터베이스에 대 한 단일 데이터베이스 평가.json 및.csv 파일로 결과 저장**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="AzureSqlDatabaseV12"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"
```

**여러 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```

**Windows 인증을 사용 하 여 단일 데이터베이스 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**SQL Server 인증을 사용 하 여 단일 데이터베이스 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**대상 플랫폼이 SQL Azure 데이터베이스에 대 한 단일 데이터베이스 평가.json 및.csv 파일로 결과 저장**

```
DmaCmd.exe /AssessmentName="TestAssessment" 
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentSourcePlatform="SqlOnPrem"
/AssessmentTargetPlatform="AzureSqlDatabase"
/AssessmentEvaluateCompatibilityIssues /AssessmentEvaluateFeatureParity
/AssessmentOverwriteResult 
/AssessmentResultCsv="C:\\temp\\AssessmentReport.csv" 
/AssessmentResultJson="C:\\temp\\AssessmentReport.json"

```

**여러 데이터베이스 대상 준비 상태 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/AssessmentSourcePlatform=SourcePlatform
/AssessmentTargetPlatform=TargetPlatform
/SourceConnections="Server=SQLServerInstanceName1;Initial Catalog=DatabaseName1;Integrated Security=true" "Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated Security=true" "Server=SQLServerInstanceName2;Initial Catalog=DatabaseName3;Integrated Security=true"
/AssessmentOverwriteResult  
/AssessmentResultJson="C:\Results\test2016.json"

(/AssessmentSourcePlatform and /AssessmentTargetPlatform are optional.)
```

**Windows 인증을 사용 하 여 서버의 모든 데이터베이스에 대 한 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**이전에 만든 기능 검색 보고서를 가져와서 대상 준비 상태 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**구성 파일을 제공 하 여 대상 준비 상태 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

구성 파일 내용을 사용 하는 경우 원본 연결:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <SourcePlatform>Source Platform</SourcePlatform> <!-- Optional. The default is SqlOnPrem -->
  <TargetPlatform>TargetPlatform</TargetPlatform> <!-- Optional. The default is ManagedSqlServer -->
  <SourceConnections>
    <SourceConnection>connection string 1</SourceConnection>
    <SourceConnection>connection string 2</SourceConnection>
    <!-- ... -->
    <SourceConnection>connection string n</SourceConnection>
  </SourceConnections>
  <AssessmentResultJson>path\to\file.json</AssessmentResultJson>
  <FeatureDiscoveryReportJson>path\to\featurediscoveryreport.json</FeatureDiscoveryReportJson>
  <OverwriteResult>true</OverwriteResult> <!-- or false -->
</TargetReadinessConfiguration>
```

구성 파일 내용 기능 검색 보고서를 가져올 때:

```
<TargetReadinessConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>Azure SQL Database/관리 되는 인스턴스 SKU 권장 CLI를 사용 하 여

이러한 명령은 Azure SQL Database 단일 데이터베이스와 관리 되는 인스턴스에 배포 옵션에 대 한 권장 사항을 지원합니다.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|인수  |Description  | 필수 (Y/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | DMA 명령줄을 사용 하 여 SKU 평가 실행 합니다. | Y
|`/SkuRecommendationInputDataFilePath` | 데이터베이스를 호스팅하는 컴퓨터에서 수집 된 성능 카운터 파일에 전체 경로 | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV 결과 파일에 전체 경로 | Y <br> (TSV 또는 JSON 또는 HTML 파일 경로가 필요)
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 결과 파일에 전체 경로 | Y <br> (TSV 또는 JSON 또는 HTML 파일 경로가 필요)
|`/SkuRecommendationHtmlResultsFilePath` | HTML 결과 파일에 전체 경로 | Y <br> (TSV 또는 JSON 또는 HTML 파일 경로가 필요)
|`/SkuRecommendationPreventPriceRefresh` | 발생 가격 새로 고침을 방지합니다. (예:, true) 오프 라인 모드에서 실행 하는 경우 사용 합니다. | Y <br> (정적 가격에 대 한이 두 인수 중 하나가 선택 하거나 아래 모든 인수를 최신 가격표를 선택 해야 합니다.)
|`/SkuRecommendationCurrencyCode` | (예: 가격을 표시 하는 통화 "USD") | Y <br> (대 한 최신 가격)
|`/SkuRecommendationOfferName` | 제품 이름 (예: "MS-AZR-0003P"). 자세한 내용은 참조는 [Microsoft Azure 제품 세부 정보](https://azure.microsoft.com/support/legal/offer-details/) 페이지입니다. | Y <br> (대 한 최신 가격)
|`/SkuRecommendationRegionName` | 지역 이름 (예: "미국 서 부") | Y <br> (대 한 최신 가격)
|`/SkuRecommendationSubscriptionId` | 구독 ID입니다. | Y <br> (대 한 최신 가격)
|`/SkuRecommendationDatabasesToRecommend` | 데이터베이스에 대 한 (예: 권장의 공백으로 구분 된 목록 "Database1" "Database2" "Database3"). 이름은 대/소문자 구분 되며 큰따옴표로 묶어야 합니다. 생략 하면 모든 데이터베이스에 대 한 권장 사항은 제공 됩니다. | N
|`/AzureAuthenticationTenantId` | Authentication 테 넌 트가 있습니다. | Y <br> (대 한 최신 가격)
|`/AzureAuthenticationClientId` | 인증에 사용 되는 AAD 앱의 클라이언트 ID입니다. | Y <br> (대 한 최신 가격)
|`/AzureAuthenticationInteractiveAuthentication` | 창을 표시 하려면 true로 설정 합니다. | Y <br> (대 한 최신 가격) <br>(옵션 1-3 인증 중 하나를 선택 하십시오.)
|`/AzureAuthenticationCertificateStoreLocation` | (예: 인증서 저장소 위치를 설정 "CurrentUser")입니다. | Y <br>(대 한 최신 가격) <br> (옵션 2-3 인증 중 하나를 선택 하십시오.)
|`/AzureAuthenticationCertificateThumbprint` | 인증서 지 문으로 설정 합니다. | Y <br> (대 한 최신 가격) <br>(옵션 2-3 인증 중 하나를 선택 하십시오.)
|`/AzureAuthenticationToken` | 인증서 토큰을 설정 합니다. | Y <br> (대 한 최신 가격) <br>(옵션 3 3 인증 옵션 중 하나를 선택)

## <a name="examples-of-sku-assessments-using-the-cli"></a>CLI를 사용 하는 SKU 평가의 예

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**Azure SQL DB/MI SKU 권장 사항 새로 고침 가격 (최신 get prices)-를 사용 하 여 대화형 인증** 

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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationInteractiveAuthentication=true 
```

**Azure SQL DB/MI SKU 권장 사항 새로 고침 가격 (최신 get prices)-를 사용 하 여 인증서 인증**

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
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationCertificateStoreLocation=<Your Certificate Store Location>
/AzureAuthenticationCertificateThumbprint=<Your Certificate Thumbprint>  
```

**가격 새로 고침 (가져오기 최신 prices)-를 사용 하 여 azure SQL DB SKU/MI 권장 사항 인증 토큰 및 권장 하는 데이터베이스를 지정 합니다.**
  
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationCurrencyCode=USD
/SkuRecommendationOfferName=MS-AZR-0044p
/SkuRecommendationRegionName=UKWest
/SkuRecommendationDatabasesToRecommend=“TPCDS1G,EDW_3G,TPCDS10G”
/SkuRecommendationSubscriptionId=<Your Subscription Id>
/AzureAuthenticationClientId=<Your AzureAuthenticationClientId>
/AzureAuthenticationTenantId=<Your AzureAuthenticationTenantId>
/AzureAuthenticationToken=<Your Authentication Token> 
```

**가격 새로 고침 (사용 하 여 정적 prices) 없이 azure SQL DB/MI SKU 권장 사항** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>참고자료
- [Data Migration Assistant](https://aka.ms/get-dma) 다운로드 합니다.
- 이 문서 [온-프레미스 데이터베이스에 대 한 올바른 Azure SQL 데이터베이스 SKU 확인](https://aka.ms/dma-sku-recommend-sqldb)합니다.
