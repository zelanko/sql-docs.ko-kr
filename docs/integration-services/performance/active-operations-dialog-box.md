---
title: "활성 작업 대화 상자 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.isoperations.executions.f1"
  - "sql13.ssis.ssms.isoperations.general.f1"
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 활성 작업 대화 상자
  **활성 작업** 대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 현재 실행 중인 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업(예: 배포, 유효성 검사 및 패키지 실행)의 상태를 볼 수 있습니다. 이 데이터는 SSISDB 카탈로그에 저장됩니다.  
  
 관련된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 뷰에 대한 자세한 내용은 [catalog.operations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md), [catalog.validations&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) 및 [catalog.executions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)를 참조하세요.  
  
 **수행 작업**  
  
-   [활성 작업 대화 상자 열기](../../integration-services/performance/active-operations-dialog-box.md#open_dialog)  
  
-   [옵션](#options)  
  
##  <a name="open_dialog"></a> 활성 작업 대화 상자 열기  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]열기  
  
2.  Microsoft SQL Server 데이터베이스 엔진 연결  
  
3.  개체 탐색기에서 **Integration Services** 노드를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **활성 작업**을 클릭합니다.  
  
## 옵션 구성  
  
###  <a name="options"></a> 옵션  
 **형식**  
 작업 유형을 지정합니다. 다음은 **유형** 필드의 가능한 값과 Transact-SQL **catalog.operations** 뷰의 operations_type 열에 표시되는 해당 값입니다.  
  
|||  
|-|-|  
|Integration Services 초기화|1.|  
|작업 정리(SQL 에이전트 작업)|2|  
|프로젝트 버전 정리(SQL 에이전트 작업)|3|  
|프로젝트 배포|101|  
|프로젝트 복원|106|  
|패키지 실행 생성 및 시작|200|  
|작업 중지(유효성 검사 또는 실행 중지)|202|  
|프로젝트 유효성 검사|300|  
|패키지 유효성 검사|301|  
|카탈로그 구성|1000|  
  
 **중지**  
 현재 실행 중인 작업을 중지하려면 클릭합니다.  
  
  