---
title: 명령줄에서 Data Migration Assistant 실행 (SQL Server) | Microsoft Docs
description: 명령줄에서 Data Migration Assistant를 실행 하 여 마이그레이션을 위해 SQL Server 데이터베이스를 평가 하는 방법을 알아봅니다.
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
ms.openlocfilehash: f98d96547a367dcf7853a5b0d7c14b2d79b7df63
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028710"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>명령줄에서 Data Migration Assistant 실행

Data Migration Assistant 설치 버전 2.1 이상에서 시기, dmacmd.exe에도 설치 됩니다 *\% ProgramFiles %\\Microsoft Data Migration Assistant\\* 합니다. Node.js를 사용 하 여 무인 모드에서 데이터베이스를 평가 하 고 그 결과를 JSON 또는 CSV 파일에 출력 합니다. 이 방법은 여러 데이터베이스 또는 방대한 데이터베이스를 평가할 때 특히 유용 합니다. 

> [!NOTE]
> Node.js는 평가 실행만 지원 합니다. 지금은 마이그레이션이 지원 되지 않습니다.

## <a name="assessments-using-the-command-line-interface-cli"></a>CLI (명령줄 인터페이스)를 사용 하 여 평가

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentSourcePlatform="SourcePlatform"]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```

|인수  |설명  | 필수 (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Node.js 도움말 텍스트를 사용 하는 방법        | N
|`/AssessmentName`     |   평가 프로젝트의 이름입니다.   | Y
|`/AssessmentDatabases`     | 공백으로 구분 된 연결 문자열 목록입니다. 데이터베이스 이름 (초기 카탈로그)은 대/소문자를 구분 합니다. | Y
|`/AssessmentSourcePlatform`     | 평가를 위한 원본 플랫폼: <br>평가에 대해 지원 되는 값: SqlOnPrem, RdsSqlServer (기본값) <br>대상 준비 평가에 대해 지원 되는 값: SqlOnPrem, RdsSqlServer (기본값), Cassandra (미리 보기)   | N
|`/AssessmentTargetPlatform`     | 평가를 위한 대상 플랫폼:  <br> 평가에 대해 지원 되는 값: AzureSqlDatabase, ManagedSqlServer, SqlServer2012, SqlServer2014, Sqlserver2016-ssei-expr, SqlServerLinux2017 및 SqlServerWindows2017 (기본값)  <br> 대상 준비 평가에 대해 지원 되는 값: ManagedSqlServer (기본값), CosmosDB (미리 보기)   | N
|`/AssessmentEvaluateFeatureParity`  | 기능 패리티 규칙을 실행 합니다. 원본 플랫폼이 RdsSqlServer 인 경우 대상 플랫폼 AzureSqlDatabase에 대해 기능 패리티 평가가 지원 되지 않습니다.  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 호환성 규칙 실행  | Y <br> AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendations가 필요 합니다.
|`/AssessmentEvaluateRecommendations`     | 기능 권장 사항 실행        | Y <br> (AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendations가 필요 합니다.)
|`/AssessmentOverwriteResult`     | 결과 파일 덮어쓰기    | N
|`/AssessmentResultJson`     | JSON 결과 파일의 전체 경로입니다.     | Y <br> (AssessmentResultJson 또는 AssessmentResultCsv가 필요 합니다.)
|`/AssessmentResultCsv`    | CSV 결과 파일의 전체 경로입니다.   | Y <br> (AssessmentResultJson 또는 AssessmentResultCsv가 필요 합니다.)
|`/Action`    | AssessTargetReadiness을 사용 하 여 목표 준비를 평가 하 고, 대상 준비 평가를 수행 하려면 작동 하지 않는 U권장 사항을 사용 하세요.   | N
|`/SourceConnections`    | 공백으로 구분 된 연결 문자열 목록입니다. 데이터베이스 이름 (초기 카탈로그)은 선택 사항입니다. 데이터베이스 이름을 제공 하지 않으면 원본의 모든 데이터베이스가 평가 됩니다.   | Y <br> (작업이 ' AssessTargetReadiness ' 인 경우 필수)
|`/TargetReadinessConfiguration`    | 이름, 원본 연결 및 결과 파일에 대 한 값을 설명 하는 XML 파일의 전체 경로입니다.   | Y <br> TargetReadinessConfiguration 또는 SourceConnections가 필요 합니다.
|`/FeatureDiscoveryReportJson`    | 기능 검색 JSON 보고서의 경로입니다. 이 파일이 생성 되 면 원본에 연결 하지 않고 대상 준비 평가를 다시 실행 하는 데 사용할 수 있습니다. | N
|`/ImportFeatureDiscoveryReportJson`    | 이전에 만든 기능 검색 JSON 보고서의 경로입니다. 원본 연결 대신이 파일이 사용 됩니다.   | N

## <a name="examples-of-assessments-using-the-cli"></a>CLI를 사용 하는 평가 예

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Windows 인증을 사용 하는 단일 데이터베이스 평가 및 호환성 규칙 실행**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```

