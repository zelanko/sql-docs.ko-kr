---
title: Data Migration Assistant (SQL Server) 명령줄에서 실행 | Microsoft Docs
description: 마이그레이션에 대 한 SQL Server 데이터베이스를 평가 하기 위해 명령줄에서 Data Migration Assistant를 실행 하는 방법 알아보기
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Command Line
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 6b364dc03d48cbc1c0487362712e10f7ab0b782e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785464"
---
# <a name="run-data-migration-assistant-from-the-command-line"></a>명령줄에서 Data Migration Assistant 실행
Data Migration Assistant 설치 버전 2.1 이상에서 시기, dmacmd.exe에도 설치 됩니다 *% ProgramFiles %\\Microsoft Data Migration Assistant\\*합니다. Dmacmd.exe를 사용 하 여 무인된 모드에서 데이터베이스를 평가 및 JSON 또는 CSV 파일로 결과 출력 합니다. 이 메서드는 여러 데이터베이스 또는 대규모 데이터베이스를 평가할 때 특히 유용 합니다. 

> [!NOTE]
> Dmacmd.exe 실행 중인 평가 지원합니다. 이 이번에는 마이그레이션이 지원 되지 않습니다.


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
|`/AssessmentDatabases`     | 연결 문자열의 공백으로 구분 된 목록입니다. 데이터베이스 이름 (초기 카탈로그)은 대/소문자 구분 합니다. | Y
|`/AssessmentTargetPlatform`     | 평가 지원 되는 값에 대 한 대상 플랫폼: SqlServer2012, SqlServer2014, SqlServer2016, 및 AzureSqlDatabaseV12 합니다. 기본값은 SqlServer2016   | N
|`/AssessmentEvaluateFeatureParity`  | 기능 패리티 규칙을 실행  | N
|`/AssessmentEvaluateCompatibilityIssues`     | 호환성 규칙을 실행  | Y <br> AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendations 이어서 필요 합니다.
|`/AssessmentEvaluateRecommendations`     | 기능 권장 사항 실행        | Y <br> (AssessmentEvaluateCompatibilityIssues 또는 AssessmentEvaluateRecommendationsis 필요)
|`/AssessmentOverwriteResult`     | 결과 파일 덮어쓰기    | N
|`/AssessmentResultJson`     | JSON 결과 파일에 전체 경로     | Y <br> (AssessmentResultJson 또는 AssessmentResultCsv 필요)
|`/AssessmentResultCsv`    | CSV 결과 파일에 전체 경로   | Y <br>(AssessmentResultJson 또는 AssessmentResultCsv 필요)




## <a name="examples"></a>예

**Dmacmd.exe**

  `Dmacmd.exe /? or DmaCmd.exe /help`

**Windows 인증 및 실행 호환성 규칙을 사용 하 여 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***Integrated Security=true*"**
***/AssessmentEvaluateCompatibilityIssues*** /AssessmentOverwriteResult
/AssessmentResultJson="C:\\temp\\Results\\AssessmentReport.json"
```



**SQL Server 인증 및 실행 기능 권장 사항을 사용 하 여 단일 데이터베이스 평가**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;***User Id=myUsername;Password=myPassword;***"
***/AssessmentEvaluateRecommendations*** /AssessmentOverwriteResult
/AssessmentResultCsv="C:\\temp\\Results\\AssessmentReport.csv"
```


**SQL Server 2012를 대상 플랫폼에 대 한 단일 데이터베이스 평가.json 및.csv 파일로 결과 저장**

```
DmaCmd.exe /AssessmentName="TestAssessment"
/AssessmentDatabases="Server=SQLServerInstanceName;Initial
Catalog=DatabaseName;Integrated Security=true"
***/AssessmentTargetPlatform="SqlServer2012"***
/AssessmentEvaluateRecommendations /AssessmentOverwriteResult
***/AssessmentResultJson***="C:\\temp\\Results\\AssessmentReport.json"
***/AssessmentResultCsv***="C:\\temp\\Results\\AssessmentReport.csv"
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



## <a name="see-also"></a>참고자료

[Data Migration Assistant 다운로드](https://www.microsoft.com/download/details.aspx?id=53595)
