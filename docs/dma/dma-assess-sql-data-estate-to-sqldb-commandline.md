---
title: Azure SQL로 마이그레이션할 SQL Server 준비 상태 평가
titleSuffix: Data Migration Assistant
description: Data Migration Assistant 명령줄 도구 (DMACMD)를 사용 하 여 Azure SQL로 마이그레이션할 SQL Server 데이터 공간을 평가 하는 방법을 알아봅니다.
ms.date: 10/02/2020
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: ''
ms.openlocfilehash: a631ed40344fc8661cef23b9758aa35feb041c45
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91729260"
---
# <a name="dmacmd-assess-readiness-of-a-sql-server-data-estate-migrating-to-azure-sql-database"></a>DMACMD: Azure SQL Database으로 마이그레이션하는 SQL Server 데이터 공간 준비 평가 

많은 조직에서 Azure로 마이그레이션하려는 경우 기존 온-프레미스 SQL Server 인스턴스를 평가 하 고 Azure Vm에서 올바른 Azure SQL 대상 Azure SQL Database, Azure SQL Managed Instance 또는 SQL Server를 식별 하는 것이 중요 합니다. 

[Data Migration Assistant (DMA)](dma-overview.md) 는 특정 azure sql 대상에 대 한 SQL Server 인스턴스를 평가 하 고, azure sql로 마이그레이션하는 SQL Server 데이터베이스의 준비 상태를 측정 하는 데 도움이 됩니다. 전체 데이터 공간에 대 한 중앙 집중식 준비 보기를 위해 DMA 평가 결과를 Azure Migrate 허브에 업로드 합니다. 

이 문서에서는 대규모로 평가를 수행 하 고 DMA 명령줄 인터페이스 (DMACMD)를 사용 하 여 Azure Migrate 허브에 결과를 업로드 하는 방법을 설명 합니다. 또는 [DMA GUI](dma-assess-sql-data-estate-to-sqldb.md) 를 사용 하 여 평가를 대신 수행할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항 

DMACMD를 사용 하 여 평가를 수행 하 고 결과를 Azure Migrate 허브에 업로드 하려면 다음이 필요 합니다. 