**SQL Server 인증을 사용 하 고 기능 권장 사항을 실행 하는 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;User Id=myUsername;Password=myPassword;"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**대상 플랫폼 SQL Server 2012에 대 한 단일 데이터베이스 평가, json 및 .csv 파일에 결과 저장**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
/AssessmentTargetPlatform="SqlServer2012"
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```

**대상 플랫폼 SQL Azure 데이터베이스에 대 한 단일 데이터베이스 평가, json 및 .csv 파일에 결과 저장**

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

**다중 데이터베이스 평가**

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

**Windows 인증을 사용한 단일 데이터베이스 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;Integrated Security=true" 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"
```

**SQL Server 인증을 사용 하는 단일 데이터베이스 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/AssessmentName="TestAssessment" 
/SourceConnections="Server=SQLServerInstanceName;Initial Catalog=DatabaseName;User Id=myUsername;Password=myPassword;" /AssessmentEvaluateRecommendations 
/AssessmentOverwriteResult 
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json" 

```

**대상 플랫폼 SQL Azure 데이터베이스에 대 한 단일 데이터베이스 평가, json 및 .csv 파일에 결과 저장**

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

**다중 데이터베이스 대상 준비 평가**

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

**Windows 인증을 사용 하는 서버의 모든 데이터베이스에 대 한 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/SourceConnections="Server=SQLServerInstanceName;Integrated Security=true"
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**이전에 만든 기능 검색 보고서를 가져와 대상 준비 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness
/AssessmentName="TestAssessment"
/ImportFeatureDiscoveryReportJson="c:\temp\feature_report.json" 
/AssessmentOverwriteResult
/AssessmentResultJson="C:\temp\Results\AssessmentReport.json"

```

**구성 파일을 제공 하 여 대상 준비 평가 평가**

```
DmaCmd.exe /Action=AssessTargetReadiness 
/TargetReadinessConfiguration=.\Config.xml
```

원본 연결을 사용할 때의 구성 파일 내용:

```
<?xml version="1.0" encoding="utf-8" ?>
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
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

기능 검색 보고서를 가져올 때 구성 파일 내용:

```
<TargetReadinessConfiguration xmlns="https://microsoft.com/schemas/SqlServer/Advisor/TargetReadinessConfiguration">
  <AssessmentName>name</AssessmentName>
  <ImportFeatureDiscoveryReportJson>path\to\featurediscoveryfile.json</ImportFeatureDiscoveryReportJson>
  <AssessmentResultJson>path\to\resultfile.json</AssessmentResultJson>
  <OverwriteResult>true</OverwriteResult><!-- or false -->
