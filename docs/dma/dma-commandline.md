---
title: "(SQL Server 데이터 Migration Assistant) 명령줄에서 실행 | Microsoft Docs"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Command Line
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6147d01802a363082baf27d6b909e2c98f9afef2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>실행 명령줄에서 데이터 마이그레이션 길잡이
데이터 마이그레이션 도우미를 설치 버전 2.1 이상에서 때도 설치 됩니다. dmacmd.exe에 *% ProgramFiles %\\Microsoft 데이터 마이그레이션 길잡이\\*합니다. Dmacmd.exe를 사용 하 여 무인된 모드에서 데이터베이스를 평가 하 고 JSON 또는 CSV 파일에 결과 출력 합니다. 여러 데이터베이스 또는 대규모 데이터베이스에 액세스할 때 특히 유용 합니다. 

> [!NOTE]
> 만 평가 실행 하는 Dmacmd.exe 지원 합니다. 이 이번에는 마이그레이션이 지원 되지 않습니다.


## <a name="command-line-arguments"></a>명령줄 인수

```
DmaCmd.exe /AssessmentName="string"
/AssessmentDatabases="connectionString1" \["connectionString2"\]
\[/AssessmentTargetPlatform="TargetPlatform"\]
/AssessmentEvaluateRecommendations|/AssessmentEvaluateCompatibilityIssues
\[/AssessmentOverwriteResult\]
/AssessmentResultJson="file"|/AssessmentResultCsv="file"
```


|인수  |Description  | 필수 (Y/N)
|---------|---------|---------------|
| `/help or /?`     | Dmacmd.exe 도움말 텍스트를 사용 하는 방법        | N
|`/AssessmentName`     |   평가 프로젝트의 이름   | Y
|`/AssessmentDatabases`     | 공간에는 연결 문자열 목록을 구분합니다. 데이터베이스 이름 (초기 카탈로그)은 대/소문자 구분 합니다. | Y
|`/AssessmentTargetPlatform`     | 대상 플랫폼을 평가, 지원 되는 값: SqlServer2012, SqlServer2014, SqlServer2016 및 AzureSqlDatabaseV12 합니다. 기본값은 SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | 기능 패리티 규칙 실행  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 호환성 규칙을 실행 합니다.  | Y <br> (AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendations이 필요 함.)
|`/AssessmentEvaluateRecommendations`     | 기능 권장 사항 실행        | Y <br> (AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendationsis 필요)
|`/AssessmentOverwriteResult`     | 결과 파일 덮어쓰기    | N
|`/AssessmentResultJson`     | JSON 결과 파일 전체 경로를     | Y <br> (AssessmentResultJson 또는 AssessmentResultCsv이 필요 함)
|`/AssessmentResultCsv`    | CSV 결과 파일 전체 경로를   | Y <br>(AssessmentResultJson 또는 AssessmentResultCsv이 필요 함)




## <a name="examples"></a>예

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Windows 인증 및 실행 되 고 호환성 규칙을 사용 하 여 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**SQL Server 인증 및 실행 기능 추천을 사용 하 여 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**단일 데이터베이스 평가 대상 플랫폼 SQL Server 2012에 대 한 고.json 및.csv 파일로 결과 저장**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
```


**대상 플랫폼이 SQL Azure 데이터베이스에 대 한 단일 데이터베이스 평가 결과.json 및.csv 파일에 저장**

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
***/AssessmentDatabases="Server=SQLServerInstanceName1;Initial
Catalog=DatabaseName1;Integrated Security=true"
"Server=SQLServerInstanceName1;Initial Catalog=DatabaseName2;Integrated
Security=true" "Server=SQLServerInstanceName2;Initial
Catalog=DatabaseName3;Integrated Security=true"***
/AssessmentTargetPlatform="SqlServer2016"
/AssessmentEvaluateCompatibilityIssues /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
/AssessmentResultJson="C:\\Results\\test2016.json"
```



## <a name="see-also"></a>관련 항목:

[데이터 마이그레이션 길잡이 다운로드](https://www.microsoft.com/download/details.aspx?id=53595)
