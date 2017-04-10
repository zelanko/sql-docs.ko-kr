---
title: "Invoke-ProcessTable cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessTable cmdlet
  특정 **RefreshType** 이 있는 **Table** 에서 **Process**작업을 수행합니다.  
  
 이 cmdlet는 SQL Server 2016 호환성 수준 1200에서 테이블 형식 모델에만 적용됩니다.  
  
## 구문  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## 매개 변수  
  
### -TableName \<string>  
 처리해야 하는 파티션이 속한 테이블의 이름입니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -DatabaseName \<string>  
 테이블이 속한 데이터베이스를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Server\<Microsoft.AnalysisSevices.Server>  
 컨텍스트에 **SQLAS** 공급자 디렉터리를 사용하지 않는 경우에는 연결한 서버 인스턴스를 선택적으로 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -RefreshType \<Microsoft.AnalysisServices.RefreshType>  
 호환성 수준 1200에서 테이블 형식 데이터베이스의 처리 유형을 지정합니다.  유효한 값은 Full, ClearValues, Calculate, DataOnly, Automatic, Add, 및 Defragment입니다. 설명 및 지침은 [데이터베이스, 테이블 또는 파티션 처리&#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)를 참조하세요.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Credential  
 이 매개 변수를 지정하면 전달된 사용자 이름 및 암호를 사용하여 Analysis Server 인스턴스에 연결합니다. 자격 증명을 지정하지 않으면 스크립트를 실행하는 사용자의 기본 Windows 계정으로 간주됩니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Whatif  
 연산을 실행하기 전에 연산의 영향에 대한 정보를 가져오려면 이 매개 변수를 포함합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Confirm  
 연산을 실행하기 전에 예 또는 아니오 응답으로 연산을 확인하려면 이 매개 변수를 포함합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치||  
|기본값||  
|파이프라인 입력 허용||  
|와일드카드 문자 허용|false|  
  
## 예제 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 이 명령은 처리할 테이블의 ID를 파이프합니다.  
  
## 예제 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 이 명령은 **enum** 새로 고침 유형을 사용하여 테이블 형식 메타데이터 테이블을 처리합니다.  
  
## 관련 항목:  
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  