</TargetReadinessConfiguration>
```

## <a name="azure-sql-databasemanaged-instance-sku-recommendations-using-the-cli"></a>CLI를 사용 하 여 Azure SQL Database/관리 되는 인스턴스 SKU 권장 사항

이러한 명령은 Azure SQL Database 단일 데이터베이스 및 관리 되는 인스턴스 배포 옵션 모두에 대 한 권장 사항을 지원 합니다.

```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true 
```

|인수  |설명  | 필수 (Y/N)
|---------|---------|---------------|
|`/Action=SkuRecommendation` | DMA 명령줄을 사용 하 여 SKU 평가 실행 | Y
|`/SkuRecommendationInputDataFilePath` | 데이터베이스를 호스트 하는 컴퓨터에서 수집 된 성능 카운터 파일의 전체 경로입니다. | Y
|`/SkuRecommendationTsvOutputResultsFilePath` | TSV 결과 파일의 전체 경로입니다. | Y <br> TSV 또는 JSON 또는 HTML 파일 경로 중 하나를 사용 해야 합니다.
|`/SkuRecommendationJsonOutputResultsFilePath` | JSON 결과 파일의 전체 경로입니다. | Y <br> TSV 또는 JSON 또는 HTML 파일 경로 중 하나를 사용 해야 합니다.
|`/SkuRecommendationHtmlResultsFilePath` | HTML 결과 파일의 전체 경로입니다. | Y <br> TSV 또는 JSON 또는 HTML 파일 경로 중 하나를 사용 해야 합니다.
|`/SkuRecommendationPreventPriceRefresh` | 가격 새로 고침이 발생 하지 않도록 합니다. 오프 라인 모드에서 실행 하는 경우 (예: true)을 사용 합니다. | Y <br> (정적 가격에 대 한이 인수 또는 모든 인수를 선택 해야 최신 가격을 가져올 수 있습니다.)
|`/SkuRecommendationCurrencyCode` | 가격을 표시할 통화 (예: "USD") | Y <br> (최신 가격)
|`/SkuRecommendationOfferName` | 제품 이름 (예: "MS-AZR-0003P"). 자세한 내용은 [Microsoft Azure 제품 세부 정보](https://azure.microsoft.com/support/legal/offer-details/) 페이지를 참조 하세요. | Y <br> (최신 가격)
|`/SkuRecommendationRegionName` | 영역 이름 (예: "WestUS") | Y <br> (최신 가격)
|`/SkuRecommendationSubscriptionId` | 구독 ID입니다. | Y <br> (최신 가격)
|`/SkuRecommendationDatabasesToRecommend` | 에 대해 권장 되는 데이터베이스의 공백으로 구분 된 목록 (예: "Database1" "Database2" "Database3"). 이름은 대/소문자를 구분 하며 큰따옴표로 묶어야 합니다. 생략 하는 경우 모든 데이터베이스에 대 한 권장 사항이 제공 됩니다. | N
|`/AzureAuthenticationTenantId` | 인증 테 넌 트입니다. | Y <br> (최신 가격)
|`/AzureAuthenticationClientId` | 인증에 사용 되는 AAD 앱의 클라이언트 ID입니다. | Y <br> (최신 가격)
|`/AzureAuthenticationInteractiveAuthentication` | 창을 팝업 하려면 true로 설정 합니다. | Y <br> (최신 가격) <br>3 인증 옵션 중 하나를 선택 합니다.-옵션 1
|`/AzureAuthenticationCertificateStoreLocation` | 인증서 저장소 위치 (예:)로 설정 합니다. "CurrentUser"). | Y <br>(최신 가격) <br> (3 인증 옵션 중 하나 선택-옵션 2)
|`/AzureAuthenticationCertificateThumbprint` | 인증서 지 문으로 설정 합니다. | Y <br> (최신 가격) <br>(3 인증 옵션 중 하나 선택-옵션 2)
|`/AzureAuthenticationToken` | 인증서 토큰으로 설정 합니다. | Y <br> (최신 가격) <br>(3 개의 인증 옵션 중 하나 선택-옵션 3)

## <a name="examples-of-sku-assessments-using-the-cli"></a>CLI를 사용 하는 SKU 평가 예

**Dmacmd.exe**

`Dmacmd.exe /? or DmaCmd.exe /help`

**가격 새로 고침을 사용한 Azure SQL DB/MI SKU 권장 사항 (최신 가격 가져오기)-대화형 인증** 

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

**가격 새로 고침을 사용한 Azure SQL DB/MI SKU 권장 사항 (최신 가격 가져오기)-인증서 인증**

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

**가격 새로 고침 (최신 가격 가져오기)이 포함 된 Azure SQL DB SKU/MI 권장 사항-토큰 인증 및 권장 되는 데이터베이스 지정**
  
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

**가격 새로 고침 없이 Azure SQL DB/MI SKU 권장 사항 (정적 가격 사용)** 
```
.\DmaCmd.exe /Action=SkuRecommendation
/SkuRecommendationInputDataFilePath="C:\TestOut\out.csv"
/SkuRecommendationTsvOutputResultsFilePath="C:\TestOut\prices.tsv"
/SkuRecommendationJsonOutputResultsFilePath="C:\TestOut\prices.json"
/SkuRecommendationOutputResultsFilePath="C:\TestOut\prices.html"
/SkuRecommendationPreventPriceRefresh=true  
```

## <a name="see-also"></a>참조
- 다운로드를 [Data Migration Assistant](https://aka.ms/get-dma) 합니다.
- 이 문서에서는 [온-프레미스 데이터베이스에 적합 한 AZURE SQL DATABASE SKU를 식별](https://aka.ms/dma-sku-recommend-sqldb)합니다.