- [Data Migration Assistant (DMA)의 최신 버전](https://www.microsoft.com/en-us/download/details.aspx?id=53595)입니다.
- [Azure Migrate 프로젝트](dma-assess-sql-data-estate-to-sqldb.md#create-a-project-and-add-a-tool)입니다. 
- Azure Migrate 프로젝트 리소스에 대 한 참가자 역할 액세스입니다.

## <a name="use-dmacmd"></a>DMACMD 사용

XML 파일을 입력으로 사용 하 여 명령줄 인터페이스 (DMACMD.exe)를 통해 대규모로 평가를 실행 합니다. 

다음 샘플 명령을 사용 하 여 XML 파일을 DMACMD에 전달 하 고 평가를 시작 합니다.

```console
C:\Program Files\Microsoft Data Migration Assistant\DmaCmd.exe /Action=Assess /AssessmentConfiguration= C:\Demo\ScaleAssessment\Assess-for-AzureSQLMI.xml
```

샘플의 내용은 `Assess-for-AzureSQLMI.xml` SQL Managed Instance 대상의 SQL Server 인스턴스를 평가 하는 요소를 정의 합니다. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<AssessmentConfiguration xmlns="http://microsoft.com/schemas/SqlServer/Advisor/AssessmentConfiguration">
   <AssessmentName>Scale-Assessment-for-AzureSQLManagedInstance</AssessmentName>
   <AssessmentSourcePlatform>SqlOnPrem</AssessmentSourcePlatform>
   <AssessmentTargetPlatform>ManagedSqlServer</AssessmentTargetPlatform>
   <AssessmentDatabases>
      <AssessmentDatabase>Server=ServerName\SQL2017;Integrated Security=true</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=AdventureWorks2016</AssessmentDatabase>
      <AssessmentDatabase>Server=ServerName\SQL2016;Integrated Security=true;Initial Catalog=TestDB</AssessmentDatabase>
   </AssessmentDatabases>
   <AssessmentResultDma>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.dma</AssessmentResultDma>
   <AssessmentResultJson>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.json</AssessmentResultJson>
   <AssessmentResultCsv>C:\Demo\ScaleAssessment\AssessmentConfiguration\Scale-Assessment-for-AzureSQLManagedInstance.csv</AssessmentResultCsv>
   <AssessmentOverwriteResult>true</AssessmentOverwriteResult>
   <AssessmentEvaluateCompatibilityIssues>true</AssessmentEvaluateCompatibilityIssues>
   <AssessmentEvaluateFeatureParity>true</AssessmentEvaluateFeatureParity>
   <AzureCloudEnvironment>Azure</AzureCloudEnvironment>
   <SubscriptionId>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx</SubscriptionId>
   <AzureMigrateProjectName>Scale-Assessment-for-AzureSQLMI</AzureMigrateProjectName>
   <ResourceGroupName>Resource-Group-Name</ResourceGroupName>
   <AzureAuthenticationInteractiveAuthentication>true</AzureAuthenticationInteractiveAuthentication>
   <AzureAuthenticationTenantId>xxxxxxxx-xxxx-xxxxxxxx</AzureAuthenticationTenantId>
   <EnableAssessmentUploadToAzureMigrate>true</EnableAssessmentUploadToAzureMigrate>
</AssessmentConfiguration>
```



## <a name="xml-elements"></a>XML 요소 

다음 표에서는 DMACMD에 전달 되는 XML 요소를 정의 합니다. 


|**XML 요소** |**정의**  |
|---------|---------|
|`AssessmentName`|평가 이름|
|`AssessmentSourcePlatform`|원본 SQL Server 플랫폼입니다. 기본값은 `SqlOnPrem`입니다.|
|`AssessmentTargetPlatform`|대상 SQL Server 플랫폼입니다.  </br> `AzureSqlDatabase` 는 Azure SQL Database 대상입니다. </br> `ManagedSqlServer` 는 Azure SQL Managed Instance 대상입니다. </br></br>**AzureSQLMI** 평가 샘플은 SQL Managed Instance 대상을 평가 합니다.|
|`AssessmentDatabases`|인스턴스의 모든 데이터베이스를 평가 해야 하는 경우에는 인스턴스 이름만 지정 하 고 각 줄에 특정 데이터베이스를 나열 합니다. </br></br>**AzureSQLMI 평가** 샘플에서는 인스턴스의 모든 데이터베이스 `Servername\SQL2017` 와 인스턴스의 두 개의 특정 데이터베이스를 평가 합니다 `Servername\SQL2016` .  |
|`AssessmentResultDma` </br> `AssessmentResultJson` </br> `AssessmentResultCsv` | 결과 파일의 형식을 지정 합니다. `.DMA``.JSON`각각, 및가 `.CSV` 있습니다. 를 두 번 클릭 `.DMA` 하 여 DMA UI에서 엽니다. <br> `AssessmentResultDma` 는 Azure Migrate 허브에 평가 결과를 업로드 하는 데 필요 합니다.  |
|`AssessmentOverwriteResult`| , 또는와 동일한 경로를 사용 하 여 기존 평가 결과 파일을 덮어쓸지 여부를 나타냅니다 `AssessmentResultJson` `AssessmentResultDma` `AssessmentResultCsv` .|
|`AssessmentEvaluateCompatibilityIssues` </br> `AssessmentEvaluateFeatureParity` |평가를 수행 하 여 각각 호환성 문제와 기능 패리티 문제를 평가 합니다.|
|`AzureCloudEnvironment`|연결할 azure 클라우드 환경, 기본값은 Azure 공용 클라우드입니다. </br></br> 지원되는 값: </br>`Azure (default)`, `AzureChina`, `AzureGermany`, `AzureUSGovernment`.|
|`SubscriptionId`|Azure 구독 ID입니다.|
|`AzureMigrateProjectName`|평가 결과를 업로드 하기 위한 프로젝트 이름을 Azure Migrate 합니다.|
|`ResourceGroupName`|리소스 그룹 이름을 Azure Migrate 합니다.|
|`AzureAuthenticationInteractiveAuthentication`|`true`인증 창을 팝업 하려면로 설정 합니다.|
|`AzureAuthenticationTenantId`|Azure Active Directory 테넌트 ID입니다. </br></br>[Azure Portal](https://portal.azure.com)에서 Azure Active Directory의 **개요** 블레이드에서이를 가져옵니다. |
|`EnableAssessmentUploadToAzureMigrate`| 로 설정 하 여 `true` 평가 결과를 업로드 하 고 Azure Migrate 허브에 게시 합니다.|
|   |   |


## <a name="results"></a>결과 

성공적으로 완료 되 면 DMACMD가 상태를 출력 합니다. 


예제 결과 출력은 다음과 같습니다. 

```console
Assessment finished for project: Scale-Assessment-for-AzureSQLManagedInstance
DATABASES:
Succeeded             : 4
Failed                : 0
SERVER INSTANCES:
Succeeded             : 2
Failed                : 0
CSV result file       : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.csv
JSON result file      : C:\Demo\ScaleAssessment\Scale-Assessment-for-AzureSQLManagedInstance.json
--------------------------------------------------------------------------------
```

전체 데이터 공간에 대 한 중앙 집중식 보기를 위해 [Azure Migrate](dma-assess-sql-data-estate-to-sqldb.md#view-target-readiness-assessment-results) 업로드 된 결과를 봅니다. . 

## <a name="best-practices"></a>모범 사례 

다음 모범 사례를 참조 하세요. 

- 전체 데이터 공간에서 모든 SQL Server 인스턴스를 평가 하는 대신 응용 프로그램을 기반으로 대상 SQL Server 인스턴스 및 데이터베이스를 논리적으로 그룹화 합니다. 
- 결과 덮어쓰기를 방지 하기 위해 각 Azure SQL 대상에 대해 별도의 Azure Migrate 프로젝트를 만듭니다. 
- 평가를 실행 하는 데 걸리는 시간은 데이터베이스 개체의 수에 따라 달라 집니다. 가능 하면 특히 많은 수의 개체가 있는 데이터베이스의 경우 프로덕션 시스템에서 평가를 실행 하 고 가상 머신 또는 스테이징 서버로 오프 로드 하지 않도록 합니다. 


## <a name="see-also"></a>참고 항목

* [DMA(Data Migration Assistant)](../dma/dma-overview.md)
* [Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
* [Data Migration Assistant: 모범 사례](../dma/dma-bestpractices.md)
